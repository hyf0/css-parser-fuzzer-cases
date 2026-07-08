# ANCHOR-CONTAINER-002: anchored query with logical fallback

## Minimal Reproduction

```css
@container anchored(fallback:self-block-start){}
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Function("anchored")` |
| oxc-css-parser 0.0.5 (`e4c405e`) | accepts |

## Triage Note

CSS Anchor Position Level 2 includes anchored fallback query examples with logical fallback positions such as `self-block-start`. This minimized case isolates the `anchored()` condition: postcss, Prettier, and OXC accept the rule structure while lightningcss rejects the function token.
