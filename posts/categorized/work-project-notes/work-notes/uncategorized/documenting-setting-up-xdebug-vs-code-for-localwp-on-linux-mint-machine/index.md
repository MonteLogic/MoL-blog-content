---
title: "Documenting: Setting Up Xdebug + VS Code for LocalWP on Linux Mint machine"
date: "2022-08-13"
category-slug: "work-notes"
---
New Day: Sat 13 Aug 2022 10:35:23 AM CDT

I have previously got it to work after editing the launch.json file and change the routing scheme to my LocalWP installation.

I am following this YT [video](https://www.youtube.com/watch?v=Zs6zhNTGZRU&t=371s&ab_channel=JeremyCaris).

I made a launch.json which worked well.

Launch.json

`{   "version": "0.2.0",   "configurations": [   {   "name": "Listen for Xdebug 3.0 (Local)",   "type": "php",   "request": "launch",   "port": 9003,   "xdebugSettings": {   "max_children": 128,   "max_data": 1024,   "max_depth": 3,   "show_hidden": 1   }   },   {   "name": "Listen for Xdebug (Local)",   "type": "php",   "request": "launch",   "port": 9003,   "xdebugSettings": {   "max_children": 128,   "max_data": 1024,   "max_depth": 3,   "show_hidden": 1   }   },   {   "name": "Launch currently open script",   "type": "php",   "request": "launch",   "program": "${file}",   "cwd": "${fileDirname}",   "port": 9000,   "xdebugSettings": {   "max_children": 128,   "max_data": 1024,   "max_depth": 3,   "show_hidden": 1   }   }   ]   }`

It appears that I cannot get the large sites I want to use to run n Xdebug so I guess I can only isolate sertain plugins.

Xdebug appears to be so slow for these large sites that I'm just gonna have to use it to only isolate plugins. I'm gonna have to use like writing logs, like writing like like files or into files with the php and ajax to debug these projects. So I also can use preserve log for console.log and maybe catch something in there.

I think Xdebug is only going to work for smaller sites.

So I'm going to start the process of learning to debug via custom made log files.

Ending article: Sat 13 Aug 2022 01:25:59 PM CDT
