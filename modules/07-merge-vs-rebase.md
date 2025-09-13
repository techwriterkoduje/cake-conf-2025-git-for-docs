# Merge vs Rebase

When you bring changes from one branch into another you have two common options:
merge or rebase. Both integrate commits from one branch into another, but they
do so differently. It's important to understand the trade offs so you can pick
the right approach for your team.

## Merge (preserves history)

Merging creates a new "merge commit" that ties two lines of history together. It
preserves the exact commits as they happened and makes the branching structure
explicit in history.

Example: merge `main` into your feature branch to pick up recent changes:

```
git checkout feature/docs-update
git fetch
git merge origin/main
```

This creates a merge commit with a default message like "Merge branch 'main'
into feature/docs-update". You keep all original commits unchanged.

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

Example: rebase your feature branch on top of the latest `main`:

```
git checkout feature/docs-update
git fetch
git rebase origin/main
```

If there are conflicts, Git will stop and ask you to resolve them. After fixing
conflicts, you `git add` the files and `git rebase --continue`.

Because rebase rewrites history, if you've already pushed your branch you'll
need to force-push the rewritten commits:

```
git push --force-with-lease
```

Use `--force-with-lease` instead of `--force` when possible — it is safer and
fails if someone else has pushed new commits to the remote branch.

When to use rebase:

- You want a linear history that's easier to read.
- You're the only person working on the branch, or your team agrees to use
  rebases carefully.

Downside:

- Rewriting public history can break other developers' work if they built on the
  previous commits.

## Default pull strategy

`git pull` is a convenience command that by default runs `git fetch` followed by
`git merge` (merging the remote branch into your current branch). Some teams
prefer rebasing on pull:

```
git pull --rebase
```

Or set it globally for your repository:

```
git config --global pull.rebase true
```

This makes `git pull` run `git fetch` + `git rebase` instead of `merge`.

**Note**: switching the default pull behavior has team-wide implications.
Discuss it with your collaborators.

## Examples for writers

Scenario: you are updating `getting-started.md` in `feature/docs-update`. The
team has been committing bug fixes to `main` while you worked.

- Merge approach: `git fetch` + `git merge origin/main` — keep your commits as
  they are and create one merge commit. History shows the merge point.
- Rebase approach: `git fetch` + `git rebase origin/main` — replay your commits
  on top of `main` for a linear history; then `git push --force-with-lease`.

If others also work on your branch, prefer merging to avoid rewriting shared
history.

## Exercise (try it)

The instructor will update `main`. Fetch the update and integrate it into your
branch. Two options below — try both to observe differences.

### Try merge

The merge method is safe for shared branches.

```
git fetch
git merge origin/main
```

This creates a merge commit on your branch. Inspect the graph:

```
git log --oneline --graph --decorate -n 20
```

### Try rebase

The rebase method rewrites local commits; requires force-push if already pushed.

```
git fetch
git rebase origin/main
```

If rebase completes, push the rewritten commits to the remote with:

```
git push --force-with-lease
```

### Compare results

Compare histories after each approach with:

```
git log --oneline --graph --decorate -n 50
```

Observe how merge keeps a branching point while rebase produces a linear
sequence of commits.

## Safety notes

- Prefer `--force-with-lease` over `--force` for safer force-pushes.
- Communicate with teammates before rebasing or force-pushing a branch that
  others may have pulled.
