# Git Basics

## Learning Goals

- Initialize a Git repository with `git init`
- Check the status of a repository with `git status`
- Track file changes with `git add`
- Create a commit and apply a commit message with `git commit`

## Introduction

In the previous lesson we learned what a VCS is and how it helps us in our work.
In this lesson, we'll learn how to use Git to track the changes we make to a
project.

The basic process consists of the following three steps:

1. Initialize the project directory as a Git repository,
2. Tell Git to track the changes we make to individual files, and
3. When we're ready, tell Git to save the changes.

That's it! This basic workflow gives you all the main benefits of using Git to
track a project.

## Initialize a Git Repository with `git init`

Git operates on a directory level. When we have a new directory that we want to
track our files in, we need to _initialize_ the directory as a Git repository.

To get started, we'll create a new directory. In your terminal, type the
following:

> **REMEMBER**: Don't type the `$`. That's the universal symbol for a command
> prompt. It's how technical documentation says "Here's a thing for the shell to
> process."

```console
$ mkdir my-git-project
```

This command creates new a directory. Then:

```console
$ cd my-git-project
```

This command moves into the newly created directory.

Now that we're **in the directory** where we want Git to watch for changes
(adding, removing, and editing files), we next need to _initialize_ this
directory as a Git repo. We only need to do this step once for each project we
want to track.

In the terminal type `git init`. It should look something like this:

```console
$ git init
Initialized empty Git repository in /Users/avi/my-git-project/.git/
```

The message above lets us know that our new directory is now being tracked by
Git. It also shows that a new subfolder `.git` has been created. This hidden
directory is where Git keeps important stuff, like the commit history. Don't go
in there and start randomly deleting things! That said, if ever you do `git
init` in the wrong directory, you can `rm -rf .git` to delete the `.git` folder
and all its contents and return the directory to a plain-old, unprotected
directory.

Be careful about making a containing directory, like our home directory or our
desktop, into a Git repository accidentally. Make sure you only type `git init`
_within_ the directory you want `git` to track.

## Check the Status of a Repository with `git status`

Now that we have Git watching this directory, let's see what it can tell us
about the directory. The command we use for this is `git status`.

```console
$ git status
```

Since we have not added any files yet, we'll see:

```console
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

> **Note:** Older repositories may state `On branch master`. Branching is beyond
> the scope of this lesson, but to briefly explain - `main` and `master` both
> refer to the same thing - the core (_**main**, get it?_) branch of a
> repository. A single repository can have many branches, but always has only
> _one_ core branch. In the past, this branch defaulted to the name `master`.
> Going forward, the branch will be named `main`. You'll likely see both as you
> work with repositories new and old.

Let's create a `README.md` that describes the project. Make our new file by
typing `touch README.md` from within the `my-git-project` directory. We won't
see any output after we run the `touch` command so to see that our new file has
been created, we'll also run the `ls` command.

```console
$ touch README.md
$ ls
README.md
```

With at least one new project file we can enable Git to start tracking changes.
Type `git status`. Git will show us what our current repository looks like and
what changes it sees.

```console
$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

  README.md

nothing added to commit but untracked files present (use `git add` to track)
```

Git confirms that it's aware of the file `README.md`, but it's not **tracking**
it. Git's not doing anything with the file and the file is not doing anything
with Git..._yet_. Let's change that!

> **IMPORTANT**: Whenever you want to check the status of your Git repository —
> which you will often — type `git status`.

## Keep Track of File Changes with `git add`

Currently, the file in our repository is not being tracked by Git. We have to
tell Git about all the files we want it to keep track of and consider as part of
our project. We can do this by _adding_ the files to our `git` repository with
`git add <filename or path>`. To add our new `README.md` to the repository and
check the status, we type:

```console
$ git add README.md
$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

  new file:   README.md
```

We can now see that Git is ready to keep track of `README.md`. All the changes
in the file at the time we `added` it are **staged**. If we were to change
`README.md`, we'd need to re-add the file. As it happens here, this staged
change is "create the file, nothing inside of it" because `touch` created an
empty file.

To have Git save a new version of our repo that includes this new file (or,
later, to "capture" changes to a file) we need to _commit_ the set of changes or
**diff**. We "save" the changes in our repository by making **commits**.

## Create a Commit and Apply a Commit Message with `git commit`

Remember: `git add` got our changes to the repository ready in the previous
step. Those changes are the ones that will be "captured" in the commit.

To make our first commit, type:

```console
$ git commit -m "Initial commit"
```

The `-m` flag tells Git that we are including a commit message, in this case
`"Initial commit"`. _Any time you make a commit, you should include a message
using this flag._

```console
$ git commit -m "Initial commit"
[main (root-commit) e55477d] Initial commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
```

We can see that Git has created a new version of our repo, represented by the
_SHA_ (Secure Hash Algorithm) `e55477d`. SHAs are the identification system that
`git` uses to keep track of versions; they're long complex numbers and letters
that are unlikely to be duplicated (the value shown above is actually a
shortened version of the full SHA). If you're following along, the SHA you'll
see in your terminal will be different.

The `commit` command committed 1 file.

Now, if we type `git status`, we'll see that it is at a "clean state": there are
no new changes which means there's nothing to commit.

```console
$ git status
On branch main
nothing to commit, working tree clean
```

We won't do this just yet, but if we were to open the README.md file in our text
editor and add some text to it, we could then add our file and commit this new
set of changes with the following:

```console
$ git add README.md
$ git commit -m "Updates README.md"
```

There are also a couple of shortcuts we can use:

```console
$ git add .
```

This command adds _all_ the files that have been changed since the last commit
(in this case, just `README.md`).

Or we can combine the two steps of adding and committing our file into a single
command:

```console
$ git commit -am "Updates README.md"
```

Here we're combining the `a` and `m` flags. As with the `add .` shortcut, the
`a` flag tells git to add 'all changes', i.e., all files that have been changed
since the last commit. The `-m` flag, like before, tells git that we want to
specify a commit message, in this case, `"Updates README.md"`. This command
could also be written as:

```console
$ git commit -a -m "Updates README.md"
```

Remember, we haven't actually made any changes to `README.md` so there's nothing
to add or commit. However, if we had, the commit would look something like this:

```console
$ git commit -am "Updates README.md"
[main (root-commit) e55477d] Updates README.md
 1 file changed, 4 insertions(+), 0 deletions(2)
```

Good work! Commits are amazingly powerful in Git. They are the heart of many of
Git's advanced features. Understanding the basic workflow of Git initialization
and setup is the foundation for success.

## Conclusion

In this lesson, we've learned the basics of using Git to track a directory.
Specifically, we learned how to:

- make a new Git repository out of a directory using `git init`
- check the status of our repo using `git status`
- track files that have been changed using the `git add <filename or path>` command
- save (commit) the changes with an explanatory message using `git commit -m "A
  message"`

So far, however, we've only been using Git with our local repo. In the next two
lessons, we'll learn how we can use Git in combination with GitHub to _share_
code with other developers.

## Resources

- [Git Basics at git-scm.com](https://git-scm.com/book/en/v1/Git-Basics)
