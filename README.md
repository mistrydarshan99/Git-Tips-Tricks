# Git-Tips-Tricks
Useful git command that display how to resolve issue in live project

## Git config commands
 git config -global user.email [user_email]

 git config -global user.name [user_name]

 The commands above are used to set current user email and name configuration.

 git config --global --edit

 And this command is very useful, as it allows for editing user configuration in a text editor.

I thought it would be the perfect use case to create some visualized examples of the most common and useful commands! 🥳 Many of the commands I'm covering have optional arguments that you can use in order to change their behavior. In my examples, I'll cover the default behavior of the commands without adding (too many) config options!

## Rebasing
We just saw how we could apply changes from one branch to another by performing a git merge. Another way of adding changes from one branch to another is by performing a git rebase.

A git rebase copies the commits from the current branch, and puts these copied commits on top of the specified branch.

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--EIY4OOcE--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/dwyukhq8yj2xliq4i50e.gif)

Perfect, we now have all the changes that were made on the master branch available on the dev branch! 🎊

A big difference compared to merging, is that Git won't try to find out which files to keep and not keep. The branch that we're rebasing always has the latest changes that we want to keep! You won't run into any merging conflicts this way, and keeps a nice linear Git history.

This example shows rebasing on the master branch. In bigger projects, however, you usually don't want to do that. A git rebase changes the history of the project as new hashes are created for the copied commits!

Rebasing is great whenever you're working on a feature branch, and the master branch has been updated. You can get all the updates on your branch, which would prevent future merging conflicts! 😄

## Reset

It can happen that we committed changes that we didn't want later on. Maybe it's a WIP commit, or maybe a commit that introduced bugs! 🐛 In that case, we can perform a git reset.

A git reset gets rid of all the current staged files and gives us control over where HEAD should point to.

### Soft reset

A soft reset moves HEAD to the specified commit (or the index of the commit compared to HEAD), without getting rid of the changes that were introduced on the commits afterward!

Let's say that we don't want to keep the commit 9e78i which added a style.css file, and we also don't want to keep the commit 035cc which added an index.js file. However, we do want to keep the newly added style.css and index.js file! A perfect use case for a soft reset.

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s---GveiZe---/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/je5240aqa5uw9d8j3ibb.gif)

When typing git status, you'll see that we still have access to all the changes that were made on the previous commits. This is great, as this means that we can fix the contents of these files and commit them again later on!

### Hard reset

Sometimes, we don't want to keep the changes that were introduced by certain commits. Unlike a soft reset, we shouldn't need to have access to them any more. Git should simply reset its state back to where it was on the specified commit: this even includes the changes in your working directory and staged files! 💣

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--GqjwnYkF--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/hlh0kowt3hov1xhcku38.gif)

Git has discarded the changes that were introduced on 9e78i and 035cc, and reset its state to where it was on commit ec5be.

## Reverting

Another way of undoing changes is by performing a git revert. By reverting a certain commit, we create a new commit that contains the reverted changes!

Let's say that ec5be added an index.js file. Later on, we actually realize we didn't want this change introduced by this commit anymore! Let's revert the ec5be commit.

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--eckmvr2M--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/3kkd2ahn41zixs12xgpf.gif)

Perfect! Commit 9e78i reverted the changes that were introduced by the ec5be commit. Performing a git revert is very useful in order to undo a certain commit, without modifying the history of the branch.

## Fetching

If we have a remote Git branch, for example a branch on Github, it can happen that the remote branch has commits that the current branch doesn't have! Maybe another branch got merged, your colleague pushed a quick fix, and so on.

We can get these changes locally, by performing a git fetch on the remote branch! It doesn't affect your local branch in any way: a fetch simply downloads new data.

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--38PuARw2--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/bulx1voegfji4vwgndh4.gif)

We can now see all the changes that have been made since we last pushed! We can decide what we want to do with the new data now that we have it locally.

## Pulling

Although a git fetch is very useful in order to get the remote information of a branch, we can also perform a git pull. A git pull is actually two commands in one: a git fetch, and a git merge. When we're pulling changes from the origin, we're first fetching all the data like we did with a git fetch, after which the latest changes are automatically merged into the local branch.

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s---X5AXldj--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/zifpnl1h6a4tk4qdc9sy.gif)

Awesome, we're now perfectly in sync with the remote branch and have all the latest changes! 

## Reflog

Everyone makes mistakes, and that's totally okay! Sometimes it may feel like you've screwed up your git repo so badly that you just want to delete it entirely.

git reflog is a very useful command in order to show a log of all the actions that have been taken! This includes merges, resets, reverts: basically any alteration to your branch.

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--MMUdOS0P--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/1aqek1py1knwl926ele7.gif)

If you made a mistake, you can easily redo this by resetting HEAD based on the information that reflog gives us!

Say that we actually didn't want to merge the origin branch. When we execute the git reflog command, we see that the state of the repo before the merge is at HEAD@{1}. Let's perform a git reset to point HEAD back to where it was on HEAD@{1}!

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--A1UMM2AH--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/9z9rhtbw7mrigp0miijz.gif)

We can see that the latest action has been pushed to the reflog!
