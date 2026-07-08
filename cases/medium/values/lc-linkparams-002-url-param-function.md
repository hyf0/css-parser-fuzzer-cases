# LC-LINKPARAMS-002: URL link parameter function

## Minimal Reproduction

```css
a{b:url(""param())}
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Function("param")` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Triage Note

CSS Link Parameters Level 1 also includes URL values followed by a `param()` function. This minimized case keeps the function form while dropping unneeded URL text, names, and parameter values.
