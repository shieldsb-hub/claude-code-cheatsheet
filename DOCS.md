# Full Docs — Claude Code with GitHub

A deeper, written-out version of the cheatsheet website. If `index.html` is the poster, this is the manual.

## Table of contents

1. [What is Claude Code?](#1-what-is-claude-code)
2. [Installation](#2-installation)
3. [Your first session](#3-your-first-session)
4. [How to talk to Claude](#4-how-to-talk-to-claude)
5. [Slash commands reference](#5-slash-commands-reference)
6. [GitHub one-time setup](#6-github-one-time-setup)
7. [The everyday flow: change → commit → push](#7-the-everyday-flow)
8. [Branches and pull requests](#8-branches-and-pull-requests)
9. [Starting a brand-new project](#9-starting-a-brand-new-project)
10. [Common phrases that just work](#10-common-phrases-that-just-work)
11. [Recovering from mistakes](#11-recovering-from-mistakes)
12. [Safety rules](#12-safety-rules)
13. [Troubleshooting](#13-troubleshooting)

---

## 1. What is Claude Code?

Claude Code is Anthropic's official command-line AI coding assistant. You run `claude` in any folder and chat with it in plain English. It can:

- Read your files and explain them
- Edit code directly
- Run shell commands (with your permission)
- Use `git` and the GitHub CLI (`gh`) to commit, push, open PRs, and review code
- Run tests and debug failures

Think of it as a teammate who lives in your terminal and has read your whole project.

## 2. Installation

**Requirements:** Node.js 18+ and a terminal.

```bash
npm install -g @anthropic-ai/claude-code
```

Verify:

```bash
claude --version
```

The first time you run `claude`, it'll prompt you to log in via a browser link. Anthropic API access is required (free tier or paid plan).

## 3. Your first session

```bash
cd ~/Desktop/some-project
claude
```

You'll see a prompt. Type a question:

```
> what does this project do?
```

Claude reads the relevant files and answers. Press `Esc` any time to interrupt. Type `/exit` or `Ctrl+D` to quit.

## 4. How to talk to Claude

Claude is good — but specific prompts get specific results.

### Bad

```
> fix the bug
> make it better
> help
```

### Good

```
> the login button on index.html doesn't redirect
   after click — find and fix it

> refactor the user controller to use async/await
   instead of callbacks; don't change the API

> add a dark mode toggle to the header that
   persists in localStorage
```

### Patterns that work

- **Name the file** if you know it: *"in `app.js`, the function `loadUsers` is..."*
- **Describe the symptom**, not the fix: *"the page is blank when I refresh"* beats *"add a useEffect"*
- **Set scope explicitly**: *"only change `header.tsx`, leave the other files alone"*
- **Ask for review first**: *"plan the change before writing any code"*

## 5. Slash commands reference

Type these into the Claude prompt:

| Command           | What it does                                                  |
|-------------------|---------------------------------------------------------------|
| `/help`           | Show all available commands                                   |
| `/clear`          | Wipe the current conversation; start fresh                    |
| `/init`           | Generate a `CLAUDE.md` memory file describing the codebase    |
| `/review`         | Code-review the current uncommitted changes                   |
| `/config`         | Open the settings UI                                          |
| `/model`          | Switch model (e.g. Opus ↔ Sonnet)                             |
| `/exit`           | Quit                                                          |

## 6. GitHub one-time setup

You only do this once per machine.

### Install the GitHub CLI

```bash
brew install gh           # macOS
sudo apt install gh       # Debian/Ubuntu
winget install gh         # Windows
```

### Log in

```bash
gh auth login
```

Pick **GitHub.com**, **HTTPS**, **Login with a web browser**. Follow the link, paste the one-time code.

### Configure git identity

```bash
git config --global user.name "Your Name"
git config --global user.email "you@email.com"
```

### Verify

```bash
gh auth status
git config --global --get user.email
```

You should see `✓ Logged in to github.com`.

## 7. The everyday flow

This is the loop. Once it clicks, you'll do it dozens of times a day.

### Step 1 — Make a change

```
> add a section to README.md explaining how to deploy
```

Claude edits the file. It will show you the diff.

### Step 2 — See what changed

```
> what changed?
```

Claude runs `git status` and `git diff` and explains them.

### Step 3 — Commit

```
> commit this
```

Claude:
1. Reads the diff
2. Drafts a conventional commit message
3. **Shows it to you for approval**
4. Runs `git add` + `git commit`

You can also say *"commit with message 'docs: add deploy section'"* to override the message.

### Step 4 — Push

```
> push
```

If the branch already tracks a remote, it just runs `git push`. If not, it runs `git push -u origin <branch>` to set the upstream.

### Step 5 — Repeat

That's it. Most days are: change → commit → push, change → commit → push.

## 8. Branches and pull requests

For anything bigger than a typo, use a branch.

```
> create a branch called feature/dark-mode and switch to it
```

Make changes, commit, push. Then:

```
> open a pull request to main with a clear title
   and bullet-point description of what changed
```

Claude runs `gh pr create` with the title and body it drafted (showing you first).

To review existing PRs:

```
> list open PRs
> review PR #42
> what's the status of PR #42 (checks, reviews)?
```

## 9. Starting a brand-new project

```bash
mkdir my-cool-app && cd my-cool-app
claude
```

Then in one prompt:

```
> initialize a git repo, build me a simple landing
   page with HTML/CSS, then create a public github
   repo called "my-cool-app" and push it
```

Claude will:
1. `git init`
2. Write the files
3. `git add` + first commit
4. `gh repo create my-cool-app --public --source=. --push`

Done. Repo is live.

## 10. Common phrases that just work

| Say to Claude                              | What it runs                                  |
|--------------------------------------------|-----------------------------------------------|
| show changes                               | `git status` + `git diff`                     |
| commit this                                | `git add` + `git commit -m "..."`             |
| push                                       | `git push` (or `git push -u origin HEAD`)     |
| pull latest                                | `git pull --rebase`                           |
| make a branch called X                     | `git checkout -b X`                           |
| switch to main                             | `git checkout main`                           |
| open a PR                                  | `gh pr create`                                |
| list PRs                                   | `gh pr list`                                  |
| undo my last commit (keep changes)         | `git reset --soft HEAD~1`                     |
| stash my changes                           | `git stash`                                   |
| what's on this branch?                     | `git log main..HEAD`                          |
| who changed this line?                     | `git blame`                                   |

## 11. Recovering from mistakes

Claude is great at undo. Just describe what happened.

```
> I committed the wrong file — undo the last commit
   but keep my changes

> I accidentally rm'd app.js — can you restore it
   from git?

> I want to throw away all my uncommitted changes
   in src/components/header.tsx
```

For destructive operations, Claude will **always** show you the command and ask before running.

## 12. Safety rules

1. **Read commands before approving them.** Especially anything with `rm`, `--force`, `reset --hard`, or `push -f`.
2. **Commit small, commit often.** Easier to undo five small commits than one giant one.
3. **Use branches for non-trivial work.** `main` should always be deployable.
4. **Never paste secrets** (API keys, passwords, tokens) into the chat. Use environment variables and `.env` files (gitignored).
5. **Don't `git add .` blindly.** Check what's staged. `.env` files and `node_modules` should never be committed.
6. **Pull before you push** if working with others, to avoid merge conflicts.

## 13. Troubleshooting

**`claude: command not found`**
Re-run `npm install -g @anthropic-ai/claude-code`. If using nvm, make sure you're on the right Node version.

**`gh: authentication required`**
Run `gh auth login` and pick HTTPS.

**`Permission denied (publickey)`**
You're using SSH but haven't set up keys. Easiest fix: `gh auth login` and choose HTTPS instead. Run `gh auth setup-git` to make git use the gh credential helper.

**Claude won't run a command**
By default, Claude asks before running anything. Approve it, or tweak permissions in `/config`.

**Pre-commit hook is blocking my commit**
Don't bypass with `--no-verify`. Read what the hook is complaining about — it's usually a lint/format issue Claude can fix in seconds.

---

## Where to go next

- Official docs: [docs.claude.com/claude-code](https://docs.claude.com/claude-code)
- GitHub CLI manual: [cli.github.com/manual](https://cli.github.com/manual)
- git basics: [git-scm.com/book](https://git-scm.com/book)

When in doubt — just ask Claude. It can read these docs too.
