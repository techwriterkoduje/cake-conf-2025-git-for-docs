# Git basics

This short introduction explains the following key concepts that you need to learn to
benefit fully from practical exercises in this workshop:

- What version control system (VCS) is
- Different types of version control systems
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

## Evolution of version control systems

Here's a brief history of version control systems that will allow you to understand
how Git is different from other tools of this type.
Images in this section comes from the "Ry's Git Tutorial" book.

### The "final" solution (aka files and folders)

Before a VCS was invented, the only way to track versions of a project
was to create a copy and give it a new name. Just think how many times you saved
a file or folder whose name contained the "final" word :)
This solution was very prone to errors, such as overwriting the wrong file or mislabelling a folder.

![Diagram showing controlling versions of a project using files and folders](img/files-and-folders.png)

### Local VCS

Because creating copies of files and folders wasn't a good solution,
developers invented local Version Control Systems. These tools stored
files and folders in a database. Instead of accessing files directly,
you "checked out" a copy of the project.
This solution was a big step forward, but it didn't offer an efficient way
of sharing code among a group of programmers because everything happened locally.

![Diagram showing controlling versions of a project using a local VCS](img/local-vcs.png)

### Centralized VCS

A centralized VCS is similar to a local VCS, but the project history is stored
on a server. You check out files and then save them back into the project over network. This solution allows you to collaborate on a project with others through
a single point of entry. To solve the issue of creating conflicting changes at the same time, a CVCS prevents you from overriding others' work (file checkout, file lock). A CVCS has another downside - it has a single point of failure. If the server goes down or becomes corrupted, you can't do your work or even lose the entire data.
An example of a CVCS is Subversion.

![Diagram showing controlling versions of a project using a centralized VCS](img/centralized-vcs.png)

### Distributed Version Control System

A distributed VCS solves the issue of collaboration in a larger group. Instead of checking out the latest snapshot of the files, you have your own local copy of the entire project. It allows you to work independently and put off merging conflicts until your convenience. A DVCS is also much faster because you don't have perform actions over a network. Also, the risk of losing data is much lower compared to a CVCS because every user has a complete copy of the entire project.
An example of a DVCS is Git.

![Diagram showing controlling versions of a project using a distributed VCS](img/distributed-vcs.png)

## Git

It's a free and open-source DVCS, which propels most of the software development industry.
When the Linux community lost their free license for BitKeeper (commercial DVCS) in 2005, they decided to develop their own system. That's an extremely short history of
Git.

## Git areas: working copy, local, remote

## Git states: untracked, staged, committed, pushed

## How Git helps your writing process

- Keep a clear history: Every commit tells you who changed what and why. That
  makes it easier to understand the evolution of a document and to write
  changelogs.
- Safe experimentation: Use branches to try different ways of phrasing or
  structuring content. If one approach doesn't work, you can switch back easily.
- Revert mistakes: If a revision introduces errors, Git lets you restore a
  previous version quickly.
- Work offline: Git records your changes locally; you don’t need an internet
  connection to save progress.

## Collaboration and resolving conflicts

When several people work on the same repo, Git helps them make changes in
parallel. Each person can work on different files or branches. When it’s time to
combine changes, Git merges them together. If two people edit the same line in a
file, Git will flag a conflict and ask someone to choose which version to keep.
Conflicts sound scary but are usually straightforward: Git shows the differing
parts, and you pick or combine the text.

> **Note:**
>
> Conflicts are not a sign that something went wrong, they are a standard part
> of the Git workflow.

Practical workflow for teams (high level):

1. Create a branch for your work (e.g., "update-installation-guide").
2. Make commits as you make meaningful edits.
3. Push your branch to the shared remote.
4. Open a pull request (or merge request) so teammates can review and discuss
   changes before merging into the main branch.

## Why technical writers should learn Git

- It's an industry standard. Many companies use Git for code and documentation.
  Learning Git makes you more effective and more hireable.
- Works with plain-text formats. Git works best with text files (Markdown,
  reStructuredText), which is common for docs and enables easy diffs and
  reviews.
- Better reviews and traceability. Review tools (pull requests) let reviewers
  comment on specific lines. You can track who changed what and understand the
  rationale behind edits.
- Reproducibility and publishing. Docs in Git can be tied to the software
  release that they describe, and they can be published automatically by
  continuous integration systems.
- Transferable skill. Git skills apply across roles and projects —
  documentation, content design, product specs, and beyond.

## Wrap-up

Git is a practical tool for writers: it keeps a safe history, enables parallel
work, improves review processes, and connects your docs to the rest of the
product lifecycle. Learning a few basic commands or using a friendly Git client
will pay off quickly in day‑to‑day documentation work.

## NOTES

Git is a Version Control System (VCS) — a tool that records snapshots of your work
over time. Think of it like a save history for your documents where every
meaningful change is recorded with a short note (a "commit"). You can go back to
any earlier snapshot, compare versions, or restore content if something goes
wrong.

Key ideas (plain language):

- Repository (repo): a folder with your project and a Git history.
- Commit: a saved snapshot with a message describing the change.
- Branch: a separate line of work where you can experiment without affecting the
  main content.
- Remote: a copy of the repo stored on a server (for example, GitHub) that your
  team can share.
