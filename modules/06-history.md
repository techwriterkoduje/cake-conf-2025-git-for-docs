# History: reading the repository

Knowing how to read Git history helps you answer questions like "when was this
page changed?", "who wrote this paragraph?", or "which commit introduced this
broken link?". As a technical writer working on documentation for a website,
these commands help you trace authorship, spot regressions, and understand why
content changed.

## Quick `git log` views

The simplest way to see recent commits is:

```
git log --oneline -n 20
```

This shows the last 20 commits as one-line summaries. Add `--graph --decorate`
for a compact visual of branches and refs:

```
git log --oneline --graph --decorate -n 50
```

Useful things you can read from the log:

- Commit messages explaining why text was changed (for example, look for `docs:`
  prefixes, if that's yur commit convention).
- When a page was updated (timestamp on each commit).
- Which branch introduced the change (with `--decorate`).

Example: find when `style-guide.md` was last changed:

```
git log --oneline -- website/style-guide.md
```

## See the full commit

To inspect a particular commit in detail (diff, author, message):

```
git show <commit-hash>
```

## Who changed this line? (`git blame`)

`git blame` annotates a file with the commit and author for each line. This is
useful if you want to ask a peer why they worded something a certain way:

```
git blame website/intro.md
```

Run it with `-L` to limit to a range of lines:

```
git blame -L 1,40 website/intro.md
```

Note: `git blame` shows the last commit that touched each line; if lines were
reformatted, blame may point to the reformat commit rather than the original
author.

## Search history for text

Find commits that mention a string (helpful for tracing when terminology
changed):

```
git log --all --grep="deprecated" --oneline
```

Or search diffs for a phrase:

```
git log -S"getting started" --oneline
```

## Exercise (try it)

1. Show the last 20 commits:

```
git log --oneline -n 20
```

2. Find when `website/style-guide.md` was last edited:

```
git log --oneline -- website/style-guide.md
```

3. Inspect that commit with `git show <hash>` and read the commit message and
   diff.

4. Run `git blame website/intro.md` and identify the author of the first
   heading. If you have questions, use the author information to start a
   friendly review comment.

5. Use `git log -S"getting started" --oneline` to find commits that added or
   removed the phrase "getting started".

## Why this helps writers

- Trace why content changed — the commit message often links to issues or
  discussions.
- Identify the best person to ask about a wording or technical detail.
- Confirm whether a regression was introduced by a specific commit.
