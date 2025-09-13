# Working with repository history

Knowing how to read Git history helps you answer questions like "when was this
page changed?", "who wrote this paragraph?", or "which commit introduced this
broken link?". As a technical writer working on documentation for a website,
these commands help you trace authorship, spot regressions, and understand why
content changed.

## Log

The most common way to see the history of changes in your repository is using the `git log` command.

Useful things you can read from the log:

- Commit messages explaining why something was changed (for example, look for `docs:`
  prefixes, if that's your commit convention).
- When a page was updated (timestamp on each commit).
- Which branch introduced the change (`--decorate` option).

The log command has many options that you can use to adjust the log view to your needs. For example, you can view the shortened version of the log by using the `--oneline` flag.

## Commit details

In Git, you can also inspect a particular commit in detail by using the `git show` command. It shows the author, date, message and the diff for the commit.

## Detailed file history

You can view a detailed history of changes for a file by using the `git blame` command. It annotates a file with the commit and author for each line. This is useful if you want to ask a peer why they worded something a certain way.

> NOTE: `git blame` shows the last commit that touched each line. If lines were reformatted, blame may point to the reformat commit rather than the original author.

## Why this helps writers

- Trace why content changed — the commit message often links to issues or
  discussions.
- Identify the best person to ask about a wording or technical detail.
- Confirm whether a regression was introduced by a specific commit.

## Exercise

1. Show the last 20 commits:

   ```shell
   git log --oneline -n 20
   ```

2. Find when `website/style-guide.md` was last edited:

   ```shell
   git log -- website/style-guide.md
   ```

3. Get the commit ID from the previous step and view its details:

   ```shell
   git show <commitId>
   ```

4. Read the commit message and diff from the information that was displayed.

5. Show changes for the `website/intro.md` file:

   ```shell
   git blame website/intro.md
   ```

6. Identify the author of the first heading. If you have questions, use the author information to start a
   friendly review comment.

7. Find commits that added or removed the phrase "getting started".

   ```shell
   git log -S"getting started" --oneline
   ```

8. Find commits that have the string "improve" in the message:

   ```shell
   git log --all --grep="improve" --oneline
   ```

9. Show commits that are in your branch but not in the `main` branch.

   ```shell
   git log main..<yourBranchName> --oneline
   ```
