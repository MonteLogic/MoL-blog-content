# MoL-blog-weba-wn-1

## Start: Thu Mar 20 2025 21:00:03 CDT

I like this component-sets idea for the .mdx.

```md
---
title: 'Advanced MDX with Custom Component Sets'
date: '2024-03-20'
description: 'This post demonstrates using multiple component sets for rich content'
author: 'Your Name'
tags: ['mdx', 'components', 'advanced']
componentSets: ['post-a', 'advanced-charts']
---
```

## Start: Mon Mar 24 2025 15:31:47 CDT

I am currently trying to compose, 'ui/address-bar.tsx' into smaller components.

The problem is if I don't have the .env vars for Stripe, it may trigger a false negative.

So the TaskBar needs to have the Stripe logic isolated and if the .env is not there than take out that part without triggering a false negative.

Okay, got that finished in the #5 issue, which is kind of going over scope. 
