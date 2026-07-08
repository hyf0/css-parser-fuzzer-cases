# OXC-CONTAINER-001: OXC rejects name-only `@container`

## Minimal Reproduction

```css
@container my-page-layout { .card { padding: 1em; } }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | accepts |
| oxc-css-parser 0.0.5 (`e4c405e`) | rejects: `expect token <ident>, but found {` |

## Spec Context

CSS Conditional Rules Level 5 says it is possible to query for a container only based on its name, and shows `@container my-page-layout { ... }` as the example shape.
