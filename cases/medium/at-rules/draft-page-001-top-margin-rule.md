# DRAFT-PAGE-001: @top margin rule inside @page

## Minimal Reproduction

```css
@page:left { @top { color: red; } }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unknown at rule: @top` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Triage Note

The broader CSS Content Level 3 spec corpus includes `@top` nested inside `@page:left` and `@page:right` examples. Keep as a medium-priority draft page-margin syntax case because implementation status is less clear than the core CSS Page margin boxes such as `@top-left`.
