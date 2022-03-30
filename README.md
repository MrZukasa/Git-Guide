<h1 align="center">🏗️ Git Commands</h1>

- In order to check if we allready have git on our system type:
  - `git --version`

- To initialize a repository into a folder that we are going to use as repository
  - `git init`

- Create a new file in the repository
  - `touch [filename.extension]`

- Show the file contents
  - `cat [filename.extension]`

- Show the status of our repository
  - `git status`

- Add to the git index (Staging area) all the file or some of them
  - `git add .` or `git add [filename.extension]` or `git add [*.extension]`

- To commit the changes use:
  - `git commit -m "[commit message]" -m "[commit description]"`

- In order to avoid to use `git add` before the commit we can do something like:
  - `git commit -am "[commit message]"`
where the `-a` parameter stand for 'all'

<hr>

- Remove file from the index (Staging area)
  - `git restore --staged [filename.extension]`

- When we want to see the history of the commits
  - `git log`

- See the references of the HEAD file
  - `cat .git/HEAD`

- See the commits list in a short way
  - `git log --oneline`

- Restore te previus commit instead of the new one by sending a new commit
  - `git revert`

- To change the message of the last commit
  - `git commit --amend -m "message"`

- To undo the commit
  - `git reset` or `git reset --soft` or `git reset --hard`
  - _--mixed_ &rarr; this remove the commit and the file in the staging area (default version) 
    - ***[TL:DR: Remove the commit and the stage area]***
  - _--soft_ &rarr; this remove commit and restore the file status to the staging area 
    - ***[TL:DR: Remove the commit]***
  - _--hard_ &rarr; this remove the commit and all the added files in the last commit, this will remove the file physically 
    - ***[TL:DR: Remove the commit, the stage area and delete the files!]***

***NOTICE:*** we can use `git reset --[parameter]` with the id of the commit or the `HEAD` and the position of the commit that we want to refer to, like so: `git reset --[parameter] HEAD~1` in case we need 1 position before the `HEAD` pointer, or `git reset --[parameter] HEAD~2` in case we need to go back of 2 commits before the `HEAD`.

<hr />

- In order to remove file from the `git add .` we need to set a `.gitignore` file which will contains all the file, extensione and folder that we need to avoid to commit, also we can apply a rule to allow a single file of a specified denied extension.

<hr />

<h2 align="center">🦺 Branch</h2> 
The common way to use a branch is to keep the stable version of the software as a main branch, and all the other features that are experimental or that can comport some bug fixing or even make the software to be unstable, are destinated to be stored in some side branch.

The `master` name is made by initialize the folder to our repository.

The branch in the beginning is a simple label that identifies the last commit of that specific branch.

- In order to see a graphical rapresentation of our branches configuration we can use such a command
  - `git log --all --decorate --oneline --graph`

Also we can create an Alias to avoid to type everytime all that.
I've made a little bit different commands to do the same thing, just a bit more clear.
Also i've placed those two commands as alias

```PowerShell
hist = log --pretty=format:\"%Cgreen%h %Creset%cd %Cblue[%cn] %Creset%s%C(yellow)%d%C(reset)\" --graph --date=relative --decorate --all
llog = log --graph --name-status --pretty=format:\"%C(red)%h %C(reset)(%cd) %C(green)%an %Creset%s %C(yellow)%d%Creset\" --date=relative
```

- To create a branch we use:
 - `git branch [name]`

In order to see all branches we type just `git branch` with no arguments.
Every new branch that is created will point to the last commit, so where the `HEAD` is.

- In order to move in between branches we need to move the `HEAD`, and to do that we can use:
  - `git checkout [branch name]`

- After that we've made some changes to the files in every branches, we may want to merge them back into the main branch.
To do that we need to use 
  - `git merge`

- Before to do that we can check the difference between the two branches by using
  - `git diff [first branch]..[second branch]`

- In order to merge those branch one in an other we need to:
  - `git checkout [first branch]`
  Then
  - `git merge [second branch]`

- The merge can be make in a different way:
  - **_FastForward_** by moving ahead the branch `master` to match the last commit of the `fix` branch.
  - ***Three Way Merge***In case you move the `HEAD` in a commit that is not a direct parent of the branch that we want to merge, git, will verify the commit that is shared in between branches and compare it to the next commit in order to check if there will be some issue.

- In order to see which branch was merged we can use
  - `git branch --merged`

- If we don't need anymore a specific branch we can remove it by using:
  - `git branch -d [branch name]`

***NOTICE:*** that if the branch was not already merged we can force the delete with uppercase `-D` parameter

- In case we want to undo some merge we can use
  - `git merge --abort`

- If we want to move and in the same time create a branch we can use
   - `git checkout -b [new branch name]`

<hr/>

<h2 align="center">🏊🏻‍♂️ Use Remote server as repository store GitHub</h2>

- Once that we made a GitHub account we can set the origin address with:
  - `git remote add origin [address]`

- To upload our local repository to the server provided by GitHub we need to type:
  - `git push -u origin master`

<hr />

- In order to see the list of our Remote origin, we can type:
  - `g remote`

this will show the origin and, if we add `-v` parameter we can even see the address.

- In order to inspect the Remote origin and check if our Local or our Remote is *up to date* and other info, we can simply type:
  - `git remote show origin`

- if we want to rename our Remote server:
  - `git remote rename origin [new name]`

- if we want to remove our Remote server:
  - `git remote remove origin`

<hr />

- In order to get the files from our Remote repo to our Local repo, we need to type:
  - `git fetch or git pull`

With the command `git fetch` we can get all the changes from the Remote repo, but only the changes non the files, to get even the files we need to merge our local branch with the origin by usin `git merge origin/master`. 

- Otherwise we can do all of that in one command, get the info and the sync from the Remote repo and also the files by using:
 - `git pull`

<hr />

- If we want to clone one online existing repo we need to use:
  - `git clone [URL]`

<hr />

## Fork a someone else repository 👨🏼‍🏭
Once that we have forked the repository into our account we can easily clone it as a normal repo with `git clone [URL]`.

After that we have made some changes to the repo, we can contribute to the original repo by asking to the owner the permission to contribute with our new forked repo.
We can do that directly from GitHub.

- If we want (and the owner allow us) we can add the remote URL of the original repo into the `origin` of our forked repo
  - `git remote add [alias] [URL of the original repo]`

- Every time that someone push something in the original repo, we can easily sync our forked repo in order to keep it up to date:
  - `git fetch [alias] and git merge [alias]/[branch]`

  or we directly pull:
  - `git pull [alias] [branch]`

once that our Local repo is up to date we can simply `git push` those changes to the Remote repo (the forked one):

<hr />

## Bonus 🛀🏼
- Command that allows the user to use VSCode as editor for the commit message 
  - `git config --global core.editor "code --wait"`
