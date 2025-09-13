# Branches

Branches are lightweight pointers to commits — they let you work on features,
fixes, or experiments without touching the shared history.

Why use branches? Because they let you develop a feature in isolation, keep the
mainline stable, and collaborate safely. For example, if you're adding a new
getting-started guide, you might create `docs/add-getting-started` and write and
test your changes there until the content is ready to merge. Meanwhile, others
can continue fixing code or other docs on `main`.

Before you create a new branch, make sure your local copy is up to date with the
remote. This avoids creating branches from an out-of-date base and reduces merge
headaches later:

```
git checkout main
git pull
```

Replace `main` with whatever your repository's default branch is.

## Branch naming conventions

Pick a consistent naming scheme and follow it. What you choose to follow depends
on your team's needs and preferences. Here are common industry practices:

- Use short, descriptive names: `feature/login-form`, `fix/null-pointer`.
- Include a type prefix: `feature/`, `fix/`, `chore/`, `docs/`.
- Use slashes to group: `feature/payment/stripe-integration`.
- Use hyphens for readability inside segments, not underscores.
- Keep names lowercase and ascii; avoid spaces and special characters.

Avoid very long names and avoid leaking sensitive data into branch names.

Examples of good names:

- `feature/add-search`
- `fix/crash-on-startup`
- `docs/update-readme`

Bad examples:

- `WIP` (not descriptive)
- `feature/Johns-new-feature` (contains personal name and caps)

## Create a branch

Create and switch to a new branch in one command:

```
git switch -c feature/add-search
```

Older Git versions use `git checkout -b` for the same effect.

## List branches

List local branches:

```
git branch
```

List remote branches:

```
git branch -r
```

List all branches (local + remote):

```
git branch -a
```

## Switch between branches

Switch to an existing local branch:

```
git switch feature/add-search
```

If the branch only exists on the remote, fetch first and then check it out:

```
git fetch
git switch -c feature/add-search origin/feature/add-search
```

## Publish a branch

To push your new branch to the remote and set the upstream tracking, run:

```
git push --set-upstream origin feature/add-search
```

After this, `git push` and `git pull` will default to the remote/branch you
created.

## Verify and tidy up

Check remote branches:

```
git fetch
git branch -r
```

Delete a local branch when you no longer need it:

```
git branch -d feature/add-search
```

Force-delete if it hasn't been merged:

```
git branch -D feature/add-search
```

Delete the remote branch:

```
git push origin --delete feature/add-search
```

## Exercise (try it)

1. Ensure you're up to date:

```
git checkout main
git pull
```

2. Create a feature branch and list branches:

```
git switch -c feature/try-branch
git branch
```

3. Publish it:

```
git push --set-upstream origin feature/try-branch
```

4. Clean up (optional):

```
git switch main
git branch -d feature/try-branch
git push origin --delete feature/try-branch
```

Expected: the branch appears locally and on the remote until it's deleted.
