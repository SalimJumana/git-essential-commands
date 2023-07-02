##### current git version


```
git --version
```

##### git global user config


```
git config --global user.name "FIRST_NAME LAST_NAME"
```


```
git config --global user.email "MY_NAME@example.com"
```

##### initialize a project

```
git init
```

##### uninitialize a project

```
rm -rf .git
```

##### git files state

```
git status
```

##### commands log

```
git log
```

##### clone a project

```
git clone URL.git
```

##### add all files or specific file to stage

```
git add .
```

```
git add somefile.java
```

##### remove files from tracked list

```
git rm --cached <file>
```

```
git rm -r --cached <directory>
```

##### commit a change

```
git commit -m 'initial commit'
```

##### add branch dev

```
git checkout -b dev
```

##### remove branch dev

```
git branch -d dev
```

##### switch branch master

```
git checkout master
```

##### merge with current branch

```
git merge otherbranch
```

##### add a remote url with "origin" alias

```
git remote add origin "URL.git"
```

##### current push and fetch remotes

```
git remote -v
```

##### force push to remote

```
git push -uf origin master
```

##### pull and update project changes into local

```
git pull origin master
```
Or you can add explicit url instead of alias:

```
git pull "URL.git" master
```

##### fix conflict hard reset 
##### Note: take a backup first

```
git fetch origin
```


```
git reset --mixed origin/master
```

### Switches

##### --hard 
makes everything match the commit you've reset to. This is the easiest to understand, probably. All of your local changes get clobbered. One primary use is blowing away your work but not switching commits: git reset --hard means git reset --hard HEAD, i.e. don't change the branch but get rid of all local changes. The other is simply moving a branch from one place to another, and keeping index/work tree in sync. This is the one that can really make you lose work, because it modifies your work tree. Be very very sure you want to throw away local work before you run any reset --hard.

##### --mixed 
is the default, i.e. git reset means git reset --mixed. It resets the index, but not the work tree. This means all your files are intact, but any differences between the original commit and the one you reset to will show up as local modifications (or untracked files) with git status. Use this when you realize you made some bad commits, but you want to keep all the work you've done so you can fix it up and recommit. In order to commit, you'll have to add files to the index again (git add ...).

##### --soft 
doesn't touch the index or work tree. All your files are intact as with --mixed, but all the changes show up as changes to be committed with git status (i.e. checked in in preparation for committing). Use this when you realize you've made some bad commits, but the work's all good - all you need to do is recommit it differently. The index is untouched, so you can commit immediately if you want - the resulting commit will have all the same content as where you were before you reset.

##### --merge 
was added recently, and is intended to help you abort a failed merge. This is necessary because git merge will actually let you attempt a merge with a dirty work tree (one with local modifications) as long as those modifications are in files unaffected by the merge. git reset --merge resets the index (like --mixed - all changes show up as local modifications), and resets the files affected by the merge, but leaves the others alone. This will hopefully restore everything to how it was before the bad merge. You'll usually use it as git reset --merge (meaning git reset --merge HEAD) because you only want to reset away the merge, not actually move the branch. (HEAD hasn't been updated yet, since the merge failed)

To be more concrete, suppose you've modified files A and B, and you attempt to merge in a branch which modified files C and D. The merge fails for some reason, and you decide to abort it. You use git reset --merge. It brings C and D back to how they were in HEAD, but leaves your modifications to A and B alone, since they weren't part of the attempted merge.