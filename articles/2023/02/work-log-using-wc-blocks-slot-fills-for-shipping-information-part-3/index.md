---
title: "Work Log: Using WC Blocks Slot Fills for Shipping Information - Part 3"
date: "2023-02-06"
categories: 
  - "work-log"
---

What I am working on in this article:

\- Move the previous extended checkout's webpack config, components and integration into @woocommerce/extend-cart-checkout-block.

\- Customizing the plugin from a slot fill rendered view.

\- How the checkoutExtensionData prop is passed through.

Questions:

Why does every single component in the OG version of Extended Checkout need it's own webpack entry point when the @woocommerce/extend-cart-checkout-block can just bring components in 'seamlessly'?

\- Why are some slot fills rendered on both sides and some aren't?

\- How do I read attributes from the frontend?

\- Why is registerPlugin() function working just fine for rending the slot fill on both sides but apparently registerCheckoutBlock() function only renders the slot fill on the frontend view?

\- How to access block attributes via "php" in WordPress Gutenberg.

Issues:

\- The edit function doesn't seem to be working right because the save function is generating an error message. See here

Summary:

The npm [package](https://www.npmjs.com/package/@woocommerce/extend-cart-checkout-block) the new block is based off of.

I wonder how much I can add in the div area below.

```
const render = () => {
  return (
  <>		 
    <ExperimentalOrderShippingPackages>
      <div>test</div>
    </ExperimentalOrderShippingPackages>
```

I am getting 'checkoutExtensionData is undefined' when I tried to add it the seamless way.

I remember that because of some way the scope is it can work some functions, I have to find that piece of documentation where it explains that.

Looking at the other checkoutExtensionData within @woocommerce/extend-cart-checkout-block.

I think I'm going to move the block newsletter block to the folder where the rest of the blocks are. Then change the paths of the webpack see how I changed the paths and then apply them to the same blocks in the folder.

I think that in the file where registerBlockType is called (index.js) is where the props of checkoutExtensionData are and 'work'.

Manipulate the newsletter-block to be one of the components I already have on the OG EC and then add another component.

I manipulated the newsletter-block to be a card component and the edit page the checkbox was still there but on the frontend the checkbox wasn't there but the card component was.

The PR example appears to reference getSetting from [get\_script\_data](https://github.com/woocommerce/woocommerce-blocks/blob/trunk/docs/third-party-developers/extensibility/checkout-block/integration-interface.md#get_script_data) function.

...

I could check if it can access (block/editor) and if that is true then, I'll know I'm on the editor side.

"

I'm going to create a fake component then a real component based on the check. The real component will be on the clientSide and use checkoutExtensionData. The fake component will just show what will be on the client side. Also the fake component won't be rendered based on an attribute saying if the checkout will use one of the components.

"

I still need to figure out how to add multiple blocks but I have managed to adapt one block already so just have to reverse engineer to add the proper webpack entry points. But if that doesn't work I could just stuff it all into one file.

...

I guess I'm going to have to add attributes to the frontend like [this](https://github.com/MonteLogic/mol-custom-blocks/blob/main/mol-custom-block.php).

...

Looking at the action:

\_\_experimental\_woocommerce\_blocks\_add\_data\_attributes\_to\_block

attributes look like this on the frontend:

```
data-local-pickup-string="Matlack Florist HQ "
```

My goal is to view attributes on the editor side. If the attribute says show then show a dummy component on index.js. This will be viewed via a Redux call and rummaging through the resulting nested object.

I know that the way I have it set up with the OG Extended Checkout it won't show on the editor side ANYways and it can still edit attributes.

...

Looking at it, I think that I was too ambitious with what I was trying to get done because it appears to be 1\* minor Pull Request which is allowing me this functionality.

I need to get a code review from one of the WC Blocks repo maintainers.

I am referencing [this](https://montelogic.com/?p=2219/#get-editor-info).

```
wp.data.select('core/block-editor').getBlocks()
```

This [codeblock](https://montelogic.com/?p=2579/#code-block-select) is exactly what I'm trying to do.

The codeblock above applied to the scenario at hand doesn't work because I think it's the first thing to load.

SO I found out that I just needed to put the async code in the example component related to the additional code to add onto npx slot-fill-test.

...

It's in the checkout contact information block which may be one of the reasons it's loaded directly there. As for the instruction to assign to a certain inner block, I'm looking for this answer.

I wonder if the clientId changes based on different variables or it's always shipped out the same.

...

The clientId does NOT persist, per this [source](https://youtu.be/9fldNvfWW7U?t=1168).

SO how are we going to reliably grab the attribute which is an inner block of checkout-contact-information?

...

The attribute in the text of slot-fill-test does change and is rich text.

...

EC Refactor has the code I'm working on.

I managed to view the attributes by using dot notation to get into the object that was created from the select statement.

But somewhere I messed up being able to setAttributes so I have to use the slot-fill-test and then add all the network code in there again.

Extended Checkout works even though I couldn't get a successful alert on the Edit page. I need to configure a test for it, so I don't accidentally disconnect the edit component of a block in the future.

I am running into the issue of block validation on the Edit page of one of the blocks and is providing the following error message in the console:

```
Block validation: Block validation failed for `extended-checkout/date-time-picker` ( 
Object { name: "extended-checkout/date-time-picker", icon: {…}, keywords: [], attributes: {…}, providesContext: {}, usesContext: [], supports: {…}, styles: [], variations: [], save: Save(_ref2)
, … }
 ).

Content generated by `save` function:

<div class="wp-block-extended-checkout-date-time-picker"></div>

Content retrieved from post body:

<div class="wp-block-extended-checkout-date-time-picker">This is something </div>
```

This error may happen because I didn't properly fill out the Integration Interface.

I have to figure out why it's showing this message and in other blocks which use a similar scheme for the Edit component aren't.

So it looks like I'm going to have to rebuild it. I'm going to have find and edit component which works and then build it up from there, testing each step of the way if the Edit component logic is still working.

Adding a blocks folder.

...

I'm rendering double check boxes and I don't know why.

"

While I was debugging the checkbox control and why daytime pick a block is doing it? I should have checked the build folder to see if there is any sort of checkbox like any sort of like logic which would point to it being a checkbox within the build folder.

"

...

I need to figure out how the children prop is rendered because through this render an attribute is viewed. See:

```
<CheckboxControl
  id="subscribe-to-newsletter"
  checked={ checked }
  onChange={ setChecked }
>
{ children || optInDefaultText }
</CheckboxControl>
```
