# DRAFT-SLOT-001: lightningcss rejects `@slot` inside `@page`

## Minimal Reproduction

```css
@page{@slot a{}}
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unknown at rule: @slot` |
| oxc-css-parser 0.0.5 (`e4c405e`) | accepts |

## Triage Note

CSS Generated Content for Paged Media drafts include page-generated slots under `@page`. The minimized input only keeps the nested `@slot` rule shape, showing that lightningcss rejects the nested at-rule while postcss, Prettier, and OXC accept the structure.
