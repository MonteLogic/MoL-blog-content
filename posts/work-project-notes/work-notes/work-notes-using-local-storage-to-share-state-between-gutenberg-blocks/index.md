---
title: "Work Notes: Using local storage to share state between Gutenberg Blocks."
date: "2023-03-05"
---

I managed to have it work but it's not updating from the original value unless I delete the Local Storage value. I still need to get it working where a useEffect can change the value within Local Storage.

I wanted to try a new solution because I wanted to share the results of an http request between blocks. Note, the fewer http requests the better.

Also, Mr. Abramov said that he would rather use Local Storage than Redux. Considering the use cases which Redux shows it's usefulness, we can reduce the few use cases of Redux and replace those use cases with Local Storage.

I notice if If I mess up the Local Storage or reset the local storage the app will crash.

So always do a check to see if Local Storage is null.

I've noticed that the Local Storage saving methods requires the page to reloaded vs. not needed to be reloaded with Redux.
