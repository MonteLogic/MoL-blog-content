---
title: "Work Notes: Creating a control panel for WooCommerce Blocks checkout blocks."
date: "2023-02-18"
---

I need to focus on getting the children param because that's where a bunch of attributes are going to be which I can't normally access from the frontend without the children prop.

Notice if you would like to know why the checkbox is rendered underneath the contact block it because of two things within the block.json of a block.

"

{

"apiVersion": 2,

"name": "extended-checkout/date-time-picker",

"textdomain": "extended-checkout",

"title": "Date/Time Picker",

"description": "Pick the date and/or time of shipping.",

"supports": {

"html": false,

"align": false,

"multiple": false,

"reusable": false

},

"parent": \[

"woocommerce/checkout-contact-information-block"

\],

"attributes": {

"lock": {

"type": "object",

"default": {

"remove": true,

"move": true

}

},

"text": {

"type": "string",

"source": "html",

"selector": ".wp-block-woocommerce-checkout-newsletter-subscription",

"default": ""

}

},

"editorStyle": "file:../../../build/style-newsletter-block.css",

"style": "file:../../build/style-card-message-frontend.css"

}

"

Those two blue blocks are why it renders under the contact block.

...

When your working in webpack with WooCommerce blocks the names of the files that will be in the build folder are dictated by line preceding path.resolve. See:

```
'vanilla-block-edit':
  path.resolve(
    process.cwd(),
      'src',
      'js',
      'blocks',
      'vanilla-block',
      'index.js'),
```

The name of the file will be vanilla-block-edit and then php and js files starting with that preface.

Side note: it would be dope if I could pipe the string preceding path.resolve into the IntegrationInterface but in a very non-blocking way.

...

There's something going on behind the scenes which makes it so that if it's saved as an edit it'll show on the frontend even if there is no return statement for block.js.

If you check the database, you'll see the HTML comments. There you'll see what the page is really showing. I think it has something to do with the RichText component.

...

I'm wondering if a value can be set permanently using Redux.

I would rather create a custom API which has what should and shouldn't be rendered in the json result of the API call.

So the component will make an API call to see if they get rendered or not.

So I have to figure out how to create a custom API in WordPress.
