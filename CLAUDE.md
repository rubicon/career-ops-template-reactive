# Agent Instructions

This is the canonical instruction file for AI coding agents working in this
repository. `AGENTS.md` is a pointer to this file.

## What this project is

career-ops-template-reactive is the reactive
[career-ops](https://github.com/santifer/career-ops) template pack: fifteen
ATS-strict CV and cover-letter theme pairs, ported from the Reactive Resume
designs and reimplemented as single-column, parser-safe HTML. See `README.md` for
the theme table and previews, and `ARCHITECTURE.md` for the layout. It is built
on the [template scaffold](https://github.com/rubicon/career-ops-template-template),
which owns the authoring guide and the design-lever taxonomy.

## What a template pack is

A pack is passive data: HTML templates, preview PNGs, and a `pack.json` manifest.
career-ops renders `cv.md` through a chosen template to produce a PDF or a cover
letter. Core never executes pack code; installing a pack copies template files
into a career-ops checkout. There is no runtime code here that career-ops runs.

## Non-negotiable invariants

- **ATS-safe templates.** Single column, system font stacks only (no
  `@font-face`, no webfonts), pt-only font sizes at or above 10pt, no images or
  tables or icons (the `{{PHOTO}}` slot is filled at generation time), ligatures
  disabled, and at most one grayscale-safe accent that never appears in body or
  bullet copy. `validate-template-pack.mjs` enforces this and runs in CI.
- **Placeholder completeness and meta agreement.** Each template fills the full
  slot set for its kind, and its `<!-- career-ops-template -->` meta `name:`
  equals the entry's `displayName` in `pack.json`.
- **Fifteen themes, each a unique coordinate.** No two templates share the
  `{face, axis, header}` triple; the validator enforces it. The taxonomy lives in
  the template scaffold's `docs/AUTHORING.md`.
- **Gazette is the only design-forward theme.** Its `atsRisk` is
  `design-forward` with a disclosure note; every other theme is `none`. Do not
  silently change a theme's risk tier.
- **Previews match templates.** Each theme ships a CV and a cover preview PNG at
  1224x1584. Regenerate them with `npm run previews` (after a one-time
  `npm run previews:setup`) whenever a template changes, so shipped equals tool
  output. They approximate the authoritative career-ops `generate-pdf.mjs`
  render, not pixel-for-pixel.
- **No personal data.** No real CV content in templates or previews.
- **The validator is the single source of truth.** Do not weaken a check to make
  a template pass; fix the template.

## Commands

- `npm run validate` runs the validator against `pack.json`.
- `npm test` runs the validator's unit tests (`node --test`).
- `npm run smoke` asserts this pack validates against its own manifest.
- `npm run previews:setup` installs Playwright + Chromium on demand (never saved
  as a dependency); `npm run previews` renders the preview PNGs from
  `sample-cv.json`. `test/previews-fill.test.mjs` (part of `npm test`) is the
  browser-free guard that the sample fills every template placeholder.
- `npm run format` / `npm run format:check` (Prettier). `templates/` is
  Prettier-ignored on purpose; the validator is their gate.

## Working conventions

- Conventional Commits; linted in CI. No AI-authorship trailers, no "Generated
  with" lines. No em-dashes, no emojis in code, comments, docs, commits, issues,
  or PRs. Use `--` for a dash separator.
- Each theme's cover letter reuses its CV masthead, face, accent, and density.
  Keep the accent out of body copy and letter furniture.
- Run `npm run validate`, `npm test`, and `npm run format:check` before opening a
  PR. When a template changes, regenerate the affected previews with
  `npm run previews` (scope with ids, e.g. `npm run previews ledger`) and commit
  the updated PNGs.
