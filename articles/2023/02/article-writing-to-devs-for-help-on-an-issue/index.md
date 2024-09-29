---
title: "Article: Writing to Devs for Help on an issue."
date: "2023-02-04"
---

I am trying to contribute to this project and I got all of the Twitter handles and some the emails of people who contributes often and I wrote to them and I only heard back from one person and they told me to make an create an issue on the repo.

Although, making an issue is helpful, I am looking for a quick piece of insight to continue my programming and a lot of times if you make an issue some who is much better at coding then you are shows up to the issue and fixes it. This isn't a problem if your a highly experienced dev with multiple successful Pull Requests to your name but if you are a new to intermediate dev, you are looking to do your own first Pull Request are just looking for quick help.

I'm going to be tweeting this at developer advocates and placing it on Slack and other various platforms which are advertised as a place to get help for pertinent issues related to a WordPress codebase and more specifically WC Blocks repo.

The Issue at hand:

```
I have this piece of code which duplicates an attribute and then sends in the current value of the attribute as such:

"
import { store as blockStore } from "@wordpress/blocks"


export const Edit = ( {
	attributes,
	setAttributes,
}: {
	attributes: {
		deuxPickupString: string;
	};
	setAttributes: ( attributes: Record< string, unknown > ) => void;
} ): JSX.Element | null => {
	const getBlocks = useSelect( ( select ) =>
		select( blockStore ).getBlocks()
	);

	const showString =
		getBlocks[ 0 ].innerBlocks[ 0 ].innerBlocks[ 4 ].attributes
			.localPickupString;

	setAttributes( {
		deuxPickupString: showString,
	} );

"

Notice how deuxPickupString is viewing the value of an attribute via a select call. However, when I just call the value of an attribute I only get a default value, I would like to factor out the select call and only use the valuof localPickupString but when I just view the value of the localPickupStringbut it won't show the current value only the default value. 

```

I submitted the above codeblock to ChatGPT it just rewrote the select and call and talked about state which isn't helpful because the select call on the file this is taken from works just fine.

This [file](https://github.com/MonteLogic/woocommerce-blocks/blob/local-shipping-edit-pr/assets/js/blocks/checkout/inner-blocks/checkout-shipping-methods-block/edit.tsx#L130) on this [line](https://github.com/MonteLogic/woocommerce-blocks/blob/8122bb09e4e10a25473cecffc12d8295282953ba/assets/js/blocks/checkout/inner-blocks/checkout-shipping-methods-block/edit.tsx#L130), I call attributes.localPickupString and it works but when I call it on the frontend or pass it as props it just read the default value. I want it to read the current value but its not.
