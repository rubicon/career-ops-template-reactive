# career-ops-template-reactive

Fifteen ATS-strict CV and cover-letter theme pairs for
[career-ops](https://github.com/santifer/career-ops), ported from the Reactive
Resume template designs and reimplemented as single-column, parser-safe HTML.

[![CI](https://github.com/rubicon/career-ops-template-reactive/actions/workflows/ci.yaml/badge.svg)](https://github.com/rubicon/career-ops-template-reactive/actions/workflows/ci.yaml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## What this is

Each theme is a CV template and a matching cover-letter template that share a
masthead, face, accent, and density. Every template is single-column, uses system
font stacks only (no webfonts), carries no images, tables, or icons, and uses at
most one grayscale-safe accent that never appears in body or bullet copy. The
point is to pass ATS text extraction reliably while still reading as a designed,
distinct document. Fourteen themes are ATS-clean with no caveats; Gazette is
marked design-forward and carries an honest disclosure in its own header.

This pack is passive data. career-ops renders your `cv.md` through a chosen
template; it never executes anything here. It is built on the
[template scaffold](https://github.com/rubicon/career-ops-template-template),
which carries the authoring guide and the design-lever taxonomy behind these
choices.

## Install

Installing is copying the theme's two files into your career-ops checkout:

```bash
cp templates/cv-template.ledger.html            /path/to/career-ops/templates/
cp templates/cover-letter-template.ledger.html  /path/to/career-ops/templates/
```

career-ops discovers templates by filename convention and reads each file's own
`<!-- career-ops-template -->` meta block, then lists them when you generate a PDF
or a cover letter. Copy as many themes as you want to try.

## Themes

| Theme    | Origin    | Face         | Header treatment              | Accent                 | Register                     | ATS risk       |
| -------- | --------- | ------------ | ----------------------------- | ---------------------- | ---------------------------- | -------------- |
| Ledger   | rhyhorn   | Georgia      | full-width rule               | monochrome             | law / finance / academe      | none           |
| Slate    | onyx      | Helvetica    | full rule, heavy name rule    | monochrome             | engineering classic          | none           |
| Meridian | kakuna    | Georgia      | centered, flanked rules       | bronze (#7A5C1E)       | ceremonial / board / gov     | none           |
| Cadence  | meowth    | Helvetica    | uppercase letterspaced + rule | indigo (#33356B)       | modern corporate / tech mgmt | none           |
| Beacon   | scizor    | Trebuchet MS | page-top letterhead bar       | steel-blue (#2B4A63)   | consulting / strategy        | none           |
| Gazette  | bronzor   | Verdana      | left-gutter section labels    | monochrome             | editorial                    | design-forward |
| Tempo    | lapras    | Calibri      | short accent tab              | ocean-blue (#1E5F74)   | product / design-adjacent    | none           |
| Harbor   | glalie    | Cambria      | small-caps, text underline    | teal (#0F5E5E)         | calm senior professional     | none           |
| Fern     | chikorita | Tahoma       | small-caps + hairline         | forest (#2D5A27)       | scientific / methodical      | none           |
| Regent   | gengar    | Palatino     | small-caps, no rule           | plum (#5B2A5E)         | distinguished senior IC      | none           |
| Herald   | ditto     | Helvetica    | name-band over heavy rule     | burgundy (#6E1E2B)     | communications / sales       | none           |
| Compass  | ditgar    | Verdana      | uppercase, no rule            | slate-navy (#2C3E60)   | operations / logistics       | none           |
| Bastion  | leafish   | Calibri      | shaded header bars            | deep-pine (#1E4D40)    | structured enterprise        | none           |
| Laurel   | pikachu   | Times        | gold top hairline, small-caps | antique-gold (#806000) | prestige / legal / academia  | none           |
| Wayfarer | azurill   | Helvetica    | thin rules, left spine        | azure (#1B5E8A)        | program mgmt / journey       | none           |

Face names above are the design intent; each template ships a full system font
stack (for example Calibri renders through Carlito on Linux). Accent hex values
are recorded in `pack.json` with their measured white-background contrast, all at
or above 4.5:1, all still legible in grayscale.

Gazette is design-forward because its section labels sit in a left gutter. The
DOM order stays strictly linear (label then content), so linear-parsing ATS read
it correctly, but a minority of position-based parsers could misread the gutter.
A labels-above fallback is documented in the Gazette template header.

## Previews

Each theme, CV and cover letter. Full-size PNGs live in `templates/previews/`.

**Regenerate them** (after editing any template, or when adding a theme):

```bash
npm run previews:setup   # one-time: installs Playwright + Chromium (not saved as a dependency)
npm run previews         # renders every template in pack.json; pass ids to scope: npm run previews ledger
```

The previews are rendered from `sample-cv.json` (non-personal sample data) at 1224x1584. They **approximate** the authoritative career-ops render (`generate-pdf.mjs`, which uses `@page` margins and `preferCSSPageSize`); the script mimics the print margin with a screen-only padding rule, so the result is close, not pixel-for-pixel. Playwright is installed on demand and is never a dependency, so the pack stays passive data.

| Theme    | CV                                                 | Cover letter                                             |
| -------- | -------------------------------------------------- | -------------------------------------------------------- |
| Ledger   | ![Ledger CV](templates/previews/ledger-cv.png)     | ![Ledger cover](templates/previews/ledger-cover.png)     |
| Slate    | ![Slate CV](templates/previews/slate-cv.png)       | ![Slate cover](templates/previews/slate-cover.png)       |
| Meridian | ![Meridian CV](templates/previews/meridian-cv.png) | ![Meridian cover](templates/previews/meridian-cover.png) |
| Cadence  | ![Cadence CV](templates/previews/cadence-cv.png)   | ![Cadence cover](templates/previews/cadence-cover.png)   |
| Beacon   | ![Beacon CV](templates/previews/beacon-cv.png)     | ![Beacon cover](templates/previews/beacon-cover.png)     |
| Gazette  | ![Gazette CV](templates/previews/gazette-cv.png)   | ![Gazette cover](templates/previews/gazette-cover.png)   |
| Tempo    | ![Tempo CV](templates/previews/tempo-cv.png)       | ![Tempo cover](templates/previews/tempo-cover.png)       |
| Harbor   | ![Harbor CV](templates/previews/harbor-cv.png)     | ![Harbor cover](templates/previews/harbor-cover.png)     |
| Fern     | ![Fern CV](templates/previews/fern-cv.png)         | ![Fern cover](templates/previews/fern-cover.png)         |
| Regent   | ![Regent CV](templates/previews/regent-cv.png)     | ![Regent cover](templates/previews/regent-cover.png)     |
| Herald   | ![Herald CV](templates/previews/herald-cv.png)     | ![Herald cover](templates/previews/herald-cover.png)     |
| Compass  | ![Compass CV](templates/previews/compass-cv.png)   | ![Compass cover](templates/previews/compass-cover.png)   |
| Bastion  | ![Bastion CV](templates/previews/bastion-cv.png)   | ![Bastion cover](templates/previews/bastion-cover.png)   |
| Laurel   | ![Laurel CV](templates/previews/laurel-cv.png)     | ![Laurel cover](templates/previews/laurel-cover.png)     |
| Wayfarer | ![Wayfarer CV](templates/previews/wayfarer-cv.png) | ![Wayfarer cover](templates/previews/wayfarer-cover.png) |

## Validate

```bash
npm install        # dev tooling only (Prettier, commitlint); the pack has no runtime dependencies
npm run validate   # shape, ATS, and render checks against pack.json
npm test           # the validator's unit tests
npm run smoke      # the pack must validate against its own manifest
npm run format:check
```

## License

MIT. See [LICENSE](LICENSE). The theme designs are derived from
[Reactive Resume](https://github.com/amruthpillai/reactive-resume) by Amruth
Pillai (MIT); the templates here are independent, ATS-safe reimplementations.

## Contributors

![Contributors](https://contrib.rocks/image?repo=rubicon/career-ops-template-reactive)
