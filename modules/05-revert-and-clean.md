# Reverting and cleaning changes

Sometimes you need to remove unwanted files or undo mistakes.

## Remove untracked files

Your repository may contain files that are temporary and should not be tracked by Git, for example, notes, generated output, or
forgotten build artifacts.
You can use the `git clean` command to remove such files.

> WARNING: This operation deletes files from your hard drive. To avoid any surprises, always preview what will be removed by running (`git clean -n`)

## Undo uncommitted changes to a single file

If you edited a file but you didn't commit it, you can undo your changes using the `git restore` (more modern) or `git checkout` commands.

This operation replaces your working copy with the last committed version. It affects only the working tree — nothing is changed in the commit history.

> WARNING: After you discard uncommitted changes, you cannot recover them unless you have local backups or the reflog contains the state.

## Undo committed changes

Git offers several ways to undo changes that were already committed. One of them is the `git revert` command.
It a safe option because it doesn't rewrite the history. Instead, it undoes the specified commit by applying a new commit.

## Exercises

### Clean untracked files

1. Add a file in the `website` folder called `draft-notes.md`.
2. Open the new file and add a short note.
3. Check the status:

   ```shell
   git status
   ```

   Expected: The new file is listed under "Untracked files"

4. Preview removal of untracked files:

   ```shell
   git clean -n
   ```

5. If the preview looks good, remove the file:

   ```shell
   git clean -f
   ```

   > TIP: To remove untracked directories (useful for build outputs), run `git clean -fd`

6. Check the status:

   ```shell
   git status
   ```

   Expected: The file is no longer listed under "Untracked files"

### Discard an accidental edit

1. Open `website/intro.md`.
2. Change the top header or a short paragraph.
3. Save changes and check the status of the file.

   ```shell
   git status
   ```

4. Preview the change.

   ```shell
   git diff
   ```

5. Restore the last committed version of the file:

   ```shell
   git restore website/intro.md
   ```

6. Check the status and the diff for unstaged changes:

   ```shell
   git status
   git diff
   ```

   Expected: The file is back to the committed state.

### Undo a committed edit

1. Open `website/style-guide.md`.
2. Add a short H2 or sentence.
3. Save changes and add the file to the staging area:

   ```shell
   git add website/style-guide.md
   ```

4. Commit your changes:

   ```shell
   git commit -m "docs: refine style guidance"
   ```

5. Push your changes to the remote branch.

   ```shell
   git push
   ```

6. Get the ID of your commit:

   ```shell
   git log --oneline -1
   ```

7. Undo the commit by applying a new commit:

   ```shell
   git revert <commitId>
   ```

   > IMPORTANT: Remember to specify the ID of the commit that you want to undo - not the stable commit that you want to return to. In other words, you tell Git "Remove these changes", not "Restore this version".

8. Ensure the new commit was added to the history:

   ```shell
   git log --oneline -2
   ```

   Expected: The history includes the original commit and the revert commit.

9. Push your changes to the remote branch.

   ```shell
   git push
   ```
