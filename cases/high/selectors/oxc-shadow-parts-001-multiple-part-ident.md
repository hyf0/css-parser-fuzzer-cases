# OXC-SHADOW-PARTS-001: OXC rejects multiple idents in `::part()`

## Minimal Reproduction

```css
x-tabs::part(tab active) { color: red; }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | accepts |
| oxc-css-parser 0.0.6 (`90911bd`) | rejects: `expect token ), but found <ident>` |

## Triage Note

CSS Shadow Parts allows `::part()` to take a list of part names. This case keeps the selector and declaration minimal; postcss, Prettier, and lightningcss accept it, while OXC rejects the second identifier inside the pseudo-element argument.
