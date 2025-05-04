---
title: "Create a React Context or add to same line, avoid prop drilling"
date: "2024-04-24"
---

TL;DR Prop drilling can be complicated and create buggy apps, try to avoid it.

When you doing props drilling it's important to know the limitations. A good rule is that if its small enough put it in the same component then do this. If it's too large to put in the same component use React context. This will avoid the creation of buggy app logic.

The input form for a CRUD page which I was working on, I found out putting it in the same file would've saved me a day and a half of work.

There is nothing wrong with having 200+ line files. Located [here](https://gist.github.com/MonteLogic/30540fb8753826f57f481fb89b025ce6) is the file of discussion (204 lines).

Still there is more CRUD logic to be created in order to edit previously submitted records.
