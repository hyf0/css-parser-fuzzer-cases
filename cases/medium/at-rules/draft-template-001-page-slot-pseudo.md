# DRAFT-TEMPLATE-001: @page slot pseudo syntax

## Minimal Reproduction

```css
@page::slot(g) { color: red; }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Colon` |
| oxc-css-parser 0.0.5 (`e4c405e`) | rejects: `expect token ;, but found ::` |

## Triage Note

CSS Template Layout Level 1 includes `@page::slot(g)` examples. This is kept as a medium-priority draft/legacy syntax case because the spec appears in the live CSSWG index, but implementation status is much less clear than modern container, selector, or anchor-positioning syntax.
