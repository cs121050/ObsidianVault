
#### core lesson:
**Never change brunch if you have uncommitted changes!!!**
Stanch OR add/commit  

```bash
#Use this when: Work is logical,Even if incomplete
git add .
git commit -m "Fix foreign key constraints with custom names"
git checkout other-branch

```
OR
```bash
#Use this when: You need to switch fast. Work is messy or experimental
git stash
git checkout other-branch

git stash push -m "WIP: what I was doing"

#see the stash
git stash list
#aply stash
git stash apply "stash@{0}"
```

➡️ Safe to switch branches
```bash
git status
#If you see:
nothing to commit, working tree clean
```


### ## The GIT workflow  correct)

> checkout → work branch → commit → push → PR → merge → pull main.


#### GitHub CLI (GIT remote control terminal)
```bash
#see if you allready have it installed
gh --version
##run terminal as admin, and run this instalation command
`winget install --id GitHub.cli`
## see if installed corectly
gh --version
## sync the CLI to you github acound
gh auth login
```
**Troubleshooting**: If 'gh --version'  would not work, after installation it might be because you have note set an environment varable: 1) go to the folder the GIT CLI was installed (propably C::/programfiles/ GitHub CLI) and copy the path. 2) press WINDOWS -> search for 'evironment variables'-> click env variables -> ath 'env variables' click 'Path', then click edit -> create a new one with the Path of the 1) -> in your way out press 'ok'. 3) Return to terminal an press 'gh --version' the problem has solved.
```bash
# install ... in order to run pipeline (or deep) commands
winget install jqlang. jq
```


```bash
#list all the repos
gh repo list cs121050 --json name,updatedAt --limit 1000 | ConvertFrom-Json | Format-Table -AutoSize
# what is the recently updated repo 
$repos = gh repo list cs121050 --json name,updatedAt --limit 1000 | ConvertFrom-Json
$newest = $repos | Sort-Object -Property updatedAt -Descending | Select-Object -First 1
$newest.name
## delete a repository 
gh repo delete cs121050/REPO_NAME --confirm




#check out to the branch
git checkout my-feature
# create new branch , checkout to it
git checkout -b my-feature
#delete a branch
git branch -d branch-name






# 1. Fetch the latest from remote
git fetch origin

# 2. Reset your local main branch to match remote EXACTLY
git reset --hard origin/main




```

```
```






---

```bash
#see the commits of the branch, that have not been pushed yet 
 git log main
#make sure the remote exist 
git remote -v
```













url: jdbc:sqlserver://localhost:1433;encrypt=true;trustServerCertificate=true;databaseName=JazzLibraryHibernate # SQL Server connection URL

username: sa # Database username

password: A123!@#alepasas # Database password





## Get a project ready foR GIT

```bash 

#1. install git 
winget --version
winget install --id Git.Git -e --source winget
git --version
#Configure Git globally
jazz git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
git config --list

#1. initialise 
git init
git status

#2. 
git add README.md
#stage all changes
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/cs121050/REPONAME
git push -u origin main

```





```bash
#better than statch: delete all unstaged changes
git restore .
```

```bash

# Check the status of your working directory (tracked/untracked files)
git status

# Stage all changes (new files, modifications) for the next commit
git add .

# Commit staged changes with a message
git commit -m "Your commit message"

# Show the changes in the last commit
git show

# Create a new branch and switch to it immediately
git checkout -b branch-name

# Switch to an existing branch
git checkout branch-name

# Rename the current branch
git branch -m new-branch-name

# Delete a local branch safely (only if merged)
git branch -d branch-name

# Force delete a local branch (even if unmerged)
git branch -D branch-name

# List all commits in compact format
git log --oneline

# Show details of a specific commit, including code changes
git show commit-hash

# Add a remote repository (link local repo to GitHub)
git remote add origin https://github.com/username/repo.git

# Remove a remote repository
git remote remove origin

# Push changes to a remote branch and set it to track upstream
git push -u origin branch-name

# Force push changes to a remote branch (used when rewriting history)
git push -u origin branch-name --force

# Create a new branch with no commit history (orphan branch)
git checkout --orphan branch-name

# Reset the current branch to a previous commit, discarding changes (hard reset)
git reset --hard commit-hash

# Delete a remote branch on GitHub
git push origin --delete branch-name

# Amend the last commit (update commit message or include new changes)
git commit --amend

# Amend the last commit including all changes in working directory
git commit --amend --all

# Continue an interactive rebase after editing a commit
git rebase --continue

# Start an interactive rebase to rewrite history from a specific commit
git rebase -i commit-hash~1




#check if the file is ignored 
git check-ignore -v application-dev.yaml
#Untrack files that were **already committed
git rm --cached application-dev.yml



```



git add src/main/resources/application-prod.yaml

git push





## get an Androidprojectto git

```bash
# Open Terminal in Android Studio (Bottom toolbar)
cd /path/to/your/project

# Step 1: Initialize git
git init

# Step 2: Add all files
git add .

# Step 3: Create .gitignore (crucial for Android)
echo ".idea/
.gradle/
build/
captures/
.externalNativeBuild/
.cxx/
local.properties
*.iml
*.apk
*.ap_
*.dex
*.class
*.log
*.temp
*.pro
/proguard/
app/build/
" > .gitignore

# Step 4: Commit
git commit -m "Initial commit - Jazz Library API project"

# Step 5: Create GitHub repository and push
# Go to: https://github.com/new
# Create repository named "jazz-library-android"
# Then:
git remote add origin https://github.com/YOUR_USERNAME/jazz-library-android.git
git branch -M main
git push -u origin main
# ifit fail, mightbe because u have created readme file 
git push -u origin main --force
```