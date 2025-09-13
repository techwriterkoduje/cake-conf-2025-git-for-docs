# Git basics

This short introduction explains the following key concepts that you need to learn to
benefit fully from practical exercises in this workshop:

- What version control system (VCS) is and how it evolved over time
- What Git is
- Why you should care about Git if you're a technical writer

## Version control system (VCS)

It's a tool that records changes to a file or set of files over time so that you can recall specific versions later.
For example, a VCS allows you to:

- Revert the entire project to a previous state
- Compare changes
- See who last modified something
- Analyze the history of changes to find a bug

Generally, using a VCS means that if something goes wrong, you can recover.

### Evolution of version control systems

Here's a brief history of version control systems that will allow you to understand
how Git is different from other tools of this type.
Images in this section comes from the "Ry's Git Tutorial" book.

#### The "final" solution (aka files and folders)

Before a VCS was invented, the only way to track versions of a project
was to create a copy and give it a new name. Just think how many times you saved
a file or folder whose name contained the "final" word :)
This solution was very prone to errors, such as overwriting the wrong file or mislabelling a folder.

![Diagram showing controlling versions of a project using files and folders](img/files-and-folders.png)

#### Local VCS

Because creating copies of files and folders wasn't a good solution,
developers invented local Version Control Systems. These tools stored
files and folders in a database. Instead of accessing files directly,
you "checked out" a copy of the project.
This solution was a big step forward, but it didn't offer an efficient way
of sharing code among a group of programmers because everything happened locally.

![Diagram showing controlling versions of a project using a local VCS](img/local-vcs.png)

#### Centralized VCS

A centralized VCS is similar to a local VCS, but the project history is stored
on a server. You check out files and then save them back into the project over network. This solution allows you to collaborate on a project with others through
a single point of entry. To solve the issue of creating conflicting changes at the same time, a CVCS prevents you from overriding others' work (file checkout, file lock). A CVCS has another downside - it has a single point of failure. If the server goes down or becomes corrupted, you can't do your work or even lose the entire data.
An example of a CVCS is Subversion.

![Diagram showing controlling versions of a project using a centralized VCS](img/centralized-vcs.png)

#### Distributed Version Control System

A distributed VCS solves the issue of collaboration in a larger group. Instead of checking out the latest snapshot of the files, you have your own local copy of the entire project. It allows you to work independently and put off merging conflicts until your convenience. A DVCS is also much faster because you don't have perform actions over a network. Also, the risk of losing data is much lower compared to a CVCS because every user has a complete copy of the entire project.
An example of a DVCS is Git.

![Diagram showing controlling versions of a project using a distributed VCS](img/distributed-vcs.png)

## Git

It's a free and open-source DVCS, which propels most of the software development industry.
When the Linux community lost their free license for BitKeeper (commercial DVCS) in 2005, they decided to develop their own system. That's an extremely short history of
Git.
This tool was built with speed, simple design and support for non-linear development in mind. It has some unique features that make it different from other tools of this type.
Images in this section comes from the "Pro Git" book.

### Snapshots

Other VCSes, like Subversion, store information as a list of file-based changes. In other words, these systems record only differences.

![Diagram showing data storage as changes to a base version of each file](img/file-based-changes.png)

Git stores data like a set of snapshots of a filesystem. In other words, every time you perform an operation, Git takes a picture of what all your files look like at the moment and stores a reference to that snapshot.

![Diagram showing data storage as snaphots](img/snaphots.png)

### Local operations

Most actions that you perform in Git are local. You don't need another computer or connection to a network.
It has two major advantages:

1. Operations are fast
2. You can work on your project without interruptions, for example on an airplane or a train, and share your changes with others when you get to a network connection to upload.

### Checksum

To ensure integrity of changes, Git checksums everything before storing it. This way,no changes can go under Git's radar.
The mechanism used for this checksumming is the SHA-1 hash:

- String composed of 40 hexadecimal characters (0-9 and a-f)
- Calculated based on the contents of a file or directory

Example:

```text
01bdc71d3bd5c9b9f0d6a8cdc4b1a7d35ef625c0
```

Checksumming is an important concept because Git stores everything in its database not by filename but by the hash value of its contents.

### Three states

There are actually four states, but only three of them are in Git.
In a Git repository, a file can be:

1. `untracked` - Git doesn't track changes for this file
2. `modified` - the file was changed but not staged or committed
3. `staged` - the file was changed and its current version was marked to go into your next commit.
4. `committed` - the file was changed and stored in your local database

These states are related to three main sections of a Git project:

1. **Working directory** - a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on your hard disk.
2. **Staging area** - a file in your Git directory that stores information about what will go into your next commit
3. **The `.git` directory (repository)** - it contains metadata and object database for your project. It's the most important part of Git and it is what is copied when you clone a repository.

![Diagram showing three sections of a Git project](img/git-project-sections.png)

The basic workflow in Git looks like this:

1. You create a new file (`untracked`) and then add it to the Git project.
2. You change the file in your working directory (`modified`).
3. You stage the file by adding its snapshot to the staging area (`staged`).
4. You commit your changes, which moves the file snapshot from the staging area to the Git directory (`committed`)

### Remote repository

It's a repository hosted on the Internet or somewhere else. It's not a requirement of Git to have one central remote repository as the "source of truth" but a process choice. It's hard to collaborate with others without such a repository. Sure, you can share changes with others in a different way, for example by creating and sending patches, but it's not a scalable solution.
With the advent of platforms like GitHub and Bitbucket, it became a convention to have a remote repository with which everyone synchronizes their changes by pulling and pushing them.
These platforms offer additional features, such as pull requests, which are useful when you work on a project with others. It's important to know what is part of Git and what is an extra thing on top of it added by a platform.

## Why technical writers should learn Git

- It's an industry standard. Many companies use Git for code and documentation.
  Learning Git makes you more effective and more hireable.
- Transferable skill. Git skills apply across roles and projects —
  documentation, content design, product specs, and beyond.
- Works with plain-text formats. Git works best with text files (Markdown,
  reStructuredText), which are commonly used in the docs as code model
- Clear history. Every commit tells you who changed what and why. That
  makes it easier to understand the evolution of a document and to write
  changelogs.
- Better reviews and traceability. You can track who changed what and understand the
  rationale behind edits.
- Reproducibility and publishing. Docs in Git can be tied to the software
  release that they describe, and they can be published automatically by
  continuous integration systems.
- Safe experimentation: Use branches to try different ways of phrasing or
  structuring content. If one approach doesn't work, you can switch back easily. If a revision introduces errors, you can restore a previous version quickly.
