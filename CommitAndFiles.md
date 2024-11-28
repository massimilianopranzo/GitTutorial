## Download remote updates without modifying the local repository
### ( 1 ) Fetch the changes from the remote repository:
```bash
git fetch
```

## Push local changes to the remote repository
### ( 1 ) Add the changes to the staging area:
```bash
git add .
```
#### ( 1.1 ) '.' adds all the changes to the staging area. If you want to add only specific files, replace '.' with the file names.

### ( 2 ) Commit the changes:
```bash
git commit -m "Commit message"
```
### ( 3 ) Push the changes to the remote repository:
```bash
git push
```

## Pull changes from the remote repository
### ( 1 ) Pull the changes from the remote repository:
```bash
git pull
```
### ( 1.1 ) If you want to pull changes from a specific branch:
```bash
git pull origin <branch_name>
```

Note: If you have uncommitted changes in the working directory, you will get an error. You can either commit the changes or stash them.

## Stash changes (save changes for later use)
### ( 1 ) Stash the changes:
```bash
git stash
``` 
Now all the changes have been saved. You can use this to make experiments starting from the latest commit or switch branches without losing the changes.

### ( 2.a ) Reapply the changes <u>losing</u> changes done after the stash:
```bash
git stash apply
```

### ( 2.b ) Reapply the changes keeping changes done after the stash:
```bash
git stash pop
```
In this case if conflicts arise, the merge editor will open to resolve them.


## Make your local repository identical to the remote repository (<u>you will lose ALL your local changes</u>) 
### ( 1 ) Ensure you are in the branch you want to reset:
```bash
git checkout <branch_name>
```
### ( 2 ) Reset the branch to the remote repository:
```bash
git fetch origin
git reset --hard origin/<branch_name>
```

## Rename a commit
### ( 1 ) List all the commits:
```bash
git log --oneline
```
Click enter to show more commits. Press 'q' to exit the log.

Example output:
```bash
<hashcode1> (HEAD -> master, origin/master, origin/HEAD) Commit message 1
<hashcode2> Commit message 2
<hashcode3> Commit message 3
<hashcode4> Commit message 4
.
.
.
```
Suppose you want to rename the commit with hashcode `<hashcode3>`.
### ( 2 ) Copy the hashcode of the commit you want to rename.

### ( 3 ) Do a rebase of n commits starting from the commit to which HEAD is pointing at (from <hashcode1> in the example):
```bash
git rebase -i HEAD~n
```
In our case n = 3, so run `git rebase -i HEAD~3`.

### ( 4 ) The file *git-rebase-todo* will open:
```
pick <hashcode1> Commit message 1
pick <hashcode2> Commit message 2
pick <hashcode3> Commit message 3

And other lines of comments explaining the rebase process.
```

### ( 5 ) Change the word *pick* to *reword* for the commit you want to rename and then save and close the opened file.
```bash
pick <hashcode1> Commit message 1
pick <hashcode2> Commit message 2
reword <hashcode3> Commit message 3
```

### ( 6 ) The file *COMMIT_EDITMSG* will open:
```
Commit message 3
```
Change *Commit message 3* to the new commit message and then save and close the opened file.

### ( 7 ) Verify the changes:
```bash
git log --oneline
```

It should return:
```bash
<hashcode1> (HEAD -> master) Commit message 1
<hashcode2> Commit message 2
<hashcode3> New commit message
<hashcode4> Commit message 4
.
.
.
```

## Unstage files before if not committed yet
To be used after adding files to the staging area but before committing them.

### All files:
```bash
git reset
```
### or choose files:
```bash
git reset <file_name>
```

## Cancel commit if not pushed yet 
Suppose you have added files to the staging area and committed them but have not pushed them to the remote repository yet and you want to cancel the commit.
### ( 1 ) Cancel the commit
```bash
git reset --soft HEAD~1
```
This will cancel the commit but the files are still in the staging area.

### ( 2 ) Unstage the files
Same as described in the previous section.

### You can do point 1 and 2 (unstaging all files) simultaneously by running (not recommended):
```bash
git reset --mixed HEAD~1
```
### You can delete commit, unstage files and <u>DELETE CHANGES</u> in the working directory by running (highly not recommended):
```bash
git reset --hard HEAD~1
``` 

## Modify the staged files after committing
### ( 1 ) Modify the files in the staging area with git add
```bash
git add <file_name> OR git add .
```

### ( 2 ) Commit the changes
If you want to keep the commit message:
```bash
git commit --amend --no-edit
```
If you want to change the commit message:
```bash
git commit --amend
```
Then the file *COMMIT_EDITMSG* will open. Change the commit message and save and close the file.

### ( 3 ) Push the changes to the remote repository
```bash
git push
```

## Create a tag for a commit
### ( 1 ) List all the commits:
```bash
git log --oneline
```

### ( 2 ) Copy the hashcode of the commit you want to tag.

### ( 3 ) Create a tag for the commit:
```bash
git tag <tag_name> <hashcode>
```

If you want to tag the latest commit, you can run:
```bash
git tag <tag_name>
```

### ( 3.1 ) Tag with a message:
```bash
git tag -a <tag_name> -m "Tag message" <hashcode>
```

### ( 4 ) Push the tag to the remote repository:
```bash
git push origin <tag_name>
```
or push all tags:
```bash
git push --tags
```

### ( 5 ) Verify the tag:
```bash
git tag
```

## Delete a tag
### ( 1 ) Delete the tag in the local repository:
```bash
git tag -d <tag_name>
```

### ( 2 ) Delete the tag in the remote repository:
```bash
git push origin --delete <tag_name>
```

**Note**: to modify a tag, you still need to delete it first and then create a new one. 

### ( 3 ) Verify the tag in the local repository:
```bash
git tag
```

### ( 4 ) Verify the tag in the remote repository:
```bash
git ls-remote --tags origin
```
