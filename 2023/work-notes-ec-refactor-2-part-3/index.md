---
title: "Work Notes: Extended Checkout - Part 3"
date: "2023-05-02"
---

\[ \] 905afg- Check EC refactor with the latest dev versions of EC to check for errors.

\[ \] 189uia - Examine the EC submitted to WC Store.

\[ \] 521iag - Release version 1.1.0

\[ \] 152agh - Make a versioning site where versions can be updated and have that setup and have users use that.

\[ \] 140ahr - Make the Fundraising Campaigns page Extended Checkout which is going to link to checkout page also analytics could be here.

\[ \] 152 - Get hot module reloading (HMR) to work.

I want to make a product which I am passionate about and care about the people who use it.

So I think I'm going to make that contracting trucking app and then re-jigger Extended Checkout to suit the needs of development. As I feel like the Legacy WooCommerce checkout process can have better analytics process.

...

The one I directly downloaded isn't working so I'm going to have to look at the one which I did in the walk through. Also, going to have to re submit the file and I want the walk through to be with the zip which is featured not some nightly release looking thing.

[EC Plus fundraiser](https://github.com/MonteLogic/ec-plus-fundraiser) works but Vanilla EC doesn't. So I need to factor down EC Plus fundraiser and still keep all of those slots.

I redid EC refactor so now it's just [Extended Checkout](https://github.com/MonteLogic/extended-checkout).

I would like to make Extended Checkout more of a library so it can be used as an add-on to affiliate and fundraiser plugins. This method will be similar to importing Composer dependencies.

I'm trying to figure out how I'm going to make this similar to a library where you can just add onto it, should I make a folder within the plugin with JUST EC stuff?

I think I'll just add a folder named extended-checkout within ec-plus-fundraiser and ec-plus-affiliate.

...

I changed the name and now the scripts aren't loading, so I have to rename names.

...

What's going on is, I need to redo the packages so it's exclusively Extended Checkout and not Affiliate or Fundraiser. I also need to write how to build it verbatim. I am also have lots of errors on startups and I need to test it in multiple environments and setup ways which users will use.

I think 'Add New' is there because it's a CPT not just a link. I can change Fundraiser Analytics to suit my needs or even call it, 'Checkout Analytics'.

Looking into [HMR](https://github.com/WordPress/gutenberg/discussions/44529).

I gotta make the extended checkout menu page link to the page which is designated as checkout by WooCommerce.

I figured it out how to link to the checkout page.

I am getting an error but every time I try to delete an usable block it keeps on popping up again.

...

I just found out ec plus fundraiser isn't working all that well, I guess the blocks just kept on breaking. This project NEEDS automated tests to run either that be on commit or a CI because I'm tired of these unexpected issues popping up.

We need E2E tests for this project, watching this [tutorial](https://www.youtube.com/watch?v=pI1hGE3IFqc&ab_channel=RyanWelcherCodes). The tutorial mentions "snapshots" with Jest.

...

I think I have to write a test for EC and one for ec-plus-fundraiser and the test will say, yo this one is good and the other isn't.

I still really want to figure out a way to develop Gutenberg components outside of WordPress, this will make development much lighter without the overhead of WordPress and it's dependencies. I may be able to run wp-env on Debian using UserLAnd (AArch64).

I want extended checkout to use Typescript rather than just, '.js'.

Focusing on a [repo](https://github.com/kienstra/augmented-reality/) with good tests with particular focus on this [PR](https://github.com/kienstra/augmented-reality/pull/120).

**New Day:** Tue Jul 11 2023 11:16:05 GMT-0500 (Central Daylight Time)

I am getting rid of emotion/styled stuff and mui because of version issues. w

I’m tempted to just rewrite this thing from scratch using .tsx. But this rewrite will not affect the admin side just the checkout.

I got date picker to show on checkout at all times so I need to refactor that down.

I would also like to do analytics but have it related to the date picker javascript/ts rather than the php.

I really wish that there was a self isolated containers related to test--and other dev things. So all you had to do was "npm i; npx jest" and the tests would run as they are supposed to.

I know there is wp-env but that involves a Docker container and more start scripts, like, it's a good project but it still cumbersome.
