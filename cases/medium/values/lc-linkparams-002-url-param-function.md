# LC-LINKPARAMS-002: URL link parameter function

## Minimal Reproduction

```css
.foo { background-image: url("image.svg" param(--color, green)); }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Function("param")` |
| oxc-css-parser 0.0.5 (`e4c405e`) | accepts |

## Triage Note

CSS Link Parameters Level 1 also includes URL values followed by a `param()` function. lightningcss rejects the function form while postcss, Prettier, and OXC accept the value structure.
