
This is what Gemini is telling me, I doubt if it's true.
Answering your question directly, the logic being referred to for handling deep links in chats and reports is a combination of validation and redirection mechanisms designed to prevent application errors and provide a seamless user experience, even when the linked content is inaccessible or invalid.

This logic can be found in the following locations within the Expensify/App codebase:

## Deep Link Handling for Reports
The primary logic for handling deep links to specific report actions resides in the ReportScreen.tsx file.

Location: src/pages/home/ReportScreen.tsx
Clues: Within this file, a useEffect hook is used to validate the reportActionID that is passed in the URL.
Core Logic: If the reportActionID from the deep link is determined to be invalid or inaccessible, the application doesn't navigate to an error page. Instead, it uses navigation.setParams({reportActionID: ''}) to remove the invalid parameter from the URL. This ensures the user is still taken to the correct report, just not scrolled to a specific, non-existent comment.
## Deep Link Handling for Chats
The logic for handling deep links to chat reports, including the initial routing, is located in the Report.ts actions file.

Location: src/libs/actions/Report.ts
Clues: Look for the openReportFromDeepLink function. This function is triggered when the application is opened via a deep link to a report.
Core Logic: This function checks if the report associated with the reportID in the deep link exists and if the current user has permission to view it. If the report is not found or is inaccessible, instead of showing an error, the application intelligently redirects the user to their most recently accessed report or to the default Concierge chat. This prevents the user from landing on a dead-end page.
## Reusing the Existing Logic
For the issue you're working on, the suggestion is to apply a similar principle of graceful error handling and redirection. Instead of relying on the default back-button behavior which may lead to an inconsistent state, you can implement a more explicit navigation flow.

When a user is on the "Hmm Not Here" page after following a broken deep link, the back button action could be programmed to:

Identify the intended report from the original deep link URL.
Navigate the user directly to that report, clearing out any invalid parameters (like a non-existent reportActionID).
By doing so, you would be replicating the existing pattern of sanitizing the navigation state and ensuring the user is always directed to a valid and accessible view within the application, thus providing a more robust and user-friendly experience.


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

buildCannedSearchQuery
To resolve this issue, we just need to update the search query to use buildCannedSearchQuery, which is the default query. I tested many solutions like updating the route or deleting the search screen, but they were too complex. So I decided to suggest a simpler solution: introduce a flag inside the Search component to reset the search query, like this:

Onyx.set(ONYXKEYS.SEARCH_RESET_QUERY, true);


## Pause: Tue Jun 10 2025 02:10:10 CDT



