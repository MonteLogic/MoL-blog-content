
# How are links stored in the backend?

## Writing

What are the difference between all of these and how they're rendered:

On mobile:
https://dev.new.expensify.com:8082/r/6491421586538563/details
Hmm not, here oops page cannot be found.
Doesn't show the desirable error page like the one below.



On desktop:
https://dev.new.expensify.com:8082/r/6491421586538563/details
Shows, 'src/pages/home/ReportScreen.tsx' in the background.



No /details:
Desktop:
https://dev.new.expensify.com:8082/r/6491421586538563/
How come this shows the screen of 
src/pages/home/ReportScreen.tsx

Mobile:
https://dev.new.expensify.com:8082/r/6491421586538563/
How come this shows the screen of 
src/pages/home/ReportScreen.tsx



https://dev.new.expensify.com:8082/search/view/4861009624462642/?backTo=%2Fsearch%3Fq%3Dtype%253Aexpense%2520status%253Aall%2520sortBy%253Adate%2520sortOrder%253Adesc12




## Writing Part 2:

Likely root cause:
It seems the malformed URL is being stored or cached on the backend. So even after clearing the browser cache, the backend continues to return the same broken URL, resulting in the persistent error page.


How do links fundamentally work and how are they tied into the backend?

## Start: Tue Jun 10 2025 02:02:53 CDT

What someone said? 
buildCannedSearchQuery
To resolve this issue, we just need to update the search query to use buildCannedSearchQuery, which is the default query. I tested many solutions like updating the route or deleting the search screen, but they were too complex. So I decided to suggest a simpler solution: introduce a flag inside the Search component to reset the search query, like this:

Onyx.set(ONYXKEYS.SEARCH_RESET_QUERY, true);


## Pause: Tue Jun 10 2025 02:10:10 CDT

## Start: Wed Jun 11 2025 04:48:53 CDT


The core question we need to answer, how are links stored in the backend?


## ...
The problem I have is I don't know enough about debugging

This thing with the link handling, I wish I could break it apart better. 

These are the issues, AI has a tough time doing and it's the wise thing to just turn it off for these kinds of issues.






We just need to get the mobile thing which is not loading good: 
https://github.com/MonteLogic/MoL-blog-content/blob/9f7db7e7282e67fe8d7512952dca1587b5b63f54/posts/categorized/work-project-notes/work-notes/categorized/expenisfy-wn/expensify-wn-62821/expensify-mechanism-for-handling-links.md#L8

We also need to fix, the something went wrong page:
https://github.com/MonteLogic/MoL-blog-content/blob/9f7db7e7282e67fe8d7512952dca1587b5b63f54/posts/categorized/work-project-notes/work-notes/categorized/expenisfy-wn/expensify-wn-62821/expensify-mechanism-for-handling-links.md#L8




