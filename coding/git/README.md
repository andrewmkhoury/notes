# Git
## Create new branch from master or main
Clone and create the new branch:
```
git clone git@git.corp.adobe.com:CQ/dam.git
git checkout master
git fetch
git pull
git checkout -b CQ-4335104
git branch --set-upstream-to=origin/master CQ-4335104
```

## Sync latest from master or main branch to your branch
```
git fetch origin
git pull
```

## Push a local branch to the remote
```
git push origin CQ-4335203-4
```

## Delete a local branch
```
git branch -d CQ-4335203-3
```

## Delete a remote branch
```
git push origin --delete CQ-4335203-3
```

## Clearing all changes on branch
Revert all local changes and commits on branch back to master or main branch:
```
git reset --hard origin/master
```
OR:
```
git reset --hard origin/main
```

## Reverting changes from a specific commit
1. Prepare staged changes required to revert the last commit:
`git revert -n HEAD`
OR
Prepare (but not commit!) staged changes to undo a specific commit:
```
git revert -n <commit>
```
2. Unstage all those changes:
`git reset`

3. Add the files you really want to revert from the commit:
```
git add a.txt b.txt c.txt
```
4. Commit the changes to revert those files:
```
git commit -m 'Undo <commit> for a.txt, b.txt, c.txt'
```
5. Get rid of stuff you don't want undone:
```
git reset --hard
```

## Unstage specific files from being included in next commit
```
git reset -- <filePath>
```

## Keep ("Stash") pending changes to apply later
[git stash](https://git-scm.com/docs/git-stash) let's you stash your changes aside to a stack and pop them back from the stack later.

Stash all pending changes:
```
git stash save "message describing changes"
```

Stash changes from a file with a description
```
git stash push -m "describe changes to overlay.jsp" src/main/content/jcr_root/libs/granite/ui/components/shell/omnisearch/overlay/overlay.jsp
```

Apply the top stash in the stash "stack" without removing it:
```
git stash apply
```

Apply the top stash in the stash "stack" and remove it:
```
git stash pop
```

Conceptually, stashing changes is the same as:
1. Creating a diff or patch file (stashing it aside):
    ```
    git diff > /tmp/patch-to-apply-later.patch
    ```
3. Running a `git reset` and `git checkout .` (at the repo's root dir) to remove the changes in your git repo:
    ```
    cd /git/repo/root_dir
    git reset
    git checkout .
    ```
5. Do whatever changes, creating branches, whatever...
6. Later applying the diff/patch file:
    ```
    git apply /tmp/patch-to-apply-later.patch
    ```

## Squashing commits in a local branch
WARNING: You cannot rebase if your changes are already pushed to origin as part of a Pull Request.

Rebase allows you to edit and squash commits.
To squash all commits starting from the creation of the branch:
1. Make sure upstream is set to the source branch the branch was created from (in most cases `orign/master` or `origin/main`).
   For example:
   ```
   git branch --set-upstream-to=origin/master ASSETS-17040
   ```
2. Run this command:
    ```
    git rebase -i
    ```
    This allows you to edit the commits - pick, reword, squash, etc.

3. Set the first commit to `reword` and all the ones after it to `squash`.
4. Then save, it will squash all the commits (that happened after the branch was created) into one commit.
5. After saving, you will be prompted to edit the commit message of the single squashed commit.  Do so, then save again and the rebase will be applied.
6. Run `git log` to see that now you only have 1 commit on your branch.

WARNING: If you do this on a branch that already exists on the remote git repository then you would have to delete the remote branch and push it to remote again.
You can delete a remote branch using `git push origin --delete remote-branch-name`.

## Migrate all changes in branch to a new branch
Start a new branch with all changes made in another branch as one squashed commit
```
git checkout master
git fetch
git pull
git checkout -b NEW_BRANCH
git merge --no-commit --squash OLD_BRANCH
git commit -m "All changes made in OLD_BRANCH as one commit"
git push origin NEW_BRANCH
```


## Managing a fork repository

### Sync'ing the fork repo with upstream
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork

#### Switching from origin to a fork
https://admcpr.com/what-the-fork/

1. Create the fork via the UI
2. Go to the folder where you cloned the source repo and run commands similar to these:
```
git remote rename origin upstream
git remote add origin git@git.corp.adobe.com:akhoury/servicepack
git remote rename origin upstream
git remote add origin git@git.corp.adobe.com:akhoury/servicepack
git remote add origin https://github.com/akhoury/servicepack
git fetch origin
git branch --set-upstream-to origin/master master
```
3. To fetch latest changes from the source repo down to the fork:

```
git fetch upstream release/650
git pull upstream release/650
```
4. Commit and push changes to the fork as desired
5. Use the github UI to file a PR to merge the fork branch's changes back to the source

## Troubleshooting
### Fix "unable to update local ref"
Example error:
```
error: cannot lock ref 'refs/remotes/origin/hackathon/test1': 'refs/remotes/origin/hackathon' exists; cannot create 'refs/remotes/origin/hackathon/test1'
 ! [new branch]            hackathon/test1           -> origin/hackathon/test1  (unable to update local ref)
```

Run these commands to fix the error:
```
git remote prune origin
git gc --prune=now
```

For explanation, see these stack overflow articles:
* https://stackoverflow.com/questions/10068640/git-error-on-git-pull-unable-to-update-local-ref
* https://stackoverflow.com/questions/58126421/cannot-lock-ref-refs-remotes-origin-master
