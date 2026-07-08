# LC-LINKPARAMS-001: URL link parameter with comma

## Minimal Reproduction

```css
a{b:url("",param())}
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Comma` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Triage Note

CSS Link Parameters Level 1 includes URL values with comma-separated `param()` entries for passing parameters to linked resources. This minimized case keeps that comma form while dropping unneeded URL text, names, and parameter values.
