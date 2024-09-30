# Getting Started with a New Code Base

## Acquiring the Source Code

The first step is to obtain your own version of the source code you want to work with.
Unless you are added to the open source repository as a contributor, you won't be able
to make commits (changes) to the code base itself.  And most code base owners won't
want to add random GitHub users they don't know to their code bases, as this gives
them lots of freedom to make changes to the code.

Instead, for open source development, you should create your own *fork* of the original
code base.  This is a GitHub repository that contains a copy of the original code base but
which only you have commit access to.

You can do this using the Fork button, from the main web page for the project's shared repository:

<img width="1706" alt="image" src="https://github.com/user-attachments/assets/6e59c41f-485f-4ff6-82a9-ddd2f6406b4c">

Now you have your own copy of the code base on GitHub.  To make real substantial changes to the code
base, you should next make a clone of your fork - that is, a copy of your fork of the main
repository (commits and all) on your own machine, where you can easily edit files, run code
quality checks, and build and run the code.  In other words, the clone should be made in
the development environment you set up on your machine earlier.

To make the clone, first check that you have a recent version of Git installed on your machine
(in your development environment).  You can do this at the terminal/shell by issuing the
command:

    git --version

The latest Git version at the time of writing was 2.45.  Anything within range of this version should be
fine (unless another version is explicitly stated as being required in the code base documentation).
You can get information on installing Git on a range of platforms at: 

https://git-scm.com/downloads

Once you have Git installed, you can go ahead and clone the repository.  Cloning can be done through
the Git inteface of all good IDEs, but we'll focus here on using the command line.

To clone a GitHub repository, you need the URI of your GitHub fork.  You can find this by clicking
the green Code button on the main web page for your fork:

<img width="1715" alt="image" src="https://github.com/user-attachments/assets/fc23cbb7-c716-4fc9-aa9a-580c60d44df1">

Copy the URI that matches how you want to authenticate with GitHub from the command line
in your development environment.  For club members, we recommend
[setting up a SSH key for GitHub
access](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account),
and using the SSH version of the URI to interact with your GitHub fork.  (Code base owners may prefer to
use [the GitHub CLI](https://cli.github.com), as it has useful features for working with pull requests.)

Now you can clone your fork into your development environment.  Decide where in your file system you want your
working copy of the code base to live.  (A common convention is to have a directory called ```git``` under your
home directory, and to keep Git repositories that don't have another more natural home there.)

    cd ~/git
    git clone git@github.com:robota-suite/robota-core.git

Notice that you don't need to create a parent directory for the repository - Git will do
that for you as part of the cloning process.

Now you can move into the folder containing your clone.  This will be the location where you
work with the code base, making changes, testing the code, building and running it.

    cd robota-core


## Setting up your Development Environment

The next step in preparing to work with a new code base is to set up your working directory
with the required *development environment*.

By this, we mean that your working space has all the software and libraries installed that
are needed to work with the code of the system, to build it and to run it.

There are other types of environment needed for different aspects of software engineering.  For
example, you might come across these common ones:

* the *production environment: that is, the technical environment where the software will be
  run for live operation by the intended users of the system.  It will need the software and
  libraries to be installed to allow the built code to be run, but it does not need to have
  tools for testing and building to code to be installed (for example).
* the *test environment*: that is, the technical environment where the software will be run
  in order to be tested.  It will need the software and libraries installed that are required
  to execute the built code, like the production environment, but it may need special test
  versions of some resources to be set up.  For example, a database application will need a
  clean test database to be set up in the test environment while in the production environment
  it needs to be able to connect to the live database.

The documentation provided by the open source code base you are working with should (ideally)
list all the installation tasks you need to perform, including required minimum or maximum
versions, to set up your machine for development.  The information might be given in the main
```README.md``` file or in a ```CONTRIBUTING.md``` file, or perhaps under a ```docs\``` folder.

> [!TIP]
> Watch out for missing requirements.  It is common for owners of research code bases that have
> only recently been open sourced to write documentation for their own immediate team, rather
> than for more general use.  Club members can help by submitting PRs that fill in the gaps in
> the developer documentation for a wider range of platforms and OSs than the code base owner
> has access to.  Think about dependencies that might seem so obvious that the code base owner
> might not think to describe them - like needing to install Python3 or the Java SDK.

Several modern languages allow the use of *virtual environments*.  This allows you to install
the dependencies for one project on your machine, alongside the (possibly conflicting)
requirements for any other projects you are working on.  Where possible, you should always
make use of virtual environments.  You may not think you will work on many other projects
on the machine you are using, but it will be very annoying if you need to add other
projects to your machine, and have to keep changing the installed software versions
depending on which project you are currently working on.

> [!TIP]
> If the documentation of your code base doesn't provide instructions to use a virtual
> environment, but they are supported by the languages in use, you can propose
> adjustments to the development environment documentation so that the set up
> does happen in a virtual environment.  Virtual environments may not be needed
> for small team projects, where the main developers are working only on that
> project.  But they are very helpful when a code base is worked on by a larger
> community, such as the one we hope to build through our club.  Part of our
> role as club members is to help our code base owners transition from internal
> development projects to full open source projects.  Changes that make the
> code base easier for open source developers to access will usually be
> welcomed by code base owners.


## Best Practice: Automating Dev Env Setup

Having good documentation about the development environment is great, but even better is when
the process of setting up the environment is automated in some way.  For example, instead of
writing documentation telling you what commands to run to set up the required libraries and
tools, it's better to provide an executable script (like a shell script) that checks that the
required dependencies are in place and issues the commands to install or upgrade any that are
not.

Even better still is when the code base uses a dependency manager tool and includes the
configuration files needed to make the dependency manager do the right things.  Examples
of such tools are Maven and Ivy for Java, pipenv and poetry for Python.

> [!TIP]
> Club members can help the code base owner by automating some common development tasks
> that currently need to be done manually, following instructions in the documentation.
> Check with the code base owner regarding their preferred route to automation, to avoid
> wasting time on a tool the code base owner doesn't like or doesn't know enough about to
> prefer it to their current set up.
