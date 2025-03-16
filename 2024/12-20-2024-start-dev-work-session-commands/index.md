---
title: "12.20.2024 - Start Dev Work Session Commands"
date: "2024-12-20"
---

1. First, ensure you're on the correct branch:

```
bash
```

```
git branch
```

2. If you need to switch branches:

```
bash
```

```
git checkout <branch-name>
```

3. Fetch all remote changes to see what's new:

```
bash
```

```
git fetch --all
```

4. Pull the latest changes from the remote repository:

```
bash
```

```
git pull origin <branch-name>
```

If you're working on a feature branch, you might also want to make sure it's up to date with the main branch:

```
bash
```

```
git checkout <feature-branch>
git pull origin main
```

Delete all the local branches which aren't in the repo anymore.

```
git branch --delete --force $(git branch -vv | grep ': gone]' | awk '{print $1}')
```

### Delete stale branches

```

git fetch --prune 
```

Then you will have to delete the local stale branches.

```
# List all branches (both local and remote)
git branch -a

```

Then find the stale branch and run.

```
# Delete a local branch if needed
git branch -d <state_branch>
```

Use a lowercase -d when deleting as you will only delete stale branches this way.

Still looking into a way to do this seamlessly through VSCode, say after a Pull Request.
