# STRICT-MQ-001: legacy `min-width` prefix mixed with range comparison

## Minimal Reproduction

```css
@media (min-width > 1024px) { color: red; }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Invalid media query` |
| oxc-css-parser 0.0.5 (`e4c405e`) | accepts |

## Triage Note

This appears to mix two media query forms. The range form `@media (width > 1024px)` is accepted by all four parsers; this case is kept as a recovery/validation difference rather than a clear syntax-parser bug.
