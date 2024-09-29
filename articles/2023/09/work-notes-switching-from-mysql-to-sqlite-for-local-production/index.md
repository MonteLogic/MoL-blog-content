---
title: "Work Notes: Switching from MySQL to SQLite for local production - Unfinished"
date: "2023-09-30"
---

there is no way I'm going to try to make another at my escrow server on my phone so I'm just going to be good at switching from sqlite and I'm sure you will be able to tell the difference. Your code will be able to run on user land which is the desirable method. This is a desirable method for writing code with Prisma and next js much better than Termux which is a dated platform.

```


const CURRENT_DB = process.env.CURRENT_DB;

if (CURRENT_DB) {
    console.log('The value of CURRENT_DB is:', CURRENT_DB);
} else {
    console.error('CURRENT_DB not found in environment variables');
}
```

Ran with:

```
bun run DB-swap/index.tsThe value of CURRENT_DB is: MYSQL
```
