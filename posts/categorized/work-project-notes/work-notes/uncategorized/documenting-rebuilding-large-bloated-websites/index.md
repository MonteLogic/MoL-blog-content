---
title: "Documenting: Researching Rebuilding Large Bloated Websites"
date: "2022-08-15"
categories: 
  - "documenting"
  - "not-working-on-now
category-slug: "work-notes"
"
---

New Day: Mon 15 Aug 2022 02:17:38 PM CDT

Okay, I often come across huge sites that have been jiggered together with plugins because the people running the site don't know how to code to create custom solutions. So what often ends up happening is ... lots of plugins and lots of complicated logic. Also, a visual builder is used which makes things even more complicated, especially when things like Gutenberg are an improvement upon them.

So, I am going to be rebuilding a large site. I won't be sharing details but rather techniques useful for any large site.

In this case we will be rebuilding a site that uses Divi theme.

There's a bunch of starter themes for Developers but I used to see job postings for Genesis so I'm just going to use that one.

Also, Genesis appears to be ran by WP Engine which is also the same people who run Local by Flywheel.

Alright so I got the theme running but it's telling me to use a child theme rather than go on their theme marketplace and look for a child theme. I am going to scaffold one with WP CLI.

The command WordPress.org asks us to use is

```
wp scaffold child-theme sample-theme --parent_theme=twentysixteen
```

But how do we find the proper parent\_theme name?

I ran wp theme list on the WP CLI and the name which makes sense is 'genesis'.

Alright let's run:

```
wp scaffold child-theme sample-theme --parent_theme=genesis
```

Alright, it worked and the name of the theme is Sample-theme.

Let's add it to a git repository.

Alright, I've added it to a git repository.

What I did was cloned another site in the LocalWP then I added the blank sample theme, so the goal is to make that blank sample theme match the reference one.

Now, the site to build is blank. My plan is to match the mobile view of the bloated site. But I don't know where to start so I'm going to copy code from other sites using Genesis. I've done this same method of copying with Bootstrap sites with mixed results so let's see I have better success with Genesis.

Ok .... the vanilla genesis framework doesn't have a whole lot of docs behind it and it has npm stuff in it .. which makes it complicated ... so I'm just going to work off of the sample.

I take that back, it appears those npm and composer commands appear to be only for linting and checking standards. I intend to use similar scripts to automate upcoming workflows.

Okay now that I'm settled on the plain theme ... Let's add a menu.

I'm going to clone the sample Genesis theme and then isolate the logic that creates and shows the menu.

Side note: Definitely going to put a night mode on this theme.

Okay, so I looked at the sample folder and I couldn't find the class that issues the mobile showing logic when I ran :vimgrep /genesis-mobile/ \*_/_ in the genesis-sample folder.

And I figured it out why that's the case when in the GitHub page it says

1. Upload the Genesis Sample theme folder via FTP to your wp-content/themes/ directory. (The Genesis parent theme needs to be in the wp-content/themes/ directory as well.)

So the theme I'm looking at (Genesis Sample ) is ACTUALLY a child theme

Okay, so I'm guessing there is only styles in the Genesis Sample theme.

Alright, concluding that it's mostly styles I found the style block that is related to menu.

This is the style block related to menus that I am adding to the starter-theme. I am focusing on the mobile menu first.

[Styles added part 1.](https://gist.github.com/dchavours/bbb4f26677e420313eba530526115f52)

Alright I added the styles and now the menu looks like a formatted list, I don't want that although that's dope it reads the styles. I want it to be the reference one where it looks like a burger menu on mobile.

Honestly, at this point I'm too lazy to look through the files of the sample-theme for the dashicons menu burger and all that so I'm going to search elsewhere on the internet and hopefully not have to bring in new assets.

I tried that it didn't work it appears most of the menu content is either about how to edit genesis-sample and the content related to the genesis from scratch one, doesn't really work.

So, back to sleuthing.

Okay, looking at the menu locations page. It says 'Primary Navigation Menu' and 'Secondary Navigation Menu'

Alright, adding the menu button for the pop-out.

I'm looking for the following string: 'genesis-mobile-nav-primary'. I have not found 'genesis-mobile-nav-primary' but I have found genesis-mobile-nav-primary. In the function add\_hamburger\_attributes.

Alright, this is not working out so I'm going to use the sample theme, get familiarized with that and then start form scratch.

I just found this [video](https://www.youtube.com/watch?v=9SpmZxbeMKc&ab_channel=DavidMartin-UXHACKS) on block based themes and a theme starter so I'm going to skip this Genesis thing and just try that.

**logged out:** Tue 16 Aug 2022 00:00:00 AM CDT

**New Day:** Thu 18 Aug 2022 02:01:17 PM CDT

I have concluded that the best way forward with my setup is to use LocalWP and rebuild large bloated sites with block based themes. So I'll be doing exactly that. To view the process of me documenting working with block based themes, view [this article](https://montelogic.com/?p=349).

**Concluding article:** Thu 18 Aug 2022 02:08:09 PM CDT
