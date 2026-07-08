# OXC-COLOR-001: OXC reports a recoverable error for `device-cmyk`

## Minimal Reproduction

```css
@color-profile device-cmyk { color: red; }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | accepts |
| oxc-css-parser 0.0.5 (`e4c405e`) | accepts with errors: `dashed identifier is expected` |

## Triage Note

CSS Color Level 5 defines `device-cmyk` as a predefined color profile name. The other parser adapters accept the rule, while OXC accepts the stylesheet with a recoverable parser error asking for a dashed identifier.
