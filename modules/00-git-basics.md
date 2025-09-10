# Git basics

This short introduction explains what Git is, why it matters for technical
writers, and the practical benefits you'll get from learning it.

## What is Git?

Git is a version control system — a tool that records snapshots of your work
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

## Distributed VCS

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

## Git is free and widely used

Git itself is free open-source software. Online hosting services (like GitHub,
GitLab, or Bitbucket) have free tiers that are more than sufficient for
documentation projects. Because Git is ubiquitous in software teams, learning it
helps you collaborate more smoothly with developers and understand their
workflows.

## Wrap-up

Git is a practical tool for writers: it keeps a safe history, enables parallel
work, improves review processes, and connects your docs to the rest of the
product lifecycle. Learning a few basic commands or using a friendly Git client
will pay off quickly in day‑to‑day documentation work.
