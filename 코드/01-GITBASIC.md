#  Git basics
Quite the interesting subject

## states of files:
untracked: file is not under version control -> ignored by git
unmodified: file IS under version control, but not modified -> no need to record changes
modified: under version control and modified -> changes should be recorded
staged: file is under version control and it is modified -> staged and prepared to be committed
commited: changes were committed -> same as the unmodified state

## three main sections
working directory: a single checkout of one version of the project
    - initially all files are unmodified
    - you can modify files here
    - select files to stage and prepare for committed
staging area: files that are staged and prepared to commit
local git repo(.git) stores commits

## workflow
git init -> initializes a git repository

git clone <existing git repo> -> clones a git repo

git add <file> -> adds file to staging area

git add . -> adds all untracked or modified files to the stage

git commit -> commits a file and becomes unmodified

git commit --amend -> commiting additional files

*literally editing a committed/unmodified file* -> file becomes modified state

git status -> checks state of files

git restore --staged <file> -> unstages a file

git restore --staged . -> unstages all staged files and becomes 
untracked

.gitignore -> can add files for git to ignore

git rm <file> -> remove a file

git rm --cached <file> -> remove a file from repo only