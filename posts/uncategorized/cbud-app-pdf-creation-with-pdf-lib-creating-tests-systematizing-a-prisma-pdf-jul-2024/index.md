---
title: "cbud.app - PDF Creation with PDF-Lib ; Creating Tests; Systematizing a Prisma PDF - Thu 13 Jun 2024 -Mon 15 Jul 2024"
date: "2024-07-16"
---

#### Contractor Buddy Work Notes – Part 5

Start: Thu 13 Jun 2024 01:54:42 PM CDT  
The project from now on is going to be focused on Test Driven Development.

Okay, so I am working on, going to back the schedule page where I will be modifying the modal by writing a test first to determine if the value is being saved in a timely manner and being kept in the relevant state vicinity.

```
test.describe("app", () => {
  test(
    "Sign in, open modal, navigate to the summary tab, write to the summary a random string, save it then close modal and reopen modal to see if the summary is still there."
  );
});
```

So, what I’m going to have to do is making it so that user is apart of a group which has schedule logic to it. We could make the seek invite functionality for new users work.

Once we get a working schedule view then we can go from there.

Start: Sun 16 Jun 2024 05:08:54 PM CDT

Just going thru the timecard process I believe the best thing to do is to focus more on timecards.

“Adding routes and can’t add shifts because it doesn’t show up on allocatedShifts.”

When I tried to do timecards with cbud.app I couldn’t, due to the fact that I couldn’t add shifts to a route among many other app breaking bugs.

```

// Testing add route functionality, for this we will test if allocatedShifts show and in another test we will see if the shifts are showing on main/schedule.
// Add a route, take a picture and then delete the route.
test.describe('app', () => {
  test(
    '

    '
  ) })

```

Start: Mon 17 Jun 2024 09:32:51 AM CDT

Currently on Routes page.

Now working on routes-page-2.

Start: Wed 19 Jun 2024 05:24:06 PM CDT

For the test I need to have it in the dev Org rather than personal account.

I also wonder if you can record the Browser view from Playwright as a .mp4.

I don’t think writing tests and having someone do the whole test correctly without changing the prospective test is doable. I still am very much interested in TDD though but the dev is going to have to change on Red Green Refactor.

I have to make the Route adding in realtime.

“Make updates to the DOM in realtime Next.js 13”

I saw on Stager’s stream of how he would look up messages which were made on his stream so he had this huge db and he could search for a string I would like this same functionality but for my blog so I can look up my/our tutorials much quicker. get current org id clerk next.js

You need to create an API file as [such](https://gist.github.com/MonteLogic/e60c6037b56045bdfc3ad5548ecdc39d):

Or better yet, bring it in from the server component.

Start: Fri 21 Jun 2024 09:02:38 AM CDT

Working on adding routes and discriminating so routes are on relevant orgs.

Am still unable to make the route data show up right after clicking Add Route the only thing that shows is an empty entry.

Why is there an empty entry which adds on to the array but doesn’t add the added data?

Okay, now that adding routes is good, ideally I would write a vRegression test for this.

But I need to get focused on why allocatedShifts isn’t uploading to the db.

Now, what I’ve noticed is that the object being sent in isn’t manicured to work well.

I could do the editing on the server to make the object parsable by the function.

Start: Tue Jun 25 01:46:38 PM CDT 2024

Trying to get the route addition parsable by the function which takes it in.

What on Earth is this ‘active’ bullsh\*t?

Parsable: Allocated Shifts:

```
{
  "allocatedShifts": {
    "afternoon": { "end": "1830", "start": "1500", "active": 1 },
    "midMorning": { "end": "0800", "start": "0500", "active": 1 }
  }
}
```

Current: Allocated Shifts:

```
[
  { "name": "First trip", "startTime": "03:16", "endTime": "05:15" },
  { "name": "Second trip", "startTime": "07:15", "endTime": "08:15" }
]
```

Start: Wed 26 Jun 2024 10:39:43 AM CDT

I think I’m just going to change main/schedule to take in an array instead of an object. This will keep it as is.

Start: Thu 27 Jun 2024 10:26:11 AM CDT

How does the allocatedShift object even get parsed by the function and which function is it?

Ok, now an issue I’m having is that all of these windows are showing Jacksonville for some reason. I think the loop may only be able to handle two cause Pleasant Plains is showing fine.

The issue was I was iterating on route id from post office which may not be unique, so I was iterating on the same ones as Jacksonville cause they all had the same route id from post office.

I need to use the id as the reference point.

Where exactly is the comparison taking place which will use the route ID from post office? But whenever we find this we are going to replace it with the first six digits of the randomly generated ID in the ID row of the table

Start: Fri Jun 28 11:51:39 AM CDT 2024 Where exactly is the comparison for post office route id being made?

Whats going on with this?

```
findRelevantEmployeeInfo
(workTimeArray, routeIDFromPostOffice, date);
```

Where exactly is the comparison for post office route id being made?

```
    findRelevantEmployeeInfo(workTimeArray, routeIDFromPostOffice, date);
```

I’m just going to change it to .id from .routePostOfficeID and fix the breaks. I may use the full id rather than a shortened one, whats the point of using a shortend id value which was taken from the db?

Then fix the issues which may arise by using id as a comparison.

“routeIDFromPostOffice” eventaully becomes loopRelevantRoute

So changing routeIDFromPostOffice to idOfRouteDBGen

routeIDFromPostOffice

I want save to be on the right side also get rid of all that save/edit logic just save button shows up after and edit is made.

Also, dim and make unchangable if a slot is already taken by another employee and then possibly make a manager mode which is a switch at the top where you can switch it and change past and present slots which have been worked.

Okay, now its not saving.

Don’t know why its not updating optimistically via the yellow changing of colors

• You are about to drop the column `routeIDFromPostOffice` on the `WorkTime` table, which still contains 195 non-null values. Dropping routeIDFromPostOffice bc it is not random enough for a delineator.

So now we need to get working on make the logic yellow based on the idOfRoute classification. Okay, so I fixed this problem by changing item.id to item.idOfRoute. Solved using console.logs.

I feel like it would be better to understand if the Day of the week was on top o f it like a card and it was a diffrent color.

See: [https://montelogic.com/wp-content/uploads/2024/06/Day-of-week-cards-Screen-Shot-2024-06-28-at-14.37.01.png](https://montelogic.com/wp-content/uploads/2024/06/Day-of-week-cards-Screen-Shot-2024-06-28-at-14.37.01.png)

Start: Mon Jul 1 09:40:03 AM CDT 2024

Okay, so my db is pulling way too many records from the db. We need to make it like 10x more effecient.

What next for schedule-page-2?

We need to get the spreadsheets working.

Select pay period range in days:

Should be replaced with, by default start of the month and end of the month set because it could be tricky if they hand pick it as 30.

I think I need to discriminate on orgId for the timecard page.

Looking for a calendar for the timecard page. This calendar will use Tailwind. Like the look of this: https://tailwindcomponents.com/component/custom-calendar

Made calendar work, still would like for it to say July and other things as well as being able to click on certain days and changing it.

Also have to set default values on this in Settings page.

Start: Tue Jul 2 09:42:35 AM CDT 2024

Okay let’s get started on template building for timecards.

Which function is being called for the Enidan selection?

EnidanTemplatePDF

Timecard shows good but I need to make employee id selector better for timecard component.

Start pay period should be linked to the calendar selection of the first day so if the the calendar which says starting on: saying 07/01/2024 then it should start on the first viz. the start pay period.

I would like a light theme so we can view the app much easier in direct sunlight. But we need the MVP first.

Would really like a dial/ input on Schedule page to show the milage as well as t he truck id.

… What’s happening is that the records aren’t being deleted if there a row goes from worked to not worked.

Would like to add functionality which shows user there may be a time conflict viz. booking an employee on the same time slot but two different shifts.

Using pdf-lib and .tsx we are going to write over a pdf which has already been created.

<span style=“color: blue;”>Start</span></br> Wed Jul 3 10:51:51 AM CDT 2024

When we/I are/am wrapping up make sure to write down what you are working on and what to do next. So we are going to use pdf-lib on draw on already made pdfs.

… Let’s move timecard menu item near schedule.

Okay, so let’s just get it to draw whatever on it. … Now we are going to white out the dates, <span style=“color: yellow;” id=“in-retrospect”> Learned there is no ‘erasing’ out things using the rectangle in pdf-lib due to the fact that the data underneath is still there just whitened out. </span></br>

After this we are going to replace them with the dates we selected earlier.

Okay, so pdf-lib DOES NOT work for erasing content.

…

Okay, let’s get Driver name and put it into the PDF.

x and y positioning is good for this:

```
const x = 165;
const y = 702.1;
```

Now, let’s get the pay period.

Working on the client side component:

For: 75 pay periods: 15 31 2024-07-03

The starting date which is for the pay period is on 2024-07-15 to 2024-07-31

The calendar logic should read the start pay period and show that one I feel lik e the start pay period should match for the user. The days should default/go to 1, or 15 for the starting day depending on what the current day in the calendar is.

But these additons could be added after the pdf, just deal with the “complicated” logic for now.

Start: Fri Jul 5 10:26:16 AM CDT 2024

I am working in the library and I am unable to get to my prod site, it may be a Namecheap thing cause I can’t get on ‘namecheap.com’

When I try to use the site from my nameceheap I get an SSL error but when I use the domain which I purchased from Vercel it works.

So I’m going to transfer out cbud.app when I get a chance because the down time is too much for Namecheap.

Now, we are going to put the Monday in the Monday slot. We are working on slotting logic.

So what it is exactly will we be discriminating? workTimeForEmployee:

```
console.log(77, "Work time data:", workTimeForEmployee);
```

Side note: I would really like a CLI for adding notes into the todo-area.

I would enter the branch and then find the task and mark it as complete or I wou ld add a task.

When it comes to this PDF, there’s a lot of guess and check would be nice if I could get a hold of a pdf-lib reference where it says where in the pdf it will render and you can measure accordingly.

toDo: I would like a ‘Generate Timecard’ button on the bottom of main/schedule.

I think we should get started on odometer logic.

Start: Sun 07 Jul 2024 05:26:42 PM CDT

Okay, I have to find a toDo manager which uses a CLI.

Start: Tue 09 Jul 2024 06:36:30 PM CDT

I’m not feeling the main/summary page.

The pdf is not showing trip number on https://cbud.app/main/timecard

I feel like with LLMs you get it done quicker and you get ‘functionality’ quicker but its like really buggy and you don’t know what it is so you have to iron out and the kinks and in that ‘ironing’ process you might as well should’ve written out without the LLM.

I still feel like doing it with LLM as described would take just as long but I think I would require less brain power.

Within routes, assocTrucks may not need to be there.

### Start: Wed 10 Jul 2024 11:19:03 AM CDT

Side Note: I think like Releases can have the Markdown or similar sort of showing where it looks like a toDo area as such:

"### Branch: timecard-page

- \[ \] – 0x0 – Make the timecard functionality work for Enidan. – Link to the PDFs showing the examples.

- \[ \] – 0x1 – Show previous timecards

- \[x\] – 0x2 – Accept date as Param. – @MonteLogic

- \[ \] – 0x2 – Discriminate to only show the org employee which the user is in. – @MonteLogic "

I need to find a way of diagramming my code but it would be like super easy and not take forever like making an Obsidian drawing thing.

Ideally this diagrammer would just take the code repo in as a param and generate a diagram showing how all of the files and functions are linked.

This is a [good tool](https://apidiagram.com) but I don’t want to make my repo public.

The extension Sapling is alright but it doesn’t really show the functions all that well and it could use more work to get it to where its the desired product for my use case.

I would like for someone to fork Sapling add more function support as well as documenting support, also have functionality where it could be turned into Mermaid files for easy visual diagramming.

I don’t think this project would be all that hard it would just be time consuming.

This [issue](https://github.com/timlrx/tailwind-nextjs-starter-blog/issues/394) discusses a dependency which is added to a repo but Sapling doesn’t need a dependency per se to make it work. This proposed VS Code/Sublime plugin would have all of the proposed features on top of not needing dependencies.

Like I heard Mr. P once say, once React starts to get large it starts to suck, which I totally agree with.

This proposed solution would make it easier to view large projects, and make working large React projects way easier on the brain.

Discussion continued [here](https://gist.github.com/MonteLogic/56ed2d575fb33b7f47dc7d171611d690).

…

Okay, now we are going to make the selector work for timecard and hopefully we can get the selection to persist among different pages within ‘main/’.

…

I feel like the enidan-template.ts is more about instating a document versus being related to creating a document with Enidan’s stylings.

So we could split the files and then use a any enidan specific logic as a param which will be a function.

We are splitting up generateEnidanPDF.

… 09:34:36 PM CDT

I think I’m going to start working on Leetcode problems and I am going to do them on UserLAnd and try to have them structured as a multi file’real’ program rather than a single file program.

Start: Thu 11 Jul 2024 11:58:42 AM CDT

Working on drawing on paper to re-organize the enidan timecard design. Starting to think relying on LLMs for code writing is bad. But learning using LLMs should be alright.

The problem is the file is using hard-coded values and just overall is sloppy code.

03:04:20 PM CDT Added another PDF, this PDF is styled different so have to adjust where the text is at.

I’m going to make it so if there is more than 7 add another sheet and add the 8th value on this 2nd sheet. Doing this after, I move the text to fit the boxes.

… 09:10:25 PM CDT

Working on this:

```
let trigger = false;
for (const day of daysOfWeek) {
  // Add multiple pages.

  // This is just a duplication of Sunday before it hits Monday.
  // We have to adjust the pages accordingly and it would be fine to just iterate
  // daysOfWeek based on how many days there are and we would just pick the first
  // one which has the earlier date.

  if (day.times.length > 1) {
    console.log(196, trigger);
    const [existingPage] = await pdfDoc.copyPages(pdfDoc, [0]);
    pdfDoc.addPage(existingPage);
  }
  startY = await drawDayWorkTimes(
    page,
    day.times,
    day.name,
    35,
    startY,
    initialRoutes
  );
  console.log(208, trigger);
  trigger = true;
}
```

Start: Fri 12 Jul 2024 10:23:28 AM CDT

No LLMs for fixing the PDF issue of multiple days. Not using LLMs probably for the rest of the day.

Working on this:

```
const howManyPagesToGenerate = (daysOfWeek: {
  name: string;
  times: WorkTime[];
}): number => {
  const count = daysOfWeek.times.length;
  return count > 1 ? count : 0;
};

const pagesToGenerate = daysOfWeek.map((day) => howManyPagesToGenerate(day));
const totalPagesToGenerate = Math.max(...pagesToGenerate);

console.log(207, totalPagesToGenerate);

// We make it -1 because one sheet is currently being made.
for (let index = 0; index < totalPagesToGenerate - 1; index++) {
  const [existingPage] = await pdfDoc.copyPages(pdfDoc, [0]);
  pdfDoc.addPage(existingPage);
}

for (const day of daysOfWeek) {
  startY = await drawDayWorkTimes(
    page,
    day.times,
    day.name,
    35,
    startY,
    initialRoutes
  );
}
```

Okay, so now we got the page number to iterate on we will use this to select the page to write onto the second page.

… 11:38:47 AM CDT

Okay so daysOfWeek will only be 7 nodes in the first dimension.

So we check to see if the first dimension has more than one times node, if so th en we assign it to write on, we would see that it is on the nth node and then pu t that use that nth number to assign to a paper.

scheduleItem:

```
{
  "id": "97080cbf-ee01-4071-b55e-656033122b0a",
  "dateScheduled": "2024-07-01T16:47:34.680Z",
  "dateAddedToCB": "2024-07-01T16:48:13.385Z",
  "idOfRoute": "clxxojuv70004g6cr7k3jgzze",
  "employeesWorkingInfo": {
    "0": {
      "shiftsWorking": {
        "Morning": true,
        "Afternoon": true
      },
      "selectedEmployeeID": "clva4yl3l0002psjcyd6kelw8",
      "selectedEmployeeName": "DJ Chavours"
    }
  },
  "summary": {},
  "organizationID": "org_2fKIXFsK3Xmp0UGghHxafJHXyYX"
}
```

I think this is a good iterator:

```
    let numberOfMultipleDays = 0;
    for (const day of daysOfWeek) {
      console.log(213, day);

      if (day.times.length > 1) {
        numberOfMultipleDays++;
        startY = await drawDayWorkTimes(
          pdfDoc.getPages()[numberOfMultipleDays],
          day.times,
          day.name,
          35,
          startY,
          initialRoutes,
        );
      }

```

Writing day.times is wrong because it puts the whole thing in so it should never happen.

This data structure problem is roughing me up. I managed to get Mondays on the second page but the first Page has Mondays and Tuesdays overlapping.

Going to make a JSON file with co-ordinates of the days of the week as they fit on the page.

I think I’m going to with the days of the week regardless of whether there a days worked there.

Then maybe I could make a set which says which ones fit where.

In reality I’m over thinking it as I could just do calculations for which day is later using the Date object as well as just searching through the array but I was/am trying to rely on iteration logic to get me to the finish line.

So I think I’m going to keep on searching the daysOfWeek array instead of self-referencing.

For this: weekDays\[i\] is a dumb indicator.

```
// weekDays[i] is a dumb indicator.
const weekDays = Object.keys(coordinates.dayOfWeekLocation);
// The for loop should only be 7 in size, instead of over engineering.
const writeToPDFDaysOfWeek = async (daysOfWeek: daysOfWeekType) => {
  for (let i = 0; i < 6; i++) {
    let j = 0; // Initialize j before the while loop
    while (daysOfWeek[i] !== undefined && j < daysOfWeek[i].times.length) {
      await drawDayWorkTimes(
        pdfDoc.getPages()[j],
        [daysOfWeek[i].times[j]], // Pass a single WorkTime as an array
        weekDays[i],
        returnDaysOfWeekCoordinates(weekDays[i])[0],
        returnDaysOfWeekCoordinates(weekDays[i])[1],
        initialRoutes
      );
      console.log(
        249,
        [daysOfWeek[i].times[j]], // Pass a single WorkTime as an array
        weekDays[i],
        returnDaysOfWeekCoordinates(weekDays[i])[0],
        returnDaysOfWeekCoordinates(weekDays[i])[1]
      );
      j++; // Increment j instead of i
    }
  }
  // comment
};
writeToPDFDaysOfWeek(daysOfWeek);
```

…08:46:20 PM CDT

Just remembered that you have to create a community to have your product truly succeed.

Start: Sun 14 Jul 2024 11:23:52 AM CDT

That weekDays\[i\] is a dumb indicator doesn’t match the days and only fires randomly.

Why does it fire randomly and how can we make it smarter?

I feel like this doesn’t fit the sophistication of the function:

```
const weekDays = Object.keys(coordinates.dayOfWeekLocation);
```

… In your code, if you don’t know what it is, delete it.

… Sun 14 Jul 2024 05:15:40 PM CDT

For the third param, it’s just the weekday which will be written on the PDF. So this is only writing Wednesday on two entries:

```
await drawDayWorkTimes(
  pdfDoc.getPages()[j],
  [daysOfWeek[i].times[j]], // Pass a single WorkTime as an array
  "Wednesday",
  returnDaysOfWeekCoordinates(weekDays[i])[0],
  returnDaysOfWeekCoordinates(weekDays[i])[1],
  initialRoutes
);
```

This only produces two entries:

```
await drawDayWorkTimes(
  pdfDoc.getPages()[j],
  [daysOfWeek[i].times[j]], // Pass a single WorkTime as an array
  "Wednesday",
  72,
  660 - additionTo(),

  initialRoutes
);
```

But why are there just two entries/WorkTimes being written to the PDF?

I think the problem is co-ordinates.

I need to get the co-ordinates, so I’m going to write a function which takes the workTime object and returns the co-ordinates for the day of the week. Within the input param there will be the dateScheduled field and from there we’ll ascertain the date and then get the day of the week from the date and then check it with the co-ordinates which will return the day of the week coordinates for the workTime object.

```
// We can get the dayName here and get it from 'coordinates.' here rather than below.
for (let i = 0; i < MAX_ENTRIES_PER_DAY; i++) {
  // What even is this?
  // That if statement doesn't make any sense.
  if (i < workTimes.length) {
    await drawWorkTimeInfo(
      page,
      workTimes[i],
      coordinates.startX,
      coordinates.startY,
      routes
    );
  }
}
```

Not sure if I got those co-ordinates returning and put in the right place cause there all jam packed in on place so to speak.

There all jam packed but I know where they are going just have to return co-ordinates from the function I last committed.

<—————>

Start: Mon 15 Jul 2024 11:29:08 AM CDT

I wonder what the workflow of writing a large branch of differences where you were figuring stuff out but you want to run a PR of changes which are much more concise.

Okay now, we are going to go thru the PDF and explain what is on the page and how it happened with the console.logs providing perspective.

Okay, so the first page for the weekday slot it is saying:

```
The first slot says, Monday

The second slot says, Tuesday/Wednesday but these two words are overlapping.

Then this third slot is blank, so, empty.

Then the fourth slot says Thursday.

The fifth slot says, Friday

The sixth slot says, Saturday.

The seventh slot says, Sunday.
```

Okay, so conjecture these results:

Okay, so this is the code which writes the days of the week:

```
await drawText(
  page,
  getDayOfWeek(workTimes[0]),
  // I think maybe here we can accurate coordinates.
  returnDaysOfWeekCoordinates(getDayOfWeek(workTimes[0]))[0],
  returnDaysOfWeekCoordinates(getDayOfWeek(workTimes[0]))[1]
);
```

This is why:

```

  "dayOfWeekLocation": {
    "Monday": [72, 660],
    "Tuesday": [72, 600],
    "Wednesday": [72, 600],
    "Thursday": [72, 480],
    "Friday": [72, 420],
    "Saturday": [72, 360],
    "Sunday": [72, 300]
  },
```

Okay, so now that we got weekdays looking good, we are going to focus on writing the rest of workTime.

Which is errantly being done with:

```
  for (let i = 0; i < MAX_ENTRIES_PER_DAY; i++) {
    if (i < workTimes.length) {
      if (workTimes[i] && workTimes[i] !== undefined) {
        await drawWorkTimeInfo(
          page,
          workTimes[i],
          // I think maybe here we can accurate coordinates.
          coordinates.startX,
          coordinates.startY,
          routes,
        );
      } else {
        console.log('Invalid work time at index', i);
      }
    }
  }`

```

This would also need to implement down\*, because there will be multiple ones of it.

So, I want the date to go down but the rest of the values to stay up.

I want to change these + and – stuff to hard coded values with the JSON file.

So right now it’s moving good after I changed the params within drawWorkTimeInfo. This thing is almost done if we don’t run into any big problems.

Currently, work the work shifts if there are multiples of them they are on the same line this shouldn’t happen, they should be in different rows.

Its starting to not look good after the first one because its too low, so we could get Monday in the correct position and that may fix this problem.

How do we position the first row though?

I think it would have something to do with lineHeight but this variable isn’t being used.

… The date string is currently in the bottom right corner.

This statement may change but its sounding confident for now: I need to make the SPACE between the lines bigger no what is being iterated.

Now, what var is controlling the space between workTime entries?

Maybe there is no line height because they are all using hard coded values and the values should just be changed on the appropriate JSON file.

… Okay, now I am focusing on getting the shifts to iterate over on the shift, ‘trip number’ column.

For this, workTime\[1\] is never fired:

```
const drawDayWorkTimes = async (
  page: PDFPage,
  workTimes: WorkTime[],
  routes: Routes[]
) => {
  getDayOfWeek(workTimes[0]);

  // We can get the dayName here and get it from 'coordinates.' here rather than below.
  await drawText(
    page,
    getDayOfWeek(workTimes[0]),
    // I think maybe here we can accurate coordinates.
    returnDaysOfWeekCoordinates(getDayOfWeek(workTimes[0]))[0],
    returnDaysOfWeekCoordinates(getDayOfWeek(workTimes[0]))[1]
  );
  //
  // This should only be concerned about filling in the workTime info not the day of the week.
  for (let i = 0; i < MAX_ENTRIES_PER_DAY; i++) {
    if (i < workTimes.length) {
      if (workTimes[i] && workTimes[i] !== undefined) {
        await drawWorkTimeInfo(
          page,
          // This may be useless:
          workTimes[i],
          // What is the minus 20 being used for?
          // Move workTime into a more appropriate place.
          returnDaysOfWeekCoordinates(getDayOfWeek(workTimes[0]))[0] -
            coordinates.workTimeSpacingX,
          returnDaysOfWeekCoordinates(getDayOfWeek(workTimes[0]))[1] -
            coordinates.workTimeSpacingY,
          routes
        );
      } else {
        console.log("Invalid work time at index", i);
      }
    }
  }
};
```

Currently trying to do something so I can put the shifts in the right place because it can be done iteratively.

Here, on line 72, is where the shifts are really showing:

```
await drawText(
  page,
  workedShifts.join(", "),
  x + coordinates.workedShiftsPositioning.x,
  y + coordinates.workedShiftsPositioning.y
);
```

Okay, so for the aforementioned code, we can go through ever node within workedShifts as a for loop of ‘workedShifts.length’ and use drawText within the for loop.

… Okay, so what’s next is bring in other values into the PDF besides whats currently on the PDF now, (Mon 15 Jul 2024 06:33:04 PM CDT).
