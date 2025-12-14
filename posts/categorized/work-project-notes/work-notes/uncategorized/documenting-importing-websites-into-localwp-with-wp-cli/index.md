---
title: "Documenting: Importing Websites into LocalWP with WP CLI"
date: "2022-08-11"
category-slug: "work-notes"
---

The process of importing things with LocalWP is the fact that you have to have the .sql file and wp-content folder of a website in the same folder, zip it and then drop it into LocalWP.

This technique is summed up perfectly in this forum thread reply.

I currently able to use SSH to get the wp-content folder of a project on a remote sever. However, the .sql file I get from the cpanel does not work with LocalWP so what I have to do is use the plugin all-in-one importer or something like that to run a backup and then get the .sql file from the backup.

I am reading this [article](https://www.digitalocean.com/community/tutorials/how-to-use-wp-cli-v2-to-manage-your-wordpress-site-from-the-command-line) I am on step 5 on the part detailing sql. The following command, "wp db cli" looks promising. But that starts a MySQL session which I don't want. I'd prefer the command, "`wp db export`" which exports a SQL file you can also import it with "`wp db import file.sql`"

New Day: Thu 11 Aug 2022 12:18:30 PM CDT

Okay, I have figured out how to use WP CLI to import a .sql file. Now, I just have to fish out that SSH command I used to download a wp-content folder.

This is the command I use to get the wp-content folder of a remote WordPress install onto my device.

`scp -P 21098 -r username@000.000.000.000:/home/username/public_html/wp-content ~/`

With the above command you should replace username with appropriate cPanel username and 000.000.000.000 with the Shared IP Address which is found in your cPanel general information area.

.. Now, I still have to figure out how to get a WP CLI instance running in a remote server which I have yet to do.

New Day: Fri 12 Aug 2022 10:20:18 AM CDT

Okay...... so so so I am trying to use SSH to SSH into a a remote WordPress server and then run WP CLI commands. Let's see what happens.

Alright, so I SSH'd into my remote server ran 'wp' and it worked.

But ... the remote server that I believe I'm on only would show and interact with the main install. But how would I get into the other install? Let's find out..

Okay, I'm watching this YouTube [video](https://www.youtube.com/watch?v=bBoL3sFPeSM&ab_channel=AlessandroCastellani) to see if it helps with this problem.

Okay, watched it, didn't really help for the problem of something like with a cPanel install but it was the only YT video I saw related to this issue so. Article time.

I found this [article](https://www.shawnhooper.ca/2017/08/08/wp-cli-remote/) helpful but still unsure about deciphering paths so I'm just going to bang around a remote install until I figure it out.

The previous command "`wp db export`" I used to get the .sql file worked to my liking so let's start with that.

Alright so I was in the root of my remote server and I ran '`wp db export`' and it said "Error: This does not seem to be a WordPress installation." Which is good because I now know more about the paths.

Alright so I have to find a WordPress install, the right folder of that WordPress install and then run the command.

Alright, so I simply entered the public\_html folder of a WordPress install and then ran the "`wp db export`" command.

Go the .sql file to output in the same folder where the "`wp db export`" was issued. Now it appears I have to run an scp to get the .sql file.

Okay, I got the scp command to work with this:

`scp -P 21098 username@000.000.000.000:/home/username/public_html/name_of_sql_file.sql ~/`

I also have this command which could get the wp-content folder:

`scp -P 21098 -r username@000.000.000.000:/home/username/public_html/wp-content ~/`

logging out: Fri 12 Aug 2022 05:10:15 PM CDT
