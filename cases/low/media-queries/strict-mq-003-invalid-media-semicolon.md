# STRICT-MQ-003: invalid media at-rule semicolon recovery differs

## Minimal Reproduction

```css
@media test;
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Semicolon` |
| oxc-css-parser 0.0.5 (`e4c405e`) | rejects: `expect token {, but found ;` |

## Triage Note

This is invalid media at-rule syntax. postcss and Prettier recover from the semicolon form, while lightningcss and OXC reject it. Keep as a low-priority recovery/leniency reference, not as a strict-parser bug.
