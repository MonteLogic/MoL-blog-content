---
title: "Documenting: Making Attribute Filter work on Category Page - Part 2"
date: "2022-10-22"
category-slug: "work-notes"
---

In the prior post, I made the point that it would be easier to use the rendering method All Products was using and then modify it with React on re-render as it is going to need pagination. Not to mention, that there could be possible 100's of products with a certain attribute and I don't think CSS tricks are going to cut it.

So let's study in-depth the rendering processes of certain blocks compared to others. I'll be re-reading this [post](https://developer.woocommerce.com/2021/11/15/how-does-woocommerce-blocks-render-interactive-blocks-in-the-frontend/) on developer.woocommerce.com and comparing it to the different methods of rendering observed in the "woocommerce-blocks" project.

"We read `data-` HTML attributes and pass them as `props` to the component."

"We created two new files, block.js and frontend.js. One will contain our shared component, and the other will render it on the front end."

So apparently block.js contains the 'shared component'.

It looks like Products by attribute doesn't even have front end dot JS. And I wonder if within that frontend.js would be logic to keep it 'alive' and not save it into the HTML file.

I'm theorizing that the products by attribute. Block is using. The server side render to save it into HTML and I'm looking within the docs of its. And it's saying that, so I still gotta do more research into it.

Looking into the Docs of ServerSideRender appears to be a legacy component which should be factored out in favor of use of newer APIs.

So in this code block it splits or maybe assigns it to the same variable as props.

```
export const ProductsByAttributeBlock = ( props: Props ): JSX.Element => {
  const { attributes, name } = props;
    if ( attributes.isPreview ) {
      return gridBlockPreview;
    }
  return <ServerSideRender block={ name } attributes={ attributes } />;
};
```

the const attributes is logged out as an object and name is a string which is 'woocommerce/products-by-attribute'.

I'm looking at the edit button with [index.tsx](http://assets/js/blocks/products-by-attribute/index.tsx) and I think the save button just saves what's there and there's no need to overthink it.

ServerSideRender know the attributes of the component.

I'm starting the transformation.

I know the old way of ServerSideRender component is just a way to see the editing portion of a block which is legacy so I know I'm going to have to update that.

**Done for the day:** Sat Oct 22 2022 20:06:21 GMT-0500 (Central Daylight Time)

I am analyzing the renderFrontend blocks and it's uses. It exports a const from [render-frontend.tsx](http://assets/js/base/utils/render-frontend.tsx).

Okay, so I'm learning within the php files is where we are putting the frontend.js for it to be loaded. Notice as in the frontend.js there are no export statements.

I couldn't find it in php files so that post made by woocommerce-blocks is outdated however there is a [webpack](http://bin/webpack-entries.js) file which goes about searching for frontend.js.

I'm looking in the attributes-filter folder to see the way frontend.ts was exported.

I commented out renderFrontend and it still loaded in the React component area.

I added a React component, <Button /> to the return value and it showed it on the edit side but not on the frontend side. And when I save that React button on the edit side it doesn't show it on the frontend even after the save.

When I comment out renderFrontend form frontend.tsx the component won't load so I think React is being funneled through there.

But now I have to figure out how to wire up a frontend.tsx component.

When the block is moved from the src folder in a php file it is moved to another js file in this [PR](https://github.com/woocommerce/woocommerce-blocks/commit/8ac4e9bfc39b892ed03a729e4a35fa43d0b3ab16).

So the -frontend was moved to src/BlockTypes/AbstractBlock.php.

However, product-attributes block uses the class of AbstractProductGrid so I wonder how those assets are loaded.

I wonder if All Products block uses the AbstractProductGrid.

I think a lot of API calls are happening in the php files.

The registering and enqueuing of assets rely isn't on AbstractProductGrid nearly as much as it is on AbstractBlock.

Ok, so All Products IS an AbstractBlock

So it looks like I'm going to have to rewrite Products By Attribute block from a AbstractProductGrid to an AbstractBlock to get my logic/JavaScript to render on the front end. With the model of what to rewrite the [AllProduct.php](http://src/BlockTypes/AllProducts.php) file.

**Done for the day**: Sun Oct 23 2022 18:13:44 GMT-0500 (Central Daylight Time)

Before I rewrite it, I want to take stock. Of all of the. Functions which are for each class so I have a checklist of what to replace.

.....

Okay, so we have to get block attributes.

When I change to AbstractBlock it goes away.

Okay, so I changed the AbstractBlock and it broke so I gotta like unbreak it.

**Done for the day:** Mon Oct 24 2022 22:05:26 GMT-0500 (Central Daylight Time)

Think that I got the console lock to work based on the fact that I changed it to abstract block. And I do some other stuff. I am got drunk, more importantly. Oh yeah, I changed it to abstract law, abstract block and then I changed products by a change. I added product detected cash, blockers, check or name products by attribute.

And then I went into the front end.TS Then I do that. So I just need to make sure not to delete my VS code and tomorrow I'm going to integrate this into my personal project and then build upon that console.log to run more JavaScript for my desired needs.

The goal is to have the same functionality as such but run in React(AbstractBlock) and not just from an HTML file(AbstractProductGrid).

....

I am looking at the types within types.ts. Not sure on what every single type does and how they're being applied. This interface in particular.

```
export interface Attributes {
	align?: BlockAlignment;
	attributes: Array< string >;
	attrOperator: 'all' | 'any';
	columns: number;
	contentVisibility: {
		image: boolean;
		title: boolean;
		price: boolean;
		rating: boolean;
		button: boolean;
	};
	orderby:
		| 'date'
		| 'popularity'
		| 'price_asc'
		| 'price_desc'
		| 'rating'
		| 'title'
		| 'menu_order';
	rows: number;
	alignButtons: boolean;
	isPreview: boolean;
	stockStatus: Array< string >;
}
```

I need to go through every single one and see how they are being interacted with and how they are in all likelihood being changed by the Gutenberg editor process. As well as an explanation of the type definition and how the type is being used.

Ok, lets look at '`align?: BlockAlignment;`'

What is BlockAlignment?

A type imported from '@wordpress/blocks'.

...

I am trying to figure out how the All Products block makes it's API call.

It appears the API call is coming from ProductListContainer.

```
<ProductListContainer attributes={ attributes } urlParameterSuffix={ urlParameterSuffix }/>
```

...

Having issues with GH today, as far as getting code to work and learning the GH system more.

But on the project I am getting this webpack error:

'There is no route for the given namespace (%s) in the store'

I am trying to figure this out and if it is related to JavaScript or php.

...

Okay, so I found the problem the commit at [5e7a571e57867297d124802d86277ae88743542e](https://github.com/MonteLogic/woocommerce-blocks/commit/5e7a571e57867297d124802d86277ae88743542e) was bad.

It appears I had to add the function hydate\_from\_api() as well as include it in the function enqueue\_data().

Now I gotta go back to doing what I was doing before that API call.

Okay, so the selector for products by attribute is off. So I got to go into like, the nitty-gritty of it and see what the selector logic is for, and how it brings in like focuses, like how the focus is on stuff. I got, like, focus on that for the products.

Then, look at how the price filters focuses on it viz. different times in which it renders.

It may have something to do with the props.

OK, so woo commerce slash products by attribute. It's not even loading as a block at all, so I'm gonna check the other one on the Dash 2 to see if it works as well.

I am re-reading '[How does WooCommerce Blocks render interactive blocks in the frontend?](https://developer.woocommerce.com/2021/11/15/how-does-woocommerce-blocks-render-interactive-blocks-in-the-frontend/)' even though it's kinda dated.

So apparently I need to master the ins and outs of dynamic blocks.

What is '`render_callback'`?

The problem that I'm running to is that the part dump that I did just running into nothing. It's just an empty string but while the other one that is working is not empty string. Need to figure out how that happens as well as like the instance of it.

Notice the following var\_dump:

```
public function render_callback( $attributes = [],  $content = '', $block = null ) {
  $render_callback_attributes = $this->parse_render_callback_attributes( $attributes );
  if ( ! is_admin() && ! WC()->is_rest_api_request() ) {
   $this->enqueue_assets( $render_callback_attributes );
  }

  var_dump($this->render( $render_callback_attributes, $content, $block ));

  return $this->render( $render_callback_attributes, $content, $block );
}
```

For the var\_dump()s I am getting the following:

```
/home/monte/Local Sites/matlackrebuild/app/public/wp-content/plugins/woocommerce-blocks/src/BlockTypes/AbstractBlock.php:90:string '
<div class="wp-block-woocommerce-price-filter is-loading" data-showinputfields="true" data-showfilterbutton="false" data-heading="Filter by price" data-heading-level="3"><span aria-hidden="true" class="wc-block-product-categories__placeholder"></span></div>
' (length=259)

/home/monte/Local Sites/matlackrebuild/app/public/wp-content/plugins/woocommerce-blocks/src/BlockTypes/AbstractBlock.php:90:string '' (length=0)
```

Why is it blank?

Why is the instance of the $block being detected or absent?

I am looking at the addition of rating filter block as a way to see how to add/change a new block.

The compiled list of changes is a follows:

[7048/files](https://github.com/woocommerce/woocommerce-blocks/pull/7048/files)

[7311/files](https://github.com/woocommerce/woocommerce-blocks/pull/7311/files)

[7370/files](https://github.com/woocommerce/woocommerce-blocks/pull/7370/files)

[7384/files](https://github.com/woocommerce/woocommerce-blocks/pull/7384/files)
