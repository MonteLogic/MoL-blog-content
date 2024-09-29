---
title: "Contractor Buddy Work Notes - 2"
date: "2024-03-22"
---

Start:  
2024-02-17 09:46:17 CST

Side note:  
I would like to make a Torah reading app and Shabbes guide for Orthodox Jewish services. This would be using Capactior with Next.js 13.

Start:  
2024-02-18 08:42:42 CST

I NEED to make a page for deliquent receipts.

Start:  
2024-02-19 17:20:52 CST

So, let's clean up that function that we made also, lets change the domain to cub.app

I need to iterate over text boxes, so there should be 4 text boxes or for however many shifts available.

If there aren't viewable text boxes just click create entry.

Instead of narrowing the tiny object, let's do a big object.

So if there is nothing there, then I am going to have a Plus button svg you can click on and a textarea will display.

Start:  
2024-02-20 10:53:34 CST

Put nice name next to the id with a - after.

Need to create shift adjustor page because Pleasant Plains, shouldn't have 4 shifts and should only have two.

Create summaries for already scheduled days but no summary.

Create summaries for new days which haven't been scheduled, but warn the user there hasn't been a schedule.

Upload images.  
Slide show for images of a day,

Start:  
2024-02-23 10:25:02 CST

- View images under each shift

- Easy link which is like very easy way to get in but only for a link, and only can access schedule and summary page. This will be usable for simple phones.

Side Note:  
Working on creating accounts for

Have OAuth preferably for Google using Clerk and it'll be done in a popup or just do the Captcha and use WordPress's system of accounts rather than duplicating them through Clerk.

Login noCaptcha by Robert Peake and Contributors

Also, disable the feature for when users change password you get notified or change the email to a different rather than your primary email for non critical updates.

Anyways, I just figured out I am trying to combine both operations or I could just do one and the hook would do what I'm looking to do.

Okay, this is what it currently looks like:

"

```
       <UploadButton
                        endpoint="imageUploader"
                        content={{
                            button({ ready }) {
                                if (ready) return <div>Upload Image for Afternoon</div>;

                                return "Getting ready...";
                            },
                            allowedContent({ ready, fileTypes, isUploading }) {
                                if (!ready) return "Checking what you allow";
                                if (isUploading) return "Seems like stuff is uploading";
                                return `Stuff you can upload: ${fileTypes.join(", ")}`;
                            }
                        }}
                        onClientUploadComplete={(res) => {
                            // Do something with the response
                            console.log("Files: ", res);
                            // The 3rd is one of four string and should be typed as such.
                            updatingObjectWithURLInShift(res[0].url, res[0].key, 'afternoon')


                            alert("Upload Completed");
                        }}
                        onUploadError={(error: Error) => {
                            // Do something with the error.
                            alert(`ERROR! ${error.message}`);
                        }}
                    />
                    {/* <Button type="submit">Upl
```

"

Still have to create the function,  
updatingObjectWithURLInShift(res\[0\].url, res\[0\].key, 'afternoon')

Start:  
2024-02-25 09:20:46 CST

What I'm trying to figure out is why does it come to an array vs. an object?  
This is what the summary object looks like:  
"  
setSummaryObject((prevSummaryObject: ObjectSummary | null) => ({  
…prevSummaryObject,  
earlyMorning: prevSummaryObject?.earlyMorning ?? \[\], // Ensure midMorning is always an array  
midMorning: prevSummaryObject?.midMorning ?? \[\], // Ensure afternoon is always an array  
midDay: prevSummaryObject?.midDay ?? \[\], // Ensure midDay is always an array  
afternoon: \[e.target.value\],  
}));

"

The DB that looks like:  
"

{"midDay":\[\],"afternoon":\[\],"midMorning":\["Today, we had more issues with the lift gate and we were 25 minutes late arriving to the post office and 20 minutes late, finishing the route. "\],"earlyMorning":\[\]}

"

Okay, it's the brackets around e.target.value.

Right now, it can only upload 1.

Start:  
2024-02-26 10:09:26 CST

\[\] get img tag working

Okay, I have to get that swiper thing working as a modal but for images so I'll have DRY code.

Side Note: Create Guternberg/WordPress plugin for uploading Markdown as a blog post.

Side note: for the job posting app, I will offer courses on how to code REALLY fast and then if they take the course the amount they earn will be brought out of their initial job.

Okay, so it's going to be a button or a preview depending on size and it's going to say, 'View (X number) of images'.

I think I'll do the button first then mini caruousel (preview) later.

\[x\] Make textarea expandable

Start:

2024-02-28 09:53:11 CST

- Get roles done so other employees can do their own timecards

- Make payments given page to track who gave what money to who.  
    \[ \] Pay summary page

- Move schedule page to main/schedule.

Need to have an accounts page so ppl can see or change privelages.

…

Admin,  
manager, employee,

Okay, so working on roles, I would like for the Admin and manager to have the same roles for now, and employee will have less privaleged roles.

https://clerk.com/docs/organizations/managing-roles  
https://clerk.com/docs/organizations/roles-permissions  
https://clerk.com/docs/users/metadata

I'm changed the private metadata on of the employees for alternate role scheme, may just use Clerk's role scheme.

currentUser() from Clerk is backend and I'm trying to get the organization a user belongs to in the backend without having to couple saved ids of my database. I would just like to query the answer based on the context, 1 trip.

I may not be able to get this information from the backend and it'll have to be frontend access to get the organization the current user is working in.

I want to see Org info from the Session variable so a user can interact with multiple Organizations.

https://organizations-demo.clerk.app/

This is semi working:  
"  
const { isLoaded, setActive, userMemberships } = useOrganizationList({  
userMemberships: {  
infinite: true,  
},  
});  
console.log(49, userMemberships);

"

From here:  
https://clerk.com/docs/organizations/multiple-orgs

"console.log the org id a user switched to clerk"

You get sessionId from useAuth

```
const { isLoaded, userId, sessionId, getToken } = useAuth();
```

I'm really wondering how people are building large scale apps, with the org stuff because the documentation isn't great.

Editing for: Jermisha B, in Baker Trucking.

Still working on the Org stuff.

Have to look at that gh repo and try to make private content for a Org but I'm probably over thinking all this stuff and it may just be really easy to do.

Then change the Dropdown for only managers.

Then, have private links to the main app page, where users can view their employees can view their schedule in a really prune down matter.

They should be able to get a magic link to view this stuff so they don't have to create account, someone will create the account for them and just send them the link to view.

d4d:  
2024-02-28 15:06:20 CST

For the schedule thing I still need to make it so that people who are not actively using it or are actively being shown to be hired  
So that it shows that it's the other person working, I need to have like that thing grayed out. Need to work on that logic.

Start:  
2024-02-29 11:00:38 CST

We should have been using the useAuth() hook the entire time.

I can only get the orgId from the client, so I would like to bring in variables from the client.

```
    {/* I need to pass that part the useAuth() stuff within the client. */}
    <h2 className="text-lg">Editing for: {fullname}, in { pass this from the client }  </h2>
```

I'm having this same issue:  
https://www.answeroverflow.com/m/1110684440448995469

I'm going to use getAuth so I don't have to deal with all that other stuff.  
import { getAuth } from '@clerk/nextjs/server';

It appears I can't though:  
https://github.com/clerk/javascript/issues/1642

I spent ages on this, and ended up fixing it by updating my version of node to v20

So, I am just going to upgrade to v20 rather than using getAuth() within a server component.

I upgraded to v20 and I didn't have the issues of finding middleware stuff.

With this I can get name with, id so it could be a two step solution rather than a one step solution.  
https://clerk.com/docs/references/backend/organization/get-organization

I can't get this organization object to work for anything:  
const { organization } = auth();  
// This works but I need to get the org name.  
console.log(37, organization?.id)

This could work but I don't see it working with multiple windows being open.

This needs to be on the client side and not on the server side or else it'll be really finnicky. But can't figure out the data flow pattern for the server.

This appears to be the solution:  

…

I think I'm going to duplicate the little bread crumbs thing but just for the main page, so I can have the dropdown org picker viewable and the authority of the user visible.

toDo:  
Make background white for org switcher.

Start:  
2024-03-03 09:20:50 CST  
I need to change once you just select a calendar thing the the API gets the stuff because it's just taking too long to like I don't want to press the view some other day I don't do that so I'm working on trying to make the app fun to use so that people want to use it more including myself

The problem right now is at the think about stuff whenever I like I on the summer page and open it up I wanted to like not think about anything is it like I just open up some repage cuz right now also the summer page is not on the current date it's on the day after

If I upload to mid day shift it breaks the whole thing.

Need to make that switcher for the shifts so that there can be two shifts for pleasant planes.

I need to have pages for like money sent and you can show what money was sent to who.

I could use this for the payment sending page:  
https://ui.shadcn.com/docs/components/data-table

I want to have preview image functionality before uploading.

I am going to use the swiper.js stuff for this.

Looking at, https://swiperjs.com/demos#effect-cube

I can just do this,  
![](images/nature-1.jpg)  
Not sure if ShadCN has an easy workflow for image sliders.

Start:

2024-03-04 09:17:20 CST

I need to change it to imgStrings and pass an array which will looped over in the component.

…

I am currently trying to refactor the summary page so, it's less lines and then I can use the refactored one to make sure that only the relevant shifts show,  
so for a route with only two shifts, two shifts will show. Now, only four shifts are showing.

Trying to get rid of repeated code, see:  
https://youtu.be/YgNm3pVnvN0?si=cj\_ObjH-HdCHtQIj&t=72

I think I'm going to have issues with the setState but let's see, working on this:  
{  
// Ensure setSummaryObject is updating the state correctly  
setSummaryObject((prevSummaryObject: ObjectSummary | null) => ({  
…prevSummaryObject,  
earlyMorning: \[  
{  
text: e.target.value || '',  
imgURL: prevSummaryObject?.earlyMorning?.\[0\]?.imgURL || 'your\_image\_url\_here', // Preserve the existing imgURL if available  
},  
\],  
midMorning: prevSummaryObject?.midMorning ?? \[\],  
midDay: prevSummaryObject?.midDay ?? \[\],  
afternoon: prevSummaryObject?.afternoon ?? \[\],  
}));  
}}

Working on allocated shifts.

Default json value for Prisma?

Use this:  
"  
jsonDBPrismaVar Json @default("{}")  
"

…

I need to figure out how to create feature branches for my git stuff so Vercel can work better.

Start:  
2024-03-05 11:33:20 CST  
I'm going to fix the multiple image upload problem, so I can upload multiple images and then after that, I'll work on the shiftAllocation stuff.

So, uploading multiple images into an array.

Check if the value exists if not add onto the array,  
for:  
onClientUploadComplete={(res) => {  
// Do something with the response  
console.log("Files: ", res);  
console.log(346, res\[0\].url);

```
                                    if (res[0].url) {
                                        setSummaryObject((prevSummaryObject: ObjectSummary | null) => ({
                                            ...prevSummaryObject,
                                            [routeComponent.shiftName as keyof ObjectSummary]: [
                                                {
                                                    imgURL: res[0].url, // Preserve the existing imgURL if available

                                                },
                                            ],
                                        }));
                                    }
                                    alert("Upload Completed");
                                }}
```

Okay, now that I got image uploading done, what I need to do is to write in that judger to show which shifts are going to be put up.

I also need to add a sort of modal view which will make the images viewable and there will be arrows to right and left to cycle through them..  
Also the image clicked will be the image shown. Also, have to be able to delete certain images as well when in the 'full' gallery view.

And hopefully, I can put in code tests by the end of the week.

I think being able to look at the gallery through open image in new tab is good enough, so going to do the shift judger for addition feature and  
then work on the aformentioned features.

I would like for uploadthing to have components where you can view the images and all of the features I just mentioned are just available to you  
just like the upload button is available to you.

Start:  
2024-03-06 09:26:40 CST

write in that judger to show which shifts are going to be put up.

Trying to add shadcn table but running into issues.

Adding shadcn introduces type errors to my project

This issue helps remedy the issue:  
https://github.com/shadcn-ui/ui/issues/167

Looking at manually installing the stuff now.

Keep running into the error of,  
Error: "OrganizationContext" not found

when using,  
const { membership } = useOrganization();

I'll probably rewrite it to use this, https://github.com/shadcn-ui/taxonomy  
I want access to ShadCN so I can focus on business logic and not styling stuff.  
Or better yet, the whole thing:  
https://github.com/shadcn-ui/ui

I guess I'm going to have to use TanStack table for the forseeable future until rewrite to Shadcn

…

Working on the Switch stuff.

I want to be be able to put the time in which it starts and ends on the route edit page.

Start:  
2024-03-08 13:53:46 CST

Images are no longer showing….

Apparently, you have to save it and the image is no longer just saved on upload.

Once you press Save Edited Stuff the image value will save into the database.

We need to add updateSummaryObject into here:  
"

```
                    if (res[0].url) {
                                        setSummaryObject((prevSummaryObject: ObjectSummary | null) => {
                                            const updatedObject = { ...prevSummaryObject };
                                            const shiftName = routeComponent.shiftName as keyof ObjectSummary;

                                            // Check if the shiftName already exists in the ObjectSummary
                                            if (updatedObject.hasOwnProperty(shiftName)) {
                                                // Find the object corresponding to the shiftName
                                                const existingArray = updatedObject[shiftName] as { text: string; imgURLs?: string[] }[];
                                                // Update the imgURLs array within the object
                                                updatedObject[shiftName] = existingArray.map((item) => ({
                                                    ...item,
                                                    imgURLs: [...(item.imgURLs || []), res[0].url]
                                                }));
                                            } else {
                                                // If the shiftName doesn't exist, initialize it with a new array containing the new URL
                                                updatedObject[shiftName] = [{ imgURLs: [res[0].url] }];
                                            }

                                            return updatedObject;
                                        });
                                    }
```

"  
Or, make a new function where it uploads to a certain shift without saving the text values or just add it like a submit fn until we get a more nuanced function to conduct that business logic.

I need to look at the route level stuff and that'll pipe into the sumarry selection so wheter or not there is midMorning will be piped in via a server component.

The dropdown selector when it finds out the names of the routes, it'll also know what shifts the route has.

Start:  
Thu 14 Mar 2024 11:18:36 AM CDT

We're going to have to clean up ui/summary-selection.tsx

Then work on that magic link thing for the app and more specifically summary page.

"  
Ideally that be a button on the right side of it with little share icon and then it'll be like a drop down and they'd be like share to Janie C or share to Ron and then you copied the link and that's going to be the magic link that you can just click on it and it'll show you and there'll be reduced privileges if they are viewing and view with via them the magic link

"

The last commit was, "Showing relevant shifts". This commit

So, we are working on discriminating between different routes which have different shifts.

Currently if allocatedShifts is null, then there will be no shifts, so if it's null, let's default to 4 and show the users the route switching page.

FR: We could put down who was scheduled for the shift in the summary page and further down we may even be able to put the car or truck which WAS  
used for the route or is it going to be used on the route and have it be easily be changed via modal or drawer functionality.

I don't think I'm going to clean up that function yet cause it works fine even though I don't know much about it.

FR: I would like for there to be an arrow sort of thing on both sides.  
Or we could have a sort of dots thing in the right corner and users can use that to swiper to either side which will correlate to which date.  
So, swipe left for past, swipe right for future.

What we really need to do is to have the times next to the shifts for when they start and end, we need the gallery feature so a modal pops up and the user  
can peruse through the images. After that, we can work on magic links within Clerk.

Work on gallery feature and hopefully we can add this as a magic link, so the magic link user would view the app within the vicinity of the day and the image  
open gallery style.

Looking through Next.js galleries using search term, '"nextjs-image-gallery" github', I found a bunch of mediocore implementations of next.js image gallery,  
I was looking for this:  
https://vercel.com/templates/next.js/image-gallery-starter

But couldn't find it until I got into the repos example found:  
https://github.com/vercel/next.js/tree/canary/examples/with-cloudinary

I think merging that code with my code would inflate the code base so I think I'm just going to re use that modal.  
For any templates in the future which we start our work flow from, it needs to have a really good modal implementation and a good Drawer implementation viz. a  
Drawer implementiaion which acts similarly to a modal, where it is brought in from the bottom and scrolled down,  
see [here](https://ui.shadcn.com/docs/components/drawer)

Get the modal we are using from the Employee dropdown stuff.

….  
Working on gh gist, you have to save it and quit in order for stuff to get saved so always run :wq

Start:  
Fri 15 Mar 2024 12:37:19 PM CDT

commit 2:  
Got working modal now just need index of the image which was clicked on.

Side Note: The functionality of the commit message to the gist, what could happen is I just load up the data from the previous commit into one of the slots  
held on my local keyboard.

Side Note: We could make a Next.js template store. Advertise on Twitch on Twitch streamer's descriptions.

Commit message:  
Index is showing

Start:  
Sun 17 Mar 2024 01:03:43 PM CDT

Passing all of that relevant data to the image modal component.

I think I'm just going to put the regular slides there but with one in the current(large) view and all of the other ones in a smaller (preview) view below.  
Then once this functionality is looking good, then we will work on the big arrows.

…  
It would be better if there was a magnifying glass kind of thing where once your in the image gallery modal you can zoom in on it a lot.

The alert that a shift doesn't work went away and what happens is it just shows an area with no shifts.

Start:  
Mon 18 Mar 2024 01:09:27 PM CDT

searchParams: write and read

useSearchParams: Read only

Working on the following:  
https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#windowhistorypushstate

```
    window.history.pushState(null, '', `?imgKey=${imgKey}?modal=${modalIsOpen}`);
```

Start:  
Wed 20 Mar 2024 02:08:33 PM CDT

Using url stuff to show images in a certain gallery.

The issue is, we have to re do all of that other stuff, so right now, I think I'm just going to focus on using urls for search functionality.

If there is stuff there as a shift being scheduled than text will appear after view summary of day which will say, Share day and Share day with link so people won't have to log in and it'll be link Share to Jermisha so she can just open the link and be right in the locale of the shift day.
