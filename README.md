# usu-slides

A Quarto extension for lecture slides in one source and three outputs:

| Format | Output | Look |
|---|---|---|
| `usu-slides-revealjs` | HTML deck | navy / gold theme (`slides.scss`), embedded resources |
| `usu-slides-beamer` | PDF deck | Metropolis, 16:9, 10pt, Fira Sans / Fira Mono, navy title page and part dividers |
| `usu-slides-typst` | PDF handout | US letter, 1in margins, table of contents |

The palette is midnight `#1B2A4A`, off-white `#F7F4EF`, slate blue `#2E5FA3`, gold `#C8962E`.

## Install

In the folder that holds your `.qmd` decks (or at a Quarto project root):

```
quarto add broughtj/quarto-usu-slides
```

Or start a new deck from the template, which also installs the extension:

```
quarto use template broughtj/quarto-usu-slides
```

## Use

```yaml
---
title: "Futures Market Mechanics"
subtitle: "Hull, Chapter 2"
author: "Tyler J. Brough"
institute: |
  DATA 5695 / 6695\
  Data Analytics & Information Systems, Utah State University
date: "September 2026"
format:
  usu-slides-revealjs:
    output-file: ch02-futures-mechanics.html
  usu-slides-beamer:
    output-file: ch02-futures-mechanics-beamer.pdf
  usu-slides-typst:
    output-file: ch02-futures-mechanics-handout.pdf
---
```

```
quarto render deck.qmd --to usu-slides-beamer     # one format
quarto render deck.qmd                            # all three
```

`output-file` is set per format because Beamer and Typst would otherwise both write `deck.pdf`.

Level-1 headings (`# Part I: ... {background-color="#1B2A4A"}`) become navy standout
frames in Beamer and navy slides in HTML. Everything else is ordinary Quarto: `.columns`,
`.fragment`, callouts with `appearance="minimal" icon="false"`, pipe tables, fenced code,
math. See `template.qmd` for the constructs that survive all three converters.

## Requirements

- Quarto 1.5 or later (Typst is bundled).
- A TeX distribution with LuaLaTeX and the Metropolis Beamer theme (TeX Live full, or
  `tlmgr install beamertheme-metropolis pgfopts`).
- Fira Sans and Fira Mono installed as system fonts. On macOS with Homebrew:
  `brew install --cask font-fira-sans font-fira-mono`. Without them LuaLaTeX falls back to
  another sans font and warns.

## Layout

```
_extensions/usu-slides/
  _extension.yml       format defaults for the three outputs
  slides.scss          revealjs theme
  beamer-header.tex    Beamer palette, navy title page, standout part frames
template.qmd           starter deck
```

To change the theme, edit the files in `_extensions/usu-slides/` here and run
`quarto update broughtj/quarto-usu-slides` in each folder that uses it.
