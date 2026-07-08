# ANCHOR-CONTAINER-001: anchored container query condition

## Minimal Reproduction

```css
a{@container anchored(fallback:bottom any){b{c:d}}}
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Function("anchored")` |
| oxc-css-parser 0.0.6 (`90911bd`) | rejects: `expect token ), but found <ident>` |

## Triage Note

CSS Anchor Position Level 2 includes `@container anchored(fallback: ...)` examples for anchored positioning fallback queries. postcss and Prettier accept the rule structure, while lightningcss and OXC reject the `anchored()` condition.
