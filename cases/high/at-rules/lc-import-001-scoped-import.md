# LC-IMPORT-001: lightningcss rejects scoped `@import`

## Minimal Reproduction

```css
@import url("x") scope(a);
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Function("scope")` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Spec Context

This came from the downloaded CSS Cascade 6 editor draft corpus. It is a scoped import modifier on `@import`, not a selector or declaration-value edge.
