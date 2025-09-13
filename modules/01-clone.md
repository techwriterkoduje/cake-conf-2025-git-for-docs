# Cloning a repo

To work on a Git repo, you need to have it on your machine — that's technically
all you need. The most basic scenario is just you working on a repo on your
machine alone.

To initialize a repo, you use the following command:

```
git init
```

This creates a `.git` folder in your repo and starts the history.

## What's a "remote"

The real power of Git as a collaborative tool comes from using a 3rd-party
service which stores your repository on a "remote". A remote is a server that
manages your Git history and provides features like authentication and access
control. Services such as GitHub, GitLab, and Bitbucket also add collaboration
features like pull requests, which we'll cover later.

You can link your local repository to a remote using the following command:

```
git remote add origin <REMOTE_URL>
```

If you already have a new project on GitHub and want to push an existing local
folder, GitHub will give you a short sequence like this:

```
echo "# Welcome to my repo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:my-username/my-repo.git
git push -u origin main
```

We won't go into committing details now; this is just background. High-level
steps:

1. Initialize the repo with `git init`
2. Add a file
3. Commit the file
4. Set the branch name
5. Add the remote (`origin`)
6. Push to the origin

## What about cloning?

To clone an existing repo, run:

```
git clone <REMOTE_URL>
```

For example:

```
git clone git@github.com:my-username/my-repo.git
```

Cloning copies the remote repository to your machine and wires up the `origin`
remote. `git clone` also checks out the repository's default branch (often
`main`).

## Where to get the remote URL

On GitHub, open the repo page and click the green **Code** button. Choose
**SSH** or **HTTPS** and copy the URL shown. Quick notes:

- SSH (`git@github.com:user/repo.git`) requires an SSH key configured in your
  GitHub account.
- HTTPS (`https://github.com/user/repo.git`) works via browser auth or a
  personal access token.

For this workshop, we choose SSH because it's convenient. You would choose HTTPS
if you preferred not to deal with SSH keys for now.

For this workshop, you can run:

```
git clone git@github.com:techwriterkoduje/cake-conf-2025-git-for-docs.git
```

## Verify your clone

After cloning (or after `git init` + `git remote add`), run these quick checks:

```
cd cake-conf-2025-git-for-docs
git remote -v
git branch --show-current
git status
```

You should see `origin` listed under `git remote -v` and a branch name (often
`main`) from `git branch --show-current`.

## Troubleshooting (brief)

- Permission denied (SSH): try the HTTPS URL or ensure your SSH key is added to
  GitHub.
- Repository not found: check the URL and whether the repo is private and you
  have access.
- Network errors: retry or check your internet connection.

## Exercise (try it)

Clone the workshop repo and verify remotes and branch:

```
git clone git@github.com:techwriterkoduje/cake-conf-2025-git-for-docs.git
cd cake-conf-2025-git-for-docs
git remote -v
git branch --show-current
```

Expected: `origin` is listed and the default branch (often `main`) is checked
out.
