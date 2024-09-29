---
title: "Notes: Webpack in WordPress Gutenberg"
date: "2022-12-18"
---

I am currently having issues where I cannot get webpack to work and I get this error.

```
Error: Cannot find module '@wordpress/scripts/config/webpack.config'
```

The only remedy I've found is move @wordpress/scripts from devDependencies to dependencies.

Also, move other webpack related things from devDependencies to dependencies and that should clear up the errors.

Why this is? I do not know yet.
