# Making changes in a branch

This module contains a walkthrough showing how to create a branch and then develop your doc in this branch.

## Commit message conventions

Before you write your first commit message, a short note on conventions. Clear
messages make history useful. A common convention used by teams is:

```text
<type>(scope?): short summary

optional longer description
```

Common `type` values: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`. For
example:

```text
docs(intro): clarify workshop purpose
```

Keep the first line under 72 characters and use the body for details when
needed.

## Auto-save in VS Code

You can set VS Code to auto-save your changes. Go to **File > Preferences > Settings**, search for **Auto Save**, and set it to **afterDelay**.

## Exercises

### Set up a branch

For exercises in this module, use the following branch name:

```text
<yourName>/docs/add-examples
```

This naming convention will allow us to recognize the branch owner easily.

To create and check out your branch, run:

```shell
git switch -c <yourName>/docs/add-examples
```

### Make a single change

We'll make an edit that will cause a conflict later when someone else
changes the same lines on the `main` branch.

1. Open `intro.md`.
2. Change the top-level header to something obvious, for example:

   ```markdown
   # Introduction to HomeSphere by <yourName>
   ```

3. Save the file.
4. Check the status and diffs for unstaged and staged changes:

   ```shell
   git status
   git diff
   git diff --staged
   ```

   Expected: The file is modified and not staged for commit. Changes from the modified file are shown only in the unstaged diff.

5. Add the file to the staging area. and then check the status and the diff for staged changes:

   ```shell
   git add website/intro.md
   ```

6. Check the status and the diff for staged changes:

   ```shell
   git status
   git diff --staged
   ```

   Expected: The file is modified and staged for commit. Changes from the modified file are shown in the staged diff.

7. Commit the change and check the status:

   ```shell
   git commit -m "edit: update intro header for conflict demo"
   git status
   ```

   Expected: Your branch is up to date and there's nothing to commit.

### Make multiple changes

1. Open `style-guide.md`.
2. Add a new H2 near the top. For example:

   ```markdown
   ## New guidance: Accessibility first

   Add a short sentence about headings and accessibility.
   ```

3. Save changes and check the status:

   ```shell
   git status
   ```

   Expected: The file is modified and not staged for commit.

4. Add the file to the staging area and check the status:

   ```shell
   git add website/style-guide.md
   git status
   ```

   Expected: The file is modified and staged for commit.

5. Make another edit. For example, add another paragraph lower down.
6. Save changes and check the status.

   ```shell
   git status
   ```

   Expected: The file is modified and is both staged and not staged for commit. This is because you only staged your first change. You saved the second change in the working directory but you didn't add it to the staging area.

7. Add the file to the staging area and check the status:

   ```shell
   git add website/style-guide.md
   git status
   ```

   Expected: The file is modified and staged for commit.

8. Commit both changes:

   ```shell
   git commit -m "docs: add accessibility guidance and extra note"
   ```

9. Push your branch to the remote server and create a tracking relationship between your local branch and the remote branch:

   ```shell
   git push --set-upstream origin yourname/docs/add-examples
   ```

### Update the last commit

You noticed a typo in your last edit. You want to fix the issue but you don't want to create a new commit in the history.
Instead, you want to modify your last commit to include the fix.

> WARNING: The operations in this exercise are considered "destructive" because they rewrite history of your local and remote branches.
> It's okay on a feature branch that only you are working on, but coordinate with others if
> anyone else might have based work on your branch.

1. Open `style-guide.md`.
2. Fix the typo.
3. Save changes and add the file to the staging area:

   ```shell
   git add website/style-guide.md
   ```

4. Commit your changes to your local branch. The `--amend` and `--no-edit` flags tell Git to update the last commit with your change and keep the same commit message.

   ```shell
   git commit --amend --no-edit
   ```

5. Push your changes to the remote branch. Because you already pushed the original commit, you need to force-push the
   amended commit to update the remote branch:

   ```shell
   git push --force
   ```

### Run final checks

1. Check the status:

   ```shell
   git status
   ```

   Expected: The branch is up to date.

2. Check the history:

   ```shell
   git log --oneline --decorate --graph --all -n 10
   ```

   Expected: The history contains your commits.

3. Check the branch information:

   ```shell
   git branch -vv
   ```

   Expected: The tracking information shows that the remote branch for your local branch is `origin/<yourName>/docs/add-examples`.
