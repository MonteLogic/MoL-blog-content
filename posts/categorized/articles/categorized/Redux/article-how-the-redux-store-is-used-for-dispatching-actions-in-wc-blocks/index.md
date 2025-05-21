---
title: "Article: How The Redux Store is used for dispatching Actions in WC Blocks."
date: "2023-01-17"
---

Code flow for updating value via Redux:

![](images/SET_SHIPPING_ADDRESS-action.png)

How is this action triggering the reducer?

Step 1:

The following import of setShippingPhone is brought in a de-structured object of useCheckoutAddress().

```

// File path:
//  assets/js/blocks/checkout/inner-blocks/checkout-shipping-address-block/block.tsx
const {	setShippingPhone	} = useCheckoutAddress();
```

Step 2:

```
// File path:
//  assets/js/blocks/checkout/inner-blocks/checkout-shipping-address-block/block.tsx
➜ ➜ ➜ 
// This is linked up to the field component of <PhoneNumber />
// Which updates with onChange(value)
setShippingPhone( value );

```

Step 3:

The setShippingPhone method is described in the interface CheckoutAddress

```
// File path: 
// assets/js/base/context/hooks/use-checkout-address.ts
interface CheckoutAddress {
	setShippingPhone: ( value: string ) => void;
}
```

Step 4:

Then a custom hook is used for exposing address functionality to the checkout address form. The constant setShippingPhone is using a callback to set what appears to be a value within an object using a returnless function. << I wonder what setShippingAddress is doing >>

```

// File path: 
// assets/js/base/context/hooks/use-checkout-address.ts
export const useCheckoutAddress = (): CheckoutAddress => {
const { setShippingAddress } = useCustomerData();


const setShippingPhone = useCallback(
  ( value ) =>
     void setShippingAddress( {
        phone: value,
      } ),
	// I guess this is an array of dependencies:
	[ setShippingAddress ]
	);
	// Here the method is returned (again).
  return {
    setShippingPhone
  };
};

```

Step 5:

setShippingAddress is a dispatch to the store. Let's look at where useCustomerData() is and how it affects setShippingAddress. So when we use useCustomerData() we should have the variables customerData and isIntialized available to us as well as the method of setShippingAddress.  
How is useDispatch used here?  
When I console.log setShippingAddress it's just an empty function.

```

// File path:
// assets/js/base/context/hooks/use-customer-data.ts

/**
 * This is a custom hook for syncing customer address data (billing and shipping) with the server.
 */
export const useCustomerData = (): CustomerDataType => {
  const { customerData, isInitialized } = useSelect( ( select ) => {
  const store = select( storeKey );
  return {
    customerData: store.getCustomerData(),
   };
   } );
   const { setShippingAddress } = useDispatch( storeKey );
  console.log(setShippingAddress);
    return {
      setShippingAddress,
     };
};
```

Step 6:

```
// File path: 
// assets/js/data/cart/actions.ts
// I guess if it's an action it looks like this:
/**
 * Sets shipping address locally, as opposed to updateCustomerData which sends it to the server.
 */
export const setShippingAddress = (
	shippingAddress: Partial< ShippingAddress >
) => ( { type: types.SET_SHIPPING_ADDRESS, shippingAddress } as const );

```

Step 7:

```
// This is step 7
➜ ➜ ➜ 
// The type is
// File path:
// assets/js/data/cart/reducers.ts

/**
 * Reducer for receiving items related to the cart.
 *
 * @param {CartState}  state  The current state in the store.
 * @param {CartAction} action Action object.
 *
 * @return  {CartState}          New or existing state.
 */
const reducer: Reducer< CartState > = (
  state = defaultCartState,
  action: Partial< CartAction >
) => {
  switch ( action.type ) {
    case types.SET_SHIPPING_ADDRESS:
      state = {
	...state,
	cartData: {
		...state.cartData,
		shippingAddress: {			   ...state.cartData.shippingAddress,				...action.shippingAddress,
			},
		},
	};
	break;
}

```

Step 8:

```
// This is step 8
➜ ➜ ➜ 

export const ACTION_TYPES = {
  SET_SHIPPING_ADDRESS: 'SET_SHIPPING_ADDRESS'
} as const;
```

I can write to it but I can't read from it.
