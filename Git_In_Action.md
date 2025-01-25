What is Git? 
Git is a DevOps tool used for source code management. It is an open-source version control system (VCS) that tracks changes in the source code files and projects allow multiple users to work together. GitHub and GitLabs are source code storage providers or repositories.  


Installation
Visit the site https://git-scm.com/ and download the package for respective OS.
**Install gitbash


SSH key generation
$ ssh-keygen -t rsa -C sam@domain.com
$ eval "$(ssh-agent -s)" # adding the generated to the ssh-agent, some env, you can't do it
$ ssh-add ~/.ssh/id_rsa

$ ssh -T sam@domain.com

-------------------------------------
Configure git
# See all config options
$ man git-config

# set global options
$ git config --global

# add an alias
$ git config alias.st status


Set user, email to be used for repo

$ git config --global user.name 'value'
$ git config --global user.name "Sam"
$ git config --global user.email "sam@domain.com"
$ git config --global credentials.helper wincred
or for Linux/win both
$ git config --global credentials.helpeer cache
$ git config --global color.ui auto	# Enable some colorization of git output

git config file
# local git config file
$ cat .git/config

# global git config
$ cat ~/.gitconfig

# list ignore file/dir list
$ cat .gitignore


Git working stages/sequence
1. Working directory - You start modifying a file. once you are done with modification, you are ready to commit. 
 $ git clone <RepoURL> # download your repo locally or git pull
 $ vi abc.txt
   This is just a test file
 wq!
 $ git status

2. Staging (Index) - You are redy to stage your change, that mean you are ready to commit the change. This is where you commit the change
 $ git add .
 $ git add abc.txt
Here, you have option to commit all changes or a single or multiple files. You can use git add or git rm commands.
  Note: you can reset your changes to go back to working stage. 

3. git directory (repository) - Once your changes are saved (committed), you can push it to the repo. git commit basically saves everything from staging area and records what the changes are made with clear message.
 $ git commit -m "First commit for learning purpose"
 $ git status
 $ git push
 $ git push -u origin master

# git push uploads your committed changes to a remote repository, sharing them with other member of you team or the world.


Git in action

1. Clone or create a repo

# Create a local repo
$ git init

# Clone an existing repo
$ git clone <Git_Repo_URL>

# pull/update the change from remote repo
$ cd landscape
$ git pull --rec


2. Update and push

# Modify chante
$ vi abc.txt

# check the status of the changed file
$ git status

# Add untracked/unstaged file 
$ git add abc.txt

# Add all changes (Untracked/unstaged) made to the landscape files
$ git add .

# Add some changes in a file to the next commit
$ git add -p 
$ git add -p <File_name>

# Delete or move file from working directory and staging area.

$ git rm <File_Name>
$ git mv <Old_File> <New_File>

# Tell git to foget about a file without deleting it. 
$ git rm --cache <File_Name>


Note: This is stage the change which means you are on staging area now.

----------------------------
# Delete all staged and unstaged changes to a file
$ git checkout HEAD <File_Name>

# Delete unstaged changes to a file
$ git checkout <FileName>

Delete all staged and unstaged changed
$ git reset --hard

# delete untracked files
$ git clean

# 'stash' all staged and unstaged changes which means to put current changes in your working directory into stash for later use.
$ git stash 

# Apply stored stash content into working directory, and clear stash.
$ git slash pop

# Delete a specific stash from all your previous stashes.
$ git stash drop

Edit Histry
# Undo the most recent commit/Unstage everything
$ git reset HEAD^

# Squash the last 5 commits into one:
$ git rebase -i HEAD^^^^^^

-----------------------------
# Track the changes. 
# git diff lists the changes between your current working directory and your staging area.
$ git diff

# Show diff between a commit and its parent
$ git show <Commit_ID>

# Show diff between a merge commit and its merged parents
$ git show --remerge-diff <Commit_ID>

# Diff two commits
$ git diff <Commit_ID1> <Commit_ID2>

# Show diff for a file
$ git diff <Commit_ID> <File_Name>

# Show summary of a diff
$ git diff <Commit_ID --stat>
$ git show <Commit_ID --start

# Diff all staged and unstaged changes
$ git diff HEAD

# diff just staged changes
$ git diff --staged

# diff just unstaged changes
$ git diff


# The comparison between can be two different files, repo, branches  
https://www.freecodecamp.org/news/git-diff-command/

------------------------------

Tagging
# List all tags
$ git tag

# Create a tag named mytag for current commit.
# Note: Use commit_ID to ag a specific commit instead of current one.
$ git tag [name] [commit_ID]
$ git tag mytag <Commit_HASH>

# Create a tag named mytag for current commit
$ git tag -a [name] [comit-HASH>
$ git tag a mytag <Commit_ID>

# remove a tag from local repository
$ git tag -d [name]
$ git tag -d mytag



# Git commit

# Make a commit
$ git commit    # it will open a text editor, write a message and save.

# Make a commit with brief message
$ git commit -m "First commit, learning git"

# Commit all unstaged changes
$ git commit -am "First commit, learning git"

-----------------------------------

Restore an old file
# get a file from another branch or commit
$ git checkout <Commit_ID> <File_Name>
or,
$ git restore <File_name> --source <Commit_ID>


Review the changes, branch history

# Log the branch
$ git log master

# show how two branches are related to each other
$ git log --graph a b

# one line log
$ git log --online

------------

Code change log:

# Limit number of commits by <limit>.
$ git log -5  # it will limit to 5 commits

# View all the commits
$ git log

# Show all commit modified to a file
$ git log <File_Name>

# Find every commit added/removed some text
$ git log -S <File_Name>

# Display full diff of each commit
$ git log --stat

# List the change over time for a specific file
$ git log -p <File_Name>

# Search for commit by a particular author
$ git log --author="<PPattern>"

# Display commits that have the specified file
$ git log -- <File_Name>

# Condense each commit to a single line.
$ git log --online

# --graph flag draws a text based graph of commits on left side of commit msgs. 
# --decorate adds names of branches or tags of commits shown.
$ git log --graph --decorate 

# Trace who made change to a file with time
$ git blame <File_Name> 

-----------------------------------
Branch and Tags

# Create a new branch
$ git branch <Branch_Name>

# Change the branch HEAD
$ git checkout <Branch_Name>

# list all branches
$ git branch -a

# Delete a branch 
$ git branch -d <Branch_Name>

# Force delete a branch
$ git branch -D <Branch_Name>

# list branches by most recently committed to:
$ git branch --sort=committerdate

Tagging - Tagging is infact specific points in a repository’s history making it as an important such as version number. like v.01
$ git tag <Tag_Name>
$ git tag v.01
# Explore for more options..


Clone and push the change
# Download the repo
$ git clone <Repo_URL>

# Get the repo URL
$ cd <Landscape>; git remote -v
# you will get remote Repo URL. Use this URL to clone the repo.

Pull the repo data locally
# Download the update from remote repository and sync with local repo (HEAD)
$ git pull 
$ git pull origin main
$ git pull --recursive
$ git pull <Remote> <Branch_name>

# Download the changes from remote repo but do not sync into HEAD. 
$ git fetch origin main
$ git fetch <Remote_repo>

# fetch changes and then rebase your current branch
$ git pull --rebase

# Fetch all branches
$ git fetch --all

# add commit the change
$ vi abc.txt
$ git add .; git commit -m "Update abc.txt file"

# Push change to remote repo
$ git push
$ git push <remote> <branch>

# Push a branch to the remote origin that you ahve never pushed before
$ git push -u origin <Name>

# Push current branch to its remote tracking branch
$ git push

# force push
$ git push --force-with_lease

# push tags
$ git push --tags


# Use your configured merge tool to solve conflicts
$ git mergetool

# Use your editor to manually solve conflicts and ( after resolving) mark file as resolved
$ git add <resolved-file>
$ git rm <resolved-file>


Undo
# Discard all your local changes in your working directory
$ git reset --hard HEAD

# Discard local changes in a specific file
$ git checkout HEAD <File_name>

# Revert a commit (by producing a new commit with contrary changes)
$ git log  
$ git revert <Commit>

# Reset your HEAD pointer to a previous commit and discard all changes since then.
$ git reset --hard <commit>

# reset your HEAD pointer to a previous commit and preserve all changes as unstaged changes.
$ git reset <Commit>


Merge and Rebase
# Merge <Branch> into your current HEAD, mean current repo.
$ git merge <Branch_Name>

# Rebase your current HEAD into the <Branch>
$ git rebase <Branch_name>

# Abort rebase
$ git rebase --abort


Make your hand dirty
---------------------

1. Start a project. 

# git init command creates a new repo.
$ mkdir myproject; cd myproject
$ git init


# Download your remote repo locally
$ git clone <Remote_Repo_URL>
$ git clone https://bac.com/def

# Update a file
$ vi hello.txt
---
add your stuff here
...
wq!

# Rebase your current HEAD into <New Branch> (optional)
$ git rebase <Branch_name>

# Check the status of the change - what changes are made
$ git status

# Add files to your staging area
# git add helps you to add all changed files to your staging area.
$ git add .   # . means all files/ directories

# To add specific file
$ git add <filename>
$ git add abc.txt


Commit all staged changes
# After git add, use git commit command to wrap your changes into git database. You can supply brief message what changes are made
$ git commit -m "Message"
$ git commit -n "Initial Configuration"

# verify the status of the staged files
$ git status

# Check the commit history. 
$ git log
Note: commit ID.

# once you verify the change, push your change from local to remote repo.
$ git push
$ git pull






Creating alias
CONFIGURE ALIASES (optional)
These are used as shorthands:
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.st status
$ git config --global alias.br branch
$ git config --global alias.hist 'log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short'
$ git config --global alias.type 'cat-file -t'
$ git config --global alias.dump 'cat-file -p'
Do rebase istead of merge always when pull:
$ git config --global branch.autosetuprebase always

# get help
$ git help <command>


# add a remote
$ git remote add <Name> <URL>

How git works

Ref: Collected from different sources
