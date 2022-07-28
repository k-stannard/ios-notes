## List of useful git commands

`git status` - show changes to be committed and/or staged

`git add` - add files to the staging process

`git add -p` - add files, but pan through each change & determine what to do at each point

`git commit -m "commit message here"` - commit changes with a message  

`git remote add origin <remote_repo_URL>` - link remote repository to local repository

## Pushing a change to a remote repository

`git push --set-upstream origin <branchname>` - creates an upstream channel to push changes to the remote

`git push` - save local changes to a remote repository

`git log` - show a log of git commits

`git diff` - shows what changes are currently made in the codebase


## Creating a branch

`git checkout -b <branchname> ` 

## Reset a branch

If you accidentally commited a change that you didn't want, you can erase that commit by doing the following:  
1. Type `git log` and copy the hash key to the commit in which you want to reset to.
2. Type `git reset --hard <hash key>`
3. To upload the change to the remote repo, type `git push --force`
  - Be very careful with this command when working with other people on the same repository.

## Squash and Rebase

If you have a series of commits you'd like to combine into a previous commit, you use squash and rebase them.

1. Type `git log` and copy the hash key that is *just beneath* the commit you want to rebase into.
2. Type `git rebase -i <hash key>` to enter into the git interactive rebase file
3. Determine which commits you want to squash, and change `pick` to `s` on each line that is to be squashed.
4. Once changes are saved, the next step is to clean up the commit messages.
- The commit you are rebasing into will be at the top, and the squashed commit messages will be below it. Simply remove what you don't want and save the changes.
5. To update the remote repository, use `git push --force` to force the changes through.

## Merge vs Rebase

When merging two branches together, the merge will respect the timeline in which changes were made, and then inserts changes from each branch in chronological order. 

Rebase will take your changes vs the repository you want to merge to and place your changes directly on top of the repository being merged to. 

## Pull Requests

Pull requests are how your changes are merged with other team members and commited to the repository that represents the project.  

