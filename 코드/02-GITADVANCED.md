# Git Advanced

## Branching
diverging from a main line of development and doing work without messing with the main line

example: fixing a bug from version 1.0 without messing with version 1.1

version 0.9 -> version 1.0 -> version 1.1

                        |___
                            |
                            ---> branch to fix a version 1.0 bug

* HEAD -> special pointer to the last commit made

### Creating a Branch
- git branch ```<name>``` -> creates a new branch ```<name>``` based on HEAD 
- git branch -> lists all the branches and the branch you are on
- git checkout ```<name>``` -> switch to branch ```<name>```
- git checkout -b ```<name>``` -> creates and switches to branch ```<name>```
- git merge ```<name>``` -> merge current branch with branch ```<name>```


### github remote repositories
two urls for repositories:
1. https://github........
    - temporary authorization
    - will always ask for username and password every commit
2. git@github.......
    - more permanent

### Git Authorization
1. Issue public and Private keys (credentials stored in /.ssh)
    run "ssh-keygen"
2. Register public key to GitHub
    1. go to SSH and GPG keys tab in Settings
    2. enter password
    3. click on "New SSH Key"
    4. copy the content of "id_rsa.pub" to the form
    5. git clone
3. git command will automatically use the keys

### remote repository code
- git remote / git remote -v -> shows the remote repositories of the current git
- git remote add ```<shortname>``` ```<url>``` -> add ```<shortname>``` to ```<url>``` repository
- git remote rename ```<oldname>``` ```<newname>``` -> rename
- git remote rm ```<name>``` -> remove
- git push / git push ```<remote_name>``` / git push ```<remote_name>``` ```<branch_name>``` -> pushes / updates your current branch to the remote repository
    - there may be errors in merging (must fix the conflict between local and remote version of the branch)
- git fetch / git fetch ```<remote_name>``` -> fetch the remote repository to local and will be in ```<origin/main>``` / if you were working on a code before the fetch, that would automatically be branched out to main
- git pull -> will fetch the remote repository and update this repository together with the local branch