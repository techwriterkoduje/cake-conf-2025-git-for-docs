# Git for docs: basics, not only for beginners

## Description

During this workshop you will learn the basics of Git. Together, we will explore
this amazing tool by not only getting our hands dirty with the most useful
commands but also by digging into the philosophy behind it and the way it works.
Mixing theory with practice will allow you to bridge gaps in your knowledge
about Git and build solid foundations for further development. That's why we
believe that not only beginners but also people who already have some Git skills
can benefit from this workshop.

## Learning objectives

- What version control is and why you should care
- What is Git and how is it different from other version control systems
- Why people use Git
- Where people use Git
- How to manage docs using Git

## Scope

### Practical exercises

- Cloning a repo
- Git config and the most important settings
- Working with branches
- Making changes: stage, commit, and push
- Revert
- Git history
  - `git log --oneline`
- Merge vs rebase
  - rebase changes history, requires force pushes - could be problematic when
    multiple people are working on one branch
  - merge preserves history, but it adds a "merge commit"
  - default pull strategy
- Create a PR
  - All of this happens in GitHub
  - Everyone has their own branch and PR
  - In this workshop, you cannot merge until you receive an approval from the
    repo owner
  - Add comments, suggestions, and give approvals
  - Cannot merge because the base branch is out of date - update your branch
  - When all is well, merge!

### Advanced concepts (theoretical)

- Create a tag
  - useful to mark releases and other important milestones
- Reset
  - Changes history
  - Soft, mixed, hard
- Force push
- Squash
  - `git config --global core.editor code --wait`
  - `git rebase -i HEAD~n`

## Hardware and software requirements

- A laptop with Git installed, preferably the latest version
- VS Code. Make sure you can launch the app from the command line:
  https://code.visualstudio.com/docs/configure/command-line#_launching-from-command-line
- A GitHub account. Make sure you have an SSH key or a Personal Access Token
  configured for your account. You will need it for cloning repos.
- This repo cloned to your machine
