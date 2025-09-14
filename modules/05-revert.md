# Reverting and cleaning changes

Sometimes you need to undo mistakes or remove unwanted files. In this module
we'll cover three common tools:

- `git checkout` (undo changes to tracked files before committing)
- `git reset` (unstage changes and move HEAD without altering history)
- `git clean` (remove untracked files)

We'll use files in `website/` for examples.

## Undo changes to a single file with `git checkout`

If you've edited a file but haven't committed yet and want to discard your
changes, use `git restore` (modern command) or the older `git checkout` form:

```
git restore website/intro.md
```

Or (older Git versions):

```
git checkout -- website/intro.md
```

This replaces your working copy with the last committed version. It only affects
the working tree — nothing is changed in the commit history.

### Exercise A — discard an accidental edit

1. Edit `website/intro.md` and change the top header or a short paragraph.
2. Run `git status` to see the change.
3. Preview the change with `git diff`.
4. Run `git restore website/intro.md`.
5. Run `git status` and `git diff` again — the file should be back to the
   committed state.

## Unstage changes and move HEAD with `git reset`

`git reset` comes in several forms. Two useful variants:

- `git reset --soft <commit>` moves HEAD to `<commit>` but leaves the index and
  working tree alone (useful when you want to keep changes staged).
- `git reset --mixed <commit>` (the default) moves HEAD and updates the index to
  match, leaving your working tree alone — effectively unstaging changes.

Common local workflow: you staged a file but decide not to include it in the
next commit. Use:

```
git reset HEAD website/style-guide.md
```

This unstages the file but keeps your edits in the working directory.

### Exercise B — unstage and recommit

1. Edit `website/style-guide.md` and add a short H2 or sentence.
2. Stage and check:

```
git add website/style-guide.md
git status
git diff --staged
```

3. Decide you don't want to include this change yet. Unstage:

```
git reset HEAD website/style-guide.md
git status
```

4. Edit the file again or run `git add` when you're ready, then commit:

```
git add website/style-guide.md
git commit -m "docs: refine style guidance"
```

## Remove untracked files with `git clean`

If you create temporary files during editing (notes, generated output, or
forgotten build artifacts), they appear as untracked files. `git clean` can
remove them. Be careful — this deletes files.

Preview what would be removed:

```
git clean -n
```

Then remove untracked files (current directory):

```
git clean -f
```

To remove untracked directories (useful for build outputs):

```
git clean -fd
```

### Exercise C — clean untracked files

1. Create an untracked file in the `website` folder called `draft-notes.md` and
   add a short note.
2. Run `git status` — you'll see the untracked file.
3. Preview removal with `git clean -n`.
4. If the preview looks right, remove it with `git clean -f`.
5. Confirm it's gone with `git status`.

## Safety notes

- Always preview `git clean` with `-n` before running it.
- `git restore` / `git checkout --` cannot recover changes after they are
  discarded unless you have local backups or the reflog contains the state.
- `git reset --hard` will throw away changes in the working tree — avoid it
  unless you're sure.

## Combined exercise

1. Start on a fresh branch: `git switch -c yourname/revert-demo`.
2. Edit `website/intro.md` (small header change) and `website/style-guide.md`
   (add a H2).
3. Check status and diffs:

```
git status
git diff
```

4. Restore `intro.md` to discard that change:

```
git restore website/intro.md
```

5. Stage and commit `style-guide.md` only:

```
git add website/style-guide.md
git commit -m "docs: add accessibility guidance"
```

6. Create an untracked file `website/draft-notes.md` and then remove it with
   `git clean -n` followed by `git clean -f`.

7. Verify the repo is clean:

```
git status
```

Expected: `intro.md` shows no modifications, `style-guide.md` is committed, and
`draft-notes.md` is removed.

You can go back to your previous branch.
