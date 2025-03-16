---
title: "Next.js Checklist:"
date: "2024-11-24"
---

Next.js Setup:

Remove the ability to commit directly to the master branch by using the UI.

Use Vercel.

In the README write down the Node version.

As for Code Analysis tools, using SonarCube comes with mixed results, ideally, you could put it in a queue of like a master level Next.js developer and they would run a code review. But I think you can do a lot of the code review issues by using static analysis tools and linters for the small changes and then eventually work towards code reviews from master tier developers.

Testing:

Write test scenarios and aim for tests which can be fulfilled by Vercel.
