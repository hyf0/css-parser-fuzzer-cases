# STRICT-URL-001: `var()` inside legacy `url()` recovery differs

## Minimal Reproduction

```css
.spec-example { background: url(var(--foo)); }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token BadUrl("var(--foo")` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Triage Note

CSS Values Level 4 says unquoted `url()` is specially parsed as a URL token and cannot provide a URL by functions such as `var()`; `src()` is the function form for that. This is kept as a recovery/strictness reference.
