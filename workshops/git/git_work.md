# GIT_WORKSHOP
## Acknowledgements

This workshop was heavily inspired by the work of the following creators and platforms:

- [ThePrimeagen](https://www.youtube.com/@ThePrimeTimeagen) — to explore some tech related subject.
- [Boot.dev](https://www.boot.dev) — for excellent backend curricula and clear explanations.
- [boot.dev.youtube](https://www.youtube.com/@bootdotdev) Animated teachings about backend
development in Golang, SQL, Python, JavaScript and TypeScript.

Many concepts, structure, and exercises were adapted with appreciation.
### Table of Contents

- [1. Introduction to Git and Version Control](#1-introduction-to-git-and-version-control)
- [2. Porcelain and Plumbing](#2-porcelain-and-plumbing)
- [3. Quick Config (we discuss configuration more in chapter 5)](#3-quick-config-we-discuss-configuration-more-in-chapter-5)
- [3. Repository](#3-repository)
- [3. How git works internally](#3-how-git-works-internally)
- [4. Config](#4-config)
- [5. Branching](#5-branching)
### 1. Introduction to Git and Version Control
Git is a powerful Version Control System (VCS) that allows developers to track code changes over
time, identify who made them, and manipulate or revert history. It is the de facto standard for all
developers, with 93% of developers reportedly using it. Git was created by Linus Torvalds in 2005,
within just five days, following license disputes over the previous VCS, Bitkeeper.

Git is a distributed Version Control System, meaning there isn't a single central authoritative
repository. Each repository is its own, and synchronisation happens between them. Platforms like
GitHub are simply hosting services for Git repositories, not Git itself.
### 2. Porcelain and Plumbing
In Git, commands are divided into high-level ("porcelain") commands and low-level ("plumbing")
commands. The porcelain commands are the ones that you will use most often as a developer to
interact with your code. Some porcelain commands are:

```bash
git status
git add
git commit
git push
git pull
git log
```
Don't worry about what they do yet, we'll cover them in detail soon. Some examples of plumbing
commands are:
```bash
git apply
git commit-tree
git hash-object
```
### 3. Quick Config (we discuss configuration more in chapter 5)
We need to configure Git to contain your information. Whenever code changes, Git tracks who
made the change. To ensure you get proper credit (or more likely, blame) for all the code you
write, you need to set your name and email.

Git comes with a configuration both at the global and the repo (project) level. Most of the
time, you'll just use the global config.

**Assignment**
Let's set your identity. Check if your user.name and user.email are already set:
```bash
git config --get user.name
git config --get user.email
```

If they aren't, set them. I recommend using your GitHub username and email.

```bash
git config --add --global user.name "github_username_here"
git config --add --global user.email "email@example.com"
```

Finally, let's set a default branch (we'll talk more about configs and branches later) so that
we're all on the same page. Run:

```bash
git config --add --global init.defaultBranch master/main
```

We're using master for now because it is Git's default, but later we'll change it to main,
which is GitHub's default. Just bear with us for a second.

### 3. Repository
- **Initialization**
A Git repository represents a single project. It is essentially a directory that contains a
project's files and a hidden .git directory. The .git directory holds the entire state of your
Git project, including all history, branches, and configuration.

Anatomy of the .git/ folder:

1. **objects/**: The core database storing all commits, files (blobs), and directories (trees)

2. **refs/**: Stores pointers (references) like branches and tags

3. **HEAD**: A file that points to the current branch or commit

4. **config**: Local configuration file for this repository

5. **index**: The Staging Area (a single binary file)

6. **hooks/**: Directory for client-side scripts triggered at Git events

7. **info/**: Contains repository-specific information like exclude files

**Assignment**

Create a new directory:``mkdir bookiStore``

Initialize a repo: ``git init``

List the contents: ``ls -a``
- **Status**
A file can be in one of [several states](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#_the_very_basics) in a Git repository. Here are a few important ones:

1. **untracked**: Not being tracked by Git
2. **staged**: Marked for inclusion in the next commit
3. **committed**: Saved to the repository's history

The git status command shows you the current state of your repo. It will tell you which files
are untracked, staged, and committed.

**Assignment**
let's make catalog for our book store.

Create a file in the root of your bookiStore directory called books-list.md and add the following
text to the file:
```md
# code-charles-petzold
```
The .md extension means it's a markdown file, which is popular for writing docs.
Save the file, then run:
```bash
git status
```
- **Staging**
The books-list.md file has been created, but as we saw, it's untracked. We need to stage it
(add it to the "index") with the git add command before committing it later.

Without staging, no files are included in the commit—only the files you explicitly [git
add](https://git-scm.com/docs/git-add) will be committed.

Here's the command:
```bash
git add <path-to-file | pattern>
```
**For example:**
git add localizationEn.txt
- **Commit**
After staging a file, we can [commit](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/about-commits) it.

A commit is a snapshot of the repository at a given point in time. It's a way to save the state of
the repository, and it's how Git keeps track of changes to the project. A commit comes with a
message that describes the changes made in the commit.

Here's how to commit all of your staged files:

```bash
git commit -m "your message here"
```

**Assignment**
Commit the books-list.md file with the message A: add books-list.md. You wouldn't normally start a
commit message with A:(A=feat(book)), you'd just write the message, but we're going to use letters
to help us easily identify commits.

Run git status again, and you should see that the file is no longer staged.
run:
```bash
git --no-pager log -n 1
```

***Quiz***

Which command adds a file to the staging area? (a.k.a the index)
- [] status
- [x] commit
- [] add
- [] pull

---

- **Log**

A Git repo is a (potentially very long) list of commits, where each commit represents the full
state of the repository at a given point in time.

The git log command shows a history of the commits in a repository. This is what makes Git a
version control system. You can see:

    - Who made a commit
    - When the commit was made
    - What was changed

***A Commit Hash***
Each commit has a unique identifier called a "commit hash". This is a long string of characters
that uniquely identifies the commit. Here's an example of mine:

9ddc0b7c42226dfa645291d2f4f653a07a42322f

For convenience, you can refer to any commit or change within Git by using the first 7 characters
of its hash. For mine, that's 9ddc0b7.

**Assignment**

Run the git log command. You should see your commit. Notice that git log (assuming the log is long
enough) starts an interactive pager. You can scroll through the log with the arrow keys, and exit
by pressing q.

Next, run git log again, but this time use the -n and --no-pager options to limit the maximum
number of commits shown, and more importantly, to run it without the interactive pager:

```bash
git --no-pager log -n 10
```
### 3. How git works internally
- **Different Hashes**
My latest Git commit hash was:

9ddc0b7c42226dfa645291d2f4f653a07a42322f

You may have noticed that even though we both have the same content in our
repositories, we have different commit hashes. While commit hashes are derived from their content
changes, there's also some [other stuff](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects#_git_commit_objects) that affects
the end hash. For example:

    - The commit message
    - The author's name and email
    - The date and time
    - Parent (previous) commit hashes
    -All this to say that hashes are (almost) always unique, and because they're generated
    automatically for you, you don't need to worry too much about what goes into them right now.

***Note: Hash = SHA***

Git uses a cryptographic hash function called [SHA-1](https://en.wikipedia.org/wiki/SHA-1) to generate commit hashes. We won't go into
the details of how SHA-1 works, but it's important to know because you might also
hear commit hashes referred to as "SHAs".

cat/xdd

- **Cat file**

Luckily, Git has a built-in plumbing command, cat-file, that allows us to see the contents of a
commit without needing to futz around with the object files directly.
```bash
git cat-file -p <hash>
```
**Assignment**
Use the cat-file command to view the contents of your last commit. (Use -p for pretty-print.)

- **Tree and blobs**

Now that we understand some of our plumbing equipment, let's get into the pipes. Here are some
terms to know:

    - tree: git's way of storing a directory
    - blob: git's way of storing a file

Here's what I got when I inspected my last commit:

```bash
git cat-file -p 9ddc0b7c42226dfa645291d2f4f653a07a42322f
```

tree 6d9bc3ca3ffbcd1d11c8be0101c264de066d3f67 

parent 1ab9c6a527bbd2b847c30eebafabe2bf424feef5

author subomega1 <sfar@gmail.com> 1755953352 +0100

committer subomega1 <sfar@gmail.com> 1755953352 +0100

A: add books-list.md

Notice that we can see:

The tree object

The author
The committer
The commit message
However, we cannot see the contents of the books-list.md file itself! That's because the blob
object stores it.
**Assignment**
Create a second file called titles.md and add the following text:
```md
# Comics

- Spiderman
- The punisher
- batman
- superman
- flash

```

Save, stage, and commit the file with any commit message you like as long as it starts with B:.
For example, B: add Comics. Use (git cat-file) to inspect the commit you just made. You should
notice one extra field in the commit object that wasn't present in the first commit.

- **Storing Data**

Git stores an entire snapshot of files on a per-commit level. This was a surprise to me! I always
assumed each commit only stored the changes made in that commit.

- **Optimization**
While it's true that Git stores entire snapshots, it does have some performance optimizations so
that your .git directory doesn't get too unbearably large.

Git [compresses](https://git-scm.com/book/en/v2/Git-Internals-Packfiles) and packs files to store them more efficiently.
Git deduplicates files that are the same across different commits. If a file doesn't change
between commits, Git will only store it once.

***Assignment***

1. [x] Use git cat-file -p to view the hash of the blob for the comics.md file in your last commit. Save
that hash somewhere in your notes.

2. Add a new directory to your project called quotes. Inside, add two files:

    1. history.md:

        - "Nikola Tesla, The inventor and visionary who pioneered alternating current (AC) electricity,
        wireless transmission, and futuristic technologies."
        - "Euclid, The “Father of Geometry” who systematized mathematical knowledge in Elements."
        - "Al-Idrisi was geographer and cartographer who created one of the most detailed medieval world
        maps."
        - "Al-Biruni was a pioneering scholar whose works in astronomy, mathematics, and geography laid
        the foundations for modern science."
        - "Al-Khwarizmi, the father of algebra, revolutionized mathematics with his systematic methods of
        calculation."

    2. computer.md:

        - A computer is an electronic machine that processes data into meaningful information.
        - The computer is often called the “universal machine” because it can simulate any other machine through programming.
        - A computer operates using the fundamental cycle of input, processing, storage, and output.
        - Modern computers are powerful tools that combine hardware and software to solve complex problems efficiently.

4. Stage and commit both files in a single commit with a message starting with C:
    For example, C: add history.md and computer.md.
5. Use the command cat-file to view the hash of the blob for the comics.md file again in the latest
   commit. You should notice that it still has the same hash because the file hasn't changed.
### 4. Config
- **Git Config**
Git stores author information so that when you're making a commit it can track who made the
change. Here's how you might update your global [Git configuration](https://git-scm.com/docs/git-config) (don't do this yet):
```bash
git config --add --global user.name "omega"
git config --add --global user.email "omagatrix@example.com"
```

Let's take the command apart:

1. git config: The command to interact with your Git configuration.
    - --add: Flag stating you want to add a configuration.
    - --global: Flag stating you want this configuration to be stored globally in your
    ~/.gitconfig. The opposite is --local, which stores the configuration in the current
    repository only.
    - user: The section.
    - name: The key within the section.
    - "omega": The value you want to set for the key.

***Assignment***

You can actually store any old data in your Git configuration. Granted, only certain keys are
used by Git, but you can store whatever you want.

Set the following useless key/value pairs in your local Git configuration for the bookiStore
repository (omit the --global flag to set them locally):

```bash
bookiStore.comics_vendor "optomega"
bookiStore.history_vendor "zmaktal"
```

Git has a command to view the contents of your config:

```bash
git config --list --local
```

You can also just view the contents of your local config file directly:
```bash
cat .git/config
```
- **Get**
We've used --list to see all the configuration values, but the --get flag is useful for getting a
single value.
```bash
git config --get <key>
```

Keys are in the format <section>.<keyname>. For example:

user.name
bookiStore.comics_vendor

***Assignment***

Use the --get flag to get the value of the bookiStore.history_vendor key from your local Git
configuration.


- **Unset**
The --unset flag is used to remove a configuration value. For example:

```bash
git config --unset <key>
```

***Assignment***

Remove the bookiStore.history_vendor key from your local Git configuration. Verify that it was
removed.

Try using --unset to remove the entire bookiStore section.

Answer the question.

What happened when you tried to unset the webflyx section?

- [x] The entire section was unset
- [] It failed because it can't unset an entire section, it needs a key

- **Duplicates**
Typically, in a key/value store, like a [Python dictionary](https://docs.python.org/3/tutorial/datastructures.html#dictionaries), you aren't allowed to have duplicate
keys. Strangely enough, Git doesn't care.

Unset All

The --unset-all flag is useful if you ever really want to purge all instances of a key from your
configuration. Conversely, the --unset flag only works with a single instance of a key.

```bash
git config --unset-all example.key
```

***Assignment***
bookiStore has multiple comics_vendor, assign them:
```bash
git config --add bookiStore.comics_vendor "Warden"
git config --add bookiStore.comics_vendor "Cansole"
git config --add bookiStore.comics_vendor "Mandack"
```

Take a look at your new  configuration:
```bash
git config --list --local
```

Remove all the comics_vendor from the bookiStore configuration at once using the --unset-all flag.

- **Remove a Section**
As I pointed out before, the bookiStore section is nonsensical because Git doesn't use it for
anything. While we can store any key/value pairs we want in our Git configuration, that doesn't
mean we should.

The --remove-section flag is used to remove an entire section from your Git configuration. For
example:

```bash
git config --remove-section section
```

***Assignment***
Remove the entire bookiStore section from your local Git config. You might notice that the
default "core" section is still there, that's okay.

- **Locations**
There are several locations where Git can be configured. From more general to more specific, they
are:

*system*: /etc/gitconfig, a file that configures Git for all users on the system
*global*: ~/.gitconfig, a file that configures Git for all projects of a user
*local*: .git/config, a file that configures Git for a specific project
*worktree*: .git/config.worktree, a file that configures Git for part of a project

In my experience, 90% of the time you will be using --global to set things like your username and email. The other 9% of the time you will be using --local to set project-specific configurations. The last 1% of the time you might need to futz with system and worktree configurations, but it's extremely rare.

**Overriding**

If you set a configuration in a more specific location, it will override the same configuration
in a more general location. For example, if you set user.name in the local configuration, it will
override the user.name set in the global configuration.

```
+------------------------------------------------------+
|                      System                          |
|   +----------------------------------------------+   |
|   |                  Global                      |   |
|   |             (overrides system)               |   |
|   |   +---------------------------------------+  |   |
|   |   |               Local                   |  |   |
|   |   |         (overrides global)            |  |   |
|   |   |   +-------------------------------+   |  |   |
|   |   |   |           Worktree            |   |  |   |
|   |   |   |       (overrides local)       |   |  |   |
|   |   |   +-------------------------------+   |  |   |
|   |   +---------------------------------------+  |   |
|   +----------------------------------------------+   |
+------------------------------------------------------+
```

***Quiz***

Suppose you set user.name='Zone' at the system level, user.name='Bruce' at the global level, and
user.name='omega' at the local level. Which value will Git actually use?

- [x] Zone
- [] pickle
- [] Bruce
- [] omega

Which is stored in the user's $HOME directory? (Remember that $HOME = ~/)

- [x] worktree
- []  system
- []  local
- []  global

### 5. Branching

- **What Is a Branch?**

A [Git branch](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) allows you to keep track of different changes separately.

For example, let's say you have a big web project and you want to experiment with changing the
color scheme. Instead of changing the entire project directly (as of right now, our *master*
branch), you can create a new branch called *color_scheme* and work on that branch. When you're
done, if you like the changes, you can [merge](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) the *color_scheme* branch back into the *master* branch
to keep the changes. If you don't like the changes, you can simply delete the *color_scheme* branch
and go back to the *master* branch.

- **Under the Hood**

A branch is just a named pointer to a specific commit. When you create a branch, you are creating
a new pointer to a specific commit. The commit that the branch points to is called the tip of the
branch.

Because a branch is just a pointer to a commit, they're lightweight and "cheap" resource-wise to
create. When you create 10 branches, you're not creating 10 copies of your project on your hard
drive.

```bash
A -- B -- C (main)
               \
                D (feature)

```

The tip of main is commit C.

The tip of feature is commit D.

***Assignment***

Check which branch you're currently on by running:

Make sure you are in the bookiStore directory before running the command.

```bash
git branch
```

- **Default Branch**

We've been using [Git's](https://git-scm.com/) default *master* branch. Interestingly, [GitHub](https://github.com/)(a website where you can
remotely store Git projects) recently changed its default branch from *master* to *main*. As a
general rule, I recommend using *main* as your default branch if you work primarily with *GitHub*, as
we will.

How to Rename a Branch

```bash
git branch -m oldname newname
```

***Assignment***

1. [] Change your global [Git configuration](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration) to use *main* as the default branch. Change the
*init.defaultBranch* key to *main*.

**Note** :Git config keys are case-insensitive, so *defaultBranch* and *defaultbranch* work the same.
Git just prefers lowercase when displaying them.

2. [] Check your current branch:

```bash
git branch
```

You should notice that you're still on *master*! That's because all you did was change the default
branch for new repositories.

3. [] To make this repo use *main*, rename the *master* branch to *main*.
4. [] Run git branch again to make sure you're on the *main* branch.

- **Visualizing Branches**

Throughout the rest of this course, we will use text to represent branches and commits. For
example:

```bash
A - B - C  main
```

means a branch called main with 3 commits. C is the most recent commit (the tip), B is the
previous commit, and A is the commit before that. To represent multiple branches, we'll use
multiple lines:

```bash
  D - E  other_branch
 /
A - B - C  main
```

***Assignment***

Answer the questions based on this diagram:

```bash
      G - H    omega_branch
     /
A - B - C - D   main
\
E - F        optimus_branch
```

1. Which commits are part of omega_branch?

    - [] A, E, F

    - [] A, B, G, H

    - [] A, B, C, D, E, F, G, H, I

    - [] A, B, C, D

2. Which commits are part of main?

    - [] A, E, F

    - [] A, B, G, H, I

    - [] A, B, C, D, E, F, G, H, I

    - [] A, B, C, D

3. Which commits are part of optimus_branch?

    - [] A, E, F

    - [] A, B, G, H, I

    - [] A, B, C, D, E, F, G, H, I

    - [] A, B, C, D

- **New Branch**

You should already be on the main branch: your "default" branch. You can always check with git
branch.

Two Ways to Create a Branch

```bash
git branch my_new_branch
```

This creates a new branch called my_new_branch. The thing is, I rarely use this command because
usually I want to create a branch and switch to it immediately. So I use this command instead:

```bash
git switch -c my_new_branch
```

The switch command allows you to switch branches, and the -c flag tells Git to create a new
branch if it doesn't already exist.

When you create a new branch, it uses the current commit you are on as the branch base. For
example, if you're on your main branch with 3 commits, A, B, and C, and then you run 
git switch -c my_new_branch, your new branch will look like this:

```bash

2 branches, same commits

     A ------> B ------> C
                          \
                           \
                            \
                             \
                              my_new_branch
                              main


commits: A, B, C
branch tips: my_new_branch, main
```

***Assignment***

1. [x] Create and switch to a new branch called *add_masterpiece*, it should have the same 
 commits as the *main* branch.

2. [x] Run git branch to verify that you are on the new branch.

- **Upleveling Our Abilities**
We'll use the *add_masterpiece* branch to add a commit to the project without affecting the main
branch. We'll be creating the following branch structure:
```bash
          D    add_masterpiece
         /
A - B - C      main
```

The *add_masterpiece* branch will have all the commits from the main branch, plus a new commit.

***Assignment***

Switch to the *add_masterpiece* branch if you're not already on it.
Create a new file called masterpiece.csv at the root of the project and copy/paste the following
content into it:
```csv
Title,Author,Year
"Introduction to Algorithms","Thomas H. Cormen, Charles E. Leiserson, Ronald L. Rivest, Clifford
Stein",1990
"Structure and Interpretation of Computer Programs","Harold Abelson, Gerald Jay Sussman, Julie
Sussman",1985
"Operating System Concepts","Abraham Silberschatz, Peter B. Galvin, Greg Gagne",1982
"Compilers: Principles, Techniques, and Tools","Alfred V. Aho, Monica S. Lam, Ravi Sethi, Jeffrey
D. Ullman",1986
"Artificial Intelligence: A Modern Approach","Stuart Russell, Peter Norvig",1995
```

Stage and commit the new file. The commit message should start with D:, in the same format as the
previous exercises.
Run git log to make sure everything looks as you'd expect.

You should be able to see which commits each branch tip points to in the log output. The main
branch should point to commit "C" which should be right before your most recent commit "D" that
add_masterpiece points to.

- **Log Flags**
As you know, ``git log`` shows you the history of commits in your repo. There are a few flags I like
to use from time to time to make the output easier to read.

The first is [``--decorate``](https://git-scm.com/docs/git-log#Documentation/git-log.txt---decorateshortfullautono). It can be one of:

    - short (the default)
    - full (shows the full ref name)
    - no (no decoration)

``--decorate`` is now automatically applied as of version ``2.12.2``. Here are more options you
should know:

Run ``git log --decorate=full``. You should see that instead of just using your branch name, it will
show the full ref name. A [ref](https://git-scm.com/book/en/v2/Git-Internals-Git-References) is just a pointer to a commit. All branches are refs, but not all
refs are branches.

Run ``git log --decorate=no``. You should see that the branch names are no longer shown at all.

The second is ``--oneline``. This flag will show you a more compact view of the log. I use this
one all the time, it just makes it so much easier to see what's going on.
```bash
git log --oneline
```

***Assignment***

Run git log with full decoration and the oneline flag.

- **Git Files**


Remember, Git stores all its information in files in the ``.git`` subdirectory at the root of your
project, even information about branches. The "heads" (or "tips") of branches are stored in the
``.git/refs/heads directory``. If you ``cat`` one of the files in that directory, you should be able to
see the commit hash that the branch points to.

***Assignment***

Use find and cat to find the commit hash that your main branch points to.

Answer the question.

- What is stored in the ``.git/refs/heads directory``?

    1. [x] One file for each commit, containing the branch that the commit belongs to

    2. [] One file for each branch, containing the commit hash that the branch points to

    3. [] One directory for each commit, containing the branches that the commit belongs to

    4. [] One directory for each branch, containing the commit hashes that the branch points to
