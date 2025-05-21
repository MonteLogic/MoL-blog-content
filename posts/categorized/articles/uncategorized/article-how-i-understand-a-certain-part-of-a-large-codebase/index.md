---
title: "Article: How I Understand A Certain Part of A Large Codebase."
date: "2023-01-05"
---

Goal: Explain to the user how I search through a large codebase so I can better implement a functionality.

I first see if it's small enough to know the whole Codebase so I skim through the file structure. If I realize I can't know the whole thing cause it's too big this is the process I go through.

I read as much of the documentation on the page as I can, then I make a path. This example would be in a React Gutenberg codebase.

I am trying to find the logic which manipulates the radio options so I can add different state triggers to them.

So I am trying to connect [block.tsx](http://assets/js/blocks/checkout/inner-blocks/checkout-shipping-methods-block/block.tsx) to [option.tsx](http://assets/js/base/components/radio-control/option.tsx). I wish there was a plugin to do this exploratory process easier.

So I would know that the radio options are option.tsx because I finely grain through the inspect element of the Firefox Devtools and then search the code base for the divs generated.

Then I search through the exports and imports of them until I find the connection. Keep in mind many of the exports and imports are aliased and you should be able to distinguish a named import for a variable import versus the default one.

If you would like to see what my investigative process looks like view the comment section for this [gist](https://gist.github.com/MonteLogic/e625e71889b9fd4919b0fe77e20a7a78).

Better yet, I write the path in which the logic is flowing from file to file as such:

[Scanned\_20230105-1339](https://montelogic.com/wp-content/uploads/2023/01/Scanned_20230105-1339.pdf)[Download](https://montelogic.com/wp-content/uploads/2023/01/Scanned_20230105-1339.pdf)

Then after I write it down, I try to make a step process and then go into detail about every step.

Flow Path of Code:

1.) option.tsx

I am looking in Option.tsx because that's where, ""wc-block-components-radio-control\_\_option" is. This is important because it's the name of the label of both of the options. I'm sure somewhere there is the logic to distinguish if the radio input is checked. On that file if I comment out the checked attribute and then it won't save it once I click off. I wonder if this "keeping" the attribute has something to do with the logic which defaults to Free Shipping once Local Shipping is clicked off.

I see that checked is a prop of Option so I'm sure state logic is passed through in a way I have yet to discern.

2.) radio-control/index.tsx

the const Option is imported and changed in name as 'import RadioControlOption from./option'. This works because const Option is a default export.

In this file the component with the checked prop looks as such:

```
{ options.map( ( option ) => (
	<RadioControlOption
		key={ `${ radioControlId }-${ option.value }` }
		name={ `radio-control-${ radioControlId }` }
		checked={ option.value === selected }
		option={ option }
		onChange={ ( value: string ) => {
			onChange( value );
			if ( typeof option.onChange === 'function' ) {
				option.onChange( value );
			}
		} }
	/>
) ) }	
```

So the checked value is now reliant upon the option =\[\] prop, more specifically option.value.

3.) ShippingRatesControlPackage/package-rates.tsx

Side Note: ShippingRatesControlPackage is a default export of a base component so it may be easily used in a third-party plugin.

The option is imported as:

```
import RadioControl, {
	RadioControlOptionLayout,
} from '@woocommerce/base-components/radio-control';
```

4.) cart-checkout/ shipping-rates-control-package/index.tsx

Then it is brought in as in internal dependency as:

```
/**
 * Internal dependencies
 */
import PackageRates from './package-rates';
```

5.) cart-checkout/shipping-rates-control/index.tsx

Again another internal dependency:

```
/**
 * Internal dependencies
 */
import ShippingRatesControlPackage, {
	PackageRateRenderOption,
	TernaryFlag,
} from '../shipping-rates-control-package';
```

Here is where the export "export default ShippingRatesControl" happens.

6.) checkout/inner-blocks/checkout-shipping-methods-block/block.tsx

The option logic is imported as:

```
import { ShippingRatesControl } from '@woocommerce/base-components/cart-checkout';
```

....

Now that I figured out the trail that the logic takes, I can manipulate it in different steps throughout the process to create my desired result. Throughout my editing I will go back and add more content or revise the trail the logic appears to take based on accuracy.
