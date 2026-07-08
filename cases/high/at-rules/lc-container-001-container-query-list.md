# LC-CONTAINER-001: lightningcss rejects a comma-separated container query list

## Minimal Reproduction

```css
@container card (inline-size > 30em), style(--responsive: true) { color: red; }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Comma` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Spec Context

This came from the downloaded conditional/container-query spec corpus. The case isolates the comma-separated alternatives in the `@container` prelude.
