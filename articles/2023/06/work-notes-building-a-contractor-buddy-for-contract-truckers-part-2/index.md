---
title: "Work Notes: Building a Contractor Buddy for Contract Truckers - Part 2"
date: "2023-06-18"
---

\[-\] **528x5** - Mock the REST api post call for Twilio, this will save money and time.

\[ \] 51cxt8 - Work on the UI for the scheduling.

\[ \] 1489fs - Redesign UI to fit this [menu](https://github.com/MonteLogic/side-menu-tsx)/[codesandbox](https://codesandbox.io/s/side-menu-forked-zms2d8?file=/index.tsx).

\[ \] 425x8m - Isolate the problem of why some weren't. This issue may be challenging.

\[ \] 52v4gm - Do other things besides the text message call. Work on the UI for the scheduling. Have it be so that you won't need\* to look at the texts to get what's going in the trucking company.

\[ \] 852vsm - Quickbooks plugin to tie Trucking Buddy with Quickbooks.

\[ \] 95fs - I need to make dev url and prod url.

\[ \] 418fs - Backup, import and export receipt information ideally in a way which can be imported by Quickbooks.

\[ \] 25af4 - How do I add a table in Prisma without dropping the whole db?

\[ \] 1452ag - How do I import from a csv file into a Prisma table?

\[ \] 15gsbg - Backup from a .csv file.

\[ \] 14ags - Add breadcrumbs at the top of the screen.

\[ \] 234asd- Switch to SQlite

\[ \] 516faw - Get Chase banking API linked as well as be able to link to smaller banks/credit unions.

**528x5** - I need to work on the mock call because I don't have Twilio., so let's see what that mock call looks like.

I guess the fetch request would look something like this:

```
const postData = {
  ToCountry: 'US',
  ToState: 'CA',
  SmsMessageSid: 'SMXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX',
  NumMedia: '0',
  ToCity: 'Los Angeles',
  FromZip: '94107',
  SmsSid: 'SMXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX',
  FromState: 'CA',
  SmsStatus: 'received',
  FromCity: 'San Francisco',
  Body: 'Hello from Twilio!',
  FromCountry: 'US',
  To: '+1415XXXXXXX',
  ToZip: '90012',
  NumSegments: '1',
  MessageSid: 'SMXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX',
  AccountSid: 'ACXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX',
  From: '+1415XXXXXXX',
  ApiVersion: '2010-04-01'
};

fetch('http://your-node-server-endpoint', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(postData)
})
  .then(response => response.json())
  .then(data => {
    // Handle the response from the server
    console.log(data);
  })
  .catch(error => {
    // Handle any errors that occurred during the request
    console.error('Error:', error);
  });
```

This is the [URL](https://contractor-trucking-app-rewrite-2.vercel.app/) of the main app, I think that's the main branch but not for sure. This [URL](https://contractor-trucking-app-rewrite.vercel.app/api/receive-texts) is where I post to.

What if I have the mock file in my app and all I have to do is run a command from the terminal to run it. Like npm run dev:send-mock-sms

...

I just figured out the server and the client side environment variables are treated differently in t3.

...

528x5:

I sent a successful mock http request.

Here is the [gist](https://gist.github.com/MonteLogic/508cfe05aaa1f0d20ccf08c461fe15a7). This file is in, 'tests/mock-sms-send.ts' of a t3 project.

This Twilio [doc](https://www.twilio.com/docs/messaging/guides/webhook-request) is very important for understanding the post request that they send.

\--

Note from the future: Tue Sep 19 2023 13:57:19 GMT-0500 (Central Daylight Time)

Will this work without credits though and what is missed by not using the Twilio API endpoint from Twilio but mocking it locally?

\--

Now that I got a mock test, I need to work on UI for the receipts now becuase this is the most important thing.

...

That would be dope for the mock test I could attach an image and in the response it will say how much is on the receipt.

...

I guess I'm going to have to work on the Next router with this [page](https://codesandbox.io/s/side-menu-forked-zms2d8?file=/App.tsx:907-915).

Notice, this is how you get the menu on this [file](https://codesandbox.io/s/side-menu-forked-zms2d8?file=/App.tsx):

```
        <MenuWrapper
          menuOptions={menuOptions}
          renderMobileToolbar={Toolbar}
          menuProps={{
            onLogOut: () => alert('Logout clicked'),
            renderHeader: MenuHeader,
          }}
        >
```

I think I'm going to test it out on this [page](https://github.com/MonteLogic/contractor-trucking-app-rewrite/blob/dev/src/pages/trucks/index.tsx#L0-L1).

I'm going to use [Responsive Drawer](https://codesandbox.io/s/s7qnyw?file=/demo.tsx) instead because it looks like the previously posted solution is outdated.

So, I need to integrate this [file](https://codesandbox.io/s/s7qnyw?file=/demo.tsx).

Then there will be a page called Employees and then on there you'll be able to see which receipts are responsible for which employee.

This [CodeSandbox](https://codesandbox.io/s/side-menu-forked-zms2d8?file=/App.tsx) highlights menu items.

Misc notes:  

"

I have to add another accouunt which is cash and then hopefully have that cash deduction be tied to an atm withdrawl or have the source be in some way related.

I think I am going to look into connecting to like a Chase API to get bank spending information.

I would like to have an option to directly take a picture on the Desktop as well as adding an image file.

[image](https://quicken-prod-documents.s3.us-west-2.amazonaws.com/original/384071639966975232_Transaction%20receipt.jpeg_image?X-Amz-Security-Token=IQoJb3JpZ2luX2VjEL7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCiAgJrtvj1Eyp4ecyxHUYrFyOAEeKHwKLwfGwTlMg2ngIhAL5FdHK2yfpkUmVfG4s5q2NyDZOl8bY7LTVm7Ut6FIqsKvQDCBcQBBoMMDkwNDk2MDUxNjgwIgw6qH3pBpdeLwOgbkgq0QMwHNu2Yjyvwsyq60XIA%2B%2Bar%2FMqoimuGcDAiMXxsihwaiLGzGnrvsGfajb3mQ8msslkt7lwPUE5XttomlFReq0gzbAdtQ%2FTC2h%2FnD34OQtJi3hH5koVIvyS7YyMKNjd1lexMg0UmbbH88BgJASolG37N7Ri6sQjAdK%2Bz7HJzPzSknvmUk3wyoTuRZSwhY35%2FcZkloz71NfEvlyW%2BEKYR55bpgKU5lE4wN02Yca4JOoammizC28rscK0W1zzQOVxqqgNmj68pPc9vyRUJV53JYZHAvcGd190uD%2FhLq7hRyqKyJ5avfgTcOq7P0FLamteWsPh0f%2B7HBvoeyS9OIFk%2FiSVbrZxfnwcc8OXkAKQQxwKMVSIqUBkKjrgueUy8BSfwU6%2BCdV7hitLS9sRuqeo3N68scvVeH1vKBgF%2B19LXVPSN7iO5RR5J309GvcE2ycqsEjLaiabOfqM5X4iMsRWtc6aGqhJsRU5WDjmZC8YBLlVTx8qsYzlEzz2eg1VtGQjgYQOSIrmVZQV5G2V%2FwjqU7R1trzyGwTqR5WBY1VIoO4nAcnoMimPGeMN9i7TQhUFvQ6azTcU7CgH%2BR2PI7VqT4%2FvG9A8zLQDYMB%2FuWKIJGXhcG0wgJCnpAY6pAEyWX2QWAJyA1g%2Fp1k6%2ByfwQwCrgDOToKvFrnsfgcRi%2FU%2F3JCjaoK79c2VeepBCa5LxrU415T0Ah%2FJHjlpCm0Up%2BAfL%2BA1gK1XroC%2FlOt3XHBRYPNuTAOIVpZr2wc%2F6uTAfw8OdZL3OSlc%2F2bYs%2BvoQO3Oco5y%2F5Nh0fRCaYNHB0%2FnsV8YwtxSGM1VNM8YuQr3yHchuyq%2BpkeN77UTfJzJAy632kg%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20230614T151239Z&X-Amz-SignedHeaders=host&X-Amz-Expires=3599&X-Amz-Credential=ASIARKEP4FHQDAQUS57X%2F20230614%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Signature=62fbc6a9dce7e0aa1bae79df6c23c2abc287463aabc8e53e9d1046d8a6a56899)

"

Fixing this type error:

"  

Type '(data: FormData) => Promise<void>' is not assignable to type '(formData: FormData) => void'.  
Types of parameters 'data' and 'formData' are incompatible.  
Type 'FormData' is missing the following properties from type 'FormData': employeeName, dateHired, dateAddedToCB, amtOfGasPurchasedThisMonth, eligibleRoutests(2322)

AddContactForm.tsx(21, 3): The expected type comes from property 'onSubmit' which is declared here on type 'IntrinsicAttributes & AddContactFormProps'  
"

I'm getting an API timeout error but [this deployment](https://vercel.com/montelogic/contractor-trucking-app-rewrite/ExA3kcaa5hKeYV945H6dxSMx9AtA) works.

I need to work on a test so that when a website is done, there is test to make sure there is no 400, 504 errors, etc. So I'm not coding for a day and a half and have to get back to find the error.

Selected menu item appear to be where the issue is at.

This [commit](https://github.com/MonteLogic/contractor-trucking-app-rewrite/commit/1222b9cd3d5e2c71dd95b272d4a7d9ad0dca092c).

I think the 504 error I am running into has to do with Vercel messing up.

So, factoring out those icons worked because they weren't SSR.

Finding the commit which I is pre-revert.

This [commit](https://github.com/MonteLogic/contractor-trucking-app-rewrite/tree/e66ee5dffdf8484de8346df64347eb43df104ac4) - 1.

So bringing it back up.

...

Make the employee addition be very mobile friendly.

I want to make the addition to be at the bottom of the page.

Make Employee page table mui.

...

The request:

```
await fetch("http://localhost:3000/api/receipts", {
    "credentials": "omit",
    "headers": {
        "User-Agent": "Mozilla/5.0 (X11; Linux x86_64; rv:104.0) Gecko/20100101 Firefox/104.0",
        "Accept": "*/*",
        "Accept-Language": "en-US,en;q=0.5",
        "Content-Type": "text/plain;charset=UTF-8",
        "Sec-Fetch-Dest": "empty",
        "Sec-Fetch-Mode": "cors",
        "Sec-Fetch-Site": "same-origin",
        "Pragma": "no-cache",
        "Cache-Control": "no-cache"
    },
    "referrer": "http://localhost:3000/employees/clj4doynn00007rn047efx577",
    "body": "{\"dateSent\":\"2023-02-02\",\"employeeName\":\"\",\"dateTimeOfGasBuying\":\"00:12\",\"amtOfGasPurchased\":\"54\",\"gasTanksAfterFillings\":\"56454\",\"img\":\"https://wp2mag.com/wp-content/uploads/2023/06/th-3080913266.jpeg\"}",
    "method": "POST",
    "mode": "cors"
});
```

If you getting a 500 error it's not setup at all if your getting a 400 error then your not sending the right fields. In both cases of this happening make sure to check the node terminal running the app for further assistance.

...

Add receipts attributed to each employee, also, I think may add employeeId on Receipts table.

Updated schema.prisma for this.

I also want to reset the field when an entry is added. I also have to add the list of receipts per employee and I would like this to correlate with employeeId rather than employeeName.

Okay so in Prisma if you want to add a column you have to delete the whole table otherwise you'll have to reset the whole db.

...

I need to add the route, and I think I can get rid of that truck extensible type.

I think once the truck drop down is selected than the TruckID can just be equated and filled in.

Side note: It's good to write down your internal dialog.

...

So when you click on /employees

Receipts area, debts area and schedule area.

If your on the employee's receipts page the url is

employees/clj4doynn00007rn047efx577

it should be employees/receipts/clj4doynn00007rn047efx577

With the two other areas as well.

...

I need to add the route, and I think I can get rid of that truck extensible type.

I think once the truck drop down is selected than the TruckID can just be equated and filled in.

...

The difference is we won't know the employee off the bat and we don't even know the TruckID on Employee receipt addition logic.

The input order:

```
The Route:

Vehicle Type: Truck or Car:

Vehicle:
```

I think I'm going to only use SQLite.

I feel like I'm just trying to ratchet down the latches versus just getting the project done.

![](images/Untitled-1-1024x499.png)

There needs to be a pane which shows active balance. There also needs to be a payments history.

[Audio](https://recorder.google.com/2dfe6549-ba6c-43de-b104-60b2fe3a1abc):

"

So like a bottom under the thing, it needs to be like, like one for, like, the receipts, like, open time card. So be like, three things like receipts time card. And then, like, just like, like timeliness, like, showing up and it'll be like three columns.

It won't be too confident like three buttons on each one and it'll be like you know be like a single page app like like it be like snappy I'll be like first come show like receipts and then like and then the second column show that and then like on top it'll just be like Like a link to it so people don't get confused.

"

toDo:

I want there to be a divider between the added receipts and it'll be like the day and the day month, year, format. Also, it would be cool if you could show how much they still have in their balance after they paid for the receipt.

I want the id for the db to have the id for the route be the first characters if that is at all possibles.

Redo the table on the Trucks page.

So I tried to do a stack today which included local development on my phone and then I learned Prisma only ships binaries for the Debian AArch64. So I got it to work on that distro on UserLAnd and then I fiddled around trying to dev with both Termux and UserLAnd. Then I figured out you can have multiple terminals on UserLAnd by pulling the drawer from the right and then clicking new session.

Working on the DateTime stuff for good createdAt logic.

Looking at this [file](https://github.com/t3dotgg/chirp/blob/main/prisma/schema.prisma).

I figured that out.

I need to get different tabs for the employees part, I also want to get the Trucks section worked on better for receipts too.

Need to make a nested list so people know where they are at in the application, [demo](https://codesandbox.io/s/5zh2kf?file=/demo.tsx) or [here](https://codesandbox.io/s/github/modularcoder/tutorial-react-tree-menu/tree/master/stage4-react-router?from-embed). Also need to work on breadcrumbs too([demo](https://codesandbox.io/s/tn3w2w?file=/demo.tsx)).

...

Got calendar to show, I have to have a window open on each day click and then go from there.

...

NO errors on Prisma still need to 'regenerate' the database.

I am trying to figure out how to fufill the date object with stuff, so I can have an easier time.

Okay, I am going to work on this one:

"

Date Selected:

2022-04-18  
Morning  
Mid-day  
Evening

"

```
    // Figuring this out 
    const [isAfternoonWorked, setIsAfternoonWorked] = React.useState(false);
```

So now that I got that good (the work time keeper) for employee (timecards), I want to do logins so I can use it myself.

Or I could just add myself as an employee and then go from there.

...

The problem is it gets all of them rather than looking for the name/employeeId.

The query is showing all of the records.

So I just need to filter down the results.

I want to get Contractor Buddy usable in the timecard sense and then focus on EC then after that work on the receipts for it as well as social login.

...

For CB, I need to get it from findMany to get it where it's only finding the employeeId and then I don't think I need to discriminate upon addition.

..

The modal isn't resetting state on blank ones. I also need to redo the url to point to employeeId rather than id.

\[ \] Reset modal state to reflect other empty ones rather than persisting.

Back to EC then after that work on the receipts for it as well as social login.
