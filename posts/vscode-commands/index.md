---
title: "VSCode commands"
date: "2024-12-15"
---

When I want to get rid of all the old traces of old branches of my git repo:

git remote prune origin

git branch --merged | grep -v "\*" | xargs -n 1 git branch -d
