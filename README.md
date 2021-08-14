# How Git Works

> If you want to master Git, don't worry about learning the commands. instead, learn the model.  

- Git is: 
  - A distributed Revision Control System.
  - A Revision Control System.
  - Stupid Content Tracker
  - A persistend Map
  - man git to see  

## Git is not What you think

### Values and Hashes
At its core Git is a Map, it's a table with keys and values. The values are just a sequence of bytes, and the key is a hash calculated by git with SHA-1.  


SHA-1 hashes are 20 bytes in hexadecimal format, they are a sequence of 40 hex digits.

Hash with git

```shell
# not usefull
git hash-object "text"

# usefull
echo "text" | git hash-object --stdin
```  

<br />  

> Every object in Git has its own SHA-1. So, what if they collide?  

<br />

```shel
git cat-file -p hash
```

![git objects](./assets/001.png)  

<br />

## Branches demystified
Git put branches in a directory called `.git/refs/heads`. A Branch is just a reference to a commit.  

<br />

> HEAD is just a reference to a branch, a pointer to a pointer.  

<br />

You can move to another branch with command:
```shell
git switch branchName
git checkout branchName
```
<hr />

### Losing your HEAD, directly checkout a commit.  

To checkout a commit is necessary to use `checkout` command.

```shell
git checkout 7789899987

cat .git/HEAD
# this point to a commit, not to a branch
```  

<br />

If you run `git branch` you can see that HEAD does not point to a branch. You see this message:
```
* (HEAD detached at 7789899987)
```   

<br />

This is a situation called `detached HEAD`

![detached HEAD](./assets/002.png)  

<br />

If we switch back to main branch with `git switch main` 
![return to main](./assets/003.png)  

If git objects can't be reached by any reference, Git run a garbage collector, look for objects in the database that cannot be reached from a branch,or HEAD, or TAG, and it will remove them to save disk space

If you want to save this commits you most act now:
- move back to the last commit
- create a branch

![move back](./assets/004.png)  

<br />   

![create branch](./assets/005.png) 

<hr />

## Rebasing made Simple  

Let's start with the repository in this state.  

![start with two branches](./assets/006.png)  

Now let's rebase `spaghetti` branch on `main` branch
```shell
git rebase main
```  

- Git looks for the first commit in `spaghetti` branch that is also a commit in `main`.  

![first commit shared](./assets/007.png)  

- Git detaches the entire  `spaghetti` branch from this commit and moves it on top of main. Its changes the base of this branche.  

![detache and rebase](./assets/008.png)  

- To sync `main` with `spaghetti` we need to switch to main and execute `git rebase spaghetti`.  

![rebase main against spaghetti ](./assets/009.png)

> When in doubt, just merge.

## Tag
Tags is one of the features that turn Git into a revision Control System.
A `Tag` is like a label for a commit.
```shell
git tag release_1
```
We can create a simple tag with just a name, like a simple label, or an annotated tag with additional metadata.
```shell
git tag release_1 -a "Some message"
```
> Switch don't work with tags, use checkout.

## Recap
Branches, merges, rebases and tags are the main features to turn Git from a `stupid content tracker` into a full Version Control System.  

<br />

## Distributed Version Control
After run `git clone` Git add a few lines to the configuration of your repository.  

```shell
vim .git/config
```  

<br />  

![config after git clone](./assets/010.png)  

<br />

You can list all branches with `git branch --all` to show all references.  

<br />

> Like a local branch , a remote branch is just a reference to a commit.  

<br />

We can use `git show-ref BranchName` to see which commits they're point at.  

<br />

> You ***fetch*** and ***merge***, then push.  

<br />

> You simplify with ***pull***, then push.  

<br />

> ***NEVER REBASE SHARED COMMITS.***  

<br />

## The open source Workflow.  

- Chose a project from another user in `github`.
- `Fork` this to your `github` account.
- Clone the project, from your `github` account, to your local machine.  <br/>

![fork and clone](./assets/011.png)  <br />

- At the point of view of git there is not connection between our project and the original project that we forked from Github.
- We want to track changes from the original project.
- We need to add another remote to point to original project.
- By convention this remote is called `upstream`.  <br/>

![two remotes](./assets/012.png) . <br />

- Now we can synchronize all our local changes with the origin.
- We can commit our local changes and just push those changes to origin.
- If there are changes on upstream we can pull them into our local project, solve conflicts, and them push them to origin.  <br />

![update fro upstream](./assets/013.png)  <br />

- To push changes to upstream we send a `PR (Pull Request)` to upstream maintainer.  <br />

![pull request](./assets/014.png)