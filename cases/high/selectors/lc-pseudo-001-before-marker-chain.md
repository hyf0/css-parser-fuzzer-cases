# LC-PSEUDO-001: lightningcss rejects `::before::marker`

## Minimal Reproduction

```css
::before::marker{}
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Invalid state` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Spec Context

CSS Pseudo-Elements Level 4 says pseudo-elements cannot be chained unless explicitly allowed, and gives `::before::marker` as an allowed chain.
