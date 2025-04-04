---
title: "Work Notes: Adding Multiple Blocks to the WooCommerce Blocks Checkout Page."
date: "2022-12-21"
---

I wrote this piece of code which takess in multiple paths rather than just one.

```
public function register_editor_scripts()
    {
// I think if it looks for a block that isn't there a critical error
		// is created this could be very bad so I need to figure out
		// a full proof way* of that not happening. 

		// But it'll apparently accept a block that's not there and 
		// continue throughout the loop.
        $script_paths = array(
            '/build/newsletter-block.js',
            '/build/custom-fields-block.js',
        );

        foreach ($script_paths as $script_path) {

            // Use a regex pattern to extract the characters after '/build/' and before '.asset.php'
            preg_match('/\/build\/(.*?)\.js/', $script_path, $matches);
            $script_name = $matches[1];

            $script_asset_path = dirname(__FILE__) . '/build/' . $script_name . '.asset.php';

            $script_asset = file_exists($script_asset_path)
            ? require $script_asset_path
            : array(
                'dependencies' => array(),
                'version' => get_file_version($script_asset_path),
            );

            $script_url = plugins_url($script_path, __FILE__);

            wp_register_script(
                'newsletter-test-editor',
                $script_url,
                $script_asset['dependencies'],
                $script_asset['version'],
                true
            );

            wp_set_script_translations(
                'newsletter-test-editor', // script handle
                'newsletter-test', // text domain
                dirname(__FILE__) . '/languages'
            );
        }
    }
```

I currently cannot get get\_editor\_script\_handles() to run within the IntegrationInterface without crashing the site.

When I put this simple piece of code in the IntegrationInterface it crashes the site as well.

```

	function function_five(){
		return 5;
	}

	function handles_output(){
		$editor_script_handles = get_editor_script_handles();
                // send email
                mail("someone@example.com", "My subject",
                    "\n \n  1 -" .
                    json_encode(function_five()) .



	}
```

Trying to figure out if making multiple integration interfaces is the way to go. Or just have one that does multiple scripts. I think the former option would be the easiest.

OG IntergationInterface, [here](https://github.com/woocommerce/woocommerce-blocks/blob/343f70d7af57f751c327349dec864f9e176d0f70/src/Integrations/IntegrationInterface.php)

OK, So what you're doing, whenever you get\_script\_handles is you are telling the integration interface something. So I need to like tell it something good so we can it can enqueue on the checkout page. I guess.

...

Okay, so I have to Place all the stuff that I was doing with strings For the magic that runs do it in iteration, loop start to replace all that with strings and see if it's still works. Then once it works go back and then replace it with the string again.

Okay I did that and it work so the issue may be the value that is in the second iteration of $script\_paths.

For some reason I wasn't checking the edit page but the checkout page. The checkout page was looking fine but the edit page was breaking the whole time so I have to retry my experiments.

I am getting the error of

```
Block validation: Block validation failed for `extended-checkout/radio-options` ( 
Object { name: "extended-checkout/radio-options", icon: {…}, keywords: [], attributes: {…}, providesContext: {}, usesContext: [], supports: {…}, styles: [], variations: [], save: Save()
, … }
 ).

Content generated by `save` function:

<div class="wp-block-extended-checkout-radio-options"></div>

Content retrieved from post body:

<div class="wp-block-extended-checkout-radio-options">I want to receive updates about products and promotions.<br><br><br></div>
```

Okay, the problem is when I add the IntegrationInterface it apparently double registers it. So I need to figure out why for multiple-blocks when I add the IntInterface it gives me an error but not for extended-checkout.

registerCheckoutBlock doesn't seem to interfere with the register process.

It's only this wp\_register\_script that does

```
// Here seems to be the issue with the double register.
wp_register_script(
 'extended-checkout-editor',
 $script_url,
 $script_asset['dependencies'],
 $script_asset['version'],
 true
);
```

The problem was in the function:

```
	public function register_editor_scripts() {
		$script_path       = '/build/js/radio-options/radio-options.js';
		$script_url        = plugins_url( $script_path, __FILE__ );
		$script_asset_path = dirname( __FILE__ ) . '/build/js/radio-options/radio-options.asset.php';
		$script_asset      = file_exists( $script_asset_path )
			? require $script_asset_path
			: array(
				'dependencies' => array(),
				'version'      => $this->get_file_version( $script_asset_path ),
			);

			// Here seems to be the issue.
		wp_register_script(
			'extended-checkout-editor',
			$script_url,
			$script_asset['dependencies'],
			$script_asset['version'],
			true
		);

		wp_set_script_translations(
			'extended-checkout-editor', // script handle
			'extended-checkout', // text domain
			dirname( __FILE__ ) . '/languages'
		);
	}
```

The problem was I registered the editor script twice rather than just the block. So I went into the block.json of radio-options and changed the editor styles.

....

OK, So what I'm trying to do is. I'm trying to get multiple blocks on the checkout page. Using the multi-blocks [repo](https://github.com/MonteLogic/multiple-blocks) that I forked, then I'm going to switch it over to the extended checkout one. But I need to have multiple blocks on there and have it look good. The one that I need is not going to be wrapped in PHP tags, it's going to be in a Div and then things are added to that did in between the div such as.

```
<div data-block-name="extended-checkout/radio-options" class="wp-block-extended-checkout-radio-options"></div></div>
```

This is the case because the problem with my other one. Was that I could have it alert something. But I can't make it show up on the checkout block because the div wouldn't be there. So I need to figure out how to put the div thing there so that it can add on to check out by can't yet figure that out.

Still trying to get the block to render to the checkout.

I need to get something like this in there:

```
<div data-block-name="woocommerce/checkout-newsletter-subscription" class="wp-block-woocommerce-checkout-newsletter-subscription">
```

I am looking at this filter:

```
add_filter('__experimental_woocommerce_blocks_add_data_attributes_to_block', [ $this, 'add_attributes_to_frontend_blocks' ], 10, 1 );
```

Okay, so what I'm going to do is for add\_attributes\_to\_frontend\_blocks, I'm going to make it return an array. Just another first block in the second block, I want to add.

If that doesn't work, then it's going to have multiple ad underscore filters with the blocking name.

...

Really tempted to like make for every single block. I'm really tempted to make for every single block an IntegrationInterface. That's the only way I can really do it because I'm I'm going to try to mess around with this for a little while and try to see if I can work.

But it I'm just going to end up doing that probably.

...

I am going to to open up an issue on GitHub repo and it will read as such:

> I've made a project with only one IntegrationInterface file which uses regexs to register multiple scripts but I wasn't able to have it render a block to the allotted slot fill. So I could only add one block to the checkout but have multiple scripts.
> 
> I am currently trying the approach of having multiple IntegrationInterface files and each file is registering it's own block. So if I have two II files I'll have two blocks.
> 
> What would be the proper way of doing this viz. registering multiple blocks with the IntegrationInterface.

On that issue I know that there is a way to extend the endpoints which could prove useful, seen [here](https://github.com/mailchimp/mc-woocommerce/blob/master/blocks/woocommerce-blocks-integration.php).

Looking at it, yeah I think that one IntInterface per block and my evidence is this action.

```
    add_action(
        'woocommerce_blocks_checkout_block_registration',
        function ($integration_registry) {
            $integration_registry->register(new Custom_Block_Integration());
        },
        10,
        1
    );
```

I got it working with current folder scheme of multiple integrations. It doesn't work yet but it is reading the location of the files.

....

What I'm doing is I'm looking to look through newsletter-test and then I'm going to be able to look at the the block. And then I can take a list of everything, thats on the checkout. Dash two page, view source.

newsletter-block-frontend is showing up in the view source.

```
<script src='https://website.local/wp-content/plugins/newsletter-test/build/newsletter-block-frontend.js?ver=2d36a7a28c9dc06eb8205ebf3ea9eebf' id='newsletter-test-frontend-js'></script>
```

For some reason I am getting this path.

```
<script src='https://website.local/wp-content/plugins/extended-checkout/integrations/build/date-picker-frontend.js?ver=2.0.0' id='date-picker-script-frontend-js'></script>
```

Also before I change that I didn't see a data-block-name with the name of the newletter-test-block.

The answer to this may be [here](https://github.com/woocommerce/woocommerce-blocks/blob/1db184daa15b348e281739d007ddfa3f74660f61/docs/third-party-developers/extensibility/checkout-block/integration-interface.md).

I got it to work but I don't think the index.asset.php is working well so I gotta figure that out as well. Also, have to spiffy up the calendar.

I managed to get it linked up but now I am getting the error.

```
Unexpected error in: extended-checkout/date-time-picker

Error: moment__WEBPACK_IMPORTED_MODULE_2___default() is not a function
```

I got rid of the part where moment was used. Now it works.

...

I am now getting this error:

```
extensions > date-picker is not of type object.
```

When I try to submit an order.

I commented out schema\_callback and I got rid of that error.

Fixed the error but date don't show

I worked to fix the error by changing newsletter-test, I wish there was more information brought up by the error message.  
However, I am getting this back from doing the following

```
            // send email
            mail("someone@example.com", "My subject",
                "\n \n  1 -" .
                json_encode($extensions) .
                "\n \n 2 -" .
                json_encode($optin) .
                "\n \n 3 -" .
                $order->id .
                "\n \n 4 -" .
                json_encode($date_data)
                . "\n \n 5 -" .
                " - 504") .
                json_encode($billing)
                . "\n \n  6 -";
```

1 -{"date-picker":{"optin":\["2022-12-28T04:13:16.531Z"\]}}

2 -\[""\]

3 -7443

4 -\[""\]

5 - - 504

Now I have to wire up the radio options component as well as the integration and have that work well.

So work on the second block.

I've noticed I haven't even linked up the script\_asset\_path and it appears to be working fine. I should look into why that variable might be important.

I got the front page checkout page working but now the edit page is broken and working on fixing it.

For some reason when I can the namespace from 'my-plugin-namespace' to 'extended-checkout/custom-fields'.

TIL the block.json is more than just a list of things. It's important to how your app rendered.

```
 Fixed checkoutExtensionData not found

It turns out I have to change what's in the block.json which is really
nuts. I wish I could have found that out sooner reason being I can now
and have refactored out a couple of functions and added more
functionality.
```

I'm having a hard time loading the webpack for the wordpress/components and I am getting this error:

```
_wordpress_components__WEBPACK_IMPORTED_MODULE_2__ is undefined
```

I am going to try this later with a different webpack setup and hopefully I won't get this error.

But for now I am just going to use MUI for what I'm trying to do.

So I have to connect that and make it go to the admin are so the admin can view which radio option the user chose.

Okay so I extended the store API and it worked, so I gotta figure out where it's at.

I linked up the custom fields I want, now I have to be like yooo where is the login page, type stuff.

I have to make a field for the card. So it can be sent to the recipient.

I just found out if you import a scss file then it'll be built but if it's not actively used in the file then it won't be built.

I got what I needed to do done as far as functionality. What I would like to do is to run a PR on WC Blocks and add the logic I'm using to make EC work becuase at the moment I am using a dev version with my own code added. If a customer were to update WooCommerce or WC blocks may edits may just go away. So I would like to add onto the repo.

Also, this may take a month or so just to be reviewed after it has been sent out so I should do it now.

Need to read through these [files](https://github.com/woocommerce/woocommerce-blocks/tree/trunk/docs/contributors) and get to work on the Pull Request.

I am going to be reviewing [this PR](https://github.com/woocommerce/woocommerce-blocks/pull/8024) in particular because it is related to SlotFill.
