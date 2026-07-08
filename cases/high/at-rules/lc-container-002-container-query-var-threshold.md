# LC-CONTAINER-002: lightningcss rejects `var()` in a container query threshold

## Minimal Reproduction

```css
@container (width > var(--query)) { color: red; }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Function("var")` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Spec Context

This came from the downloaded conditional/container-query spec corpus. It isolates the `var()` threshold in a container query comparison.
