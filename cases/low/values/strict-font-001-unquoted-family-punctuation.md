# STRICT-FONT-001: invalid unquoted font family punctuation recovery differs

## Minimal Reproduction

```css
.spec-example { font-family: Ahem!, sans-serif; }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Delim('!')` |
| oxc-css-parser 0.0.5 (`e4c405e`) | accepts |

## Triage Note

CSS Fonts Level 4 lists declarations such as `font-family: Ahem!, sans-serif;` as invalid because unquoted font family names are limited to identifier sequences. This is a strict value-validation reference.
