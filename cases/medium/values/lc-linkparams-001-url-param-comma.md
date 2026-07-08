# LC-LINKPARAMS-001: URL link parameter with comma

## Minimal Reproduction

```css
.foo { background-image: url("image.svg", param(--color, green)); }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Comma` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Triage Note

CSS Link Parameters Level 1 includes `url("image.svg", param(--color, green))` as a CSS example for passing parameters to linked resources. lightningcss rejects the comma form while the other parsers accept the value structure.
