## Clone a repository
### ( 1 ) Go on github.com and create a new repository.
### ( 2 ) Copy the URL of the repository by clicking on HTTPS.
### ( 3 ) Open a terminal and navigate to the directory where you want to clone the repository.
### ( 4 ) Run the following command:

```bash
git clone <URL>
```

## Rename a repository
### ( 1 ) Go on github.com and rename the repository .

### ( 2 ) Locally, open a terminal and navigate to the directory of the repository and run
```bash
mv <old_name> <new_name>
```
#### ( 2.1 ) If a permission error occurs, rename manually the folder in the file explorer.

### ( 3 ) Copy the URL of the remote repository and set it to the local one:
```bash
git remote set-url origin <new_URL>
```

### ( 4 ) Verify the new URL:
```bash
git remote -v
```
It should return
```bash
origin  <new_URL> (fetch)
origin  <new_URL> (push)
```


## Create a new branch and push it to the remote repository
By default, you are on the master branch. Do the following to create a new branch and push it to the remote repository:
### ( 1 ) Create a new branch and switch to it:
```bash
git checkout -b <branch_name>
```
### ( 2 ) Push the branch to the remote repository:
```bash
git push origin <branch_name>
```

## Get a remote branch to your local repository
### ( 1 ) Check the available branches in the remote repository:
```bash
git fetch
git branch -r
```
Example result
```
  origin/HEAD -> origin/master
  origin/master
  origin/new_branch
```
Suppose you want to get the branch `new_branch` to your local repository.

#### ( 1.1 ) If the remote branch does not show up in the list of branches:
```bash
git fetch --all
git branch -r
```

### ( 2 ) Create a new branch in your local repository and point it to the remote branch:
```bash
git checkout -b new_branch origin/new_branch
```
### ( 3 ) Verify the tracking of the branches:
```bash
git branch -vv
```
It should return
```
master  <hashcode> [origin/master] Commit message
* new_branch  <hashcode> [origin/new_branch] Commit message
```

## Rename a branch
### ( 1 ) Ensure you are in the branch you want to rename:
```bash
git checkout <branch_name>
```

### ( 2 ) Rename the branch:
```bash
git branch -m <new_branch_name>
```

### ( 3 ) Delete the old branch in the remote repository:
```bash
git push origin --delete <old_branch_name>
```

### ( 4 ) Push the new branch to the remote repository:
```bash
git push origin <new_branch_name>
```

### ( 5 ) Update the tracking of the branches:
```bash
git branch --set-upstream-to=origin/<new_branch_name> <new_branch_name>
```

## Delete a branch
### ( 1 ) Delete the branch in the local repository:
```bash
git branch -d <branch_name>
```

### ( 2 ) Delete the branch in the remote repository:
```bash
git push origin --delete <branch_name>
```

## Change branch name
### ( 1 ) Ensure you are in the branch you want to rename:
```bash
git checkout <branch_name>
```

### ( 2 ) Rename the branch:
```bash
git branch -m <new_branch_name>
```

### ( 3 ) Push the new branch to the remote repository:
```bash
git push origin <new_branch_name>
```
