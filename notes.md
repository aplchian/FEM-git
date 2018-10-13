# GIT Notes

## Good Commits Are Important

Good commits help preserve the history of a code base

They help with:
 - debugging and troubleshooting
 - creating release notes
 - code reviews
 - rolling back
 - associating the code with an issue or ticket

commit message should be in future tense - "fix" vs "fixed"

description should be context. dont explain how you did something .. not "i moved file a to b".. you should say how you did something.. the code will describe what you did.. mention any side effects, etc. 

Anatomy of a good commit:
- good commit message
- encapsulate one logical idea
- doesnt introduce breaking changes
    - ie. your tests pass
    - shouldnt leave your code in a broken state

## Git Log

```
git log

basic command that shows you the history of your repo
```

```
the site has been slow in the past week.. what happened since then?
git log --since="yesterday"
git log --since="2 weeks ago"
```

## Referencing Commits

Referencing commits by their parents with ~ and ^ .. good for easily going to commits... rather than copying the commit hash and going that way

 A = A^0

 B = A^ = A^1 = A~1

 C = A^2

 D = A^^ = A^1^1 = A~2

 E = B^2 = A^^2

 ## Git Show - Look at a commit

 ```
 -> show commit and contents
 git show <commit>
 ```

 ```
 show files changed in commit:
 git show <commit> --state
 ```

 ```
 look at a file from another commit
 git show <commit>:<file>
 ```

## Git diff

shows changes:

- between commits
- between staging area and the repo
- whats in the working area


```
-> unstaged chages
git diff
```

```
stages changes
git diff --staged
```

can also pass file arguments in diff command

```
git diff A B

-> shows you all the changes that are on branch B, but not branch A
```

## "Diff" branches


```
-> Which branches are merged with master, and can be cleaned up?
git branch --merged master
```

```
-> Which branches arent mergedd with master yet?
git branch --no-merged master
```

```
-> if you want to force a checkout.. if it says 'there are uncommited changes', etc
git checkout -f <branch>
```

```
git log --author=alex --since=2.weeks
```

# Fixing Mistakes

checkout
reset
revert
clean

in order to know how to fix mistakes, you need to have a clear idea of how those 3 areas where code lives work:
- working area
- staging area
- repository

and how we move data between them

## Git checkout out

restore working tree files or switch branches

What happens when you git checkout a branch?

1. Change HEAD to point to the new branch
2. copy the commit snapshot to the staging area
3. update the working area with the branch contents

## Git Clean

Git clean will clear your working area by **deleting** untracked files.

**This operation cannot be undone**

You can use `--dry-run` to see what would be deleted
    - `-f` flag to do the deletion
    - the `-d` flag will clean directories


## Git Reset

Reset is another command that performs differenct actions depending on the arguments

understanding this is important

- with a path
- without a path
    - by default, git performs a `git reset -mixed`
- for commits:
    - Moves the HEAD pointer, optionally modifies files
- for file paths:
    - does not move the HEAD pointer, modifies files


3 options for reset:
- soft - not used frequently  
    - `git reset --soft HEAD~` - just moves the head pointer to the previous commit
- mixed
    - this is default `git reset --mixed HEAD~` - just moves the head pointer to the previous commit, and moves file of previous commit to staging area
- hard
    - `git reset --hard HEAD~` - just moves the head pointer to the previous commit, and moves file of previous commit to staging area **and working area** - destructive


### Git Reset -- <File>

```
-> doesnt move head pointer, just moves file from commit to staging area
git reset <file>
```
```
git reset <commit> -- <file>
```

### Undue a git reset with ORIG_HEAD

- in case of accident git reset
- git keeps the previous value of HEAD in a cariable call ORIG_HEAD
- To go back to the way things were:
    - `git reset ORIG_HEAD`



## Git Revert

this is a safe reset..  reseting code you shared, on public repos, etc. The original commit stays in the repo

git creates a commit that is the mirror opposite of the one you specified

```
git revert [hash]
```

**if you want to revert a revert... its not going to work.. the best option is to cherry pick your changes**








