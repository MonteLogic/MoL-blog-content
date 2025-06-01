Start: Tue May 27 2025 16:49:31 CDT





What happens when the Expense menu item is pressed 


React Dev Tools has been coming in clutch. 


I think its going to be MenuItemList 

function MenuItemList({menuItems = [], shouldUseSingleExecution = false, wrapperStyle = {}, icon = undefined, iconWidth = undefined, iconHeight = undefined}: MenuItemListProps) {

It IS SearchTypeMenu 


## Start:  Thu May 29 05:31:13 PM CDT 2025


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




Aside: When I'm working with these large codebsaes,what I neeed to do is search for files which have two of the same string of texts I am looking for.



Okay, I think the core file I am looking at is: 
src/components/BlockingViews/FullPageNotFoundView.tsx



....


Bro, that URL is like poisoning the app because the search state is going back to the thing.

We may need to keep this due to the fact that it may be used for other functionality	


Unless there's a use case where we are using %25%25 then I don't see a reason why we can't snip to Adesc


I was thinking about doing it so, where you would change the arrow button in the particular case where the %25%25 but then ig you would have to change all of them.....

.... 


How about when there's a something wrong state then we snip back the URL to not have the %25%25 stuff, and change it to Adesc at the end. 


I found all of the error loading screen files, I just need to find the logic which manipulates the URL and manipulates it.


Here, looks like a place where I can handle logic for the URL errors:
This is where I'm cooking at:
src/components/Search/index.tsx


## Start: Sun Jun 01 2025 15:43:40 CDT


A workaround could be, to shave off the URL to the ADesc but may be too technical to be workable.  




