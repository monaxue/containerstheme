# Containers Theme

A Quarto Reveal.js extension that provides styled card-based presentations with rounded corners, tabsets, and background color persistence.

## Example Slides

```markdown
---
title: Container Theme
subtitle: Mona Xue
format:
  containerstheme-revealjs:
    center: true
    touch: true
    incremental: true
    smaller: true
    chalkboard:
      theme: whiteboard
    preview-links: true
    title-slide-attributes:
        data-state: "hide-menubar"
        data-background-color: "rgba(237, 251, 255, 1)"
    transition: slide
    section-divs: false
    menu: false
    simplemenu:
      flat: true
      barhtml:
        header: "<div class='menubar'><ul class='menu'></ul></div>"
      scale: 0.70
revealjs-plugins:
    - tabset
    - simplemenu
---

# Some Lists {data-stack-name="Some Lists"}

## Incremental lists

- These
    - are 
        1. some
        1. incremental
- lists

## Nonincremntal lists {background-color="rgba(255, 237, 228, 1)"}

::: {.nonincremental}

1. These lists
    1. are
    1. nonincremental
1. A new background color is set using
    - {background-color="color-of-choice"}
    - Otherwise, it inherits the background color of the previous slide

:::

# Panels and Columns {data-stack-name="Panels and Columns" background-color="rgba(255, 251, 228, 1)"}

## Panel tabset 

:::::: {.panel-tabset}

## Tab 1

- This is tab 1
- With a normal list

## Tab 2

1. This is tab 2
1. With a numbered list

::::::

## Centered slide {.center}

::: card-list-center

- Some centered cards!
    - Inner cards!
- Next line!

:::

## Columns {background-color="rgba(254, 248, 237, 1)"}


:::::: columns

::::: {.column width = "33%" .nonincremental}

- Item 1
    - Item 2
- Item 3
    - Item 4

:::::

::::: {.column width = "33%"}

1. Item 1
    1. Item 2

:::::

::::: {.column width = "33%"}


- [ ] Item 1
    - [ ] Item 2
- [ ] Item 3

:::::

::::::

# Thanks! {data-stack-name="Thanks!"}

::: {.card-list-center .nonincremental}
- You can find more information about this theme at <https://github.com/monaxue/>
- For information about the header menu, see <https://github.com/Martinomagnifico/quarto-simplemenu>
- For information about the incremental tabset, see <https://github.com/mcanouil/quarto-revealjs-tabset>
:::
```

See [example.qmd](example.qmd) for the source.

## Styling

### Card Lists

Lists (both bullet and numbered) are styled as rounded cards with colored backgrounds. The primary card color is calculated from the slide's background color using OKLCH color space - it slightly decreases lightness and increases chroma to create subtle contrast:

```scss
--li-bg-1: oklch(from var(--bg) calc(l - 0.07) calc(c + 0.04) h);
--li-bg-2: var(--bg);
```

- **First-level items**: Use `--li-bg-1` (slightly darker/saturated)
- **Nested items**: Use `--li-bg-2` (same as slide background)

Use the `.normal-list` class to reset to browser-default list styling.

### Centered Card Lists

Use `.card-list-center` for centered card lists:

```markdown
::: card-list-center
- First item
- Second item
:::
```

### Panel Tabsets

Panel tabsets (`.panel-tabset`) are styled with rounded tab buttons and a colored border:

```markdown
:::::: {.panel-tabset}

## Tab 1

Content for tab 1

## Tab 2

Content for tab 2

::::::
```

### Columns

Columns get automatic equal-height styling with `.column-card` wrappers. Use `.nonincremental` on a column to show it immediately without fragment animation:

```markdown
:::::: columns

::::: {.column width="33%"}

Content here

:::::

:::::
```

## Background Color Persistence

Background colors set on any slide **persist forward** to all subsequent slides until a new background color is set.

```markdown
# Section Title {background-color="peach"}

## This slide is peach

## This slide is also peach (inherits)

## Different slide {background-color="cream"}

## This slide is cream
```

If no background color is set, white (#ffffff) is used as the default.

The extension includes a small JavaScript that propagates the background color and sets a CSS custom property (`--bg`) that the SCSS uses for calculating card list colors.

## Other Extensions

This theme works with these additional Quarto extensions:

- **simplemenu** - Flat navigation menu bar
- **tabset** - Incremental panel tabsets

## Installation

To use this extension, add it to your Quarto project:

```yaml
format:
  revealjs:
    theme: containers.scss
    include-after-body: bg.html
```

Or reference it directly in your format options:

```yaml
format:
  containerstheme-revealjs:
    # options here
```

## Configuration

All standard Reveal.js options are supported:

```yaml
format:
  containerstheme-revealjs:
    center: true
    touch: true
    incremental: true
    smaller: true
    transition: slide
    section-divs: false
    menu: false
    chalkboard:
      theme: whiteboard
```

## Credits

- Author: Mona Xue
- Simplemenu: [Martinomagnifico](https://github.com/Martinomagnifico/quarto-simplemenu)
- Tabset: [mcanouil](https://github.com/mcanouil/quarto-revealjs-tabset)