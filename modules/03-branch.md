# Working with branches

Branches are lightweight pointers to commits — they let you work on features,
fixes, or experiments without touching the shared history.

Why use branches? Because they let you develop a feature in isolation, keep the
mainline stable, and collaborate safely. For example, if you're adding a new
getting-started guide, you might create `docs/add-getting-started` and write and
test your changes there until the content is ready to merge. Meanwhile, others
can continue fixing code or other docs on `main`.

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

## Basic commands

- Create and switch to a new branch in one command:

  ```shell
  git switch -c <yourBranchName>
  ```

  or

  ```shell
  git checkout -b <yourBranchName>
  ```

- List local branches:

  ```shell
  git branch
  ```

  List remote branches:

  ```shell
  git branch -r
  ```

  List all branches (local + remote):

  ```shell
  git branch -a
  ```

- Switch to an existing local branch:

  ```shell
  git switch <yourBranchName>
  ```

  or

  ```shell
  git checkout <yourBranchName>
  ```

  If the branch only exists on the remote, fetch first and then check it out:

  ```shell
  git fetch
  git switch -c <yourBranchName> origin/<yourBranchName>
  ```

- Push your local branch to the remote and set the upstream tracking:

  ```shell
  git push --set-upstream origin <yourBranchName>
  ```

  After this, `git push` and `git pull` will default to the remote branch you
  created.

- Delete a local branch:

  ```shell
  git branch -d <yourBranchName>
  ```

- Force-delete a local branch (if it contains unmerged changes):

  ```shell
  git branch -D <yourBranchName>
  ```

- Delete a remote branch:

  ```shell
  git push origin --delete <yourBranchName>
  ```

## Exercise

1. Before you create a new branch, make sure your local copy is up to date with
   the remote. This avoids creating branches from an out-of-date base and
   reduces merge headaches later:

   ```shell
   git checkout main
   git pull
   ```

2. Create a feature branch:

   ```shell
   git switch -c feature/<yourBranchName>
   ```

   or

   ```shell
   git checkout -b feature/<yourBranchName>
   ```

3. List all local branches to verify your branch was created:

   ```shell
   git branch
   ```

   Expected: The branch named `feature/<yourBranchName>` is listed.

4. Publish your local branch as a remote branch:

   ```shell
   git push --set-upstream origin feature/<yourBranchName>
   ```

5. Delete the branch.

   ```shell
   git switch main
   git branch -d feature/try-branch
   git push origin --delete feature/try-branch
   ```
