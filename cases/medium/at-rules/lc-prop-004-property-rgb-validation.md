# LC-PROP-004: lightningcss validates `rgb()` against `@property syntax`

## Minimal Reproduction

```css
@property --x { syntax: "<length>"; inherits: false; initial-value: rgb(20 40 60 / 80%); }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Function("rgb")` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Triage Note

This is descriptor validation: `rgb()` is a color, while the registration syntax is `<length>`.
