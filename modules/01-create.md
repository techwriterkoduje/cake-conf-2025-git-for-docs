# Creating a repo

To work on a Git repo, you must have it on your machine. Technically, that's all
you need. The most basic scenario is just you working on a repo on your machine
alone.

## Option 1: Initialize

To initialize a repo, run:

```shell
git init
```

This creates a `.git` folder in your repo and starts the history.

### Linking to a "remote"

You can link your local repository to a remote using the following command:

```shell
git remote add origin <remoteUrl>
```

If you already have a new project on GitHub and want to push an existing local
folder, GitHub will give you a short sequence like this:

```shell
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

1. Initialize the repo with `git init`.
2. Add a file.
3. Commit the file.
4. Set the branch name.
5. Add the remote (`origin`).
6. Push to the origin.

## Option 2: Clone

To clone an existing repo, run:

```shell
git clone <remoteUrl>
```

For example:

```shell
git clone git@github.com:my-username/my-repo.git
```

Cloning copies the remote repository to your machine and creates a link to the
`origin` remote. `git clone` also checks out the repository's default branch
(often `main`).

### Get the remote URL

On GitHub, open the repo page and click the green **Code** button. Choose
**SSH** or **HTTPS** and copy the URL shown. Quick notes:

- SSH (`git@github.com:user/repo.git`) requires an SSH key configured in your
  GitHub account.
- HTTPS (`https://github.com/user/repo.git`) works via browser auth or a
  personal access token.

For this workshop, we choose SSH because it's convenient. You would choose HTTPS
if you preferred not to deal with SSH keys for now.

### Verify your clone

After cloning (or after `git init` + `git remote add`), run these quick checks:

```shell
cd <localRepoPath>
git remote -v
git branch --show-current
git status
```

You should see `origin` listed under `git remote -v` and a branch name (often
`main`) from `git branch --show-current`.

## Exercise

1. Clone the workshop repo:

   ```shell
   git clone git@github.com:techwriterkoduje/cake-conf-2025-git-for-docs.git
   ```

2. Verify remotes and branch:

   ```shell
   cd cake-conf-2025-git-for-docs
   git remote -v
   git branch --show-current
   ```

   Expected: `origin` is listed and the default branch (`main`) is checked out.

## Troubleshooting

### Permission denied (SSH)

Try the HTTPS URL or ensure your SSH key is added to GitHub.

### Repository not found

Check the URL and whether the repo is private and you have access.

### Network errors

Retry or check your internet connection.
