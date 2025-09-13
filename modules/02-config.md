# Configuring Git

Git stores several pieces of personal and behavior information in a
configuration file. The most important for day-to-day work are your name and
email (they become part of each commit), your preferred editor, and some
convenience settings like autocorrect.

This module shows the basic commands to set those up and how to inspect or edit
your configuration.

## Where config lives

Git has three levels of configuration:

- System: applies to every user on the machine.
- Global: applies to your user account. Stored in `~/.gitconfig`.
- Local: applies only to a single repository. Stored in `.git/config`.

Most people use the `--global` flag to set personal preferences once.

## Set your name and email (please do this)

Your name and email are recorded in each commit. Without them, commits will look
anonymous or broken. Set them once with `--global`:

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Verify the values:

```
git config --global user.name
git config --global user.email
```

Or list all global settings:

```
git config --global --list
```

If you need to override name/email for a particular repo, run the same commands
without `--global` from inside that repo.

## Set the editor (we use VS Code)

Git will sometimes open an editor for you (for commit messages, merge messages,
rebase, etc). Set yours to VS Code so these prompts open a familiar UI:

```
git config --global core.editor "code --wait"
```

The `--wait` flag tells VS Code to hold the editor process open until you finish
editing the file; Git waits for that to continue. Test it quickly by running
`git commit` in a repo with staged changes — your editor should open.

## Autocorrect (what it does and how to set it up)

Git can autocorrect mistyped commands with a short delay. This is handy but can
surprise you. The setting is `help.autocorrect` and its value is a number of
tenths of a second to wait before executing the suggested command. Example:

```
git config --global help.autocorrect 50
```

This will wait 5.0 seconds (50 tenths) before running the closest match. Set it
to `0` to disable, or to a small number like `10` (1 second) if you want shorter
waits.

A quick demo:

```
git st
```

If autocorrect finds `git status` as the closest match, Git will display the
correction and, after the configured delay, run `git status`.

If you prefer more explicit behavior, don't enable autocorrect.

## Manage config: list, unset, edit

- List settings (local): `git config --list`
- List global settings: `git config --global --list`
- Read a single value: `git config <key>` or `git config --global <key>`
- Unset a value: `git config --global --unset <key>`
- Edit the config file directly (global): `git config --global --edit`

Editing lets you remove or tweak settings by hand; use it when the value is
complex or you want comments.

## Verify your configuration

Run these quick checks to confirm common settings:

```
git config --global user.name
git config --global user.email
git config --global core.editor
git config --global help.autocorrect
```

If a value returns nothing, it's not set at that level. Check local settings
with the same commands without `--global`.

## Troubleshooting

- If `code` isn't found when setting the editor, ensure VS Code is installed and
  its `code` CLI is on your PATH (open the Command Palette in VS Code and run
  "Shell Command: Install 'code' command in PATH").
- If `git config --global --edit` opens a different editor, check `core.editor`
  and `GIT_EDITOR` environment variables.
- If unset doesn't work, check whether the value is defined at the local or
  system level and unset it there (remove `--global` or add `--system`).

## Exercise (try it)

1. Set your name and email:

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

2. Set VS Code as your editor:

```
git config --global core.editor "code --wait"
```

3. Enable a gentle autocorrect (optional):

```
git config --global help.autocorrect 10
```

4. Verify everything:

```
git config --global --list
```

Expected: your name, email, `core.editor=code --wait` and the `help.autocorrect`
value appear in the list.
