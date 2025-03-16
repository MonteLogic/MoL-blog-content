---
title: "Using Clerk metadata to manage Stripe payments"
date: "2024-12-24"
---

Okay, so once a webhook fires from the checkout we will send the user's payment info to Clerk metadata.

## Segregate dev vs. prod concerns.

Make the same product but on the test and prod side.

Also make your prod and your dev .env values reflect a dev or prod instance.

Use a test card number for purchases, use '42424242424242', just a bunch of 42s and the date on the card needs to be a time in the future and the cvc can just be 123.

### ...

Currently I have the test checkout working and it's being redirected to the correct URL. Now I have to figure out how to send the Stripe data to Clerk.com.

### Setting up a Stripe webhook to send Clerk metadata

I'm running: "stripe:listen": "stripe listen --forward-to localhost:3000/api/webhooks/stripe".

So I downloaded the Stripe CLI, see [here](https://docs.stripe.com/stripe-cli?install-method=apt).

Then I authenticated it to my local machine and now the command, 'stripe:listen' works.

### Using the Webhook secret

Throughout this setup phase, you'll run the command, 'pnpm run stripe:listen' and then you'll see as an output:

```
> @ stripe:listen /home/MonteLogic/Downloads/temp/your-project
> stripe listen --forward-to localhost:3000/api/webhooks/stripe

> Ready! You are using Stripe API Version [2022-11-15]. Your webhook signing secret is whsec_12345abcd (^C to quit)


```

Notice the string which prefix is 'whsec\_'. You will be using this output from your command line to fill in the .env variable, STRIPE\_WEBHOOK\_SECRET.
