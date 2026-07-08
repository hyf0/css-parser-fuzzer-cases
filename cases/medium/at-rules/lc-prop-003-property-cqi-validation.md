# LC-PROP-003: lightningcss validates a `cqi` initial value against `@property syntax`

## Minimal Reproduction

```css
@property --x { syntax: "<color>"; inherits: false; initial-value: 2cqi; }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Dimension ... unit: "cqi"` |
| oxc-css-parser 0.0.5 (`e4c405e`) | accepts |

## Triage Note

This is descriptor validation rather than plain tokenization: the rule structure parses, but the initial value does not match `syntax: "<color>"`.
