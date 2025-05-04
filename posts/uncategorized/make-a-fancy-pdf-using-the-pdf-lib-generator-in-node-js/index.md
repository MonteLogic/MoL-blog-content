---
title: "Make a fancy pdf, using the pdf-lib generator in Node.js"
date: "2024-07-05"
---

Whether you're doing your taxes and TurboTax generates your tax records for you or you got a new certificate from an online education platform, PDF generation is an important service of an experienced web dev.

This isn't going to be a click and follow step-by-step tutorial, this tutorial will give you the tools to make your own PDF according. You'll be able to understand file generation on a deep level.

I would say the trickiest part of the process to understand would be the

Okay, so this:

```
addHeading(page, name, 50, 750, font);
```

We make a change:

```
addHeading(page, name, 150, 750, font);
```

This moves the heading to the right.

How big is a PDF page according to pdf-lib?

If the y value is lower it will get lower on the page.
