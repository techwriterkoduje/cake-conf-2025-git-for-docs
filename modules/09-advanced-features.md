# Tags, reset, force-push, and squash (theory)

This module is theory only — no exercises. It explains a few advanced Git
concepts that are useful to understand as a technical writer collaborating on
documentation: tags (for releases), `git reset` (to move or edit history),
force-pushing, and squashing commits via interactive rebase.

## Tags

Tags are named pointers to commits that are often used to mark releases,
milestones, or stable snapshots. For documentation teams, tags are handy for
marking documentation that matches a particular product release (e.g.,
`v1.0.0-docs`).

You can create two types of tags:

- Lightweight

  ```shell
  git tag v1.0.0-docs
  ```

- Annotated (recommended for releases — includes a message and signing support):

  ```shell
  git tag -a v1.0.0-docs -m "Docs for v1.0.0 release"
  ```

After you create a tag, you can push it to the remote:

```shell
git push origin v1.0.0-docs
```

You can check out a tag the same way you check out a branch:

```shell
git checkout v1.0.0-docs
```

### Example

When you prepare a documentation release that matches a code release,
tag the commit that corresponds to the published docs site. This makes it easy
to check out the exact state later (for bug fixes or audits).

## Reset

The reset option in Git allows you to:

- Change where `HEAD` points
- Update the index (staging area)
- Update working tree

The result of the operation depends on the selected options.

Resetting is primarily a local operation that modifies history or staging without creating new commits.

The reset feature has three common modes:

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

### Example

You accidentally committed three small edits to `intro.md` as three
separate commits but want to combine them into one. You can soft `reset` to the
parent commit, which keeps the changes staged, then create a new single commit
with a better message:

```shell
git reset --soft HEAD~3
git commit -m "docs(intro): tidy and combine edits"
```

## Squash commits

Squashing combines multiple commits into one. Interactive rebase is the common
tool for this:

```shell
git rebase -i HEAD~n
```

The `n` parameter is the number of last commits that you want to squash.

An editor opens showing the last `n` commits. You can mark commits as `pick`,
`squash` (`s`), or `fixup` to combine them. After editing, Git will replay
the commits and produce a new sequence with the selected squashes applied.

### Example

You have several small commits while drafting a new guide. Before
opening a PR, you prefer a single tidy commit. Use interactive rebase to squash
those drafts into one logical commit with a clear message, then
`git push --force-with-lease` to update the branch.

## Safety first

- Rewriting history (reset, rebase, squash) is fine for local or private
  branches but becomes dangerous on shared branches. Avoid rewriting public
  history others may base their work on.
- Always prefer `--force-with-lease` over `--force` when updating a remote.
- Keep tags for published documentation to make it easy to check out earlier
  site states.
