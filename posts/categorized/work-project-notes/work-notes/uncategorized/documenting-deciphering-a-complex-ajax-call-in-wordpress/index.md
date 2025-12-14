---
title: "Documenting: Deciphering A Complex Ajax Call in WordPress"
date: "2022-08-23"
categories: 
  - "documenting"
  - "working-on"
category-slug: "work-notes"

---

**New Day:** Tue 23 Aug 2022 06:19:42 PM CDT

I will be referencing this stackoverflow answer related to an AJAX operation which changes a radio view.

[stackoverflow answer](https://stackoverflow.com/questions/48156469/remove-shipping-cost-if-custom-checkbox-is-checked-in-woocommerce-checkout)

The answer says in order for this to work we have to manipulate the shopping sessions data.

```
// CODE FOR NO SHIPPING CHARGE ON LOCAL pickup 
// function that gets the Ajax data
add_action( 'wp_ajax_woo_get_ajax_data', 'woo_get_ajax_data' );
add_action( 'wp_ajax_nopriv_woo_get_ajax_data', 'woo_get_ajax_data' );
function woo_get_ajax_data() {
    if ( $_POST['billing_ups'] == 'pickup' ){
        WC()->session->set('billing_ups', 'pickup' );
    } else {
        WC()->session->set('billing_ups', '0' );
    }
    echo json_encode( WC()->session->get('billing_ups' ) );
    die(); // Always at the end (to avoid server error 500)
}
```

If you would to view the step by step process in which AJAX functions are written--which is called a dynamic hook--view this YouTube video [here](https://youtu.be/Tyzt4-oso8k?t=34).

Describing the formation of an AJAX call:

You have to the prefix of the name of the function such as:

Defining the logic of a dynamic hook in WordPress:

It always start out as:  
'wp\_ajax'

then other letters are appended to it.

The next part of the hook call which is appended is going to be appended by the action call  
in our AJAX function.

For example:

```
$.ajax({
url: ajaxurl
data: {
action: 'save_sort'
}
)};
```

We would then name append wp\_ajax with save\_sort making 'wp\_ajax\_save\_sort'.  
I have yet to see what the syntax for this would be without AJAX.

I have yet to see what the syntax for this would be without AJAX.

Then the function that's going to be in parameter two is the name of the php function.

Further more, there is another WordPress dynamic hook that is in this code as well: "wp\_ajax\_nopriv\_{$action}"

The description for wp\_ajax\_nopriv is: Fires non-authenticated Ajax actions for logged-out users. So if nopriv action wasn't included and just "wp\_ajax\_{$action}" then it would only work FOR logged in users.

What starts the process?

"When the action hook gets called it knows it's linked to that AJAX request and it calls your function."

So I'm assuming that it's the JavaScript that gets called first.

Keep in mind that the session data is on the server and is going to need to use php to communicate with it.

So that JavaScript check of:

`if ( $('#shipping_optn_1_pickup').is(':checked') )`

is triggered and the AJAX call is ran via the 'action' param with 'woo\_get\_ajax\_data''

What does `url: wc_checkout_params.ajax_url` mean?

I think that that may be reference point which is in Checkout.js.

I think that may have a hard time running that same AJAX call in plain JavaScript because Checkout.js is in jQuery.

I find this [article](https://newdevzone.com/posts/list-of-all-js-events-in-woocommerce) to be of value as well.

This [question](https://wordpress.org/support/topic/add-a-custom-fee/) could be answered.

"url:" field:

The url is "the end point in which to hit."

This can easily be checked by entry the url value into the console and it will return the endpoint. So in this instance, "wc\_checkout\_params.ajax\_url" which returns "/wp-admin/admin-ajax.php".

Which would be [this](https://github.com/WordPress/WordPress/blob/master/wp-admin/admin-ajax.php) file.

The data is the stuff that we're sending so I guess the php function has something related to the information that's on the server and interaction logic in it.

Connecting the AJAX Call to an input

In the function there is "billing\_ups" that is assumed to be a field. Also, this could be expected to be changed.

But before that, let's drill down what the cost of the session is so we can better change it.

Because, "to **alter Shipping methods costs** will only work if **you manipulate the shipping sessions data**".

I am working on logging the function conditional\_custom\_shipping\_cost. View the results:

logged [conditional\_custom\_shipping\_cost()](https://gist.github.com/MonteLogic/53929230613dc3d9a48bbcedd825056b) gist

https://gist.github.com/MonteLogic/53929230613dc3d9a48bbcedd825056b

Really, the function just gets a AJAX call to it from the client and then the server changes the cookies from Local Pickup or Delivery and then throughout the lifecycle of the checkout certain hooks will be fired which will check that cookie and then certain logic is conducted.

**Logging out:** Wed 24 Aug 2022 02:02:03 AM CDT

**New Day:** Wed 24 Aug 2022 02:53:30 PM CDT

I am now deciphiring the function refresh\_shipping\_methods():

```
add_action( 'woocommerce_cart_calculate_fees', 'refresh_shipping_methods', 10, 1 );
function refresh_shipping_methods( $post_data ){
    $bool = true;
    if ( WC()->session->get('billing_ups' ) == 'pickup' ) $bool = false;

    file_put_contents($log,"Message: ". ":114" . PHP_EOL, FILE_APPEND);
    file_put_contents($log,  WC()->cart->get_shipping_packages() . PHP_EOL, FILE_APPEND);

    // Mandatory to make it work with shipping methods
    foreach ( WC()->cart->get_shipping_packages() as $package_key => $package ){
        WC()->session->set( 'shipping_for_package_' . $package_key, $bool );
    }
    WC()->cart->calculate_shipping();
}
```

Alright, it does make sense, because [in the source code](https://github.com/woocommerce/woocommerce/blob/b2c3ef8f29535056265392cb251d8270026ba67d/plugins/woocommerce/includes/class-wc-shipping.php#L329) it appears to be required.

It is in the WC\_Shipping class and is apart of the function calculate\_shipping\_for\_package().

I still don't quite understand but I know it could be useful.

This [article](https://wp-qa.com/get-woocommerce-shipping-methods-programmatically) could be a good article to read further.

**Logging Out:** Wed 24 Aug 2022 10:39:12 PM CDT
