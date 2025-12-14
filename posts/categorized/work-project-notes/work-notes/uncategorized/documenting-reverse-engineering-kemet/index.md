---
title: "Documenting: Reverse Engineering Kemet"
date: "2022-09-22"
category-slug: "work-notes"
---

So I need to load up what the website looks like before the addition and see what was added exactly.

I am viewing the [GitHub repo](https://github.com/MonteLogic/kemet-fork) which I forked and making observations of it.

"Enable Sticky Header" functionality < commit 6

It looks like the commit for 'mobile logo' is the main scaffold to add it which commit #3.

The addition where the knob can be pressed and it works is on "block settings" commit which is #4.

But I also need to figure out how to add custom settings into Full Site Editing in WordPress.

On commit #4 it doesn't work but the knobs are there which is what I am interested in. However.... it appears to be in the build folder. This is problematic because it's suppose to be generated. It may be the case that they are writing code directly to the build folder rather than relying on an npm process to do it.

There's a Composer.json already on commit #4 I wonder what use Composer is going to play in the project.

On [templates-parts.js](https://github.com/MonteLogic/kemet-fork/blob/5957a0cc6517056c62911ccaad13ba342780fea8/inc/blocks/react/src/Blocks/template-parts.js) appears to be the React code for the toggler of the Enable Sticky Menu.

Okay, I've added templates-parts.js to my project now I have to access the build. The logic which enqueues it is located in inc/blocks/[class-kemet-blocks-settings.php](https://github.com/MonteLogic/kemet-fork/blob/5957a0cc6517056c62911ccaad13ba342780fea8/inc/blocks/class-kemet-blocks-settings.php). So I have to figure out how THAT gets connected.

This [article](https://dev.to/alexstandiford/make-webpack-configuration-easy-with-wordpress-scripts-26kk) explains how to use webpack with the WP scripts
