# Contributing

Thanks for considering a contribution! This project is small on purpose, but typo fixes, clarifications, and tip improvements are very welcome.

## Quick fixes (typos, small wording)

The fastest path:

1. Fork the repo on GitHub
2. Edit `index.html` or `DOCS.md` directly in the GitHub web editor
3. Submit a PR

## Local changes

```bash
git clone https://github.com/<you>/claude-code-cheatsheet.git
cd claude-code-cheatsheet
git checkout -b fix/short-description

# edit files
open index.html        # preview in browser

git commit -am "fix: describe the change"
git push -u origin fix/short-description
gh pr create
```

Or — easier — open Claude Code in the repo and say *"fix the typo in section 3"*. Claude will branch, edit, commit, push, and open the PR for you. (Yes, this is a project about Claude Code; we use it on itself.)

## What we accept

✅ **Likely to merge:**
- Typo and grammar fixes
- Clarifying confusing wording
- Updating commands/links that have gone stale
- New tips that are genuinely beginner-friendly and short
- Accessibility improvements (semantic HTML, contrast, alt text)

🤔 **Open an issue first:**
- New sections (we may have already decided not to include the topic)
- Visual redesigns
- Adding any kind of build step, framework, or external dependency

🚫 **Probably won't merge:**
- Tracking scripts or analytics
- Advanced topics aimed at power users (subagents, hooks, custom skills, MCP setup) — those belong in `DOCS.md`, if anywhere
- Refactoring the inline CSS into separate files
- Adding a JavaScript framework

## Style

- Match the existing tone: friendly, terse, practical.
- Don't add emoji unless it's already established in the surrounding section.
- Code examples should be runnable as-is.
- If you add to `index.html`, mirror the same content in `DOCS.md` (and vice versa).
- Update `CHANGELOG.md` for user-visible changes.

## Local preview

No build step. Just open `index.html` in a browser. Refresh after edits.

## Code of conduct

Be kind. Assume good intent. We're all beginners at something.
