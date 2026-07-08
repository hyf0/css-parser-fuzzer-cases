# LC-SEL-002: lightningcss rejects the Selectors 5 reference combinator

## Minimal Reproduction

```css
label:is(:hover, :focus) /for/ input { color: red; }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Invalid dangling combinator in selector` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Spec Context

Selectors Level 5 defines the reference combinator as two slashes surrounding an attribute name, such as `/for/`.
