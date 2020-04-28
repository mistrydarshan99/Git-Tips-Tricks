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

(https://res.cloudinary.com/practicaldev/image/fetch/s--EIY4OOcE--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/dwyukhq8yj2xliq4i50e.gif)
