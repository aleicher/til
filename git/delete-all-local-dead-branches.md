# delete all local dead git branches

delete all local (dead) branches -- i.e, the branches which are deleted (merged) in remote, but present locally

NOTE: this assumes you have a script pullallbranches.sh, which [pulls alls remote branches](pull-all-branches.md)

```
git pull --rebase; pullallbranches.sh ; git push; git branch -a; git remote prune origin; git branch -r | awk '{print $1}' | egrep -v -f /dev/fd/0 <(git branch -vv | grep origin) | awk '{print $1}' | xargs git branch -D; git branch -a 
```
