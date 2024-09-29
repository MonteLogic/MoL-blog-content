---
title: "Work Notes: Implementing Stripe payments for CB"
date: "2023-10-23"
---

I think we've been overthinking this.

I just have to have a record of users and the status of those users. Then use the Stripe API or PayPal API to update the status of those users.

Tie sign in logic with stripe logic, so we can see a list of users and the values they have, right now, I think it's anyone who signs in can see whatever.

I gotta work on Clerk.

When a new user is created or the uses hasn't been created before I need to add that to the system.

This is what we're doing a [paid trial](https://stackoverflow.com/questions/73111342/how-to-setup-paid-trial-in-stripe).

[Implement 1](https://dev.to/stripe/try-before-you-buy-adding-a-trial-period-to-subscriptions-248d)

Looking at adding [webhooks](https://stripe.com/docs/webhooks) and reading this [guide](https://nkrkn.me/writing/t3-stripe).

I am going to make a sub article of this about pinging the customer list of Stripe.

Now that I figured out how to ping the list of customers, there is not customer list obviously because we haven't had customers, also I would like to know whom is a customer for which product.

Now, we have to create a payment gateway to get a new customer.

...

I copied this website and now I just need to redo the .env.local for my own Stripe product and keep it moving.

Working on webhooks for Stripe, see [here](https://dashboard.stripe.com/webhooks/create?endpoint_location=local).

This [here](https://github.com/vercel/nextjs-subscription-payments) is what I'm looking for but it only works if your subscribed ig this is fine if it opens a popup to signin and then directly takes you to the checkout.

....

This subscription page is much more complex than just the dono site.

...

When the subscribe button is hit the following code is ran:

```
    try {
      const { sessionId } = await postData({
        url: '/api/create-checkout-session',
        data: { price }
      });

      const stripe = await getStripe();
      stripe?.redirectToCheckout({ sessionId });
    } catch (error) {
      return alert((error as Error)?.message);
    } finally {
      setPriceIdLoading(undefined);
    }
```

The business logic for the checkout session can be found, [here](https://github.com/vercel/nextjs-subscription-payments/blob/main/app/api/create-checkout-session/route.ts).

Currently trying to eliminate supabase anyone can pay for monthly (testing obv).

This [one](https://github.com/BastidaNicolas/nextauth-prisma-stripe) will work better for us because it uses Prisma and MySQL rather than being more different like the Vercel example mentioned earlier is.

...

We have to rewrite it to use clerk rather than nextauth then after that we will integrate that project into CB.

So we have to figure out,

{ getServerSession } from "next-auth";

equivalent in clerk.

This helps, [here](https://stackoverflow.com/questions/76309154/next-js-typeerror-failed-to-parse-url-from-when-targeting-api-route-relati) for my error.

Trying to get session data from the server, reading [this](https://clerk.com/docs/references/nextjs/read-session-data).

Okay, so we figured out how to get the client id via a fetch call. You have call it from the client NOT from a server component!

Then the route.ts file should look like:

```
import { auth } from '@clerk/nextjs';


export async function GET(request: Request) {
    const { userId } = auth();
    // Access user session data
    console.log(userId);

    if (userId) {
        return new Response(userId.toString(), {
            status: 200,
        });
    }
}
```

and the client, 'use client' should look like:

```
async function callClerkSessionRequest() {
    try {
        const response = await fetch('/api/clerk/user-session', {
            method: 'GET',
            // You can add any additional headers or options here if needed.
        });

        if (response.ok) {
            // The request was successful, you can now handle the response.
            const data = await response.text();
            console.log(data);
        } else {
            // Handle the case where the request was not successful (e.g., 404 or 500).
            console.error('Request failed with status:', response.status);
        }
    } catch (error) {
        // Handle any network or other errors that may occur.
        console.error('Request failed:', error);
    }
}
```

Reading this [README](https://github.com/BastidaNicolas/nextauth-prisma-stripe).

...

I think I'm going to add another account from zchavours@gmail.com and be like you can't access this cause your not dchavours@gmail.com and have it be only an account page with the account status of unpaid.

I just found out Clerk has Organization logic just out of the box.

We could work on that organization logic but we're still focused on getting that Stripe payment gateway working.

**Get payment gateway to work.**

Focusing on the [upgrade page](http://localhost:3000/upgrade).

I think I can make a rudimentary option based on emails but I'd much rather tie the clerk id and the stripe customer id together.

Save all clerk ids, I should be able to have a drop down of all relevant users which will tell me the user's Stripe id.

**Figure out how to get the Stripe customer id.**

The only thing I'm going to need is to like save the customer ( stripeID) with the clerkID. Everything else can just be like, pinged via the Stripe server

**Figure out how to get the products a customer is subscribed via their Stripe Customer ID used to ping the Stripe servers.**

https://stripe.com/docs/api/payment\_intents/list#list\_payment\_intents-customer

https://stripe.com/docs/api/charges/list#list\_charges-customer

This, [here](https://stripe.com/docs/api/subscriptions/list) is what I'm looking for but I'm still working on the params.

We would like to add the Organization switcher and get scheduling routine right. Also, integrate more route ID codes (415VNA, 258AVO).

**Adding Organization Switcher, get console.log off the organization a user is in.**

Working on the following code:

```
import Clerk from '@clerk/clerk-js';

    const clerkFrontendApi = `{{pub_key}}`;
    const clerk = new Clerk(clerkFrontendApi);
    await clerk.load({
      // Set load options here...
    });
```

Looking at [getOrganization()](https://clerk.com/docs/references/javascript/clerk/organization-methods#get-organization)

We should have been destructing the object like this rather than putzing around with those Interfaces.

```

    const { status,
        start_date,
        current_period_end,
        trial_end,
        items
  } = subscriptions.data[0];
```

Doing something like this could've fixed it but I'm going to keep on rolling:

```
interface SubscriptionWithPlan extends StripeSubscription {
  plan: string;
}
```

...

7 - refresh is the commit which fixed the issue of the constant refresh bug.
