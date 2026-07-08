# STRICT-IMPORT-001: late `@import` recovery differs

## Minimal Reproduction

```css
a { color: red; } @import url("late.css");
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `@import rules must precede all rules aside from @charset and @layer statements` |
| oxc-css-parser 0.0.5 (`e4c405e`) | accepts |

## Triage Note

This is a strictness difference. CSS import rules are order-sensitive, so this is kept as a recovery reference rather than a likely strict-parser bug.
