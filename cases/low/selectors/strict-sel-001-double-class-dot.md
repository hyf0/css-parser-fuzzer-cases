# STRICT-SEL-001: invalid double-dot class selector recovery differs

## Minimal Reproduction

```css
.a..b { color: red; }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Expected identifier in class selector, got Delim('.')` |
| oxc-css-parser 0.0.6 (`90911bd`) | rejects: `expect token <ident>, but found .` |

## Triage Note

This is invalid selector syntax. It is useful as a leniency comparison because postcss and Prettier accept it, but it should not be treated as a strict parser bug without a separate recovery-mode requirement.
