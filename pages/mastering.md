# Mastering Git
<br />

> <br /> Learning the "Git way of thinking"  
<br/>

## The Four Areas: Introduction
1. The project directory in file system or Woring Area.
2. Repository, contains the history of the project.
3. Index, place where we put your files before a commit.
4. Stash, a temporary storage area.  <br />

![four areas](../assets/mast-001.png)  <br />

![two questions](../assets/mast-002.png) <br />

## Repository
The `Repository` lives in `.git` folder in object database. In `Object database` there are few different kinds of objects.
- **Blobs:** Objects that represents the content of a file at some point in the project history.
- **Trees:** Objects that represents folders in the project.
- **Commits:** Objects created when we run git commit. <br />

All of these objects are immutable. These objects are linked together in a structure that represents your project's history.  <br />

![database objects linked](../assets/mast-003.png)   <br/>

## Index
- **Clean status:** When the `Working Area` and `Repository` are aligned.
- Thinking in `Index` as just another area that holds everything, just like the working area and the repository. When you execute `git status` and see the message `nothing to commit, working tree clean` it means that the `Index` contains the same blobs and trees as the `Repository`.
- Update: the clean status is where the three areas are all aligned.  <br />

![clean status](../assets/mast-004.png)  <br />

We can check this with `git diff`, but this will compare the **Working Area** with the **Index Area**, that contain exact same data in clean status. To see difference between **Index Area** with **Repository** we use the command `git diff --cached` .In this case we compare the stuff I want to commit with the stuff I already commited.