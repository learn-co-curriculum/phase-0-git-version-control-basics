# Git Basics

## Learning Goals

- Identify how to initialize a Git repository with `git init`
- Check the status of a repository with `git status`
- Keep track of file changes with `git add`
- Create a commit and apply a commit message with `git commit`

## Introduction

In our overview of version control systems, we saw that using a VCS helps us
organize our work and keep track of changes we make. We also determined that the
VCS we're going to use is Git. Now we can begin learning the commands we need to
make Git work for us.

## Identify How to Initialize a Git Repository with `git init`

Git operates on a directory level. When we have a new directory that we want to
track our files in, we need to _intialize_ the directory as a Git repository.
That means Git will then pay attention to what goes on in the directory and give
us all the Git superpowers.

To get started, we'll create a new directory. Go to the terminal (accessed
through the 'Sandbox' or Learn IDE) and type the following:

**REMEMBER** Don't type the `$`. That's the universal symbol for a command prompt.
It's how technical documentation says "Here's a thing for the shell to interpret."

```
~ $ mkdir my-git-project
```

This command creates new directory. Then:

```
~ $ cd my-git-project
```

This command moves into the newly created directory.

Now that we're in the directory where we want Git to watch for changes (adding,
removing, and editing files), let's set up this directory by _initializing_ it.
In the terminal type `git init`. It should look like this:

```
my-git-project $ git init
Initialized empty Git repository in /Users/avi/my-git-project/.git/
```

After entering `git init`, the output in our terminal reads `Initialized empty Git repository in /our/path/here/my-git-project/.git/`. Git is letting us know
that it created a new repository within the hidden `.git` folder in `my-git- project`. This hidden directory, `.git`, is what Git uses to keep track of our
log of changes. So, don't go in there and start randomly deleting things!

> Be careful about making an entire directory, like our home directory or our
> desktop, into a Git repository accidentally. Make sure you only type `git init`
> within the directory you want `git` to track.

## Check the Status of a Repository with `git status`

Now we have Git watching this directory, let's see what it can tell us about the
directory. The command we use for this is `git status`.

```
my-git-project $ git status
```

Since we have not added any files yet, we'll see:

```
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

Let's create a `README.md` that describes the project. Make our new file by
typing `touch README.md` from within the `my-git-project` directory. We won't
see any output after `touch`, but we will see a new file has been created if we
type `ls`, which gives a list of all the files in the directory.

```
my-git-project $ touch README.md
my-git-project $ ls
README.md
```

With at least one new project file we can enable Git to start tracking changes.
Type `git status`. Git will show us what our current repository looks like and
what changes it sees.

```
my-git-project $ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

  README.md

nothing added to commit but untracked files present (use `git add` to track)
```

As expected, Git confirms that it's not watching or tracking anything in this
directory. Let's change that!

Whenever we want to check the status of our Git repository—which we do quite
often—type `git status`.

## Keep Track of File Changes with `git add`

Currently, the file in our repository is not being tracked by Git just yet. We
have to tell Git about all the files we want it to keep track of and consider as
part of our project. We can do this by adding the files to our `git` repository
with `git add <filename or path>`. To add our new `README.md` to the repository
and check the status, we type:

```
my-git-project $ git add README.md
my-git-project $ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

  new file:   README.md
```

We can now see that Git is ready to keep track of `README.md` and recognizes
that the file is new to this repository. However, while we've told Git that
there is a new file, we still haven't told Git that this new file is considered
a change to our repository. We create changes in our repository by making
_commits_.

**Tip: The standard way to capture all changes in a directory is to type
`git add .`, where the `.` refers to the entire current directory.**

## Create a Commit and Apply a Commit Message with `git commit`

Git knows that the state of `README.md` is "to be recorded as part of this
commit" because our last use of `git status` listed `README.md` under `Changes to be committed:`. That's why a _commit_ is composed of two steps: adding the
files in the snapshot (_commit_) and then doing the commit with your message.

To make our first commit, type: `git commit -m "Initial commit"`. This tells
`git` that our commit message, represented by the `-m` flag, is `"Initial commit"`.

```
my-git-project $ git commit -m "Initial commit"
[master (root-commit) e55477d] Initial commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
```

We can see that Git has created a new version of our code, represented by the
_SHA_ `e55477d` (SHAs are the identification system that `git` uses to keep track
of versions). The commit changed 1 file. Now, if we type `git status` ask to
see the status of our project, with no other changes to any files, we'll see
that it is at a "clean state", and there is nothing to commit and no new changes.

```
my-git-project $ git status
On branch master
nothing to commit, working directory clean
```

If we make another change, for example, to README.md, we can add another commit
with this new set of changes with `git commit -am`:

```
my-git-project $ git commit -am "Updates README.md"
[master (root-commit) e55477d] Updates README.md
 1 file changed, 4 insertions(+), 0 deletions(2)
```

**A faster way to capture all outstanding changes for files that are _already
being tracked_ in a commit is to use `git commit -am "Our commit message"`,
where the `a` refers to adding 'all changes' and `m` assigns a commit message
of `"Our commit message"`.**

Commits are amazingly powerful in Git. With a commit you can move your project
back to a past commit and throw away bad ideas. You can tell Git to create a new
"parallel universe" based off of a past commit and you can start working in that
universe and decide later to keep that work or throw it away. We'll cover these
more advanced features later.

## Conclusion

To make a new Git repository out of a directory—which we'll only have to do once
per project—use `git init`. Whenever you make a change to a file or create a
new file, you can check the status of these changes with `git status`. When
you're ready to keep track of changes, you can add them individually with the
`git add <filename or path>` command, or collectively with the `git add .`
command. Once your changes have been added, use `git commit -m` to commit them
with a explanatory message.

If we've followed all these steps, our `my-git-project` directory is now a `git`
repository. We can retain the directory as a sandbox for Git experimentation, or
delete or ignore it.

## Resources

- [Git Basics at git-scm.com](https://git-scm.com/book/en/v1/Git-Basics)
