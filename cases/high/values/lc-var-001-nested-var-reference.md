# LC-VAR-001: nested var() custom property reference

## Minimal Reproduction

```css
:root { --result: var(var(--myvar)); }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Function("var")` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Triage Note

CSS Variables Level 2 includes an example where the custom property name looked up by an outer `var()` comes from an inner `var()` function. This minimized case keeps the same parser surface: postcss, Prettier, and OXC accept the nested `var()` form, while lightningcss rejects it.
