# Pull Requests (PRs)

This module uses GitHub to demonstrate Pull Requests (PRs). PRs are not a
feature of Git itself but of repository hosting platforms (GitHub, GitLab,
Bitbucket). In short, a PR is a request to merge changes from one branch into another.

## Why PRs help writers

### Reviewing and approving

- A PR offers a web UI with useful features.
- Reviewers can read the exact changes and suggest edits by adding inline comments. They don't have to edit the file directly.
- The **Add a suggestion** feature lets reviewers propose an exact edit that the
  author can accept with one click.
- You can configure default reviewers that are notified automatically every time you create a PR.
- A PR acts as a gate for automated checks (CI) and human approvals

### Tracking

- A PR adds another layer of history tracking on top of the commit history in Git.
- A PR acts as a discussion thread
- The PR timeline records decisions (who approved what, what changed) which is
  valuable for audits and handovers.

## Exercises

Follow these exercises using the branch you created earlier in the workshop (for
example `<yourName>/docs/add-examples`).

### 1. Create a PR

1. On GitHub, go to the repository page.
2. If you see a banner to compare & pull request for your recently pushed branch, click it.
3. If you don't see the banner:

   1. Click **Pull requests** → **New pull request**
   2. Choose your branch as the head and `main` as the base.

4. Give the PR a clear title (use the commit convention if you like) and a short
   description of the change and why it's needed.
5. Add reviewers (the instructor or repo owner).

### 2. Add a suggestion

The repo owner (instructor) follows these steps:

1. In the PR UI, go to the tab showing changed files.
2. Add a comment on a line in a file.
3. Explain why you need this change.
4. Use the **Add a suggestion** feature to propose
   an exact edit (GitHub provides a small editor that modifies the file in the
   suggestion).
5. Submit the comment.

### 3. Accept a suggestion and update your local repository

1. In the PR UI, accept the suggested change by clicking the **Apply suggestion**
   button. After you accept it, GitHub will add a new commit to the PR branch
   that applies the change.
2. Update your local branch with changes from the remote branch on GitHub:

   ```shell
   git fetch
   git pull
   ```

   or

   ```shell
   git pull origin <yourName>/docs/add-examples
   ```

   Expected: The changes from the suggestion are in your local file.

3. Check the repository history:

   ```shell
   git log
   ```

   Expected: The commit with the suggested change is in the repository history.

### 4. Add a comment

Some comments are not simple suggestions and require manual edits
The repo owner (instructor) follows these steps:

1. Add a comment on a different line asking the author to reword a sentence.
   Don't use the **Add a suggestion** feature.
2. Submit the comment.

### 5. Edit the file in the local repository

1. Open the file.
2. Apply the requested changes.
3. Add the file to the staging area:

   ```shell
   git add <filePath>
   ```

4. Commit and push it:

   ```shell
   git commit -m "docs: apply review feedback — clarify intro"
   git push
   ```

5. In the PR UI, go to the tab with commits.

   Expected: The commit with changes from the comment appears in commit history.

### 6. Approve

The repo owner (instructor) reviews and approves the PR on GitHub.

### 7. Merge

After the PR is approved and checks pass:

1. From the menu in the **Merge pull request** button pick the option that matches your workflow:
   - **Create a merge commit** - preserves the history
   - **Squash and merge** - rewrites the history by combining commits into one commit
   - **Rebase and merge** - rewrites the history by creating a linear timeline of commit
2. Click **Merge pull request**.

### 8. Update `main` in the local repository

1. Switch to `main` and pull the merged changes:

   ```shell
   git checkout main
   git pull
   ```

2. Check if the merged changes are present in `website/` files.

## Troubleshooting

### Conflicts prevent merge

GitHub will show a message and block merging if there are conflicts with the base branch.
To fix the issue:

1. Pull changes to your local the branch.
2. Resolve conflicts.
3. Commit and push. The PR will update automatically.

### Commit with a suggestion not pulled to the local repository

If the `git pull` operation didn't fetch the PR commit after you accepted a suggestion:

1. Ensure you pulled the PR branch (`git pull origin <yourName>/docs/add-examples`)
2. Ensure your local branch is tracking the correct remote branch.

### Someone else merged or force-pushed the branch

If your local branch diverged from the remote branch:

1. Fetch updates.
2. Either rebase or merge to reconcile.
3. Push changes.

### Approvals missing

1. Ensure the requested reviewers were added to the PR.
2. Ensure the reviewers approved the PR in the GitHub UI.

## Best practices

- Use the **Add a suggestion** feature for small edits. It keeps history clean
  and is easy to accept.
- If you must force-push, prefer `--force-with-lease` and warn reviewers.
- Leave clear PR descriptions and link to issues or tasks when relevant.
