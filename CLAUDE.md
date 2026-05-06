# CLAUDE.md

Project memory for the **claude-code-cheatsheet** repo. Loaded automatically at the start of every Claude Code session.

## What this project is

A single-page static site that teaches Claude Code basics to beginners, with a focus on the everyday GitHub flow.

- Audience: people brand-new to Claude Code and/or git
- Tone: friendly, terse, practical — *not* corporate
- Scope: deliberately small. Don't bloat with advanced features that overwhelm beginners

## Stack

- **`index.html`** — the website. Plain HTML + inline CSS, no build step, no JS framework.
- **`README.md`** — project intro and quick start
- **`DOCS.md`** — long-form companion manual (same content as the site, expanded)
- **`CHANGELOG.md`** — change history
- No package.json, no node_modules, no bundler. Keep it that way.

## Conventions

- **HTML/CSS only.** Don't introduce JavaScript, frameworks, or a build step unless we explicitly decide to.
- **Inline CSS.** All styles live in the `<style>` block at the top of `index.html`. Don't extract to a separate file.
- **Anthropic palette.** Accent color is `#d97757` (orange). Background is dark (`#0f0f10`). The CSS variables at the top of the `<style>` block are the source of truth — change them, don't override inline.
- **Mobile-responsive.** Test at <640px (single column).
- **Code blocks** use `<pre class="code">` with `<span>` classes (`prompt`, `comment`, `string`, `keyword`, `you`) for highlighting. Don't add a syntax highlighter library.

## Content rules

- Beginner-first. If a tip needs a paragraph of context, it probably belongs in `DOCS.md`, not `index.html`.
- Numbered sections in the website map to numbered sections in `DOCS.md`. When you add to one, mirror it in the other.
- Keep the **TL;DR cheatsheet table** (section 6 of the site) tight — it's meant to be screenshot-able.

## Workflow

- `main` is the only branch by default; small fixes commit straight to it.
- For anything bigger than a typo, branch: `git checkout -b feature/<thing>`, then PR.
- Use the GitHub CLI (`gh`) for repo operations — it's already set up.
- GitHub Pages auto-deploys from `main` root. Live URL: https://shieldsb-hub.github.io/claude-code-cheatsheet/
- Update `CHANGELOG.md` when adding a new section or making user-visible content changes. Skip for typos and internal cleanups.

## What NOT to do

- Don't add tracking, analytics, or external scripts.
- Don't add advanced topics (subagents, hooks, custom skills, MCP) to `index.html` — they belong in `DOCS.md` if anywhere.
- Don't bury the GitHub flow under feature creep. The whole point is "first day with Claude Code."
- Don't rewrite working sections to "improve" them without a specific reason — small, targeted edits.
