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


## Start: Wed Jun 18 2025 16:42:23 CDT

For the PDF formatting, 
Like I don't know how it knows when it's about to experience a break in the line and I would have to figure all that stuff out again and I don't feel like doing that I wonder if I blogged about this in the past.


This is a useful file from my prior project:
https://github.com/MonteLogic/contractor-bud/blob/ae7c65af69962c6b4a08468ffe4b8e74a75610bf/utils/timecards/pdf-coordinates.json#L4


... 



That's better but we need it to be like


-----
Page 1.)
Elohai Neshamah (My God, the Soul)

-----
Page 2.)

Elohai Neshamah (My God, the Soul)  *continued 

----
So we just continue it.

That's better but we need it to be like

Aside: I wonder if there's like a hotkey or function I could do where I could copy the latest commit hash for whatever project I'm in.

-----
Page 1.)
Elohai Neshamah (My God, the Soul)

-----
Page 2.)

Elohai Neshamah (My God, the Soul)  *continued 

----
So we just continue it.


Question to answer: 
### What should every Temporary Siddur have?




... 

## Start: Thu Jun 19 2025 17:16:42 CDT


I think there should be a customizing like backway where you can select the MySiddur code shipment you would like your Siddur from viz. the codebase at a certain time.



... 

## Start: Sun Jun 22 2025 08:53:11 CDT

Right now they are all even and they don't continue into other pages but that's what we want.

We need to break this up into multiple files:
utils/siddur-pdf-utils/siddurMainFile.ts

I am currently working on the thing so it doesn't go into new pages:


https://gemini.google.com/u/1/app/34dee3c602f4624b


Currently a verse like this can't share two pages

```md
Elohai Neshamah (My God, the Soul)
My God, the soul You placed within
me is pure. You created it, You
formed it, You breathed it into me,
and You preserve it within me. You
will eventually take it from me, and
restore it to me in the time to
```

## Start: Thu Jun 26 2025 05:27:26 CDT

From Gemini:

Is there logic in there which says if the whole section will not fit on the page, default to adding the section to the page after


Yes, there is logic in ashkenaz-content-generation.ts that attempts to determine if a whole section, or a whole prayer within a section, will fit on the current page, and if not, it defaults to adding a new page and placing the content there.

This logic is present in the following conditional checks:

For an entire section's header (title and description):

```ts

if (y < siddurConfig.pdfMargins.bottom + estimatedSectionHeaderHeight + siddurConfig.verticalSpacing.pageBuffer) {
    page = pdfDoc.addPage();
    y = height - siddurConfig.pdfMargins.top;
    commonPdfParams = { ...commonPdfParams, page, y };
}
```

This block checks if the current y position is too close to the bottom margin to accommodate the estimatedSectionHeaderHeight. If it's not enough space, a new page is added, and y is reset to the top of the new page.

For an entire prayer (title and content):

TypeScript
```ts

if (y < siddurConfig.pdfMargins.bottom + prayerTitleTextHeight + estimatedPrayerContentHeight + siddurConfig.verticalSpacing.pageBuffer) {
    page = pdfDoc.addPage();
    y = height - siddurConfig.pdfMargins.top;
    commonPdfParams = { ...commonPdfParams, page, y };
}

```

Similarly, this block checks if the prayerTitleTextHeight plus the estimatedPrayerContentHeight will fit on the current page. If not, a new page is added.

For blessing groups and part groups within a prayer:
There are also similar checks within the blessings and parts loops, though these are estimating for a single blessing/part pair rather than the entire group:


```ts
// Inside blessings loop
if (blessingY - estimatedBlessingHeight < siddurConfig.pdfMargins.bottom + siddurConfig.verticalSpacing.pageBuffer) {
    page = pdfDoc.addPage();
    blessingY = height - siddurConfig.pdfMargins.top;
    commonPdfParams = { ...commonPdfParams, page, y: blessingY };
}
```

And for parts (especially if a part.source exists):


```ts
// Inside parts loop
if (partY - estimatedPartHeight < siddurConfig.pdfMargins.bottom + siddurConfig.verticalSpacing.pageBuffer) {
    page = pdfDoc.addPage();
    partY = height - siddurConfig.pdfMargins.top;
    commonPdfParams = { ...commonPdfParams, page, y: partY };
}
```

The core idea is to perform these height estimations and page break checks before attempting to draw the content block. If the check indicates insufficient space, a new page is added, and the y coordinate is reset to the top of the new page, ensuring the content starts on the fresh page.


Siddur 31 - 
file:///home/monte/Downloads/basic_siddur%20(31).pdf

The first page doesn't look good, the h2 text titles are having text too close to the head of it's text. Also, there's lots of white space. 

## Start: Sun Jun 29 2025 11:28:12 CDT

I feel like I need better debugging.


...

Prompt: 
> Why for this project do we constantly have to refresh the page for PDF Creation to access new logic written is there dev tooling for PDF Creation which will have sort of a hot reload 
  functionality but on the .ts "server" side of things?



I need to move all of my .ts logic for pdf creation into a lib folder

✦ That sounds frustrating. The standard Next.js development server (next dev) is designed to handle hot-reloading for server-side code, including API routes and other modules, so you
  shouldn't need to manually restart it. When you change a file in the lib/ or app/ directory, the server should automatically pick up the new logic.


### Remove debugging logic in prod

I would like to remove debugging logic in prod.
No console.logs when it's deployed on Vercel.

### I am moving to branch editing now. 


On issue 16, why do I even have a utils folder.

Aside: I would like to make an Expensify like clone using Next.js. 

## For the mangled text:

So if there are sources listed there needs to be a sources section which would increment upon the JSON.


## Start: Sun Jul 06 2025 13:15:58 CDT

So, working on the color transliterations. 


What I'm thinking:

"

How about we just pair something like Ani and if it's not directly translated good then we put an astericks in there and describe it in the commentary section below. 




Show thinking
This is an excellent approach! It allows for the precision of word-level (or small phrase-level) alignment where possible, while gracefully handling the complexities of translation and providing valuable extra context.

To achieve this, your JSON structure would need to be re-formatted to break down each prayer into an array of smaller, paired segments. Each segment would contain its Hebrew and English text, plus an optional reference to a commentary if a direct translation isn't sufficient.

Here's how you could structure the JSON for a prayer like "Modeh Ani" or "Asher Yatzar":

Proposed JSON Structure
You would transform the hebrew and english string fields within your prayer objects into a new array of segments. Each segment would represent a small, translatable unit.

JSON

{
  "title": "Modeh Ani (I Give Thanks)",
  "instructions": "Upon awakening, while still in bed:",
  "contentSegments": [ // New array to hold paired segments or other content types
    {
      "type": "pair", // Indicates this segment is a Hebrew-English pair
      "hebrew": "מוֹדֶה אֲנִי",
      "english": "I give thanks"
    },
    {
      "type": "pair",
      "hebrew": "לְפָנֶֽיךָ",
      "english": "before You"
    },
    {
      "type": "pair",
      "hebrew": "מֶֽלֶךְ חַי וְקַיָּם.",
      "english": "living and enduring King.",
      "commentaryRef": "eternalKing" // Reference to a commentary entry
    },
    {
      "type": "pair",
      "hebrew": "שֶׁהֶֽחֱזַֽרְתָּ בִּי נִשְׁמָתִי",
      "english": "for You have restored my soul within me;"
    },
    {
      "type": "pair",
      "hebrew": "בְחֶמְלָה.",
      "english": "with mercy."
    },
    {
      "type": "pair",
      "hebrew": "רַבָּה אֱמֽוּנָתֶֽךָ׃",
      "english": "Your faithfulness is great.",
      "commentaryRef": "greatFaithfulness"
    }
  ],
  "commentaries": [ // New section for commentaries, referenced by IDs
    {
      "id": "eternalKing",
      "hebrewOriginal": "מֶֽלֶךְ חַי וְקַיָּם",
      "description": "Literally 'King, living and existing.' 'Enduring' or 'eternal' captures the nuance of 'וְקַיָּם' (v'kayam), which implies sustained existence."
    },
    {
      "id": "greatFaithfulness",
      "hebrewOriginal": "רַבָּה אֱמֽוּנָתֶֽךָ",
      "description": "This phrase speaks to God's abundant and reliable trustworthiness, not just a numerical 'great' amount."
    }
  ]
}
Key Elements of This Format:

contentSegments Array (New):

Instead of hebrew and english as single strings at the prayer level, you'd introduce an array called contentSegments.

Each object in this array represents a small, logical chunk of the prayer.

type Field within Segments:

This is crucial for flexibility. For most cases, it would be "pair".

You could also imagine other types like "instructions", "lineBreak", etc., if you wanted to manage more complex layout elements directly in the data.

hebrew and english Fields within type: "pair":

These would hold the small, corresponding Hebrew and English text snippets. The goal is to make these as short and direct as possible for good pairing.

commentaryRef (Optional) within type: "pair":

If a hebrew segment's translation needs further explanation (i.e., it's not a perfect direct translation, or has deep meaning), you add a commentaryRef field.

The value of commentaryRef should be a unique ID that points to an entry in the commentaries array.

commentaries Array (New):

A separate array, typically at the prayer object level (or even higher, globally, if commentaries are shared across prayers).

Each object in this array represents a single commentary.

id: A unique identifier for the commentary.

hebrewOriginal: It's very helpful to store the original Hebrew text that the commentary refers to, making it easy to display in the commentary section.

description: The actual explanation of the nuance, meaning, or reason for the translation.

How to Implement in Your Code:
Data Transformation: The biggest challenge will be manually (or semi-automatically) converting your existing hebrew and english strings into this new contentSegments and commentaries array structure for every prayer. This is a significant data entry task.

PDF Generation Logic Update:

Your generateSiddurPDF function would no longer just draw prayer.hebrew and prayer.english.

It would iterate through prayer.contentSegments.

For each segment of type: "pair":

Draw segment.hebrew in the Hebrew column and segment.english in the English column.

If segment.commentaryRef exists, you would:

Draw an asterisk (or a similar visual indicator like a small number) next to the segment.english text.

Store the commentaryRef for later rendering.

Commentary Section Rendering: You'd need a new section in your PDF (e.g., at the bottom of the page, or a dedicated "Notes" section after the main prayer) where you iterate through the prayer.commentaries array (only for the commentaries that were actually referenced on the current page to avoid blank space) and display them with their hebrewOriginal and description.

This approach gives you fine-grained control and clarity for the user, clearly indicating when a translation is a direct equivalent and when it carries deeper or more complex meaning that warrants further explanation.



## Start: Fri Jul 11 2025 14:05:05 CDT
Okay, so we have to move that Shacharis Service to a sort of dashed line functionality. 







## Start: Sun Jul 27 2025 16:49:59 CDT



## Start: Mon Aug 11 04:07:44 PM CDT 2025



So in this file we can just note it's Modei Ani and be like "40-0rwa"

"
It looks like I can't import it the way I want to on a YAML file so it looks like I'm going to just write in .ts

So, at this moment it's the fact that I cannot reliably import multiple JSON files at the precise values without using a programming language. So not going to use YAML which I wish had this natively or a preprocessed JSON system. 




## Start: Sun Aug 17 08:17:32 AM CDT 2025


So, we need to granulate this file:
lib/siddur-pdf-utils/ashkenaz/ashkenaz-content-generation.ts


We need to take a bunch of files as an input and have it be like a stanadard process

The logic / file process itself should be impartial.

There should be a regular part, and an upcoming holiday part.

In the top there should be a section for like how it's different.

This process shouldn't be all that hard/complicated. 



So ...

// Get list of needed JSON objects and check them. 


// Waking Prayers
// // Get list of always in Waking Prayers from JSON files  
// // // Take this list and find the word mapped prayers. 

// Shacharis


// Mincha 


// Maariv 






// Attempt 2:

// Get the necessary files and bring them in and make that work good and then get do validation after.

// Build the machine and then try to validate it. 


Start: Tue Aug 19 05:58:04 AM CDT 2025

Okay, what I have to do is make it three columns. I think I will default to the three columns. 







Start: Wed Aug 20 05:45:51 AM CDT 2025

Getting to work on adding the transliterations. 





