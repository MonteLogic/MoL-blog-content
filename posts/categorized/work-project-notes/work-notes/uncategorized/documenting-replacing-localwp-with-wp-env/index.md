---
title: "Documenting: Replacing LocalWP with wp-env on Linux Mint"
date: "2022-08-16"
categories: 
  - "documenting"
  - "not-working-on-now
category-slug: "work-notes"
"
---

New Day: Tue 16 Aug 2022 09:37:22 AM CDT

Alright before I start this I think LocalWP is really dope and is certainly an improvement upon the method used prior of working on a remote server or running a XAMP install on your local machine. I am very grateful that the upcoming generations have a streamlined experience with possible use of LocalWP. Also if I were to recommend a Local workflow to a new dev, I would recommend LocalWP as wp-env seems to be based heavily on command line interaction which can be tricky for newbies.

Alright so I watched this [video](https://www.youtube.com/watch?v=9SpmZxbeMKc&ab_channel=DavidMartin-UXHACKS) on block based themes.

Before the host talks about block based themes he touches on wp-env over LocalWP and how to set it up.

Alright, tried to install Docker and it doesn't appear to be easy on Linux mint but I did a bunch of stuff and ran sudo docker run hello-world.

That ran but I still don't have the Docker GUI I saw on the tutorial.

Alright, I'm following this [tutorial](https://developer.wordpress.org/block-editor/getting-started/devenv/) on how to get it to run. Wish I would've started with the Ubuntu WordPress [dev](https://developer.wordpress.org/block-editor/getting-started/devenv/docker-ubuntu/) environment install.

Alright, on this tutorial now and it is saying to cd into the path and run wp-env.

So I'm going to run [theme generator](https://fullsiteediting.com/block-theme-generator/) for the block based theme I am going to be using.

I am going to be choosing the basic option from the theme generator.

It appears you can't run docker ps like you can on windows and have it just work. You have to add sudo to it.

I was having some issues with the Node version because it needs the latest version of Node.js for details related to that view these [docs](https://developer.wordpress.org/block-editor/getting-started/devenv/).

Alright, I'm running into issues with setting up Linux Mint, it appears I have to use a Docker group.

Okay, I've ran into a substantial challenge. I cannot run docker properly because of root access issues. I'm going to have to use a Docker group. But the thing is I'm pretty clueless with Docker. So I have to figure out how to set up groups and all that.

It appears I'm going to have to go through these [instructions](https://docs.docker.com/engine/install/linux-postinstall/) because of a related GitHub [issue](https://github.com/WordPress/gutenberg/issues/20180).

Following the instructions about logging in and out command on Linux.

```
 newgrp docker 
```

I read in one thread that it clears history but it doesn't clear your command history so I would recommend issuing that command and then that'll log you out and then back again automatically with one command

I followed the instructions of the post-install ran wp-env start and now it works.

Now it's time to restart the project and use this block based themes way of customizing.

The reading matieral for tommorow will be:

[Source 1](https://developer.wordpress.org/block-editor/reference-guides/packages/packages-env/)

[Source 2](https://fullsiteediting.com/)

**Logging out:** Tue 16 Aug 2022 05:13:54 PM CDT

I would like to import my site data to the WP-Env docker instance but I don't know how. 

It looks like WP-CLI offers some commands that could be used for importing but you're going to use XHR file.

The [link](https://developer.wordpress.org/cli/commands/shell/) to this is helpful because it talks about the shell which could be useful for what we're trying to do. It appears I need to run: 

wp-env run cli as if it was wp-cli

It [appears](https://mkaz.blog/wordpress/the-wordpress-command-line-tool/) I need to run: 

wp-env run cli as if it was wp-cli

**New Day:** Wed 17 Aug 2022 11:54:51 AM CDT

Okay, a problem I am having with this is the fact that I don't know how to run imports/exports with the the exception of a WXR file.

Because at this moment I only have a blank theme and not the data of the large site I am trying to edit.

I am watching this video on how to move [sites](https://www.youtube.com/watch?v=5g8tz69zuVU&ab_channel=WPShout) with WP-CLI.

It was helpful but it looks like it's going to be an all day project to get it setup right.

Right now I am going to create a post with that's a random string and look for it in my entire system. I am also going to 'run wp-env start' in different places.

Okay, so I tried to start wp-env in the root folder of one of my LocalWP sites and it gave me the error.

⚠ Warning: could not find a .wp-env.json configuration file and could not determine if '/home/<username>/Local Sites/montesite' is a WordPress installation, a plugin, or a theme.

Alright so, let's make that post then.

Okay the post thing didn't really work so let's install a plugin instead.

Okay, I tried to download the plugin through WordPress plugin store it didn't work so I'm going to use the CLI instead.

I could have the site where if people want to link to a documented one which is the latest they can. As tech updates very often and somethings in the past that used to work can sometimes not work.

Okay, I ran 'wp-env run cli plugin install bbpress --activate'

It appeared to try to run it but I got a warning saying permission denied.

But let's double check that it was a correct command before seeing the permission issues. It appears to be a correct command so let's look into the permission issue.

Okay, this [thread](https://wordpress.org/support/topic/wp-cli-show-me-warning-could-not-create-directory/) seems to answer the permission issue.

But I have to find the php.ini file.

Okay, this [stackoverflow](https://stackoverflow.com/questions/66390649/running-wordpress-with-wp-env-prompts-for-ftp-credentials) thread seems to be the answer.

Alright, I searched for the wp-config folder in my root folder and I found out where the paths are to wp-env. It is at "/home/<username>/.wp-env/"

But the other question ... is how to find the one that related to the right php.ini.

I figured out .... where the wp-content folder is for wp-env. Go into the .wp-env folder of the root, then you'll see folders with a random looking name click on it then .. go ahead it's in there.

Okay, time to try to add the data. I am going to start by replacing the wp-content folder.

I'm having a hard time finding the .sql file for this wp-env thing.

I was running into an error and I needed to add this flag. --authors=create

**New Day:** Thu 18 Aug 2022 01:50:02 PM CDT

Okay, I do not think that wp-env can replace LocalWP on Linux Mint. However, wp-env does have things in it which can replace the issues I'm having with LocalWP, more specifically testing. There appears to be built in functions for xdebug. If I wanted to continue in the path I was on the day prior to today, I would research Docker more and issue more Docker commands. However, I am a WordPress dev and not DevOps so I'm not going to do that. But I do think that wp-env ran on x86 Windows or MacOS has a much higher chance of replacing LocalWP than wp-env on Linux.

Concluding article: Thu 18 Aug 2022 01:59:28 PM CDT
