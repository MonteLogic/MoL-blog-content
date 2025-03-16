---
title: "Work Log: Settings Up Google Analytics Properly on Next.js 13+"
date: "2025-02-02"
---

## **Note**\*\*\* You are better off using [Vercel Analytics](https://vercel.com/docs/analytics/quickstart#add-the-analytics-component-to-your-app) as the setup is 10x easier.

## Compose concerns

Compose concerns means to break it up into components rather than writing all of your script tags hard coded onto the app/layout.tsx page.

```
    <html lang="en">
      <GoogleAnalytics gaId={process.env.NEXT_PUBLIC_GA_ID as string} />
      <body>{children}</body>
    </html>
```

## Use the third party library from Next.

The Next.js third party library provides a ready made Google Analytics component seen, [here](https://nextjs.org/docs/app/building-your-application/optimizing/third-party-libraries#google-analytics).

Note, you don't NEED to upgrade to the latest version for it to work simply use the following install command with your preferred package manager.

```
pnpm install @next/third-parties@latest
```

## Use the a public env variable to store the gaId.

Note in this code, [the file](https://github.com/vercel/next.js/blob/58e1bd29a1563032244ee6d3ca689eb255756e0d/examples/with-google-analytics/app/layout.tsx#L16).

```
   <GoogleAnalytics gaId={process.env.NEXT_PUBLIC_GA_ID as string} />
```

## Issues with Google Analytics and Clerk

Note, when using clerk, Google Analytics won't be able to verify your state when your not signed in.

## Next.js 15+

In order for it to work properly you must upgrade to this version in above. This may require a significant rewrite of the web app.
