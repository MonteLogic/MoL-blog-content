---
title: "Proposal: 'Code Switchboard' for managing project complexity"
date: "2025-02-23"
---

Ideally it would be like a video game look of say a game like Mass Effect where you go through each solar system selection, this UI but instead you are going though project complexity viz. each node will show the possible permutations.

Also within each node, you can click on each node to get a 'permutation view' and it would immediately load the app in the selected permutation's described state, which was chosen on the 'Switchboard'.

Notes:

Feature board

It should be a graph (nodes) of how everything works when it was tested last. Almost like a suite for current features, a switchboard if you will.  
Code Switchboard

Not seeing an off the shelf solution for this probably going to have to create a custom solution for this.

…

Local solution which will rely on GH Issues for marking and managing issues.

You could just run 'pnpm start switchboard'  
Focusing on Issue 200

This message:

"You are not a part of an organization, Create Organization"

Rather it should always show the slider.

"Ideally you could press a button on the node graph and it starts up the app in THAT state."

Page app/main/schedule/page.tsx

…

Solution:
