# STRICT-MQ-002: invalid media query list recovery differs

## Minimal Reproduction

```css
@media (example, all,), speech { color: red; } @media &test, speech { /* only applicable to speech devices */ }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Comma` |
| oxc-css-parser 0.0.5 (`e4c405e`) | rejects: `expect token <ident>, but found &` |

## Triage Note

Media Queries Level 5 says a media query that does not match the grammar is replaced by `not all` during parsing, and a mismatch does not wipe out the entire media query list. This case is kept as recovery behavior, not as valid media-query syntax.
