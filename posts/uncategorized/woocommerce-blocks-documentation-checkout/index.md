---
title: "WooCommerce-Blocks Documentation: Checkout"
date: "2022-09-29"
categories: 
  - "documentation"
---

**useCheckoutAddress**: This is a hook found in [use-checkout-address.ts](https://github.com/woocommerce/woocommerce-blocks/blob/trunk/assets/js/base/context/hooks/use-checkout-address.ts) this hook is found in various files of [checkout-shipping-methods-block](https://github.com/woocommerce/woocommerce-blocks/tree/trunk/assets/js/blocks/checkout/inner-blocks/checkout-shipping-methods-block) folder. I beleive the value within it is used to hide the billing field. Found as a reliant boolean in this [file](https://github.com/woocommerce/woocommerce-blocks/blob/trunk/assets/js/blocks/checkout/inner-blocks/checkout-shipping-address-block/frontend.tsx).

In detail:

```
const { showBillingFields } = useCheckoutAddress();

if ( ! showBillingFields ) {
  return null;
}
```

**setBillingAddress**: I think this is used in the data store and will be sent of as information for the order. Found [here](https://github.com/woocommerce/woocommerce-blocks/blob/4fcb6b28d69903b00dd296dec08db32a8d5ee67a/assets/js/blocks/checkout/inner-blocks/checkout-shipping-address-block/block.tsx#L137), it does not change the view of the billing shipping field.

**setUseShippingAsBilling**(checked): This is a method which appears to take in a boolean if checked, if it is the case it won't pop up the billing address field. So I think that the Billing Address form is reliant upon this to show. Reading the official documentation it appears to be an action. This action can be fired anywhere in the store as their is one source of truth for state.

**showBillingFields**: This variable is declared on the [frontend.tsx](https://github.com/woocommerce/woocommerce-blocks/blob/4fcb6b28d69903b00dd296dec08db32a8d5ee67a/assets/js/blocks/checkout/inner-blocks/checkout-billing-address-block/frontend.tsx#L41) file of the checkout-billing-address-block. It is declared in the interface CheckoutAddress within the file of [use-checkout-address.ts](https://github.com/woocommerce/woocommerce-blocks/blob/4fcb6b28d69903b00dd296dec08db32a8d5ee67a/assets/js/base/context/hooks/use-checkout-address.ts#L33). But I think the assignment within the interface use-checkout-address.ts is for typescript compliance and not integration within business logic per se.

Within the use-checkout-address.ts there is the exported const of useCheckoutAddress which operates on the interface of CheckoutAddress. The const showBillingFields is then equated to useCheckoutAddress(). When showBillingFields is viewed in console.log it outputs true or false. If the checkbox for "Use same address for billing" is checked than it will be false. If it is not checked then it will be true.
