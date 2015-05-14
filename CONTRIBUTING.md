## Style guide
TODO

## Testing your code
TODO

## Preparing your pull request for submission
Say you have a pull request ready for submission into the main repository - it has
been code reviewed and tested.
It's convenient for project committers if you:

1.  Condense branch history to 1 or a few commits that describe what you did.  This
eliminates internal code review fixes from being separate in history,
like refactors, typos, etc.
2.  Resolve merge conflicts with master.  As the author of the PR, you're in the
best position to resolve these correctly.  Even if the merge is a fast-forward,
doing the merge yourself allows you to test your code after incorporating others'
changes.

If you are new to github, here's an example workflow.
We'll assume you are working from your local repository
which is a clone of a fork of brunobowden/j2objc-gradle, that your feature
branch is called 'patch-1' and that your pull request is number 46.

```
# have a clean working directory and index
# from the tip of your patch-1 branch: first save away your work
git branch backup46
# now don't checkout or touch branch backup46 from here on out.
# if things go terribly wrong below, you can then return to a state of LKG sanity with:
#git rebase --abort
#git merge --abort
#git checkout patch-1
#git reset --hard backup46
# this will return your patch-1 branch to the state before merging & rebasing
```
First ensure you've setup your upstream remote as per 
https://help.github.com/articles/configuring-a-remote-for-a-fork/,
then do https://help.github.com/articles/syncing-a-fork/.
Your local master should now be equal to upstream/master.
Push your local master to your origin remote:
```
# While in your local master branch
git push
```

Now you can work on merging in master to your branch.  We'll assume a simple
branch history here, where patch-1 first diverged from master at commit
@5665f0a5ff774005ce30e088ab2e1b76caca5a43.
```
git checkout patch-1
# condense this down to one commit to preserve proper project history
git rebase -i 5665f0a5ff774005ce30e088ab2e1b76caca5a43
# within the rebase editor, replace the word 'pick' with 'fixup' on
# every line except the very first one. 
# when you exit that editor, you should be given a chance to give
# your entire PR a single detailed commit message.
git merge master
# resolve and finish the merge as usual
git push
```