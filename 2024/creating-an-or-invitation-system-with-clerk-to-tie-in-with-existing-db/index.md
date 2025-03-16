---
title: "Creating an or invitation system with Clerk to tie in with existing db"
date: "2024-09-01"
---

Search Phrases: "Onboarding users with Clerk Organizations"

  
This presentation shows invitation logic and UI but we are trying to tie it with our database, if we were relying solely on Clerk and not creating a user in our db then it would work.

Our app will have data about the user already setup and will stay on our db as we are doing complex operations on our db and relying on Clerk may not be good for our use case.

What we will be doing is setting up data for the expected user and invite them they take the invite and immediately tie themselves to the data/data system we have created for them.

We will be doing this with the page, /onboarding.

Making a full page can be hard, so we are just going to redo the menu so it says onboarding and we have time we can work on a full screen functionality for this.
