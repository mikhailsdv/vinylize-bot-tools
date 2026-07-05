# AGENTS.md

## Project Context

This repository contains a GitHub Pages site with tools for working with `@VinylizeBot`, a Telegram bot for creating vinyl-style circle videos.

The site currently has two tools: a UTM link generator for `@VinylizeBot` and a brandbook text formatter. The main `public/index.html` page is a navigation menu, and tools live in separate static HTML files with semantic names.

## Deployment

The project is deployed to GitHub Pages from the `public` directory.

Deployment is configured in `.github/workflows/deploy-pages.yml` and runs on pushes to `main` or manually via `workflow_dispatch`.

## Current App Behavior

`public/utm-link-generator.html` builds Telegram bot start links in this format:

```text
https://t.me/VinylizeBot?start=s_<utm_source>_m_<utm_medium>_c_<utm_campaign>
```

The generator accepts `utm_source`, `utm_medium`, and `utm_campaign`.

Input values are lowercased and limited to Latin lowercase letters, digits, and hyphens. Underscores are rejected with a visible error because the generated start payload itself uses underscores as separators.

The Telegram start payload length limit is treated as 64 characters.

`public/text-brandbook-formatter.html` formats pasted text in-place and then switches to a read-only copy mode. It supports Telegram and Instagram modes; Instagram mode separates paragraphs with the invisible space character `⠀`.

The text formatter applies the current brandbook rules: trim each line, collapse repeated spaces and extra blank lines, remove final periods from paragraphs and bullet items, use non-breaking spaces before emoji and around short function words where appropriate, use a regular space after emoji when text follows, reject two or more consecutive emoji even with spaces between them during validation, remove periods after emoji, add missing spaces after punctuation, use non-breaking hyphens inside compounds, normalize long dashes to `–`, avoid `ё` except preserved cases like `её` and `всё`, and convert quotes to `«елочки»`.

## Project Shape

There is no build step, package manager setup, or framework in the current project. Keep changes compatible with a static GitHub Pages deployment unless the user explicitly asks to introduce tooling.

## Agent Notes

Keep changes narrowly scoped to the user's request.

Do not reformat unrelated code.

Update this `AGENTS.md` when important project details appear in conversation or when current guidance in this file changes.
