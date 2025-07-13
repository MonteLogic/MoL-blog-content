---
title: "Contractor Buddy Work Notes - 3"
date: "2024-04-11"
---

# Starting part 3

Fri Mar 22 02:01:57 PM CDT 2024

I was running into the issue: “Uncaught Error: OrganizationContext not found”

I decided to ditch const { membership } = useOrganization();

And all of this stuff: const rolesShow = () => { if (membership?.role === “admin”) { return “Role: Admin”; } if (membership?.role === “basic\_member”) { return “Role: Employee”; } if (membership?.role === “guest\_member”) { return “Role: Guest”; } }

So, we have to get the current org id the user is on and then tie that to the user useUser object.

“get role of user within organization clerk”

[https://dev.to/musebe/implementing-role-based-access-control-in-nextjs-app-router-using-clerk-organizations-566g](https://dev.to/musebe/implementing-role-based-access-control-in-nextjs-app-router-using-clerk-organizations-566g)

From that article,

The navbar: [https://github.com/musebe/nextjs-clerk-organizations-rbac-authentication/blob/711ed2c78e9c96dcb8eed3cc6c8c1bc22fc89aa0/components/Navbar.jsx#L8](https://github.com/musebe/nextjs-clerk-organizations-rbac-authentication/blob/711ed2c78e9c96dcb8eed3cc6c8c1bc22fc89aa0/components/Navbar.jsx#L8)

Which will use user utils: [https://github.com/musebe/nextjs-clerk-organizations-rbac-authentication/blob/711ed2c78e9c96dcb8eed3cc6c8c1bc22fc89aa0/utils/userUtils.js](https://github.com/musebe/nextjs-clerk-organizations-rbac-authentication/blob/711ed2c78e9c96dcb8eed3cc6c8c1bc22fc89aa0/utils/userUtils.js)

Start:

Sun 24 Mar 2024 12:04:56 PM CDT

I forgot to save because it doesn’t work unless you hit :wq , :w is just for local stuff.

The only thing I can do is :q then, when in terminal ctrl + p then ctrl + o Also, use !! when in csh to run the last command.

Working on getting the default route to show

Working on creating search functionality integrated with URL search see: [https://dev.to/stephengade/build-a-functional-search-bar-in-nextjs-mig](https://dev.to/stephengade/build-a-functional-search-bar-in-nextjs-mig) or [https://nextjs.org/learn/dashboard-app/adding-search-and-pagination](https://nextjs.org/learn/dashboard-app/adding-search-and-pagination)

I’m on this one: [https://nextjs.org/learn/dashboard-app/adding-search-and-pagination#4-updating-the-table](https://nextjs.org/learn/dashboard-app/adding-search-and-pagination#4-updating-the-table)

Not sure if this is going to work for my use case: " export default async function Summary({ searchParams, }: { searchParams?: { query?: string; page?: string; }; }) {

"

Start: Wed Mar 27 10:13:34 AM CDT 2024 Redirect everything to cbud.app

Move schedule to /main

Home page of ‘/’ which is going to say view app.

… The issue which I am facing is that I would like to persist state between the routes and I’m pretty sure I’m going to have to use Context to get this done.

“Using query parameters instead of browser storage” From, [https://dev.to/jeffsalive/solving-the-challenge-of-state-persistence-in-nextjs-effortless-state-management-with-query-parameters-4a6p](https://dev.to/jeffsalive/solving-the-challenge-of-state-persistence-in-nextjs-effortless-state-management-with-query-parameters-4a6p)

Note, anything is better than using Redux.

I think its going to be a mix of “query parameters” and use context.

…

What I do know is that, the link on the Summary page is just /summary and not anything special, what if we saved the summary button link as something like: " “/main/summary?date=2024-03-06&route=626L4” "

This is the last saved URL state / ‘query parameter’ in the URL bar.

The issue is the other one is a the summary button is apart of a server component.

It looks like I’m going to have to rewrite ui/tab-group.tsx and account for the client interactions.

I’m going to have to rewrite tab as well (ui/tab.tsx).

Or pass it from local storage if I’m unable to persist the state in the manner I am trying to do.

I’m pretty sure setState doesn’t work for this router thing, and that I would have to use React context in it’s totality to work effectively or use local storage.

I think we could use React Context for this but that would complicate the app and I’ve yet to gain experince in React Context.

So I’m going to use Local Storage and the client side Tab Group will just nab that from the Local Storage and hopefully its fast enough.

I gotta move that new ui thing into a different component so it doesn’t mess up the rest of the app.

Start: Thu Mar 28 07:15:00 AM CDT 2024

What are the limits of setState?

Features: End of shift checklist

Viewing this: [https://montelogic.com/wp-content/uploads/2024/03/Viewing-client-context-for-dynamic-url-functionality-2024-03-28-at-07-29-42.png](https://montelogic.com/wp-content/uploads/2024/03/Viewing-client-context-for-dynamic-url-functionality-2024-03-28-at-07-29-42.png)

“react context for multiple values”

I think that we could do multiple setStates use the context provider but the code could get pretty verbose.

So, we could do something like, <MyContext.Provider value={{ value: \[value, setValue\], value2: \[value2, setValue2\] }}

Okay, so starting to wrap summary selection in a context provider so those slugs can be changed via context.

Start: Fri Mar 29 09:24:32 AM CDT 2024

Add the timecard page to the main thing also have a drop down for Temple heats so the Ayers/Enidan template and other trucking companies templates as well appeared also add an option for make your own template.

We have to make it so that there is a button which says select template and to the side of it it will say view example template.

Side note: I wonder if there is a cli library which has select by arrow functionality so that we could create a work flow which would be like select the arrow for the work flow and it is then immediately instantited.

We also need a time range which would by default be set to the current date and then there would be like bi weekly, or custom date range selection.

Before I write all of that business logic on how to do timecards I’m going to sit down with the lady who gave me the timesheet.

2x3 - Questions: Trip number, I’m guessing that means the runs, so the first morning run for a run, would be 1 and so on until 4.

Paused: 2:20

But for smaller routes, it would just go up to 2.

Mon 01 Apr 2024 09:46:28 AM CDT Notice, no April fools reference today.

Today, I’m having what appears to be issues with my cname stuff because I changed from my old domain of contractbud.app to cbud.app and if you go on cbud.app it’s redirecting to the old one. I think this may have to do with the cnames, so I’m going to wait 48 hours and hopefully it resolves. Note, I did a perminant redirect rather than doing the recommeded\* (by Vercel) temporary redirect. So I think this may be one of the reasons why its taking so long to update.

Covering: New domain is redirecting old domain “clerk”

Also, in the future I am skipping Namecheap domain buying and transfer for web app related stuff, and using the Vercel domain buying marketplace.

Okay, I think today I’m going to work on a fresh buyer’s journey, so someone from Boise, ID opens up the app and they can find use in it. Or someone in my local area can find even more use in it because they will have data already about the local area.

Okay, so now we are working on a /startup page.

I don’t want any users to view stuff they shouldn’t or edit stuff they shouldn’t.

… Okay, so we have to make it so that only certain orgs can see their own stuff and if a user has a personal account he can see his personal account.

Looks like I’m why behind on privilege logic.

How do I know the difference between a personal account and an organization?

It discriminates to only show user whose logged in which is some discrimination logic already implemented.

…

Okay, so now I just figured out the point of that branch is to get timecard working good for a certain company. So, I’m going to finish that logic before I forget then after that work on private-privileges branch.

Start: Tue 02 Apr 2024 01:16:13 PM CDT

So right now based on the input we are trying to render/generate a template but it’s, challenging.

This is what I’m working on: [https://stackblitz.com/edit/react-starter-typescript-rwb6hm?file=App.tsx](https://stackblitz.com/edit/react-starter-typescript-rwb6hm?file=App.tsx)

I wanted to do a case switch function but we’ll have to do something like:

```typescript
// Define a mapping between cases and functions
const functionMap: { [key: string]: () => void } = {
  case1: function1,
  case2: function2,
  case3: function3,
};
```

I don’t like the way this looks but ig it works:

```typescript
   <Menu.Button onClick={async () => {
                        const result = await generateTimeCardMapFunc[timeCardTemplate];
                        result;
```

So apparently, just instantiating the object literal runs it.

I’m giving up on the following ‘solution’:

```typescript
    const generateTimeCardMapFunc: { [key: string]: Promise<void> } = {
        1: AyersTemplatePDF([{
            id: selectedEmployeeID,
            routeNiceName: selectedEmployeeName,
            routeIDFromPostOffice: '',
            routeIDRandomGen: '',
            employeesWorkingInfo: null,
            summary: null,
            organization: '',
            organizationID: '',
            dateScheduled: new Date(),
            dateAddedToCB: new Date(),
        }], selectedEmployeeID)
    }
```

Okay, so if by tomorrow, its not working, I’m just to delete my clerk app and redo it.

Start: Wed 03 Apr 2024 12:46:18 PM CDT

I’m trying to figure out what is forcing a user to auth so we can dismantle it.

I’m going to try to hard code the sign url within the ClerkProvider prop:

```Typescript
    <ClerkProvider signInUrl='cbud.app'>
```

Okay so that, ^^^ works.

Side note: if I would like to get a mentorship what I could do is find someone who is further along, document and annotate their work.

If i were to do it again I would just run a new app instead of banging my head on the wall trying to get those redirects to work.

This a better idea because way more projects are created than projects are pointed to a new URL so the dev tooling and build tooling would thus be way more optimized for creation rather than redirection.

I would assume the vast majority of redirections are simple redirections and not being tangled up by complex auth managers.

Start: Fri 05 Apr 2024 12:41:46 PM CDT

Okay so I had a really hard time getting my domain switched from [https://contractorbud.app/](https://contractorbud.app/) to cbud.app

This was mainly due to old cname issues and clerk didn’t look like it was updating the main auth anchor URL.

I think was due in part to Clerk is not used to such requests. However, Clerk is extremely optimized for new project instantiations.

It’s also a good idea to keep up the new one and not delete it (out of frustration) so you can copy the env variables.

toDo: Get a headset and do STT for the notes so more is recorded. I could have the recorder being triggered by a macro and then its good STT (speech to text) to record stuff.

The mic should look like this:

And have a REALLY loud mic, so STT can have an easier interpreting it.

… Back to working on CB features cause the redirect problem has been fixed.

Ok, currently there is not a way for the db to know how many users the system has.

So, we need to figure that out and add it to the Users table.

“On account creation clerk in a next.js app”

This is what I’m looking to do: [https://www.youtube.com/watch?v=NgBxrIC1eHM&t=318s](https://www.youtube.com/watch?v=NgBxrIC1eHM&t=318s)

Or more precisely: [https://clerk.com/docs/integrations/webhooks/sync-data](https://clerk.com/docs/integrations/webhooks/sync-data)

So we gotta figure out webhooks.

Start: Sun 07 Apr 2024 02:58:03 PM CDT

Working on fresh install path.

This means knowing who is in the database of users so authorization can be divvied out.

Got webhooks to work, the thing is that the endpoint needs to be:

[https://yourapp.com/api/webhooks](https://yourapp.com/api/webhooks)

I don’t like the fact that I think I can only test the webhooks on prod instances of Clerk because of the redirects.

Start: Mon 08 Apr 2024 08:26:14 AM CDT

Time to work on syncing clerk stuff with Prisma.

I’m looking at this and re-evaluating whether to use webhooks: From, [https://www.timveletta.com/blog/integrating-clerk-and-planetscale-in-your-nextjs-applications](https://www.timveletta.com/blog/integrating-clerk-and-planetscale-in-your-nextjs-applications) " One mistake I made initially when using PlanetScale and Clerk was trying to model user data within my database schema, something Clerk is very good at. Previously, I had set up a webhook within Clerk to create a user in the database when a user signs up. However, this operation is asynchronous and sometimes caused timing conflicts because the database would try to pull data for a user that didn’t yet exist. In the future, I would consider using something like Clerk metadata for this purpose. " Clerk metadata info here, [https://clerk.com/docs/users/metadata](https://clerk.com/docs/users/metadata)

Okay, so private metadata: " { “example”: “data” } "

So, I think I’m going to get rid of the Users table and rely on clerk’s private Metadata.

… So, I guess the api folder is for network stuff(?).

Okay, so I know its going to be just users first.

I think I’m going to check Clerk to see if the user has private meta data and/or if they are apart of organizations if both of these statements aren’t true, show nothing.

Start: Tue 09 Apr 2024 11:39:12 AM CDT

I think I’m going to make a Users table in the future just for backups.

… If there is no

Okay, so if there is no orgID then lets put the user id

Then we will check the work time stuff to see if a user has entries related to hi m/her.

I’m thinking that I’ll have to use front end stuff to figure out orgs because current org from what I understand is only viewable on the frontend.

I think I might make a sample page which shows the timecard functionality.

Okay, what I’m doing is just do it all based off of orgId.

Okay, so every time a user submits to WorkTime they will need to have organizationID.

It would be dope if there was a sample page, user interacted with it and then in order to save it or print out timecard they would have to create an account.

Start: Wed 10 Apr 2024 11:19:33 AM CDT

So, I have to connect that showing logic stuff to organizationID

Okay, lets keep issuing authorization logic.

Working on adding employee form which will include orgId.

Gotta figure out how to get orgId from the client side.

This is my api file to try to get the orgId from the API:

```typescript
import { NextRequest, NextResponse } from 'next/server';
import { clerkClient, currentUser, auth } from "@clerk/nextjs";

export async function GET(req: NextRequest, res: NextResponse) {

    const { userId, orgId } = auth();
    const currentUser_ = await currentUser();
    const user = userId ? await clerkClient.users.getUser(userId) : null;
    // console.log({ userId, currentUser_, user });
    // console.log(15, user?.privateMetadata);
    console.log(14, orgId);

    if (req.method !== "GET") {
        return NextResponse.json({ message: "Method not allowed" });
    }
    try {
        return NextResponse.json(orgId);
    } catch (err) {
        console.error(err);
        return NextResponse.json({ message: "Something went wrong" });
    }
}
```

Now we just have to call that file and hopefully it will retrieve the data in time because any other time I try to call from the client to try to get the organization id I get an error of: Unhandled Runtime Error

Error: SessionContext not found

```typescript
const { session } = useSession();
     |                              ^
  48 | console.log(47, session?.user.getOrganizationMemberships())
  49 |
```

Start: Thu 11 Apr 2024 01:54:07 PM CDT Started using this plugin for showing my gists which I use as work notes: [https://wordpress.org/plugins/gist-github-shortcode/](https://wordpress.org/plugins/gist-github-shortcode/)

Start: Sun 14 Apr 2024 12:45:15 PM CDT

This looks like its not even adding employee. app/api/add-employee/route.ts

Start: Mon 15 Apr 2024 09:08:02 AM CDT

Okay, so I gotta make it so if a user sees no Routes they are shown text which says, to create route, click here. - done

So I have to create shifts with their accommodating times.

So, I gotta add shifts and the default will just be afternoon and morning with a simple time.

Also, I would like to have a number slot for the add work time so that it can be very precise.

Start: Tue 16 Apr 2024 10:43:22 AM CDT

Problem I’m having now is that I don’t quite now what to do first because I think I’m at 1.0, so need beta testers.

I need to work on getting the Summary page not opaque.

If you click on it, it should show a spinner where it loads the summary info and shows the summary for the current day.

Before I do that, what I want to do is make the landing page ‘/’ not automatically redirect to a sign in page. In order to this just add ‘/’ to the public routes in the middleware.

Start: Working on the summary-page because its very useful for the daily stuff.

Thu 18 Apr 2024 04:59:44 PM CDT

Make the current day default for showing.

The page I’m working on is a page, I was working on 3 months ago with loads of ternary operators. Ternary operators aren’t good for readable code.

This block:

```typescript

    const [routeIDs, setRouteIDs] = useState(initRoutes.initRoutes[0]); // Add the 'routes' property with an empty array as the default value
    console.log(57, routeIDs);
    console.log(58, routeIDs[0]);

    // {routeIDs && routeIDs.routeIDInfo && routeIDs.routeIDInfo.routes && routeIDs.routeIDInfo.routes.length > 0 ? (
    //     routeIDs.routes.map((route: [string, string]) => (
    //         <option key={route[0]} value={route[0]}>
    //             {`${route[0]}-${route[1]}`}
    //         </option>
    //     ))

```

… I just now remember that routeID is the summary of it.

When you are coding on a feature try to document it, write readable code and do it right the first time because its going to be hard to remember.

routeIDInfo is a column within the database, so I thought it wasn’t there because of erroneous code but the value was undefined cause it wasn’t written into the db.

Working on this file: app/api/search-shift/route.ts

Start: Sun 21 Apr 2024 10:50:42 AM CDT

Okay, so a successful app should have easy invitations for viewing content.

Working on the app, I’m getting the error of: shifts.find is not a function:

```typescript
 |
  212 | function getActiveShifts(id: string): void {
> 213 |     const location = shifts.find((entry: any) => entry[0] === id);
      |         

```

… We only want view summary of day to pop up after the drop down or calendar is toggled and the default state is always the current day.

Right now, there’s no WorkTime record to even add onto it with.

…

This code base has a bug with date and time, I think if its past midnight in GMT, it goes forward.

This is the buggiest app of all time!

I’m working on making it so that a drop down selection updates the form.

I have to make an article on this for good CRUD action for form logic.

Start: Mon 22 Apr 2024 09:48:44 AM CDT I am going to write a write-up/article on this topic

So, I gotta add a shift thing to the Routes page.

…

I just found out Tailwind UI works on my template.

End part 4
