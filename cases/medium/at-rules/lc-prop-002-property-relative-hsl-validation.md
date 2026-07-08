# LC-PROP-002: lightningcss validates relative `hsl()` against `@property syntax`

## Minimal Reproduction

```css
@property --x { syntax: "<length>"; inherits: false; initial-value: hsl(from var(--accent) h s calc(l + 10%)); }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Function("hsl")` |
| oxc-css-parser 0.0.5 (`e4c405e`) | accepts |

## Triage Note

The same relative `hsl()` works as a normal declaration value in all four parsers. The disagreement here is descriptor validation for `@property`, not ordinary color parsing.
