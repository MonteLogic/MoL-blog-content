---
title: "Article: Don't use saveEntityRecord for saving user meta within WordPress Gutenberg"
date: "2023-04-15"
---

I am trying to get something like this working:

  
I tried to use saveEntityRecord for changing user meta and it didn't work. In order to change user meta you have to register\_meta in php with show in rest set to true. Then, use a POST request to post to the endpoint with the body of the message with the meta\_key you would like to change.

The PHP:

```
/**
 *  Register user meta which will be changed via REST call.
 */
function my_register_user_meta() {
	register_meta(
		'user',
		'my_meta_key',
		array(
			'type'              => 'string',
			'description'       => 'My User Meta',
			'single'            => true,
			'show_in_rest'      => true,
			'sanitize_callback' => 'sanitize_text_field',
		)
	);
}
add_action( 'init', __NAMESPACE__ . '\my_register_user_meta' );
```

The JavaScript:

```
userDataThree = {
  meta: {
    'my_meta_key': 'my_new_meta_value'
  }
};

fetch('/wp-json/wp/v2/users/2', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'X-WP-Nonce': wpApiSettings.nonce // replace with your WordPress nonce
  },
  body: JSON.stringify(userDataThree)
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error(error));
```
