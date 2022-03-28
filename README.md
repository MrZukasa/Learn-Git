# Git Commands 🏗️
In order to check if we allready have git on our system type:
```
git --version
```
To initialize a repository into a folder that we are going to use as repository
```
git init
```
Create a new file in the repository
```
touch [filename.extension]
```
Show the file contents
```
cat [filename.extension]
```
Show the status of our repository
```
git status
```
Add to the git index (Staging area) all the file or some of them
```
git add . or git add [filename.extension] or git add [*.extension]
```
To commit the changes use:
```
git commit -m "[commit message]" -m "[commit description]"
```
In order to avoid to use `git add` before the commit we can do something like:
```
git commit -am "[commit message]"
```
where the -a parameter stand for 'all'

<hr>

Remove file from the index (Staging area)
```
git restore --staged [filename.extension]
```
When we want to see the history of the commits
```
git log
```
See the references of the HEAD file
```
cat .git/HEAD
```
See the commits list in a short way
```
git log --oneline
```
Restore te previus commit instead of the new one by sending a new commit
```
git revert
```
To change the message of the last commit
```
git commit --amend -m "message"
```
To undo the commit
```
git reset or git reset --soft or git reset --hard
```
- _--mixed_ &rarr; this remove the commit and the file in the staging area (default version) 
  - ***[TL:DR: Remove the commit and the stage area]***
- _--soft_ &rarr; this remove commit and restore the file status to the staging area 
  - ***[TL:DR: Remove the commit]***
- _--hard_ &rarr; this remove the commit and all the added files in the last commit, this will remove the file physically 
  - ***[TL:DR: Remove the commit, the stage area and delete the files!]***

***NOTICE:*** we can use `git reset --[parameter]` with the id of the commit or the `HEAD` and the position of the commit that we want to refer to, like so: `git reset --[parameter] HEAD~1` in case we need 1 position before the `HEAD` pointer, or `git reset --[parameter] HEAD~2` in case we need to go back of 2 commits before the `HEAD`.

<hr />
- Change the commit message
```
git commit --amend
```
- In order to remove file from the git add . we need to set a .gitignore file which will contains all the file, extensione and folder that we need to avoid to commit, also we can apply a rule to allow a single file of a specified denied extension.
<hr />

### Branch 🦺
- Graphical rapresentation of our branches configuration
```
git log --all --decorate --oneline --graph
```
In order to avoid type everytime all this command in our system we can add all of this into an Alias by using our powershell:

![Alias](https://i.ibb.co/tKGJ2N6/Untitled.png)

- To create a branch we use:
```
git branch [name]
```
- To see the existing branches:
```
git branch
```
- To move the HEAD in between the branches we need to use:
```
git checkout [branch name]
```
<hr />

In the image below we can see that there are 3 different branches.
Two of them already have some changes into the same files, as we can see in the 'split' branch rapresentation
![Branch](https://i.ibb.co/6ZRKjZR/Capture.png)

we can also inspect the differences between two branches by using:
```
git diff [first branch]..[second branch]
```

In order to merge one of those branch to the master one we need to:
```
git checkout master
git merge fix
```

After that done we see as follow
![Merge](https://i.ibb.co/s6C5D5d/Capture.png)

```
git config --global core.editor "code --wait"
git remote -v
git ls-remote
```