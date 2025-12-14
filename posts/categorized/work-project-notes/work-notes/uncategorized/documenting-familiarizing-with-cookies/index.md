---
title: "Documenting: Familiarizing with Cookies"
date: "2022-08-19"
category-slug: "work-notes"
---

**New Day:** Thu 18 Aug 2022 10:15:05 PM CDT

Okay, I have this issue where I would like to run the business logic of my JavaScript but I couldn't I looked up on Google 'call javascript function as a parameter in php'. But that didn't really work because php only see JavaScript as a series of symbols and not something to receive usable logic from. So it's up to the client to execute it. So my plan is to have the client execute the business logic I wrote and then save it in Cookies for the php interpreter to view.

Side Note: Cookies is the only browser storage method where it is viewable from the server so ... this same technique wouldn't work on Local Storage or Session Storage.

I learned you can get information about Cookies from the console by running 'document.cookie'. But that will output all of the Cookies and if you would like to view them in a usable manner, run 'document.cookie.split(';'); '.

Or more verbosely:

```
document.cookie
  .split(';')
  .map(cookie => cookie.split('='))
  .reduce((accumulator, [key, value]) => ({ ...accumulator, [key.trim()]: decodeURIComponent(value) }), {});
```

In the course of writing this I found that incognito mode will not wreck this scheme because it's just a fresh install.

Okay, so in my JavaScript in the function of my business logic I wrote "value=0".

So, now it's time to use php to search for that value.

**New Day:** Fri 19 Aug 2022 04:59:47 PM CDT

It looks like the solution I want to make with checking the zip code won't really work with Cookies so I'm going to have to use a local file to run the business logic.

**New Day:** Sun 21 Aug 2022 07:50:19 PM CDT

The solution of using cookies as a arbiter between the execution of server-side php and JavaScript didn't really work. So, I would imagine Cookies being a tool to manage the users versus a communication tool.

**Logging out:** Sun 21 Aug 2022 07:53:21 PM CDT

Sources:

[Source 1](https://www.youtube.com/watch?v=u4HmQjLvNe8&ab_channel=DaveHollingworth)

[Source 2](https://gist.github.com/codebubb/ab5cfaf8b70d198e55a5642e9a63ab37)
