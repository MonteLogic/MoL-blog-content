---
title: 'My Siddur Work Notes - 1 '
date: '2025-05-16'
start-date: 'Thu May 15 2025 17:34:15 CDT'
last-updated: 'Thu Mar 20 2025 14:00:38 CDT'
category: 'Work/Life Notes'
status: 'public'
---


## Start: Thu May 15 2025 17:34:33 CDT

I don't want to putz around with DBs if I can abstract it away to Clerk.



What we NEED is 

Shma 
And shmone esrai 



So we will start that off first and we will put the flagship product front and center.

## Start: Fri May 16 2025 17:51:17 CDT

The gh submodule needs to be changed. 

Aside: I think I'm going to watch programming streams and document what they're doing similar to how I document my own coding sessions. 
Worth documenting
Geohotz: https://www.youtube.com/watch?v=nyDGXlLp578
Rfleury: https://www.rfleury.com
Strager(When available)
RyanSolid: https://www.twitch.tv/ryansolid
Tsoding: https://www.twitch.tv/tsoding

A lot of (S&D) streamers who are popular are more focused on broad audience appeal and don't get into the very nitty gritty.

Would like to know more about golang streamers am going to research:
 https://www.youtube.com/channel/UC_BzFbxG2za3bp5NRRRXJSw
(https://www.twitch.tv/mdlayher, https://www.youtube.com/channel/UChgqV1LNU9tBWcRnAP6tKGQ)
(https://www.youtube.com/c/MichaelStapelberg, https://www.twitch.tv/stapelberg)


The way I did it was:

gh repo clone MonteLogic/MoL-blog-content MySiddur-blog-content

Then go into MySiddur-blog-content delete the .git folder and init the repo on GH.

I have to do more work to make it so the string can change easily from project to project. In the package.json it mentions the hard coded values for the content-submodule would be better if we could import this but we can't so we have to off load it into a script.

Also, markdown-paths.json is a bit of an issue.

## Start: Sun May 18 2025 10:21:26 CDT

Right now, we are working on string so we don't have to change every MoL tech blog thing we can just rely on strings.json


Working on [issue 2](/MoL-blog-content/posts/categorized/work-project-notes/work-notes/categorized/MySiddur/issues/issue2/index.md)


## Start: Mon May 19 05:08:44 PM CDT 2025


Okay, so I'm starting up CBud and found that the timecard page works but not the timecard per employee. 


So just going to stuff a bunch of logic in there until I can get some sort of timecard


This stuff works:

```ts
      <Button
        onClick={generatePDFClientSide}
        className="w-full justify-center rounded-md bg-blue-500 px-4 py-2 text-sm font-bold text-white hover:bg-blue-600 focus:outline-none focus-visible:ring-2 focus-visible:ring-white/75"
      >
        Generate Timecard
      </Button>

```







## Start: Fri May 23 2025 13:47:19 CDT


This is a useful article minus the Alphabet talk.
https://www.jewcy.com/religion-and-beliefs/write_your_own_siddur/

mαkesiddur.com is good 









## Start: Mon May 26 08:56:04 PM CDT 2025

I want to make a page called 'Custom Siddur' but I don't want it to be behind a paywall. 

I don't like the idea of just all of a sudden entering the login page, very jarring.


## Start: Sun Jun 01 2025 16:33:20 CDT


I want a schedule for lifters/ jumpers which will be year round and feature periodization and we all PR at the same time. 


## Start: Fri Jun 06 2025 17:05:07 CDT

I would like to imprint sections on to a image because I know the drawing capabalities are very limited. 


Aside: I want to switch from index.md to the name of project for easier lookup.


## Start: Tue Jun 10 2025 04:09:35 CDT

What I would love is to color coat it viz. 

This would be blue:

שֶׁהֶֽחֱזַֽרְת

and this would be blue also:

for You have mercifully restored

.... 


Fixing the start scripts.

Error: Command "pnpm install && cd MoL-blog-content && pnpm install && cd .." exited with 1 


... 

I guess I'm getting errors with Stripe subscription stuff. 

## Start: Wed Jun 11 2025 04:29:06 CDT


Fixed the .env by putting an appropriate var in. 

Added issues.
