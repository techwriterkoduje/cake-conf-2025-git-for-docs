# Tags, reset, force-push, and squash (theory)

This module is theory only — no exercises. It explains a few advanced Git
concepts that are useful to understand as a technical writer collaborating on
documentation: tags (for releases), `git reset` (to move or edit history),
force-pushing, and squashing commits via interactive rebase.

## Tags — marking releases and milestones

Tags are named pointers to commits that are often used to mark releases,
milestones, or stable snapshots. For documentation teams, tags are handy for
marking documentation that matches a particular product release (e.g.,
`v1.0.0-docs`).

Create a lightweight tag:

```
git tag v1.0.0-docs
```

Create an annotated tag (recommended for releases — includes a message and
signing support):

```
git tag -a v1.0.0-docs -m "Docs for v1.0.0 release"
```

Push a tag to the remote:

```
git push origin v1.0.0-docs
```

Example: when you prepare a documentation release that matches a code release,
tag the commit that corresponds to the published docs site. This makes it easy
to check out the exact state later (for bug fixes or audits).

```
git checkout v1.0.0-docs
```

## Reset — moving HEAD and changing history

`git reset` changes where `HEAD` points and can update the index (staging area)
and working tree depending on the flags you use. It's primarily a local
operation that modifies history or staging without creating new commits.

Three common modes:

- `git reset --soft <commit>`: move `HEAD` to `<commit>` but leave the index and
  working tree untouched. The changes from the moved commits become staged. Use
  this when you want to combine or rework commits but keep the edits staged for
  a new commit.

- `git reset --mixed <commit>` (the default): move `HEAD` and reset the index to
  match `<commit>`, but leave the working tree alone. This unstages the changes
  while keeping the file edits. It's useful when you accidentally staged the
  wrong files.

- `git reset --hard <commit>`: move `HEAD` and reset both index and working tree
  to `<commit>`. This throws away any uncommitted changes. Use with extreme
  caution.

Example: you accidentally committed three small edits to `intro.md` as three
separate commits but want to combine them into one. You can `reset` soft to the
parent commit, which keeps the changes staged, then create a new single commit
with a better message:

```
git reset --soft HEAD~3
git commit -m "docs(intro): tidy and combine edits"
```

## Force push — rewriting remote history

When you rewrite commits locally (for example after a rebase or reset) the local
commit hashes no longer match the remote. Pushing these rewritten commits
requires a force push. Use `--force-with-lease` to reduce risk:

```
git push --force-with-lease
```

Why `--force-with-lease`? It only force-pushes if the remote branch still has
the last commit you expected — it refuses if someone else pushed meanwhile.

Example: after you squash or tidy commits locally to improve history, you
force-push the branch so the PR contains the cleaner sequence of commits. Warn
reviewers before force-pushing a branch that others might have fetched.

## Squash commits — `git rebase -i HEAD~n`

Squashing combines multiple commits into one. Interactive rebase is the common
tool for this:

```
git rebase -i HEAD~4
```

An editor opens showing the last 4 commits; you can mark commits as `pick`,
`squash` (or `s`), or `fixup` to combine them. After editing, Git will replay
the commits and produce a new sequence with the selected squashes applied.

Example: you have several small commits while drafting a new guide. Before
opening a PR, you prefer a single tidy commit. Use interactive rebase to squash
those drafts into one logical commit with a clear message, then
`git push --force-with-lease` to update the branch.

## Notes and cautions

- Rewriting history (reset, rebase, squash) is fine for local or private
  branches but becomes dangerous on shared branches — avoid rewriting public
  history others may base work on.
- Always prefer `--force-with-lease` over `--force` when updating a remote.
- Keep tags for published documentation to make it easy to check out earlier
  site states.
