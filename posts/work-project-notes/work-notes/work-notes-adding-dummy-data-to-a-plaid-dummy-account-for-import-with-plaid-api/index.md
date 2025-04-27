---
title: "Work Notes: Adding Dummy data to a Plaid Dummy account for import with Plaid API"
date: "2023-09-03"
---

"

I was unable atm to insert dummy data onto the used\_good accounts so I'm going to have change it from the transactions which was loaded.

It looks like you can interdict the transactions and change the categories, see [here](https://plaid.com/blog/transactions-categorization-taxonomy/).

I guess I can add transactions to a dummy account with [this](https://plaid.com/docs/sandbox/user-custom/)."

I would eventually like this "dummy" data to be real data which I imported from Quicken as a .csv file.

So just copy and paste the object schema from this part of the documentation,  
[Configuration object schema](https://plaid.com/docs/sandbox/user-custom/#configuration-object-schema).

...

Now that I got that working, I need to load it full of transaction data which is from the .csv imported from Quicken.

...

"Set the username and [configuration object](https://plaid.com/docs/sandbox/user-custom/#configuration-object-schema) in the Dashboard, then log into the Sandbox with that username and any non-empty password."
