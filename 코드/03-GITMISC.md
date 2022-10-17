# Git Misc + Code Editor

## Commit logs
git log
q -> exit

## Tagging commits
- giving a human-readable name to a commit
git tag -a <tag_name> -m <message> -> gives <tag_name> to main branch
git push origin <tag_name> -> explicitly pushing <tag_name> (git push does not push tags by default)

## Branch vs Tag
Branch: a line of development
Tag: an alias for a complex commit id
git checkout <branch_name>/<tag_name> -> checkout the commit that a branch or tag refers to
branch pointer advances through a branch every time you make a commit
tag never changes unless you delete and create a new one

## Comparing Code
git diff -> shows changes between commits
git diff --cached -> shows changes between the index and your last commit
git diff HEAD -> shows changes in the working tree since last commit

                    git diff --cached               git diff
Last Commit (HEAD) <------> Changed Staged Index <------> Changed / Not staged working tree
                    <----------------------------------------->
                                    git diff HEAD

## Stashing Changes
- done when something must be fixed immediately when your working with something else / forgot to pull changes from a remote
- temporarily store the changes and bring them back later
git stash -> store the current status
edit "emergency fix"
git commit -a -m "Fix in a hurry" - example of tagging
git stash pop -> call stash status

(merge conflicts can occur for this one)
git stash
git pull
git stash pop

## Git Reset
git reset -> changes the commit history
git reset --soft HEAD~ -> soft reset: only moved what HEAD points to
HEAD~: parent of HEAD
HEAD~2: parent of the parent of HEAD
git reset [--mixed] HEAD~ -> mixed reset: moves what HEAD points to and updates the index as well
git reset --hard HEAD~ -> hard reset: moves what HEAD points to and updates index and working tree as well

git reset --soft HEAD~ -> rarely used
git reset HEAD~ -> Give me a second chance. I will modify and commit it again
git reset --hard HEAD~ -> I was totally wrong. Reset everything to the second last commit

reset type                  HEAD                    Index               WOrking directory
original                    v3.0                    v3.0                v3.0
soft reset                  v2.0                    v3.0                v3.0
mixed reset                       v2.0                    v2.0                v3.0
hard reset                  v2.0                    v2.0                v2.0

## Git restore
git restore -> does not move HEAD (does not change the history)
git restore --staged <file> -> unstages files
git restore <file> -> discards changes and unstages file

## restore reset summary
forgot to add files or want to edit the last commit message
    git commit --amend 

did something wrong but havent committed yet
    git restore --staged <file> ->unstage file
    git restore <file> -> unstage and discard changes

did something wrong and committed changes
    git reset --soft HEAD~ -> rarely used
    git reset HEAD~ -> Give me a second chance. I will modify and commit it again
    git reset --hard HEAD~ -> I was totally wrong. Reset everything to the second last commit

## Git Rebase
git rebase -> replays the changes committed to a branch on a different branch
git rebase --onto <newparent> <oldparent> <until> -> rebases the common branch of <oldparent> and <until> behind <newparent>
git rebase --continue -> used after resolving merge conflicts

merge and rebase -> both methods to handle diverged commit history

merge -> combines the branches
git rebase <branch> -> connects the current branch behind <branch>

merge example
git checkout main
git merge experiment

                    experiment                                                      experiment
                  __--C4                                                            __-- C4
                /_                                                                /_        \  
C0 <-- C1 <-- C2 <-- C3                                           C0 <-- C1 <-- C2 <-- C3 <-- C5   
                   main                                                                      main


rebase example
git checkout experiment
git rebase main(can have conflict)

        experiment             
                  __--C4             
                /_                                                                         experiment
C0 <-- C1 <-- C2 <-- C3                                           C0 <-- C1 <-- C2 <-- C3 <-- C4'   
                   main                                                               main
(continued)
git checkout main
git merge experiment
                        experiment
C0 <-- C1 <-- C2 <-- C3 <-- C4'  
                            main


git rebase --onto example:

git rebase --onto main server client

--------------main                                    -------------------main----------client
    \___                                                      \___
        -----------server                                         --------server
            \____
                --------client

(continued)
git checkout main
git merge client

--------------client/main
    \___
        --------server

(continued)
git rebase server
git rebase main

-----------client/main-----------server

(continued)
git checkout main
git merge server
git branch -d client
git branch -d server
-----------------------------------main


## Benefits of rebase and merge

Rebase: makes the commit history linear as if only one developer worked, does not create merge commits

Merge: Preserves the complete commit history, preserves the context of branches

https://www.atlassian.com/git/articles/git-team-workflows-merge-or-rebase