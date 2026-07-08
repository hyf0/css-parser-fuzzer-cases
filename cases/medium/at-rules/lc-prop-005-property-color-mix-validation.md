# LC-PROP-005: lightningcss validates `color-mix()` against `@property syntax`

## Minimal Reproduction

```css
@property --x { syntax: "<length>"; inherits: true; initial-value: color-mix(in oklab, red 30%, blue); }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Function("color-mix")` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Triage Note

Plain declaration use of `color-mix(in oklab, red 30%, blue)` is accepted by all four parsers. This case is about validating an `@property initial-value` against a registered `<length>` syntax.
