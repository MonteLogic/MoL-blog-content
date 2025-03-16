---
title: "Work Log: Using WC Blocks Slot Fills for Shipping Information - Part 2"
date: "2022-12-19"
---

Summary:

\- I worked on regex to have my webpack work write for Extended Checkout.

So, I have to take that checkbox fixed, turn it that well first about to fix it. So it's not like just showing nothing so to fix that, you know, and try to figure out why it's not working. And then have to turn that it's like an input and then have like the other master block, be able to, like, like do something with it.

Also need figure out how to even have like a master block showing

Is that's the one rendering it, that'll show and that's gonna have to be my master panel because I know that there's editor, inspector settings for the other one. So that's the only ass thought. My only entry point is to take that newsletter, dash test original original logic and then add the inspector panel to that and then go from there.

Tapping. If they make a change on the master panel, I'm gonna have to say like a works like red marks like for load required to view the changes that's gonna be after I make it. So that's not just be, but on the editor section, Editor section.

...

The addition button above the shipping dress, I'm getting the icon mixed in, check out and whenever I press the plus button underneath the order underneath the shipping stuff at the bottom, I'm getting Order notes, in terms of conditions, I want to know what's the logic? That's a certain that that area, so I can take advantage of it.

Maybe this has something to do with it:

```
"parent": [
"woocommerce/checkout-contact-information-block"
]
```

Or maybe this gives it away to be in that spot and render it in the edit section right below the address section.

```
import { CheckboxControl } from '@woocommerce/blocks-checkout';
```

...

Okay, so now I fixed it, so I would like to add radio buttons to send data related to the checkout process.

But I need to figure out how to make it work on the edit page not just the frontend page. So I'm watching this tut:

...

I am getting into the process of writing tests even for stuff on my development GitHub projects so I don't accidentally break stuff.

...

It. I know that if I wanted to I could add it to two blockchains I needed and would work but that's going to like mess up a lot of Business logic because I don't know if I can have multiple multiple return statements returning something like returning to component. So I'd much rather have that be in custom fields block.

So I need to add that there and hopefully I don't have to worry about the web pack. Configuration issues period. Also I really, really wish I could find a way to to, to test like to outputs in the web packs, so, I can my troubleshoot what's going on. So I because I know it's the issues happening wet pack, but I don't, I don't have this, the facilities.

I don't have the data on the way with all to do it yet.

Side Note: It appear the MC WooCommerce sends two values rather than one I have been able to send.

The file: https://github.com/mailchimp/mc-woocommerce/blob/master/blocks/woocommerce-blocks-integration.php

...

I am going to keep the woocommerce prefect to the text domains of the projects for the time being.

...

The example provided in newsletter-test it only allows for one really, so I'm rewriting it to loop through multiple paths for easier additions.

...

I am trying to use a regex expression to find the name of the block by searching through $script\_asset\_path for the characters after '/build/' and before '.asset.php'.

With the following regex:

```
$script_asset_path = dirname(__FILE__) . '/build/newsletter-block.asset.php';

// Use a regex pattern to extract the characters after '/build/' and before '.asset.php'
preg_match('/\/build\/(.*?)\.asset\.php/', $script_asset_path, $matches);
$script_name = $matches[1];

echo $script_name; // Outputs: "newsletter-block"
```

This'll make the for loop much easier to use.

...

I could make this function return the names of the blocks which will then be used in the IntegrationInterface.

//  
function create\_block\_multi\_block\_plugin\_block\_init()  
{

```
$blocks = array(
    'block-one/',
    'block-two/',
```

)

}

The commit which made it so that a slot fill can be viewed in the editor, I am unable to take advantage of this. The latest WC Blocks plugin doesn't show the slot fill view in the editor.

The problem that I'm running into is that it's not showing up on the editor page and I can't add extended checkout to the area.

Focusing on this [Pull Request](https://github.com/woocommerce/woocommerce-blocks/pull/8111) and using the functionality displayed.

I built the plugin Pull Request specified should be built and it works on the editor side but I noticed that you don't need to drag and drop the component to have it work.

I started a [Part 3](https://montelogic.com/?p=2637).
