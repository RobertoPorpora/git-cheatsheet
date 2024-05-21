# git-cheatsheet

## DEFINITIONS
- **Repository**: A storage space where your project's files and their revision history are kept.
- **Remote**: A version of your repository that is hosted on the internet or another network, tipically on a git server.
- **Clone**: Make a copy of a remote repository on your local machine.
- **Commit**: Save (locally, only on your computer) a retrievable snapshot of your project's state to the repository.
- **Stage**: Any change to be committed must be staged first. Prepare changes to be included in the next commit.
- **Stash**: Temporarily save changes that are not ready to be committed.  
	This allows you to switch branches or work on something else without losing your current work.  
	The changes are stored in a stack, and you can apply them later when you're ready.
- **Branch**: A separate line of development in your project.
- **Merge**: Combine changes from one branch into another.
- **Fetch**: Download updates from a remote repository without merging them into your local branch.
- **Diff**: Show the differences between two sets of changes in your project.
- **HEAD**: A reference pointer that represents your current position within the Git repository. It points to the latest commit in your currently checked-out branch.
- **Tag**: static labels that are used to mark specific points in the project's history, usually to indicate release versions (such as v1.0, v2.0).


## COMPUTER SETUP
Configuring user information used across all local repositories.

`git config --global user.name “[firstname lastname]”`  
Set a name that is identifiable for credit when review version history.

`git config --global user.email “[valid-email]”`  
Set an email address that will be associated with each history marker.

`git config --global color.ui auto`  
Set automatic command line coloring for Git for easy reviewing.


## INIT new repo from scratch

### Suggested way
1. Create a new repository on the server (Github, GitLab, GOGS...) with something in it:
	- make it generate the empty README.md file
	- make it generate the LICENSE file
	- this speeds up things because it already creates a branch with an upstream and you don't to set it up manually.
2. Proceed to downloading it to your computer with the clone command.


### Alternative way, maybe for local only repo.
1. Create a folder with some content in it (things you want to version).
2. Open a terminal in this folder.
3. Type `git init`  
	This will create a .git folder inside your current working directory.


## CLONE
1. Open the terminal in the folder where you want to place your repository.  
	**Don't create a sub-folder**, the clone command creates a sub-folder (in the current working directory) by itself.
2. Type `git clone [url]`  
	For example: `git clone https://github.com/RobertoPorpora/git-cheatsheet`


## GET UPDATES FROM SERVER / REMOTE
Retrieving updates from another repository and updating local repos

`git remote add [alias] [url]`  
Configure a git URL as an alias

`git fetch [alias]`  
Fetch all the branches from that Git remote

`git merge [alias]/[branch]`  
Merge a remote branch into your current branch to bring it up to date

`git pull`  
Fetch + merge any commits from the tracking remote branch


## COMMIT CHANGES LOCALLY

`git add [file]`  
Add a file as it looks now to your next commit (stage)

`git add .`  
Stage all changes

`git commit -m "[message]"`  
Commit staged changes with a message.


## SEND UPDATES TO SERVER / REMOTE

`git push -u origin [branch]>`  
Set upstream for the current branch

`git push [alias] [branch]`  
Transmit local branch commits to the remote repository branch

`git push`  
Pushes the current branch to its upstream branch if set, or defaults to pushing the current branch to the same branch on the remote origin if upstream is not set.



## STAGE & SNAPSHOT
Working with snapshots and the Git staging area

`git status`  
show modified files in working directory, staged for your next commit

`git add [file]`  
add a file as it looks now to your next commit (stage)



`git diff`  
diff of what is changed but not staged

`git diff --staged`  
diff of what is staged but not yet committed

`git commit -m “[descriptive message]”`  
commit your staged content as a new commit snapshot


## DELETE COMMITS

`git reset [file]`  
Unstage a file while retaining the changes in working directory

`git reset --soft [hash]`
Snapshots after the specified hash are deleted, contents of the working directory are untouched (and staged).
Moves the HEAD to the specified commit, keeps all changes in the staging area.

`git reset --hard [hash]`
Moves the HEAD to the specified commit and discards all changes in the working directory and index.


## BRANCH

`git branch [branch]`  
Create a new local branch with the specified name, but does not switch to it. It remains on the current branch.

`git checkout [branch]`  
This command switches to the specified branch, making it the active branch for future commits and changes.

`git checkout -b [new_branch_name] [hash]>`  
Create a new branch named 'new_branch_name' starting from the specified commit hash, and switch to this new branch.


## TEMPORARY COMMITS
Temporarily store modified, tracked files in order to change branches

`git stash`  
Save modified and staged changes

`git stash list`  
List stack-order of stashed file changes

`git stash pop`  
Write working from top of stash stack

`git stash drop`  
Discard the changes from top of stash stack


## TAGS

`git tag [tag_name]`  
Lightweight Tag: A simple label attached to a commit.

`git tag -a [tag_name] -m "[tag_message]"`  
Annotated Tag: Contains metadata such as the tagger's name, date, and a message.

`git tag`  
List tags

`git show tag_name`  
To see details of an annotated tag:

`git push origin tag_name`  
Push a single tag to Remote

`git push origin --tags`  
Push all tags to Remote

`git tag -d tag_name`  
Delete a Tag locally

`git push origin --delete tag_name`  
Delete a Tag remotely