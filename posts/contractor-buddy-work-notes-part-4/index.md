---
title: 'The Power of Static Typing in Programming'
publishedAt: '2024-04-07'
summary: 'In the ever-evolving landscape of software development, the debate between dynamic and static typing continues to be a hot topic.'
---


What I learned from April to June

- Testing is really important and there comes a point where testing is NEEDED.
- TDD appears to be the best option after the initial first couple of days of coding on a project.

Start: Tue 23 Apr 2024 10:48:29 AM CDT

Now, I have to turn those input results into object which will then be saved to the DB.

I need to pipe a setState into:

```typescript
export const AddRouteShifts: React.FC<{ allocatedShifts: any }> = ({
  allocatedShifts,
}) 
```

allocatedShifts is sending but not well, I still need to accommodate it in the API file.

Start: Wed 24 Apr 2024 10:34:27 AM CDT

Okay. So What I’m working on right now. Hey, so I’m trying to figure out, I just I did that props, chilling. And then I got the object, object object, to save The time is 10. 48. Am I got that objects to save And then I gotta like show the routes area.

Then I want to edit the edit thing. Turn it to delete button And then I gotta make that work. So yeah.

Have to figure out how to clear the form when the answer has been submitted.

… I would have to wrap it in a Context provider in order for it to work as desired but I’m just going to add it all to the same component.

I need to wrap this thing in a context provider or put the whole thing in the same file other wise I’m just in no man’s land.

Start: Fri 26 Apr 2024 10:58:50 AM CDT Now we have to list the Routes already up and have an ability to edit or delete them.

We should have the app reload once a route is added or other similar logic because the route doesn’t appear in /main/schedule until after a reload.

What if we just make the Page area move.

I don’t like getting into the date input thing, I’d much rather swipe.

So, I’m having issues with the fact that if there is no WorkTime record then there can’t be anything written down.

Start: Sun 28 Apr 2024 12:31:56 PM CDT

There needs to be a record creation for writing to the Summaries page if there is no record already.

Need to figure out why its showing on the preview even though its not from the db. Looks like its in the queue of whats about the be added.

In app/main/summary/page.tsx we are only bringing the routes in we could also bring in the WorkTime(s) as well.

Could not find matching day trips if an error is present.

The issue I’m having is if there is no record create one but having a tough time with no record logic.

Check in summary-selection if there is no id, then pass then we’ll know that for the record creation.

How to setState through components:

```typescript
  setSummaryObject: React.Dispatch<React.SetStateAction<any>>
```

This is my current object how about I move up the other stuff which isn’t relevant to the summaryObject:

```json
{
 "summaryObjectWithDateAndRoute": {
  "dateScheduled": "2024-05-08",
  "earlyMorning": [
   {
    "imgURLs": [],
    "text": "ummary?date=2024-05-08&route=626M5"
   }
  ],
  "midMorning": [
   {
    "imgURLs": [],
    "text": "ummary?date=2024-05-08&route=626M5"
   }
  ],
  "routeIDFromPostOffice": "626M5"
 }
}

```

I don’t think I need that useEffect because it could be replaced by data being piped into the server component.

Start: Tue 30 Apr 2024 12:03:26 PM CDT [https://github.com/scottgallant/seinfeld-calendar](https://github.com/scottgallant/seinfeld-calendar)

[https://github.com/yungjurick/kalendar](https://github.com/yungjurick/kalendar)

I like the home page of this: [https://github.com/nguyend-nam/nextjs-calendar](https://github.com/nguyend-nam/nextjs-calendar)

For this, use can use demo account maybe we can use a similar mechanism for sharing links. [https://dwarvesf-boilerplate.netlify.app/login](https://dwarvesf-boilerplate.netlify.app/login)

Start marking metadata: [https://montelogic.com/wp-content/uploads/2024/04/upload-documents-starting-marking-metadata.png](https://montelogic.com/wp-content/uploads/2024/04/upload-documents-starting-marking-metadata.png)

Make it so that uploading an image, saves it and there isn’t a need to hit the save button after uploading an image.

It’s setting an empty object: 17 2024-04-30 626XX ℹ UPLOADTHING 1:08:48 PM UploadThing dev server is now running! ℹ UPLOADTHING 1:08:51 PM SIMULATING FILE UPLOAD WEBHOOK CALLBACK [http://localhost:3000/api/uploadthing?slug=imageUploader](http://localhost:3000/api/uploadthing?slug=imageUploader) ℹ UPLOADTHING 1:08:51 PM UploadThing dev server is now running! Upload complete for userId: fakeId file url [https://utfs.io/f/43d8d0bf-287a-4f52-a0b1-cb5bb5b0f89e-z6p2js.png](https://utfs.io/f/43d8d0bf-287a-4f52-a0b1-cb5bb5b0f89e-z6p2js.png) ✓ UPLOADTHING 1:08:52 PM Successfully simulated callback for file 43d8d0bf-287a-4f52-a0b1-cb5bb5b0f89e-z6p2js.png 69, body: { entryID: ‘6cf21784-b674-4fe9-ae94-9d75fb0c98f0’, summaryObject: {} } 74 {} 76, id: 6cf21784-b674-4fe9-ae94-9d75fb0c98f0 113 true, id already exists (existingWorkTime), let’s try to update it. response bad { params: undefined } 69, body: { entryID: ‘6cf21784-b674-4fe9-ae94-9d75fb0c98f0’, summaryObject: {} } 74 {} 76, id: 6cf21784-b674-4fe9-ae94-9d75fb0c98f0 113 true, id already exists (existingWorkTime), let’s try to update it. response bad { params: undefined }

69, body: { entryID: ‘6cf21784-b674-4fe9-ae94-9d75fb0c98f0’, summaryObject: { earlyMorning: \[ \[Object\] \] } } 74 { earlyMorning: \[ { text: ‘asdfasdf’, imgURLs: \[\] } \] } 76, id: 6cf21784-b674-4fe9-ae94-9d75fb0c98f0 113 true, id already exists (existingWorkTime), let’s try to update it. response bad { params: undefined } 17 2024-04-30 626XX

The files in question: [https://gist.github.com/MonteLogic/a0a703e360439b676884fdc5f3cbe227](https://gist.github.com/MonteLogic/a0a703e360439b676884fdc5f3cbe227) [https://gist.github.com/MonteLogic/798f8b9429449425f782a50afe2628c7](https://gist.github.com/MonteLogic/798f8b9429449425f782a50afe2628c7)

Need to figure out how to save the image / summaryObject to db after uploading.

Start: Fri 03 May 2024 11:00:12 AM CDT [http://localhost:3000/main/summary?date=2024-05-03&route=626M5](http://localhost:3000/main/summary?date=2024-05-03&route=626M5)

Unable to view current day.

It looks like when the URL is being set its not doing a good search.

626XX doesn’t appear to be getting wrote to the db.

I wonder if the summaryObject is overwriting the routeID.

We need to make an edit routes page and when the route number is changed we need to have an operation to change the old route IDs to the new ones.

Fresh start search isn’t working.

I think I need to set the URL as part of the search function within that init useEffect.

The change input thing seems to be only thing which is finding it correctly.

It might be because that useEffect is messing it up.

New strategy move HTML to server component.

Start: Sun 05 May 2024 10:54:27 AM CDT

For like the toDo chamber I think I’m going to add stuff like

" ### Branch: summary-page

\[ \[x\] - Add route time adder

\]

"

To the Pull Request notes

Start: Mon 06 May 2024 10:47:21 AM CDT

Would really like to hit ctrl+enter to save.

We’re having issues with WorkTime and saving it per organization because the dev one and prod one appears to be sharing orgID which shouldn’t be happening we should be discriminating for orgID.

I gotta fix that so work on schedule-page real quick so that gets fixed. Fixed it. Now, lets focus on:

- \[x\] - 0x1 - Only have shifts from allocatedShifts show up.

So we can get the routeID from the post office pretty easily.

Start: Thu 09 May 2024 10:12:58 AM CDT

Now we have to pipe in the date selection.

I just have to get a good GET API call.

ui/modal-schedule.tsx // Looks like I need to the id from either one of these: console.log(299, workTimeForEmployee, localWorkTimeForEmployee);

Start: Fri 10 May 2024 09:52:06 AM CDT

Maybe the check checks shiftsWorking got something and if not creates a new record.

For getting summary-schedule.

Still need to get the id of the entry as well as work on non-record editing.

What I am going to do is add that dispatch setState and whats going to happen is I’m going to need a prop to fill in that prop from network-fns and thats just going to come from the parent file.

AAAnd Redux is avoided.

Start: Sun 12 May 2024 12:40:28 PM CDT

Issue, the schedule isn’t updating dynamically like it should.

I am going to link to certain portions of a README.md.

Start: Mon 13 May 2024 10:01:39 AM CDT

For some reason clicking “View of Summary of Day” is creating a POST request when it should create a GET request.

For the diagramming, I am trying, Markdown Preview Mermaid Support

Okay so we are going to have this function:

```typescript

const saveWorkTime = async (localWorkTimeForEmployee: WorkTime) => {
  try {
    const response = await fetch('/api/work-time', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(localWorkTimeForEmployee),
    });

    // Okay, so this post I need to pipe the return value 
    // of them all into /main/schedule.
    if (response.ok) {
      console.log('Work time updated successfully');
      return 'Has updated';
    } else {
      console.error('Error updating work time');
    }
  } catch (error) {
    console.error('Error updating work time', error);
  }
};

```

We would like that return value to query the whole db part where orgID is equivalent. Why? Because the return value can then be used to prop drill up to update the schedule carousel file.

Then once we get the return value we would then prop down it back up to ui/modal-schedule.

I think its better to use the { use} hook rather than prop drill up or down. What Claude said:

In Next.js 13 with the app router, the recommended way to update data is by using the use hook in combination with the fetch function. The use hook allows you to fetch and cache data on the server, and it automatically handles data updates when the underlying data changes. Here’s an example of how you can update data in a Next.js 13 app router component:

```typescript

import { use } from 'react';

async function fetchData(id) {
  const res = await fetch(`https://api.example.com/data/${id}`);
  return res.json();
}

export default function MyComponent({ params }) {
  const { id } = params;
  const data = use(fetchData(id));

  // Render the component using the fetched data
  return (
    <div>
      <h1>{data.title}</h1>
      <p>{data.description}</p>
    </div>
  );
}
```

Start: Tue 14 May 2024 02:56:04 PM CDT

We really need to get it to the point where you can go in schedule-page as a website and interact with that one.

The state of the app for main/schedule

Is that if you want to update from Summaries you have to write it and then refresh the page.

using the use hook “next.js 13”

use() hook

[https://react.dev/reference/react/use](https://react.dev/reference/react/use)

Use isn’t stable on the client side, see

[https://github.com/vercel/next.js/issues/46084](https://github.com/vercel/next.js/issues/46084)

esp. [https://github.com/vercel/next.js/issues/46084#issuecomment-1439844760](https://github.com/vercel/next.js/issues/46084#issuecomment-1439844760)

Start: Wed 15 May 2024 09:54:20 AM CDT

The use hook would only work on the server side, so I’m not sure if that would be a total solution or we would have to prop drill.

Let’s work on the prop drilling than integrating the canary feature of use().

Said previously: What I am going to do is add that dispatch setState and whats going to happen is I’m going to need a prop to fill in that prop from network-fns and thats just going to come from the parent file.

…

Working on trying to get those cards to turn to yellow: What variable is responsible for changing it to yellow?

```typescript
     <SwiperSlide
          key={i}
          className={`flex flex-col items-center ${
            hasTrueShift && fullTrueForID ? 'bg-yellow-500' : 'bg-white'
          }`}
          />


```

There appears to be a type mismatch on slider-component so thats bad, ideally it would take to the form of workTimeTop.

So I guess have to change setWorkTime for employee to something like workTimeTop rather than relying on a useEffect because this is kind of a ghetto solution.

I feel like I need to have an encyclopedia of variables, kind of like header files in C++.

Now we have to overhaul the summary part of the modal.

I don’t even know how the summaries thing is working for the modal which is bad because should be very strict on responsibility.

How does the yellow changing work?

Recording: [https://recorder.google.com/3b40098e-b689-47c4-88c3-b4e708f9bc96](https://recorder.google.com/3b40098e-b689-47c4-88c3-b4e708f9bc96)

" Okay. The file with all the slides on, it is going to be Slider. Dash component and slider Dash component, There’s a file called model schedule. And in there there is set work time for employee pipedon. Pat inside, which I worked out from employee, which is Changed by handlestick button.

Click. And then once the button is saved, it does use effect. And then that’s how you get the new one. And then it’s the, the use effect that is on cider dash component, Which triggers the new yellow changing is a use effect, which Changes set work time top. Ideally we would go into that.

You didn’t, we wouldn’t need to use effect and we could just do props steering but that’s that’s how that works.

"

Working on the summary part. It appears that when there is no record and a summary is trying to be submitted the following error occurs: Error submitting summaries TypeError: updatedData.data is undefined

Even when the record is submitted the process for updating it is taking too long around 3 seconds.

So what in the summary page which is occurring to have that business logic work well because we are going to need to integrate this logic into the summary page of the modal schedule area.

Start: Thu 16 May 2024 10:34:04 AM CDT

In the summary page what is the value which it is reading is this value come in from workTimeTop?

… toDo, make the summary part of the schedule modal update in real time rather than waiting on waiting on the useEffect(\*) which is relying on workTimeTop to run. Okay, so its changing but its not changing in a quick way. Why?

But honestly, its good enough, there are more important features to do.

I feel link deleting the Summary page and just using the sliders on slider-component would be better.

The feature I really need to work on is getting those timecards made.

Start: Fri 17 May 2024 01:59:25 PM CDT

Here: [http://localhost:3000/main/timecard](http://localhost:3000/main/timecard)

Its getting the name of the employees rather than the ID which it should, add this functionality to the schedule area.

Okay, so how does the timecard functionality work?

Okay, the functionality is work but by no means is it prod, we have to add loads of error messages.

Why is utils/GenerateTemplateB.ts not in the folder it should be?

Start: Mon 27 May 2024 01:54:20 PM CDT

Why are all these shiftSlots all messed up:

```typescript
  useEffect(() => {
    if (Array.isArray(initialRoutes)) {
      initialRoutes.forEach((route) => {
        setShiftSlots(route.allocatedShifts);
      });
    }
  }, [initialRoutes]);

```

Thu 30 May 2024 09:46:19 AM CDT Has the value in the array and we need to find it: 179,

What other prior mechanism were established to show this?

When we do the visual test show the screenshot and what we’re expecting.

Start: Fri 31 May 2024 08:45:08 AM CDT

So we are going to get the switches working and write a test for it and make this test required for merging commits.

How does the switching even work?

## Modal Switches explainer

There’s a ModalSwitches component. Which takes in a parameter of shiftSlots.

```tsx
   <ModalSwitches
       employeeName={employeeName}
              employeeID={employeeID}
              workTimeForEmployee={
                editable ? localWorkTimeForEmployee : workTimeForEmployee
              }
              setWorkTimeForEmployee={setLocalWorkTimeForEmployee}
              shiftSlots={shiftSlots}
/>

```

shiftSlots variable which is being piped in is currently an empty object (09:25:09 AM CDT) but it should be allocatedShifts see the buggy useEffect written.

```typescript
  useEffect(() => {
    if (Array.isArray(initialRoutes)) {
      initialRoutes.forEach((route) => {
        setShiftSlots(route.allocatedShifts);
        console.log(272.3, shiftSlots);
      });
    }
  }, [initialRoutes]);

```

Alright, switches are back, now we have to write a test.

## Add Visual Regression testing to a Next.js project

“how to add visual regression testing to a Next.js project” What you want to do is go through the prompts in here: [https://nextjs.org/docs/app/building-your-application/testing/jest](https://nextjs.org/docs/app/building-your-application/testing/jest)

Make additional downloads: pnpm install -D @babel/preset-react  
pnpm install -D jest jest-environment-jsdom @testing-library/react @testing-library/jest-dom

After it you won’t have JSX access so get a .babelrc file in your root folder and it would look something like:

```.babelrc
{
    "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

### different types of testing besides attempting visual regression

I like these ‘e2e’ tests better: [https://github.com/ixartz/Next-js-Boilerplate/blob/main/tests/e2e/Guestbook.spec.ts](https://github.com/ixartz/Next-js-Boilerplate/blob/main/tests/e2e/Guestbook.spec.ts)

Start: Mon 03 Jun 2024 08:00:12 AM CDT

## Issue/Snag: “next.js syntax error missing initializer in const declaration”

If your getting something along the line of this issue, your issue is probably in your babel implementation. I added babel onto this repo with the intention of testing .jsx/.tsx my experience in testing and setting up testing environments isn’t robust enough to do this.

Alright, we are going to do testing but not use .jsx, our tests will be based off of something like, [this](https://github.com/ixartz/Next-js-Boilerplate/blob/main/tests/integration/Guestbook.spec.ts%3E).

Working on testing thru clerk: [https://clerk.com/docs/testing/overview](https://clerk.com/docs/testing/overview)

Working with playwright using clerk/testing, [view](https://github.com/clerk/javascript/tree/main/packages/testing#playwright)

This is a good test, [here](https://github.com/p-stoney/sisyphus/blob/main/e2e/.auth/login.spec.ts).

This testing with Clerk and making it good, its a huge headache.

The provided code doesn’t do enough to show it.

## Issue/Snag: “testing next.js application which use clerk and playwright”

They say cypress is still in expreimental in some articles so we use playwright.

This repo [here](https://github.com/p-stoney/sisyphus/blob/main/e2e/.auth/login.spec.ts), appears to be using a good testing architecture.

The issue I’m having is I can’t get outside of the ‘/’ route.

We will studying that repository for better testing within this environment.

Start: Wed 05 Jun 2024 12:53:21 PM CDT

## How to test Next.js, Clerk app

Okay, we are trying for the portable version.

You want to install puppeteer as well as the package for testing clerk, [@clerk/testing](https://github.com/clerk/javascript/tree/main/packages/testing).

I was getting the errors of:

```bash
  ({"Object.<anonymous>":function(module,exports,require,dirname,filename,jest){import { setupClerkTestingToken } from '@clerk/testing/playwright';
                                                                                      ^^^^^^
    SyntaxError: Cannot use import statement outside a module
```

Add on your tsconfig.json so you may not get these errors.

```.json

  "~/e2e": ["./e2e/*"],
   "~tests/*": ["./tests/*"],

```

… We won’t be using jest for this rather, playwright with vitest.

Follow these [instructions](https://nextjs.org/docs/app/building-your-application/testing/vitest) to quick start the program to have Next.js on your app.

… We will also be using Playwright over Puppeteer.

I keep on getting this error:

```bash
AIL  tests/e2e/app.spec.ts [ tests/e2e/app.spec.ts ]
Error: Playwright Test did not expect test.describe() to be called here.
Most common reasons include:
- You are calling test.describe() in a configuration file.
- You are calling test.describe() in a file that is imported by the configuration file.
- You have two different versions of @playwright/test. This usually happens
  when one of the dependencies in your package.json depends on @playwright/test.
 ❯ TestTypeImpl._currentSuite node_modules/.pnpm/playwright@1.44.1/node_modules/playwright/lib/common/testType.js:71:13
 ❯ TestTypeImpl._describe node_modules/.pnpm/playwright@1.44.1/node_modules/playwright/lib/common/testType.js:104:24
 ❯ Function.describe node_modules/.pnpm/playwright@1.44.1/node_modules/playwright/lib/transform/transform.js:256:12
 ❯ tests/e2e/app.spec.ts:4:6

```

Start: Thu 06 Jun 2024 10:01:13 AM CDT

Figuring out this Vitest stuff today.

### Fixing the ‘did not expect error’

The VS code extension seems to be working well.

If I go to /tests and run ‘npx playwright test’ it’ll work but running this command in the root it’ll show the multiple use error.

This issue thread helped to remedy the issue, see [here](https://github.com/microsoft/playwright/issues/13092).

Start: Fri 07 Jun 2024 09:56:15 AM CDT

The tests are running we now have to craft the tests to be Visual Regression and/or test functionality.

Following this [tutorial](https://www.youtube.com/watch?v=Y1eTK-j66PU).

This test works for a screenshot, [here](https://gist.github.com/MonteLogic/497dd5a9c12d2e0f80775225b8d3508e).

Now we have to get the auth stuff to work so we can vRegress test ‘main/schedule’.

Code repos with tests:

[https://github.com/p-stoney/sisyphus/blob/db60032679cd902d0302c9b91bff5415d8b856d8/e2e/.auth/login.spec.ts#L2](https://github.com/p-stoney/sisyphus/blob/db60032679cd902d0302c9b91bff5415d8b856d8/e2e/.auth/login.spec.ts#L2)

[https://github.com/colonial-heritage/colonial-collections/blob/main/apps/dataset-browser/e2e/content-pages.test.ts](https://github.com/colonial-heritage/colonial-collections/blob/main/apps/dataset-browser/e2e/content-pages.test.ts)

[https://github.com/clerk/playwright-clerk-nextjs-example](https://github.com/clerk/playwright-clerk-nextjs-example)

articles/docs: [https://blog.bitsrc.io/how-to-handle-authentication-in-e2e-testing-with-playwright-2d070c5815b1](https://blog.bitsrc.io/how-to-handle-authentication-in-e2e-testing-with-playwright-2d070c5815b1)

[https://playwright.dev/docs/auth](https://playwright.dev/docs/auth)

forums: [https://www.reddit.com/r/programming/comments/tdvxms/how\_to\_handle\_authentication\_in\_e2e\_testing\_with/](https://www.reddit.com/r/programming/comments/tdvxms/how_to_handle_authentication_in_e2e_testing_with/)

[https://www.reddit.com/r/programming/comments/tdvxms/how\_to\_handle\_authentication\_in\_e2e\_testing\_with/](https://www.reddit.com/r/programming/comments/tdvxms/how_to_handle_authentication_in_e2e_testing_with/)

[https://www.reddit.com/r/programming/comments/tdvxms/how\_to\_handle\_authentication\_in\_e2e\_testing\_with/](https://www.reddit.com/r/programming/comments/tdvxms/how_to_handle_authentication_in_e2e_testing_with/)

[https://www.reddit.com/r/programming/comments/tdvxms/how\_to\_handle\_authentication\_in\_e2e\_testing\_with/](https://www.reddit.com/r/programming/comments/tdvxms/how_to_handle_authentication_in_e2e_testing_with/)

Regardless of the authentication strategy you choose, you are likely to store authenticated browser state on the file system.

Start: Sun 09 Jun 2024 11:00:33 AM CDT

SO we need to focus on saving that auth state.

So how exactly is auth state stored?

… Okay for sisyphus, there is a saving of a storage state but what mechanism is automatically calling the [login.spec.ts](https://github.com/MonteLogic/sisyphus/blob/main/e2e/.auth/login.spec.ts) file.

According to this [tutorial](https://playwright.dev/docs/auth).

It looks like you don’t need global-setup.ts

It looks like according to this, we may not need to download and mess around with some JSON file which saves the auth state: example repo: [https://github.com/clerk/playwright-clerk-nextjs-example/tree/main](https://github.com/clerk/playwright-clerk-nextjs-example/tree/main)

Following [this](https://avinchadee.medium.com/how-to-auth-clerk-with-playwright-8acf0fc77ee5) article now.

That one is too complicated and there is no repo for it.

Now looking at this repo, [here](https://github.com/colonial-heritage/colonial-collections/tree/main/apps/researcher).

The repo says: Testing accounts are created for each test worker, and are deleted after the tests are done. In case the tests are interrupted, the accounts might not be deleted. Just to be sure, check for old testing accounts, and delete them. This is not needed for successful test runs, it’s just for keeping a clean testing environment.

What exactly does await clerkSetup(); do?



Okay, so these testing tokens just by pass bot detection it’s not about authenticating and saving the auth state: " await page.goto(“/”);

await page.locator(‘\[id=“\_\_next”\] div’).click(); await page .getByRole(“button”, { name: “Sign in with Google Continue” }) .click(); await page.getByLabel(“Email or phone”).click(); await page.getByLabel(“Email or phone”).fill(username || “”); await page.getByRole(“button”, { name: “Next” }).click(); await page.getByLabel(“Enter your password”).click(); await page.getByLabel(“Enter your password”).fill(password || “”); await page.getByRole(“button”, { name: “Next” }).click(); await page.getByRole(“button”, { name: “Continue” }).click();

const pageContext = await page.context(); let cookies = await pageContext.cookies();

while (!cookies.some(© => c.name === “\_\_session”)) { cookies = await pageContext.cookies(); }

await pageContext.storageState({ path: authFile }); "

So, we have to use the login from here and then saving it as a JSON file I guess.

[https://github.com/clerk/playwright-clerk-nextjs-example/blob/ef46d2972a764b36ce4a238b258af374e9e86542/e2e/app.spec.ts#L11\`](https://github.com/clerk/playwright-clerk-nextjs-example/blob/ef46d2972a764b36ce4a238b258af374e9e86542/e2e/app.spec.ts#L11%60)

Okay, so this works for an isolated test see:

```ts

// I feel like if you run the test right here
// it doesn't hit the global pre-requisite test.
test.describe('app', () => {
  test('sign in', async ({ page }) => {
    await clerkSetup({ publishableKey, frontendApiUrl });

    await setupClerkTestingToken({
      page,
      options: { frontendApiUrl: process.env.CLERK_FRONTEND_API_URL },
    });
    await page.goto('/main/schedule');
    await expect(page.locator('h1')).toContainText('Sign in');
    await page.waitForSelector('.cl-signIn-root', { state: 'attached' });
    await page
      .locator('input[name=identifier]')
      .fill(process.env.E2E_CLERK_USER_USERNAME!);
    await page.getByRole('button', { name: 'Continue', exact: true }).click();
    await page
      .locator('input[name=password]')
      .fill(process.env.E2E_CLERK_USER_PASSWORD!);
    await page.getByRole('button', { name: 'Continue', exact: true }).click();
    await page.waitForURL('**/main/schedule');
    // await page.waitForTimeout(2000);


    await page.waitForLoadState('networkidle');
    await page.screenshot({ path: 'screenshot6.png' });
  });
});


```

Start: Mon 10 Jun 2024 11:00:00 AM CDT

- I think what I may do is list the test which I am trying to fulfill and then provide commentary on that test.
    
- I don’t like this work notes general sort of look cause it’s too vague. I wouldn’t mind an overarching type of thing underneath the toDo chamber or something like this but I think the notes would be better off if they were based on a a Test via the TDD arrangement we are aiming for.
    
- I wonder if its easy or not to execute tests from a mobile device.
    

… I guess I just do a simple node app where I am testing it and I just test cbud.pp or rather an alternative deployment.

Ideally, only cbud.app would have production credientals showing or I can have an a domain called test.cbud.app and use that for testing puposes and that’ll have a development deployment of Clerk.
