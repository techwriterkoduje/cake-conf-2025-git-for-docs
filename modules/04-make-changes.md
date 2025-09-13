# Make changes in your branch

For this exercise we'll follow a branch naming convention that makes ownership
explicit: `username/some-descriptive-name`. Use your own username for the prefix
so it's easy to spot who created the branch.

For the walkthrough below, use this branch name:

```
yourname/docs/add-examples
```

Replace `yourname` with your username and run:

```
git switch -c yourname/docs/add-examples
```

This creates and checks out the branch.

## Deliberate conflict setup

We'll make a couple of edits that will cause a conflict later when someone else
changes the same lines on the main branch. First, change the header in
`intro.md` (this is our deliberate conflict):

Open `intro.md` and change the top-level header to something obvious, for
example:

```
# Introduction to HomeSphere by <YOUR NAME>
```

Save the file and then check your status and diffs:

```
git status
git diff
git diff --staged
```

> **Aside:** Keep forgetting to save? You can set VS Code to auto-save your
> changes. Go to **File > Preferences > Settings**, search for "Auto Save", and
> set it to "afterDelay".

You should see the change in the unstaged diff. Now stage and observe the status
again:

```
git add get-your-hands-dirty/intro.md
git status
git diff --staged
```

---

### Aside: commit message conventions

Before you write your first commit message, a short note on conventions. Clear
messages make history useful. A common convention used by teams is:

```
<type>(scope?): short summary

optional longer description
```

Common `type` values: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`. For
example:

```
docs(intro): clarify workshop purpose
```

Keep the first line under ~72 characters and use the body for details when
needed.

---

Now commit the change:

```
git commit -m "edit: update intro header for conflict demo"
git status
```

If you make new changes now, remember to add them again before committing.

## Multiple edits and staging behavior

Next, edit `style-guide.md` and add a new H2 near the top. For example, add:

```
## New guidance: Accessibility first

Add a short sentence about headings and accessibility.
```

Check status — you should see the file as modified but unstaged:

```
git status
```

Now make another change to the same `style-guide.md` file (a second, different
edit) — for example add another paragraph lower down. Check status again; the
file is still unstaged because you haven't added it yet.

```
git status
```

Stage the file and commit both changes together:

```
git add get-your-hands-dirty/style-guide.md
git status
git commit -m "docs: add accessibility guidance and extra note"
```

Push your branch to the remote and set the upstream:

```
git push --set-upstream origin yourname/docs/add-examples
```

## Amend the last commit and force-push

Now, if you notice a typo in your last commit message or want to add a small
change to the same commit, make the change (edit a file), stage it, then run:

```
git add <file>
git commit --amend --no-edit
```

`--no-edit` keeps the same commit message; omit it if you want to edit the
message.

Because you've already pushed the original commit, you'll need to force-push the
amended commit to update the remote branch:

```
git push --force
```

Note: force-pushing rewrites history on the remote branch. It's okay on a
feature branch that only you are working on, but coordinate with others if
anyone else might have based work on your branch.

## Final checks

Run these commands to confirm the state:

```
git status
git log --oneline --decorate --graph --all -n 10
git branch -vv
```

You should see your branch, your commits, and the remote tracking information.

## Exercise summary

- Create `yourname/docs/add-examples` and switch to it.
- Edit `intro.md` (header) and `style-guide.md` (add H2 + another change).
- Use `git status`, `git diff`, `git add`, `git commit`, `git push` as shown.
- Amend the last commit and force-push.

Expected: you will have a published feature branch with several commits; one
amended commit will be force-pushed.
