---
title: 'Current Style of Generating PDFs for CBud- 1 '
date: '2025-05-19'
start-date: 'Thu May 15 2025 17:34:15 CDT'
last-updated: 'Sun May 18 2025 15:02:31 CDT'
category: 'Work/Life Notes'
status: 'public'
---


# Crafting Timecards: An In-Depth Look at PDF Generation in cbud.app

Trying to deliver an excellently formatted PDF document is hard and took me 2+ months to do it effectevely for my use case, granted I was a new Next.js Dev.


Here I will outline how I designed CBud to deliver pdfs along with the dates and formatting.

This process centers around using the pdf-lib library as well as a myriad of custom functions. 





## User Interaction: The `TimeCardComponent`

The user interaction point for this functionality resides within the `TimeCardComponent`. This client-side React component provides the interface for selecting an employee, choosing a timecard template type (like "Acme Trucking" or "Standard Template"), defining the pay period using date inputs and a calendar interface, and ultimately triggering the generation process.


### From `TimeCardComponent.tsx`:

```typescript
// timeCardTemplate state manages the selected template
const [timeCardTemplate, setTimecardTemplate] = useState<TemplateType>(
  TemplateType.Acme,
);
// startPayPeriod and endPayPeriod manage the selected date range
const [startPayPeriod, setStartPayPeriod] = useState<number>(
  payDefaults.payPeriod1[0],
);
const [endPayPeriod, setEndPayPeriod] = useState<number>(
  payDefaults.payPeriod1[0],
);
// dateSelection is likely tied to the calendar input
const [dateSelection, setDateSelection] = useState(
  new Date().toISOString().split('T')[0],
);
// ... other state and useEffect hooks ...

// generatePDFClientSide is triggered by the button click
const generatePDFClientSide = async () => {
  // ... date formatting and data preparation ...

  switch (timeCardTemplate) {
    case TemplateType.Acme:
      CBudTemplatePDF(
        workTimeArray,
        selectedEmployeeID,
        selectedEmployeeName,
        initialRoutes,
        startPayPeriodFormatted,
        endPayPeriodFormatted,
        routeShiftInfoData,
      );
      break;
    case TemplateType.Standard:
      // ... call to GenerateTemplateB ...
      break;
  }
  // ... metadata update ...
};

return (
  <div className="space-y-4">
    {/* ... template and pay period selectors ... */}
    <Button
      onClick={generatePDFClientSide}
      // ... button styling ...
    >
      Generate Timecard
    </Button>
    {/* ... generated count display ... */}
  </div>
);

```

Upon clicking the "Generate Timecard" button, the generatePDFClientSide function in TimeCardComponent is invoked. This function acts as a dispatcher, determining which template is selected. For the "Acme Trucking" template (TemplateType.Acme), it calls the CBudTemplatePDF function, passing along the collected employee details, date ranges, and relevant work time and route data.

### Server-Side Data Fetching and Initial Processing: CBudTemplatePDF
The CBudTemplatePDF function, located in utils/timecards/acme/CBudTemplatePDF.ts, takes these parameters and initiates the server-side data fetching and PDF processing. It first retrieves the latest work time data from the /api/pdf-worktime-info endpoint to ensure accuracy.

From utils/timecards/acme/CBudTemplatePDF.ts:
```ts


export const CBudTemplatePDF = async (
  // ... parameters ...
) => {
  try {
    // Fetch updated work time data from the API
    const response = await fetch('/api/pdf-worktime-info');
    if (!response.ok) {
      throw new Error('Failed to fetch work time data');
    }
    const { data: workTimeData } = await response.json();

    // Create date objects for the pay period
    const startDateObj = new Date(startPayPeriod);
    const endDateObj = new Date(endPayPeriod);

    // Filter work time data for the specific employee and date range
    const employeeWorkTime = workTimeData.filter((wt: WorkTimeShiftType) => {
      const shiftDate = new Date(wt.dayScheduled);
      return (
        wt.userId === selectedEmployeeID &&
        wt.occupied &&
        shiftDate >= startDateObj &&
        shiftDate <= endDateObj
      );
    });

    // Sort by date and shift time
    const sortedEmployeeWorkTime = employeeWorkTime.sort((a: WorkTimeShiftType, b: WorkTimeShiftType) => {
      // First sort by date
      const dateA = new Date(a.dayScheduled);
      const dateB = new Date(b.dayScheduled);
      if (dateA.getTime() !== dateB.getTime()) {
        return dateA.getTime() - dateB.getTime();
      }
      // If same date, sort by shift time
      const shiftA = routeShiftInfo.find(shift => shift.id === a.shiftWorked);
      const shiftB = routeShiftInfo.find(shift => shift.id === b.shiftWorked);
      if (shiftA && shiftB) {
        return shiftA.startTime.localeCompare(shiftB.startTime);
      }
      return 0;
    });

    // ... call to generateCBudPDF and download logic ...
  } catch (error) {
    console.error('Error generating PDF:', error);
    throw error;
  }
};
``` 
This data is then filtered to include only the shifts relevant to the selected employee and falling within the specified pay period. Crucially, the filtered data is sorted chronologically, first by date (dayScheduled) and then by shift start time (shiftWorked), making the timecard clear and organized.

Core PDF Drawing Logic: generateCBudPDF
The sorted and filtered data is then passed to the core PDF drawing function, generateCBudPDF. This function is responsible for the heavy lifting of manipulating the PDF document and is also located within the utils/timecards/acme/ directory, likely in a file like generateCBudPDF.ts or pdfDrawer.ts.

From the file containing generateCBudPDF (perceived path utils/timecards/acme/generateCBudPDF.ts or pdfDrawer.ts):

```ts

export const generateCBudPDF = async (
  // ... parameters ...
): Promise<ArrayBuffer> => {
  try {
    // Calculate total weeks based on pay period
    const dateRanges = getWholeDateRangesWeek(startPayPeriod, endPayPeriod);
    const totalWeeks = dateRanges.length;

    // Fetch the PDF template
    const templatePath =
      '/timecard-pdfs/cbud-acme-timecard-template-no7_10_20_2024.pdf';
    const response = await fetch(templatePath);
    // ... error handling ...
    const existingPdfBytes = await response.arrayBuffer();

    // Load the PDF document
    const pdfDoc = await PDFDocument.load(existingPdfBytes);
    const boldFont = await pdfDoc.embedFont(StandardFonts.HelveticaBold);

    // Generate pages for each week
    const pages = [pdfDoc.getPages()[0]];
    for (let i = 1; i < totalWeeks; i++) {
      const [newPage] = await pdfDoc.copyPages(pdfDoc, [0]);
      pdfDoc.addPage(newPage);
      pages.push(newPage);
    }

    // ... data processing and grouping by week ...

    // Process each page
    for (let i = 0; i < totalWeeks; i++) {
      const page = pages[i];
      const dateRange = dateRanges[i];

      // Always draw the header
      await drawPageHeader(
        page,
        selectedEmployeeName,
        dateRange[0][0],
        dateRange[1][0],
        i,
        totalWeeks,
        boldFont,
      );

      // Process work times if they exist for this week
      const weekWorkTimes = Object.values(workTimesByWeek)[i] || [];
      if (weekWorkTimes.length > 0) {
         // ... grouping work times by day of week ...
        for (const day of daysOfWeek) {
          if (day.times.length > 0) {
            let yLower = 0; // Used to offset Y coordinate for multiple entries
            drawDateOfWorkTimes(page, day.times, day.name);
            for (let j = 0; j < day.times.length; j++) {
              // Draw each work time entry for the day
              totalHours =
                (await drawDayWorkTimes( // drawDayWorkTimes calls drawWorkTimeInfo
                  page,
                  [day.times[j]], // Pass a single WorkTime object in an array
                  initialRoutes,
                  routeShiftInfo,
                  yLower, // Pass the current Y offset
                )) || 0;
              yLower -= coordinates.workTimeSpacingY2; // Decrease Y offset for the next entry on the same day
            }
          }
          // ... calculate and write total hours ...
        }
      }
    }

    // Save and return the PDF
    return await pdfDoc.save();

  } catch (error) {
    console.error('Error generating PDF:', error);
    throw error;
  }
};

// Helper function within the same file
const getWholeDateRangesWeek = (
  startDate: Date,
  endDate: Date,
): string[][][] => {
  // ... logic to calculate weekly date ranges ...
};
```
This function handles the core logic:

### Template Loading and Page Preparation
It fetches a base PDF template file (e.g., /timecard-pdfs/cbud-acme-timecard-template-no7_10_20_2024.pdf) using a standard Workspace request. The pdf-lib library then loads this existing PDF's bytes into a modifiable document object. The code determines the number of weeks spanned by the selected pay period using the getWholeDateRangesWeek helper function; this dictates the number of pages needed in the output PDF (one page per week range). If more than one page is required, the initial template page is copied and added to the document accordingly.

### Data Structuring by Week and Day
The fetched work time data is grouped by the ISO week number they fall into (getWeekNumber). This grouped data is then iterated through, processing one week (and thus one page) at a time. Within each week's data, the work times are structured by day of the week.

### Drawing Page Elements
For each page (representing a week), several drawing operations occur, utilizing helper functions likely located in utils/timecards/acme/fns/pdfFns.ts:

- Page Header: The drawPageHeader function (likely in the same file as generateCBudPDF) is called to place standard header information like employee name, the week's date range, and page number.
- Daily Information: For each day within the week that has recorded work times, the drawDateOfWorkTimes function writes the date string onto the page at coordinates specified for that day of the week in the pdf-coordinates.json file.
- Work Time Entries: The code iterates through each work time entry for a given day. For each entry, the drawDayWorkTimes function is called. This function in turn calls drawWorkTimeInfo for the specific entry.

### Drawing Helper Functions in pdfFns.ts

From utils/timecards/acme/fns/pdfFns.ts:
```ts
// Function to draw work time information on the PDF
export const drawWorkTimeInfo = async (
  page: PDFPage,
  workTime: WorkTimeShiftType,
  x: number,
  y: number,
  routes: RouteType[],
  routeShiftInfo: RouteShiftInfoType[],
) => {
  // ... find route and shift info ...
  // ... calculate start/end/total time ...

  // Shift Name (Trip Number)
  await drawText(
    page,
    shiftInfo?.shiftName || 'N/A',
    x + coordinates.tripNumberPositioning.x,
    y + coordinates.tripNumberPositioning.y,
  );

  // Start time
  await drawText(
    page,
    startTime,
    x + coordinates.timeTextPositioningStart.x,
    y + coordinates.timeTextPositioningStart.y,
  );
  // End time
  await drawText(
    page,
    endTime,
    x + coordinates.timeTextPositioningEnd.x,
    y + coordinates.timeTextPositioningEnd.y,
  );
  // Total time
  await drawText(
    page,
    totalTime.toString(),
    x + coordinates.totalTimePositioning.x,
    y + coordinates.totalTimePositioning.y,
  );

  // Route Nice Name
  await drawText(
    page,
    routeNiceName,
    x + coordinates.routeNiceNamePositioning.x,
    y + coordinates.routeNiceNamePositioning.y,
  );
   return totalPageTime; // Likely accumulates hours per day
};

// Function to draw work times for a specific day (calls drawWorkTimeInfo)
export const drawDayWorkTimes = async (
  page: PDFPage,
  workTimes: WorkTimeShiftType[], // Note: Often passed as a single-element array [entry]
  routes: RouteType[],
  routeShiftInfo: RouteShiftInfoType[],
  yLower: number, // Used to adjust vertical position
) => {
  if (workTimes.length === 0) return;

  const dayOfWeek = getDayOfWeek(workTimes[0]); // Get day name from the entry
  const [x, y] = returnDaysOfWeekCoordinates(dayOfWeek); // Get base coordinates for the day section

  // This draws the day name (e.g., Monday, Tuesday)
  await drawText(page, dayOfWeek, x, y);

  // This calls drawWorkTimeInfo for a single entry (workTimes[0])
  // and applies horizontal and vertical offsets.
  // yLower is added to the base Y coordinate for vertical stacking.
  const returnValue: number = await drawWorkTimeInfo(
    page,
    workTimes[0],
    x - coordinates.workTimeSpacingX, // Apply horizontal offset
    yLower + y - coordinates.workTimeSpacingY, // Apply vertical offset including yLower
    routes,
    routeShiftInfo,
  );
  return returnValue || 0.159;
};

// Basic text drawing utility
export const drawText = async (
  page: PDFPage,
  text: string,
  x: number,
  y: number,
  size: number = FONT_SIZE,
) => {
  const font = await page.doc.embedFont(StandardFonts.Helvetica);
  page.drawText(text, {
    x, y, size, font, color: rgb(0, 0, 0),
  });
};
``` 

**drawWorkTimeInfo** retrieves details like the shift name (referred to as "Trip Number" in notes), start and end times, calculates the total time for that shift, and finds the corresponding route name. 
These are drawn using drawText at coordinates relative to a calculated starting point. 
- A key challenge noted in the work logs was positioning multiple entries on the same day without overlap. The generateCBudPDF logic addresses this by iterating through each entry for a day and calling drawDayWorkTimes (which then calls drawWorkTimeInfo) for each, passing a decreasing yLower value. This effectively stacks the work time details vertically within the section of the page allocated for that specific day, using coordinates.workTimeSpacingY2 for the vertical spacing between entries.

Coordinate Management: pdf-coordinates.json
The pdf-coordinates.json file is central to managing these positions.

From a conceptual pdf-coordinates.json structure inferred from notes and code:
``` JSON
{
  "driverNamePosition": [165, 702.1],
  "startDatePosition": [400, 720],
  "endDatePosition": [480, 720],
  "dateDashPosition": [440, 720],
  "dayOfWeekLocation": {
    "Monday": [72, 660],
    "Tuesday": [72, 600],
    "Wednesday": [72, 600],
    // ... rest of days ...
  },
  "dayMonthYearCoordinates": {
     "Monday": ["X1", "Y1"],
     "Tuesday": ["X2", "Y2"],
     // ... rest of days ...
  },
  "tripNumberPositioning": {"x": 50, "y": 0},
  "timeTextPositioningStart": {"x": 150, "y": 0},
  "timeTextPositioningEnd": {"x": 200, "y": 0},
  "totalTimePositioning": {"x": 250, "y": 0},
  "routeNiceNamePositioning": {"x": 300, "y": 0},
  "workTimeSpacingX": 20,
  "workTimeSpacingY": 10,
  "workTimeSpacingY2": 15,
  "bottomHourTimes": ["X_bottom", "Y_bottom"],
  "bottomBottomHourTimes": ["X_final_bottom", "Y_final_bottom"]
}
```
### Weekly Hours Summary
At the bottom of each page, the writePageHoursBottom function is called to display the total hours for that specific week. The logic differentiates between the last page of the document and earlier pages, potentially showing a cumulative total on the final page, using different coordinates (bottomHourTimes vs bottomBottomHourTimes).

### Handling Drawing Complexities
The work notes highlight the iterative process and occasional "guess and check" required to get the positioning right. The move to a pdf-coordinates.json file with specific X and Y values for various elements, including separate coordinates for each day of the week's location and for dating drawing, was a significant step in systematizing this. The notes also reveal the discovery that pdf-lib's drawing capabilities do not truly "erase" underlying content; attempting to do so with white rectangles merely obscures the information – "Learned there is no ‘erasing’ out things using the rectangle in pdf-lib due to the fact that the data underneath is still there just whitened out."

### Finalization and Download
Once all pages have been processed and populated with data, the pdfDoc.save() method is called to generate the final PDF as an ArrayBuffer. This buffer is then used in CBudTemplatePDF to create a Blob, a URL is generated for the blob, and a temporary anchor element is used to trigger a download in the user's browser, naming the file based on the employee and start date. Finally, the temporary URL is revoked to free up resources.

## Summary
In summary, the PDF generation in cbud.app is a sophisticated client-initiated process. It involves fetching and preparing data, dynamically creating PDF pages based on the time period's duration, strategically positioning various data points onto a predefined template using coordinate mapping derived from a JSON configuration, and handling the display of multiple work entries per day by vertically offsetting them. The use of pdf-lib provides the low-level drawing capabilities, while helper functions and a coordinate configuration file manage the complexity of accurately populating the timecard layout. The development process, as shown in the notes, involved iterative refinement and learning the specific capabilities and limitations of the chosen PDF library.

