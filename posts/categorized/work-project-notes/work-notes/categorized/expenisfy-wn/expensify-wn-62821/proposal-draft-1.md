The thing is, Lorenzo is we still have the issue with the errant state. 



## Proposal

### Please re-state the problem that we are trying to solve in this issue.
Solve the issue of the errant state when a problematic URL like the one stated in 

### What is the root cause of that problem?
The cause is the lack of error correction when the URL bar is used as state. Also the issue of the App being stuck in an errant state because of the problematic URL. 

### What changes do you think we should make in order to solve the problem?
<!-- DO NOT POST CODE DIFFS -->
Add state correction which would 'snip' the URL back into correct form. 

This state correction comes in the form of a useEffect on src/components/Search/index.tsx

The useEffect shortened from what I have to not post a 'wall of text': 
```ts

    useEffect(() => {
        const {sortOrder: currentSortOrderInQueryJSON} = queryJSON;
        let needsCorrection = false;
        const correctedQueryJSON: SearchQueryJSON = {...queryJSON};
        if (typeof currentSortOrderInQueryJSON === 'string' && /%+$/.test(currentSortOrderInQueryJSON)) {
            correctedQueryJSON.sortOrder = currentSortOrderInQueryJSON.replace(/%+$/, '') as SortOrder;
            needsCorrection = true;
        }
        if (needsCorrection) {
            const newQueryString = buildSearchQueryString(correctedQueryJSON);
            const currentRawQueryString = (route.params as {q?: string})?.q;
            if (newQueryString !== currentRawQueryString) {
                // Use navigation.dispatch with StackActions.replace:
                navigation.dispatch(
                    StackActions.replace(SCREENS.SEARCH.ROOT, {
                        // Target screen name
                        q: newQueryString, // Params for the target screen
                    }),
                );
            } 
        }
        // eslint-disable-next-line react-hooks/exhaustive-deps
    }, [queryJSON, navigation, route.params]); // Dependencies for the useEffect hook.

```





### What specific scenarios should we cover in automated tests to prevent reintroducing this issue in the future?
<!-- Clearly describe the different test cases you recommend adding or updating. Explain how they will ensure the problem is fully covered and that any future changes do not cause a regression. Consider edge cases, input variations, and typical user interactions that could trigger this issue. To get guidance on how to write tests, refer to the [README.md](https://github.com/Expensify/App/blob/main/tests/README.md) in the tests folder. -->

The scenarios of other problematic URLs and other wildcard URLs, the QA team or other team might have. 


Reason being:
As I am unsure of the total variety of problematic URLs as I've inputted dozens of URLs and they seemed fine but maybe the team knows of ones which will not pass.



### What alternative solutions did you explore? (Optional)

**Reminder:** Please use plain English, be brief and avoid jargon. Feel free to use images, charts or pseudo-code if necessary. Do not post large multi-line diffs or write walls of text. Do not create PRs unless you have been hired for this job.

Manually update the URL, this works on Desktop or Mobile but this would work on the Mobile app as there is no place to edit the URL. 

What this looks like: 

Problematic URL:
https://dev.new.expensify.com:8082/search?q=type%3Aexpense%20status%3Aall%20sortBy%3Adate%20sortOrder%3Adesc%25%25%25

URL after manually updated:

https://dev.new.expensify.com:8082/search?q=type%3Aexpense%20status%3Aall%20sortBy%3Adate%20sortOrder%3Adesc
