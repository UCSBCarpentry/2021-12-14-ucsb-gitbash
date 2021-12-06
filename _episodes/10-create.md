---
title: Creating a Repository
teaching: 10
exercises: 0
questions:
- "Where does Git store information?"
objectives:
- "Create a local Git repository."
- "Describe the purpose of the `.git` directory."
keypoints:
- "`git init` initializes a repository."
- "Git stores all of its repository data in the `.git` directory."
---

Once Git is configured,
we can start using it.

The usage we will demonstrate is making a repository of <a href="https://ucsbcarpentry.github.io/2021-12-14-ucsb-gitbash-online/06-script/"><strong>shell scripts</strong></a>.

First, let's create a directory in `Desktop` folder for our work and then move into that directory:

~~~
$ cd ~/Desktop
$ mkdir shell-scripts
$ cd shell-scripts
~~~
{: .language-bash}

Then we tell Git to make `shell-scripts` a [repository]({{ page.root }}{% link reference.md %}#repository)
-- a place where Git can store versions of our files:


~~~
$ git init
~~~
{: .language-bash}

It is important to note that `git init` will create a repository that
includes subdirectories and their files---there is no need to create
separate repositories nested within the `shell-scripts` repository, whether
subdirectories are present from the beginning or added later. Also, note
that the creation of the `shell-scripts` directory and its initialization as a
repository are completely separate processes.

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

~~~
$ ls
~~~
{: .language-bash}

But if we add the `-a` flag to show everything,
we can see that Git has created a hidden directory within `shell-scripts` called `.git`:

~~~
$ ls -a
~~~
{: .language-bash}

~~~
.	..	.git
~~~
{: .output}

Git uses this special subdirectory to store all the information about the project,
including all files and sub-directories located within the project's directory.
If we ever delete the `.git` subdirectory,
we will lose the project's history.

Next, we will change the default branch to be called `main`.
This might be the default branch depending on your settings and version
of git.
See the [setup episode](02-setup.md) for more information on this change.

~~~
git checkout -b main
~~~
{: .language-bash}
~~~
Switched to a new branch 'main'
~~~
{: .output}


We can check that everything is set up correctly
by asking Git to tell us the status of our project:

~~~
$ git status
~~~
{: .language-bash}
~~~
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
~~~
{: .output}

If you are using a different version of `git`, the exact
wording of the output might be slightly different.

> ## Places to Create Git Repositories
>
> To track different types of scripts,
> we will first create a `user-input` project inside of `shell-scripts`
> project with the following sequence of commands:
>
> ~~~
> $ cd ~/Desktop        # return to Desktop directory
> $ cd shell-scripts    # go into shell-scripts directory, which is already a Git repository
> $ ls -a               # ensure the .git subdirectory is still present in the shell-scripts directory
> $ mkdir user-input    # make a subdirectory shell-scripts/user-input
> $ cd user-input       # go into user-input subdirectory
> $ git init       # make the user-input subdirectory a Git repository
> $ ls -a          # ensure the .git subdirectory is present indicating we have created a new Git repository
> ~~~
> {: .language-bash}
>
> Is the `git init` command, run inside the `user-input` subdirectory, required for
> tracking files stored in the `user-input` subdirectory?
>
> > ## Solution
> >
> > No. we do not need to make the `user-input` subdirectory a Git repository
> > because the `shell-scripts` repository will track all files, sub-directories, and
> > subdirectory files under the `shell-scripts` directory.  Thus, in order to track
> > all information about user-input, we only needed to add the `user-input` subdirectory
> > to the `shell-scripts` directory.
> >
> > Additionally, Git repositories can interfere with each other if they are "nested":
> > the outer repository will try to version-control
> > the inner repository. Therefore, it's best to create each new Git
> > repository in a separate directory. To be sure that there is no conflicting
> > repository in the directory, check the output of `git status`. If it looks
> > like the following, you are good to go to create a new repository as shown
> > above:
> >
> > ~~~
> > $ git status
> > ~~~
> > {: .language-bash}
> > ~~~
> > fatal: Not a git repository (or any of the parent directories): .git
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}
> ## Correcting `git init` Mistakes
> Now we know how a nested repository is redundant and may cause confusion down the road.
> Say we would like to remove the nested repository. How can we undo
> our last `git init` in the `user-input` subdirectory?
>
> > ## Solution -- USE WITH CAUTION!
> >
> > ### Background
> > Removing files from a Git repository needs to be done with caution. But we have not learned
> > yet how to tell Git to track a particular file; we will learn this in the next episode. Files
> > that are not tracked by Git can easily be removed like any other "ordinary" files with
> > ~~~
> > $ rm filename
> > ~~~
> > {: .language-bash}
> >
> > Similarly a directory can be removed using `rm -r dirname` or `rm -rf dirname`.
> > If the files or folder being removed in this fashion are tracked by Git, then their removal
> > becomes another change that we will need to track, as we will see in the next episode.
> >
> > ### Solution
> > Git keeps all of its files in the `.git` directory.
> > To recover from this little mistake, we can just remove the `.git`
> > folder in the user-input subdirectory by running the following command from inside the `shell-scripts` directory:
> >
> > ~~~
> > $ rm -rf user-input/.git
> > ~~~
> > {: .language-bash}
> >
> > But be careful! Running this command in the wrong directory will remove
> > the entire Git history of a project you might want to keep.
> > Therefore, always check your current directory using the command `pwd`.
> {: .solution}
{: .challenge}
