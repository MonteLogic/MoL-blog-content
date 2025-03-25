# Establish Private vs. Public posts logic using Clerk.

Okay, how is frontmatter even parsed how cna we discriminators to it?

Now, we can get it where they can't SHOW it, we need to get it where, the user cannot see it at all and in order to do that we need to denote roles. 


## No Orgs just public metadata.


Okay, we got the Org functionality back because ig we NEED an org because this seems to be the only way to connote roles but this is a busted option because if we want to have a bunch of people comment then it's going to ruin the org, so I think we are just going to use private metadata. 


...

Getting private metadata seems easy, [here](https://clerk.com/docs/users/metadata#retrieve-private-metadata).

...

Hopefully I don't ruin this with bad code. 


Aside: The invitation logic isn't working will for localhost using Clerk.

toDo: It's a good idea to add backup functionality for this in case someone wrongly turns on org functionality.

Turn off, org functionality.

### The various roles in public metadata:

Okay, so the roles. 

Commenter, Admin, Contributor





