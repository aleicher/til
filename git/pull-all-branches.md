# Pull all branches from a git remote

to pull all branches from a git remote, you can create the following script.

```
#!/bin/bash
#pullallbranches.sh
for branch in `git branch -a | grep remotes | grep -v HEAD | grep -v master`; do
  git branch --track ${branch##*/} $branch
done
git pull --all -v
git fetch --all -v
```

