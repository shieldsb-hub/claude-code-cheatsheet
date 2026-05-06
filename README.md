# Claude Code Cheatsheet

A single-page, beginner-friendly website that teaches the basics of using **Claude Code** with **GitHub** — install, talk to Claude, commit, push, and open pull requests.

Built as a one-file static site: just open `index.html` in a browser.

![Made with HTML](https://img.shields.io/badge/made%20with-HTML%20%26%20CSS-d97757)
![No build step](https://img.shields.io/badge/build%20step-none-7ec699)
![License](https://img.shields.io/badge/license-MIT-blue)

---

## Quick start

```bash
git clone https://github.com/<your-username>/claude-code-cheatsheet.git
cd claude-code-cheatsheet
open index.html        # macOS
# or just double-click index.html
```

That's it. No npm install, no build, no server.

## What's inside

| File              | Purpose                                                    |
|-------------------|------------------------------------------------------------|
| `index.html`      | The full single-page website (HTML + inline CSS)           |
| `DOCS.md`         | Full markdown reference — same content, deeper examples    |
| `README.md`       | This file                                                  |
| `CLAUDE.md`       | Project memory loaded by Claude Code in every session      |
| `CONTRIBUTING.md` | How to propose changes                                     |
| `CHANGELOG.md`    | User-visible change history                                |
| `LICENSE`         | MIT                                                        |

## What it covers

1. **What Claude Code is** — and how to install it (`npm install -g @anthropic-ai/claude-code`)
2. **Talking to Claude** — vague vs. specific prompts, useful slash commands
3. **One-time GitHub setup** — `gh auth login` and `git config`
4. **The everyday flow** — change → commit → push → open a PR, all by chatting
5. **Starting a brand-new project** from an empty folder
6. **A 10-second cheatsheet** of common phrases
7. **Safety rules** — branches, secrets, reading commands before running them

## Design notes

- Single HTML file, no external dependencies
- Anthropic-style dark theme with the signature orange accent (`#d97757`)
- Mobile-responsive (stacks to one column under 640px)
- Monospace code blocks with simple syntax highlighting
- All CSS is inline — easy to fork and customize

## Customizing

Open `index.html` in any editor. The CSS variables at the top of the `<style>` block control colors:

```css
:root {
  --bg: #0f0f10;
  --panel: #17171a;
  --accent: #d97757;   /* change me */
  --text: #ececec;
  /* ... */
}
```

Change `--accent` to recolor the entire site. Section content lives in clearly-labeled `<section>` blocks below.

## Contributing

Spotted a typo or want to add a tip? PRs welcome.

```bash
git checkout -b fix/your-thing
# edit index.html or DOCS.md
git commit -am "fix: short description"
git push -u origin fix/your-thing
gh pr create
```

Or — easier — open Claude Code in this folder and say *"fix the typo in section 3"*. It'll do all of the above for you.

## License

MIT — do whatever you want with it.
