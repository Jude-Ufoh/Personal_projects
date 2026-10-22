# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A collection of small, independent web projects. Each project is a single self-contained HTML file (inline CSS and JS, no build step, no dependencies, no tests). To run one, open the file directly in a browser. The only external resource is Google Fonts.

- `tic-tac-toe/index.html`: tic-tac-toe vs. computer (Easy / Unbeatable) or 2 players
- `calculator.html`: desk calculator with keyboard support
- `prompts.docx`: notes and prompts used to create these projects (Word file, published publicly on purpose)

`README.md` has a table listing every project and how to open it. Add a row when you add a project.

## Conventions shared across projects

- **Theming**: colors are CSS custom properties on `:root`, overridden for dark mode both under `@media (prefers-color-scheme: dark)` (guarded by `:root:not([data-theme="light"])`) and under `:root[data-theme="dark"]`. Keep both dark blocks in sync when changing a palette.
- Mobile-safe layout: side padding is `max(16px, env(safe-area-inset-*))`, and `prefers-reduced-motion` turns animations off.
- A one-line `/* Layout: ... */` comment at the top of the `<style>` block describes the page's visual concept.
- Each file is a single page with no modules: keep new code inline in the same file.

## Project notes

**Tic-tac-toe** (`tic-tac-toe/index.html`): all logic is in one IIFE. The human is always X and the computer is O. "Unbeatable" uses full minimax (depth-weighted scores, random corner/center opening on an empty board). "Easy" takes an obvious win or block 50% of the time, otherwise moves at random. Mode, level, scores and who starts next are saved to `localStorage` under key `ttt`. Changing mode or level resets scores. The starting player alternates each round. Marks and the winning strike are SVG paths animated with `stroke-dasharray` using a `--len` custom property.

**Calculator** (`calculator.html`): this is an HTML fragment (no `<!doctype>`, `<html>` or `<head>`), written in Claude Artifact style. Browsers render it fine. State is held in the globals `acc`, `op`, `cur`, `fresh` and `error`. On load the state is pre-filled with an example (`128 × 12`) rather than `0`. Values are formatted to 12 significant digits and switch to exponential notation outside that range. Keyboard input is mapped to button ids through `KEYMAP` and replayed as clicks on those buttons, so on-screen keys and keyboard share one code path.

## Git workflow

The remote is `origin` → https://github.com/Jude-Ufoh/Personal_projects (public), branch `main`. After every meaningful change, make a focused commit and push. Word lock files (`~$*`) are gitignored.
