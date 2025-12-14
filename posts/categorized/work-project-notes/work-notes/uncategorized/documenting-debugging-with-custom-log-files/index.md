---
title: "Documenting: Debugging WordPress With Custom Log Files"
date: "2022-08-13"
category-slug: "work-notes"
---

New Day: Sat 13 Aug 2022 02:29:10 PM CDT

Alright, after trying and failing

This is not going to be specific to LocalWP--even though I'm using it for this--because this should work on the same PHP/WordPress installations.

After looking around I found this dope [talk](https://youtu.be/ss3-xXGxHhg?t=162) where the speaker discusses different uses for the console object. More than just console.log(). However, I won't be outputting into the console I am trying to AVOID 'endless' console.log statements. So I think I'm going to write those console.log's to a file and then include the timestamp inside that file.

I had stuff written out about debugging with log files but I can't seem to find them so I'm going to just start off by writing to a file in php.

I do have experience in writing to a file with JavaScript in the JSON object. But I'm guessing php is going to be different and hopefully easier.

Okay, so I'm going to make a folder called sandbox in my public folder. The route would be /home/<username>/Local Sites/test-3/app/public

Okay so now that I got my sandbox, let's watch YT vids to learn how to write to a file.

Okay watching this [video](https://www.youtube.com/watch?v=1vS2KXf0Esc&ab_channel=VeryAcademy).

I found this comment helpful:

@Emanuel Benetti

"My two cents for anyone interested:  
file\_put\_contents can accept a third parameter "flag". You can specify if you want the file to keep adding data instead of erasing it (like a log, a list, etc).

In the example of this video, it will be something like this: file\_put\_contents($file, $comment, FILE\_APPEND);

For more info about file\_put\_contents() you can visit the php wiki and see the technical stuff as well as the examples."

I am unsure if this is going to work with WordPress or I am going to have to do a different solution. But ... it has worked in my sandbox.

This block of code will create a file and write to it, fairly unsophisticated.

```
<?php
?>
<h1>file-1</h1>
<?

$log = "log.txt";

if (file_exists($log)){
 $current = file_get_contents($log);
} else{
  $myfile = fopen($log, "w");
  header("Refresh:0");
}

// Starting the writing process.
file_put_contents($log, "This is a statement");

```

Okay, so now .... I have to ... add this into my project and to log console errors. Thus, successfully debugging server side code.

While I'm trying to do that, I noticed my LocalWP blueprints were gone. So I'm fishing that out, also I noticed LocalWP hasn't published their path structure to access LocalWP's blueprints folder so I have to figure out what path that is in.

I figured it out and took a screenshot... but it's the end of the workday.

Logging out: Sat 13 Aug 2022 08:28:05 PM CDT

New Day: Mon 15 Aug 2022 01:27:05 PM CDT

Alright, now that I got that figured out now it's time to put it in the right spotsss.

Alright, because this blog is mainly dedicated to WordPress I got the WordPress stuff working with this.

```
// Create text file. 

$log = plugin_dir_path( __FILE__ ) . '/errors-log.txt'; 
$open = fopen( $log, "a" ); 


if (file_exists($log)){
 $current = file_get_contents($log);
} else{
  $myfile = fopen($log, "w");
  header("Refresh:0");
}

// Starting the writing process.
file_put_contents($log, "This is a statement");



```

Now, I am going to add the Append flag so my stuff doesn't get written over.

Okay, the append flag worked. After it worked for testing I changed the content added to it to be "".

**New Day:** Fri 19 Aug 2022 08:48:11 PM CDT

```
file_put_contents($log, $fields[ 'billing_postcode' ] ." == " . zipToState( 62711 ) . PHP_EOL, FILE_APPEND);
```

Run :e to refresh the test file.

Tidbit: You don't have to reload the WooCommerce checkout form when you're working with php

**New Day:** Wed 24 Aug 2022 04:30:00 PM CDT

The php function written in this [stackoverflow answer](https://stackoverflow.com/a/55246456) could help to get more information for debugging.
