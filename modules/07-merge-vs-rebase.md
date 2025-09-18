# Merge vs Rebase

When you bring changes from one branch into another you have two options:

1. Merge
2. Rebase

Both integrate commits from one branch into another, but they do so differently.
It's important to understand the trade offs so you can pick the right approach
for your team.

## Merge (preserves history)

Merging creates a new "merge commit" that ties two lines of history together. It
preserves the exact commits as they happened and makes the branching structure
explicit in history.

When to use merge:

- You want a complete, honest history showing how branches combined.
- Multiple people work on a branch and rewriting history would be unsafe.

Downside:

- History becomes more complex with merge commits; some teams prefer a linear
  history instead.

## Rebase (rewrites history)

Rebasing moves your commits on top of another base commit, producing a linear
history. It rewrites the commit hashes because it creates new commits that
contain the same changes but with different parents.

If there are conflicts, Git will stop and ask you to resolve them. After fixing
conflicts, you `git add` the files and `git rebase --continue`.

Rebase rewrites history. If you already pushed your branch, you'll need to
force-push the rewritten commits.

When to use rebase:

- You want a linear history that's easier to read.
- You're the only person working on the branch, or your team agrees to use
  rebases carefully.

Downside:

- Rewriting public history can break other developers' work if they built on the
  previous commits.

### Safety first

- Communicate with teammates before rebasing or force-pushing a branch that
  others may have pulled.
- Use `--force-with-lease` instead of `--force` when possible. It prevents you
  from accidentally destroying your teammate's work. If someone else pushed
  changes while you were working, the rebase operation will fail.

## Default pull strategy

`git pull` is a convenience command that by default runs:

1. `git fetch`
2. `git merge` (merging the remote branch into your current branch)

Some teams prefer rebase over merge when they pull changes. Use the `--rebase`
flag for that:

```shell
git pull --rebase
```

This flag makes `git pull` run:

1. `git fetch`
2. `git rebase` (rewriting your branch's history)

If you always want to rebase on pull, change the default strategy:

```shell
git config --global pull.rebase true
```

> **Note**: switching the default pull behavior has team-wide implications.
> Discuss it with your collaborators.

## Exercises

The instructor will update the `main` branch. Fetch the update and integrate it
into your branch. Try both merge and rebase to observe differences.

### Try merge

1. Update your repository.

   ```shell
   git fetch
   ```

2. Merge the update into your branch.

   ```shell
   git merge origin/main
   ```

3. Inspect the history:

   ```shell
   git log --oneline --graph --decorate -n 20
   ```

   Expected: A merge commit is listed in the repository history at the point of
   time when the instructor made the change. Your original commits remain
   unchanged.

### Try rebase

The rebase method rewrites local commits; requires force-push if already pushed.

1. Update your repository.

   ```shell
   git fetch
   ```

2. Rebase `main` onto your branch.

   ```shell
   git rebase origin/main
   ```

3. If the rebase operation completes, push the rewritten commits to the remote:

   ```shell
   git push --force-with-lease
   ```

4. Inspect the history:

   ```shell
   git log --oneline --graph --decorate -n 20
   ```

   Expected: The repository's history changed. The update made by the instructor
   is listed before your updates.
