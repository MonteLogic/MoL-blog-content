---
title: "Documenting: Setting Up and using WP CLI on LocalWP"
date: "2022-08-11"
categories: 
  - "documenting"
---

TL;DR I didn't have to do much work because LocalWP ships with WP CLI just click 'Open site shell'

New Day: Thu 11 Aug 2022 11:59:00 AM CDT

The WP CLI is offered kind of as an alternative to SSH but I have yet to get really familiar with it. It offers the promise of speeding up workflows dramatically, thus, we (Advanced Developers) have an interest in it.

I am going to be testing WP CLI functionality with LocalWP by pressing 'Open site shell' then you'll have access to the variables necessary for implementing WP CLI.

Then after I am familiarized with the LocalWP side, I am going to start the process with a remote hosting setup.

I ran wp db export and the .sql file is outputted to the folder I was currently in so that was the public folder which was, '~/Local Sites/test1/app/public'.

Okay, so what I'm doing is using the .sql file by putting it in a folder I will then add wp-content dir into that folder. Then, zip it and then see if that is a valid import for LocalWP.

Okay, I did that and it worked.

This strat will definitely replace the one I've been using that is the one where I run a backup of the .sql file with all-in-one importer.

Now that I got the .sql file downloaded I wonder if I can download the wp-content folder with WP CLI.

Granted, I can do this fairly easily with SSH but one tools beats two.

I am checking out their GitHub [repo](https://github.com/wp-cli/core-command) on wp core-command

I'm kind of getting tied up on the phrase, "WordPress Installation". I think it means the WordPress folder of a site but not entirely sure.

Okay, looking around I haven't found a WP CLI command that could download the wp-content folder. I guess I'll be doing SSH and WP CLI for the time being. But I have found these cool resources that list out the WP CLI commands and other helpful information. I could possibly make a custom command for this viz. downloading wp-content folder.

This [image](https://montelogic.com/wp-content/uploads/2022/08/wp-cli-commands-cheat-sheet.png)

This [GitHub repo](https://github.com/maheshwaghmare/wp-cli-commands-cheat-sheet)

There is a command where you can import and export WordPress Data/Content to a WXR file. So I'm thinking, that would've took the place of downloading the wp-content folder.

But now that I got that figured out I am now going to use SSH and go back to writing the [documenting article](https://montelogic.com/?p=129) where I discuss the importation of sites with LocalWP and various command tools.

**Ending Article:** Thu 11 Aug 2022 01:44:37 PM CDT
