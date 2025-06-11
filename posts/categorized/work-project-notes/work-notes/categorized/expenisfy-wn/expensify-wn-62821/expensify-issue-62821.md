# Issue 62821
https://github.com/Expensify/App/issues/62821

## Start: Tue May 27 2025 16:49:31 CDT

What happens when the Expense menu item is pressed

React Dev Tools has been coming in clutch.

I think its going to be MenuItemList

```ts
function MenuItemList({menuItems = [], shouldUseSingleExecution = false, wrapperStyle = {}, icon = undefined, iconWidth = undefined, iconHeight = undefined}: MenuItemListProps) {
```

It IS SearchTypeMenu

## Start: Thu May 29 05:31:13 PM CDT 2025

I realize it's called the /search page

I also realized I can delete whatever I want in the codebase because I can just discard changes in git.

Okay, so what happens when the Expense button is being pressed.

...

Maybe the desired action occurs on all menu items and not JUST expenses.

....

This App is giving me bare problems

The page where it says hmm, don't look good:
https://dev.new.expensify.com:8082/edit/submit/description/8371724703650691128/2774337950294908/?backTo=%2Fsearch%2Fview%2F7406454132531793%2F%3FbackTo%3D%252Fsearch%253Fq%253Dtype%25253Aexpense%252520status%25253Aall%252520sortBy%25253Adate%252520sortOrder%25253Adesc%25%25%25

Look wrong link:
https://dev.new.expensify.com:8082/search?q=type%3Aexpense%20status%3Aall%20sortBy%3Adate%20sortOrder%3Adesc%25%25%25

Good look URL:

https://dev.new.expensify.com:8082/search?q=type%3Aexpense%20status%3Aall%20sortBy%3Adate%20sortOrder%3Adesc

Why is there the %25 stuff?

....

Okay, so the look wrong link, if you enter than into the URL it's bad but if you enter in the url of Good look URL, it's good.

So if we can just swap the URL, then it would be good.

How do we swap the URL?

....

Aside: If we just get rid of the percents at the end, the error goes away but maybe we could include some logic where it resends back to a correct URL instead of a pecent added at the end URL. Currently I think the thing sends back to an errant link using the URL as the state of the truth.

...

Currently we are trying to figure out where that button is pressed so we can interdict it with the correct URL.

Aside: When I'm working with these large codebases,what I need to do is search for files which have two of the same string of texts I am looking for.

Okay, I think the core file I am looking at is:
src/components/BlockingViews/FullPageNotFoundView.tsx

....

Bro, that URL is like poisoning the app because the search state is going back to the thing.

We may need to keep this due to the fact that it may be used for other functionality

Unless there's a use case where we are using %25%25 then I don't see a reason why we can't snip to Adesc

I was thinking about doing it so, where you would change the arrow button in the particular case where the %25%25 but then ig you would have to change all of them.....

....

How about when there's a 'something wrong', state then we snip back the URL to not have the %25%25 stuff, and change it to Adesc at the end.

I found all of the error loading screen files, I just need to find the logic which manipulates the URL and manipulates it.

Here, looks like a place where I can handle logic for the URL errors:
This is where I'm cooking at:
src/components/Search/index.tsx

## Start: Sun Jun 01 2025 15:43:40 CDT

A workaround could be, to shave off the URL to the ADesc but may be too technical to be workable.

The issue is still if there is a bogus URL it's stuck in the suspended state so we need to fix this 'suspended state'.

It will take in any variations of the URL and return it without the ADesc.

...

But what's going on with decodeURIComponent, need to understand this function.

...

I feel like we need to know where the arrow is going so we can interdict it as such.

### Address the issue directly

trailingPercentEncodingRegex = /(%25)+$/;

### Hmm.

What is going on with:

```ts
const route =
  useRoute<RouteProp<SearchFullscreenNavigatorParamList, 'Search_Root'>>();
````

Looking for the correspondence to Search_Root.

....

Okay, so I solved it but I feel like I need to do some further distillations.

Prior notes:

I don't want to touch this file,

src/components/Search/index.tsx

Maybe one or two lines onto this file.

Ideally I would go into the modal overfolding something wrong page, or the page which says not found and stuck.

There's a lot that goes into there.
But these are just UI components:

src/components/BlockingViews/FullPageNotFoundView.tsx

This is the magnifying glass looking thing:

```ts
if (hasErrors) {
  return (
    <View
      style={[
        shouldUseNarrowLayout
          ? styles.searchListContentContainerStyles
          : styles.mt3,
        styles.flex1,
      ]}
    >
      <FullPageErrorView
        shouldShow
        subtitleStyle={styles.textSupporting}
        title={translate('errorPage.title', {
          isBreakLine: !!shouldUseNarrowLayout,
        })}
        subtitle={'Hi'}
      />
    </View>
  );
}
```

These are all UI components with the exception of index.ts

## What exactly did I add?

## The useEffect:

Aside: I would like a code block here so I can go line by line and discuss the hook.

```ts
useEffect(() => {
  // Destructure sortOrder (and potentially other parameters) from queryJSON.
  // Renaming sortOrder here to avoid confusion if queryJSON itself is modified directly later,
  // though we are using a correctedQueryJSON copy.
  const { sortOrder: currentSortOrderInQueryJSON } = queryJSON;
  let needsCorrection = false;

  // Create a mutable copy of queryJSON to hold potential corrections.
  const correctedQueryJSON: SearchQueryJSON = { ...queryJSON };

  // --- Parameter Correction Logic ---
  // Check if sortOrder is a string and ends with one or more literal '%' characters.
  if (
    typeof currentSortOrderInQueryJSON === 'string' &&
    /%+$/.test(currentSortOrderInQueryJSON)
  ) {
    Log.info(
      `[Search] Malformed sortOrder detected in queryJSON: "${currentSortOrderInQueryJSON}"`,
    );
    // Remove all trailing '%' characters.
    correctedQueryJSON.sortOrder = currentSortOrderInQueryJSON.replace(
      /%+$/,
      '',
    ) as SortOrder;
    Log.info(
      `[Search] Corrected sortOrder to: "${correctedQueryJSON.sortOrder}"`,
    );
    needsCorrection = true;
  }

  // FUTURE: You could add similar checks for other string parameters in queryJSON
  // if they are also susceptible to this "%%%" suffix issue. For example:
  // if (typeof correctedQueryJSON.status === 'string' && /%+$/.test(correctedQueryJSON.status)) {
  //     Log.info(`[Search] Malformed status detected: "${correctedQueryJSON.status}"`);
  //     correctedQueryJSON.status = correctedQueryJSON.status.replace(/%+$/, '');
  //     Log.info(`[Search] Corrected status to: "${correctedQueryJSON.status}"`);
  //     needsCorrection = true;
  // }
  // --- End of Parameter Correction Logic ---

  // If any parameter was corrected, proceed to update the URL.
  // Inside your useEffect for URL correction:
  if (needsCorrection) {
    const newQueryString = buildSearchQueryString(correctedQueryJSON);
    const currentRawQueryString = (route.params as { q?: string })?.q;

    if (newQueryString !== currentRawQueryString) {
      Log.info(
        `[Search] Dispatching REPLACE action for screen <span class="math-inline">\{SCREENS\.SEARCH\.ROOT\}\. Old raw q\: "</span>{currentRawQueryString ?? 'undefined'}", New q: "${newQueryString}"`,
      );

      // Use navigation.dispatch with StackActions.replace:
      navigation.dispatch(
        StackActions.replace(SCREENS.SEARCH.ROOT, {
          // Target screen name
          q: newQueryString, // Params for the target screen
        }),
      );
    } else {
      Log.info(
        `[Search] Correction applied, but newQueryString is identical to currentRawQueryString ("${
          currentRawQueryString ?? 'undefined'
        }"). No navigation needed.`,
      );
    }
  }

  // eslint-disable-next-line react-hooks/exhaustive-deps
}, [queryJSON, navigation, route.params]); // Dependencies for the useEffect hook.
```

Line 177\*



## Start: Sun Jun 08 2025 09:39:35 CDT

Why, can I not go back to the back page? 

.....


What did @huult add? 
https://github.com/Expensify/App/compare/main...huult:App:62443-test?expand=1


### Check a PR on a large repo, quickly, as quick as possible and very lightweight as well. 


Figured it out. 

There's some difficulties with the npm install script but that didn't take too long. I think what takes the longest is setting up the dev environment. 

Make sure to replace the project specific names. 

Some of the commands: 

```bash
# In your local clone of Expensify/App
git remote add huult https://github.com/huult/App.git

git fetch huult 62443-test

git checkout -b huult-62443-test huult/62443-test

# Generating this diff isn't all THAT helpful but can be useful
git diff main..huult-62443-test -- package.json

# Gemini says:
# Review the output of this command. It will show you any lines added or modified in the dependencies or devDependencies. If you see new packages or version changes, install only those specific packages.
# But it would be easier to just run 'rm -rf' node_modules and do it again, this works well if your not under internet data constraints.  

```

Also he kept on working on the branch, so what to do in order to get an accurate reading is clone or pull or checkout whichever one works, the exact commit which they are referencing. 

I would think doing this from scratch would be the best way to capture the thereabout. 




### 
I don't know why he got rid of onBackButtonPress

### 
I'm getting the oops something wrong page rather than hmm.. its not here. 
Going to do fresh clone.



### 
I tried to chase down the issue took way too long but I'm looking through the diffs and I should just add them judiciously.

### 
Also, you can't just click view commit details.

You need to view the file and go from there basically never rely on GitHub.com UI to be more accurate than the terminal access. 

You need to check the last edited and make sure it matches the sha. 

So that would end up being:

https://github.com/huult/App/blob/952c1846f49e8eb2d9d3b35ccc0e2f45e3b965eb/src/components/BlockingViews/FullPageNotFoundView.tsx

### 

Adding just a character for me, for some reason, makes it so the modal stops folding. 

But breaks when the simple character is added. 

Aside:
Before I tackle/"go back into" an issue: 

What is something I could have looked over?


Is there a way to avoid this by refactoring/simplifying the app/solution?  

... 

The solution huult proposed works for mobile for the specific link, broadening the issue


... 
I thought going back to the home screen was bad. But I guess on Mobile it's good, "On small screens, the app should ideally route back to the Home screen on pressing back button on the RHP when a url fails to load — similar to how we handle invalid chat/report."


... 

"What is something I could have looked over?"
"I could have looked over," the different URLs and how each can produce different results.

"I could have looked over,"



Is there a way to avoid this by refactoring/simplifying the app/solution?  

... 

toDo @builderbot: Bash Requests: 
Output the current path in the terminal, bonus if it adds it to the clipboard. 

... 
Aside:
What if there was a way to request an LLM fix or suggest what I'm trying to do and put it and article.
and just @builderbot but make it also comment look so everyone doesn't know and have builderbot link back to where it found it's own reference and why it built it the way it built it.
... 



I'm not sure if this [response](https://github.com/Expensify/App/issues/62821#issuecomment-2933855910), is directed at me or just a general response not accounting for my proposal. 


Not going to respond with this: 
"
I AM under the assumption that that response was directed to me because MY solution does bring the user back to the reports page for mobile. While staging doesn't(?)
"

Anyways:


I have to make mobile like my Desktop solution viz.  

"
On mobile (small screens), pressing the back button on a malformed URL like
https://dev.new.expensify.com:8082/r/6491421586538563/details navigates the user back to the Home page, instead of showing the error page (for https://dev.new.expensify.com:8082/r/6491421586538563/) — unlike the behavior on desktop.
We might want to consider making the Search page behavior consistent with this, so that on mobile, users are taken back to the Home page when a url fails to load the RHP.

"

Why is mobile and Desktop so different? 


On here, 
"
For the second issue specifically, I think we already implement a similar handling mechanism for deep links in chat/report. Could you please review that implementation to see if we can apply a similar approach here?

"


...

On desktop the intervening logic of pressing the back button isn't present so I think it would 'bypass' this process. 

What is it avoiding by using the back skip button which doesn't hit my useEffect? 


... 

I also think I should look into what they mean by the deep handling mechanism for links? What is he talking about? 

... 

I'm not sure about the mechanism you're talking about. 


.... 

Okay so on mobile smaller screens:
Mobile View:
URL 1 -
https://dev.new.expensify.com:8082/r/6491421586538563/details

[URL 1](media/URL-1-mobile-view-details.png)


Mobile View:
URL 2 - 
https://dev.new.expensify.com:8082/r/6491421586538563

[URL 2](media/URL-2-mobile-view-no-details.png)

... 

He likes "chat or expenses" in the background.


Okay, So for the mobile part of my solution the user may not know they entered in a bogus report/expense. 

Why is it not showing the error for 


... 


I wonder if on staging it shows the correct error prompt, it does.

https://staging.new.expensify.com/r/6491421586538563/details

....

I couldn't get it to show the correct error for mobile.
So, make it so 

... 

Also, I need to make a test branch and not just commit to main, ideally, named after the exact same error I am trying to fix. 

...

I also have yet to fix the former part of the issue, I have to put all of those wildcards in there and change it with a useEffect when I could handle the bad caching on the backend but right now, I'm going to finish my thought of showing the correct error page. 


... 

I have to get this view on mobile page:
https://dev.new.expensify.com:8082/r/6491421586538563/


... 

We may still need the useEffect or a similar mechanism because we will have to update the state.


We click on this from the chat:
https://dev.new.expensify.com:8082/search/view/7244371145701894/?backTo=%2Fsearch%3Fq%3Dtype%253Aexpense%2520status%253Aall%2520sortBy%253Adate%2520sortOrder%253AdescRandomChars

And from there 



## The task
We click on this from the chat:
https://dev.new.expensify.com:8082/search/view/7244371145701894/?backTo=%2Fsearch%3Fq%3Dtype%253Aexpense%2520status%253Aall%2520sortBy%253Adate%2520sortOrder%253AdescRandomChars

So, it's going to show the proper error screen on Desktop and Mobile and then it's going to clear cache and go back to where it was supposed to be and stay on the reports page or go on the home page. 


I feel like we need to do an overhaul of this backend caching thing.


## Start: Wed Jun 11 2025 04:43:58 CDT

There's a lot to study here:
https://github.com/Expensify/App/blob/3bb4fb3897f9393340aebc846f6cfedf18a6116e/src/libs/actions/Link.ts#L157



... 


Really what we need to do is mock the setup 

and ig in the background we can have a machine 


but whenever an action happens we need to list everything that happens but it also needs to be in a detailed view.


.... 

So we need to have like a mock setup of where it's at also we would include everything we know about the app at that specific time and then when it goes onto the next process we get the intermediary action info and then we list in detail where it's currently at in it's current state, similar to how we would in the first step. 

and then we can have mobile view and desktop view 


Mobile view () => () => () 


Desktop view () => () => () 

