# Architecture

career-ops-template-reactive is sixteen ATS-strict CV and cover-letter theme
pairs for career-ops. A pack is passive data that career-ops renders `cv.md`
through; there is no runtime code here that career-ops executes. The pack is built
on the [template scaffold](https://github.com/rubicon/career-ops-template-template),
which owns the authoring guide and the design-lever taxonomy.

## Layout

```text
career-ops-template-reactive/
  pack.json                          # the manifest: 16 template entries with levers, accent, attribution
  templates/
    cv-template.<theme>.html         # 16 CV templates
    cover-letter-template.<theme>.html   # 16 matching cover-letter templates
    previews/
      <theme>-cv.png                 # 32 render previews, 1224x1584
      <theme>-cover.png
  validate-template-pack.mjs         # the dependency-free pack validator (vendored from the scaffold)
  test/
    validate.test.mjs                # the validator's unit tests (node --test)
    smoke.mjs                        # self-check: this pack validates against its own manifest
```

The sixteen themes are Ledger, Slate, Meridian, Cadence, Beacon, Gazette, Tempo,
Harbor, Fern, Regent, Herald, Compass, Bastion, Laurel, Wayfarer, and Ember.

## One coordinate per theme

Each theme occupies a unique point in the design-lever taxonomy: a face class, an
alignment axis, and a header treatment. The validator rejects any two templates
that share the `{face, axis, header}` triple, which is what keeps sixteen
single-column, parser-safe templates visibly distinct. Accent hue and density
vary too, but they are texture, not the thing that separates one theme from
another. The taxonomy and the reasoning behind each port live in the scaffold's
`docs/AUTHORING.md`.

## The naming contract

The link to career-ops is a filename convention: a CV template is
`cv-template.<id>.html` and a cover template is
`cover-letter-template.<id>.html`. career-ops discovers templates by that
convention and reads each file's own `<!-- career-ops-template -->` meta block, so
installing a theme is copying its two files, with zero core changes.

## The validator

`validate-template-pack.mjs` is vendored unchanged from the scaffold and is the
single source of truth for what the pack must satisfy: `pack.json` shape, unique
lever coordinates, per-accent contrast, and the per-file ATS and render contract.
It has no dependencies and runs in CI. `test/validate.test.mjs` covers it;
`test/smoke.mjs` runs it against this repo's own pack.

## Cover letters

Every theme's cover letter reuses its CV masthead, face, accent, and density, so
the letter reads as a visual match to the resume. Structural moments (dateline,
greeting, closing) carry the theme's header and rule treatment; the accent stays
out of body copy and letter furniture. Four themes carry a distinct letter device
(Beacon's page-top band, Gazette's gutter discipline, Wayfarer's border-left
spine, Tempo's accent tab); the rest derive purely from their CV levers.

## Why templates are Prettier-ignored

The templates are validated data artifacts with a strict render contract. The
pack validator is their gate, not Prettier. Keeping `templates/` out of Prettier
avoids reflow churn and any risk of a formatter altering a template in a way that
changes the rendered PDF.
