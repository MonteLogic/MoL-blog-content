---
title: "Work Notes: Modifying the Shipping Options page on the editor view. - Part 3"
date: "2023-01-26"
category-slug: "work-notes"
---

**The goal:** To have it so the Local pickup option is selected then the Shipping Fields will be replaced with a message which says the order will be delivered to the store's HQ. This is going on to be the frontend as well as the edit page. While on the edit page the user will be able to edit the message of where the Local pickup is at if they would like to change the default message.

\- Working on

toDo:

I moved the block to the edit page, but when I change the radio component which changes an attribute it prompts the user if they want to leave. I do not feel as if this is a robust solution, so I'll be looking into this [file](https://github.com/woocommerce/woocommerce-blocks/blob/trunk/assets/js/base/context/providers/editor-context.tsx) to try to add context logic to do what I am trying to do.

...

I'm focusing on this now:

```
const { shippingMethodsSelection } = useEditorContext();
const [ newShippingMethodsSelection, setShippingMethodsSelection ] =
useState( shippingMethodsSelection );
```

I need to add a function to this [file](https://github.com/woocommerce/woocommerce-blocks/blob/trunk/assets/js/base/context/providers/editor-context.tsx) which will then update the string because you have to define the function and just can't call an edit on a string which isn't defined in the context(?).

I scaffolded a new function onto this [file](https://github.com/woocommerce/woocommerce-blocks/blob/trunk/assets/js/base/context/providers/editor-context.tsx).

I just realized I had a editing function within that file the WHOLE time.

```
	const editingPostId = useSelect(
		( select ): number =>
			currentPostId
				? currentPostId
				: select( 'core/editor' ).getCurrentPostId(),
		[ currentPostId ]
	);
```

I made the functionality, I was aiming for, so the core functionality is done BUT I have to clean it up and still working on lingering issues.

I'm having a hard time seeing the edited view of the attribute as I am only able to output the default value.

This [article](https://www.binarymoon.co.uk/2021/06/how-to-get-a-list-of-all-wordpress-blocks-in-the-editor/) is helpful.

How do I get the value of another attribute from another block consider scope issues?

...

I think I already figured out how to do this but I deleted it so it's somewhere nested in my WC Blocks GitHub repo.

Okay, I found [it](https://github.com/MonteLogic/woocommerce-blocks/blob/701dbe72d39bcd4dce97381470c1cd626e5aa96b/assets/js/blocks/checkout/inner-blocks/checkout-shipping-address-block/block.tsx). While I don't think it works it's a good starting point.

Whenever you are coding be very careful to avoid assumptions. What you assumed on it's face value to have worked may not be. Be diligent and detail oriented when assessing if a functionality is doing the desired functionality.

This statement is relevant cause I think may initial assessment was incorrect.

I have to go into the previous solution references directly above and work out that for the current solution but for the attribute I would like to refer to in shipping-method from shipping-address block.

Okay, so I got it to work on the edit page now I just need to get it to work on the front view of the website.

I'm having a tough time trying to figure out how to pipe the value of an edited attribute onto the front page, so I'm going to look at how else it is being done in the project.

So I am editing the code block as such, below:

Which comes from this [file](https://github.com/MonteLogic/woocommerce-blocks/blob/trunk/assets/js/blocks/checkout/inner-blocks/checkout-shipping-address-block/edit.tsx).

```
<Block
showCompanyField={ true }
showApartmentField={ showApartmentField }
requireCompanyField={ true }
showPhoneField={ showPhoneField }
requirePhoneField={ requirePhoneField }
localPickupString={ attributes.deuxPickupString }
/>
```

The above code block doesn't make it so the company field is shown on the frontend but it is show on the backend.

So the way that it's shown on the edit page is arbitrary to the frontend only for changing attributes I should've focused on the frontend.tsx.

Okay, so I got it to work by focusing on frontend.tsx. Now I just have to clean it up, run tests and send it to the official WC Blocks GitHub repo.

Okay now that I got all of the core functionality I need finished, now I just need to do clean up.

Now I'm trying to get rid of these type errors...

deuxPickupString is undefined on my block.tsx but not my frontend.tsx. So I really have to figure out how these props are being passed.

This is because on the edit side, I have this.

```
localPickupString={ attributes.deuxPickupString }
```

toDo:

"

Could have it so like on the edit page it'll be like an admin side, put the address of the shop's location.

Check to see how WC Legacy works and if it appears to look the same for a Local Pickup.

Also, see if I can get a second opinion to change how localPickupString is being duplicated into deuxPickupString just so that it can be changed and not read the default value of localPickupString.

Isolate the parts where I added them, as well as pull in new as well as document the PR which I am about to do.

"

Side note: WC Blocks shows the order being submitted when the order page has been opened not when the place order button is clicked and the process has been successful.

I am working on factoring out the duplication of localPickupString.

But I also need to do a git update.

But I don't really know how to do git updates so I'm just going to clone the most up to date version of the WC Blocks trunk and just add my edits manually.

I am taking a second look at viewing the attributes real value.

I think that I am able to view the attributes well on edit.tsx because props are passed into them via this [file](https://github.com/MonteLogic/woocommerce-blocks/blob/local-shipping-edit-pr/assets/js/blocks/checkout/inner-blocks/checkout-shipping-methods-block/index.tsx). But I'm not for sure. I am curious as to how Edit is being called in the [index.tsx](https://github.com/MonteLogic/woocommerce-blocks/blob/8122bb09e4e10a25473cecffc12d8295282953ba/assets/js/blocks/checkout/inner-blocks/checkout-shipping-methods-block/index.tsx#L23) file but I am not seeing it fill the props for the Edit function as I normally see props being piped into functions.

But while I'm waiting on input from different people I am going to update my GitHub repo and send the Pull Request.

For some reason I am getting a critical error on my site after git cloning the latest dev version of WC Blocks.

Because I am getting this critical error I am going to have to go through every commit of WC Blocks and see which push pushed to the repo created the critical error.

The commit at

4728ace09c0de5735ace44eb48ad08a23eae865d

is still bad.

So somewhere between the commit of, "e0ca483fe88f21bff5794258cb850267e148bf38" and the commit listed above a critical error occurs.

This commit is good:

80c6b26f1fd17f55877776ab471a6f1690ebbaeb

So current trunk to, 80c6b26f1fd17f55877776ab471a6f1690ebbaeb there is a critical error.

8ba1261e58c9bb638befae3382769e20fd21796a

4728ace09c0de5735ace44eb48ad08a23eae865d is good

error is in between 4728ace09c0de5735ace44eb48ad08a23eae865d and bfec2f3ad85d5f8affad8074d6c3f8bc1b9bd7e2

736eb493918c1dd15e5acd14b97b45e36f88b894 to 7631019fa73e4e38600f5187b945f2ad91cd1307 is the error.

The bad commit is on this [page](https://github.com/woocommerce/woocommerce-blocks/commits/trunk?after=436956b09ec71749717f476b0e96e037a02e0a39+69&branch=trunk&qualified_name=refs%2Fheads%2Ftrunk).

The bad commit is 8bd0d4d3e1d4bd0ef6b80022b54f520dd1b9e3a1

...

Alright, so what happened is, I'm having a tough time bringing the repo up to date. What I should have done was started with a first issue and get the hang of running git commands to pull the most recent repo. Then once I get the first issue done then I should start working on those large Pull Requests.

I am just going to release Extended Checkout.

...

I will be returning to working on Extended Checkout until I can not have a critical error.

See blog [post](https://montelogic.com/?p=1890).
