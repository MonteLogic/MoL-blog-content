---
title: "Work Notes: End to End (e2e) testing for the WooCommerce Checkout page"
date: "2023-07-16"
---

\[ \] twt155 - I don't know how to tests to see the user side, I would like for these tests to be comprehensive.

\[ \] 153gsaa - Turn this post into a video for YouTube and Odysee.

I would like to use that Snapshot feature to just check if the blocks are still there and working good. This usage case could be used for testing capabilities of the Checkout without loading a product into the cart and going to woowebsite.local/checkout to see what the checkout looks like on the user side. This technique could also be used on the Edit page too.

I just got wp-env to work on my system.

I really wish that there was a self isolated containers related to test--and other dev things. So all you had to do was "npm i; npx jest" and the tests would run as they are supposed to.

I know there is wp-env but that involves a Docker container and more start scripts, like, it's a good project but it still cumbersome.

The wp-scripts package comes with a default testing suite. Notice the e2e and unit test scripts, [here](https://developer.wordpress.org/block-editor/reference-guides/packages/packages-scripts/#setup).

Side Note: Testing WC Blocks, [PR](https://github.com/woocommerce/woocommerce-blocks/issues/9783).

Side Notes: I could redo Ryan Kiejstra's video on how to test blocks as the testing suite from wp-scripts has made the previous video outdated.

https://www.youtube.com/live/pI1hGE3IFqc?feature=share&t=4876
