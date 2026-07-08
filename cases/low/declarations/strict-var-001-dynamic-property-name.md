# STRICT-VAR-001: `var()` cannot provide a property name

## Minimal Reproduction

```css
a{var(--x):;}
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Semicolon` |
| oxc-css-parser 0.0.6 (`90911bd`) | rejects: `expect token :, but found (` |

## Triage Note

CSS Values Level 5 explicitly uses this shape as an incorrect attempt to use a variable as a property name. This is kept as a recovery/strictness reference rather than a likely strict-parser bug.
