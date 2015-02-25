Rebasing

Assuming that you creat a branch 'mywork' on your remote branch 'master'.

```
$git checkout -b mywork origin
```

After switch to it you make some change 

```
$touch file
$git add file
$git commit -m "add file"
```

On the same time  your colleague have pulled two requests to origin branch ,which means the 'master' and 'mywork'  will have conflict on each other. It is similiar to the 'Merge conflict' you have encountered in lab1.

But merge will creat a new merge commit on 'master' which you dont want to commit. You want to keep the commits on the 'mywork' branch without merge, then you can use git rebase:
```
$git checkout mywork
$git rebase origin
```

This command will save all your commits in 'mywork' under a directory '.git/rebase' in patch format. When you updated origin to "already up-to-date" the patch will patch back to new 'mywork' without leaving merge commits.

Once your 'mywork' point to a new commit, the old one will be through away. If you run 
```
$git gc
```
(garbage collection), they may be removed.

If the rebase process find a conflict, after you fix the conflict, use git add and continue with
```
$git rebase --continue
```

or you want to back to status before rebase, run
```
$git rebase --abort
```



#Inerteractive Rebasing -i
Under this mode, you could rewrite your commits before pull request.(If I know this before my first commits, I would not have messed up my commits and had to delete the repo and forked again.) 
It facilitates you to separate merge and re-order commit and remove commits that you have already pulled to your laptop.

You can add '-i' after git rebase or '--interactive' to apply interactive mode to commit
```
$git rebase -i origin/master
```

Once you run the command, you will turn to edit mode :
```
pick fc62e55 added file_size
pick 9824bf4 fixed little thing
pick 21d80a5 added number to log
pick 76b9da6 added the apply command
pick c264051 Revert "added file_size" - not implemented correctly

# Rebase f408319..b04dc3d onto f408319
#
# Commands:
#  p, pick = use commit
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```

That is to say, you have five commits and every one follow this format:
```
[action][partial-sha][short commit message]
```

Now you can change the action (which is 'pick' in default) to 'edit', 'squash' or delete the line that you dont want to push




