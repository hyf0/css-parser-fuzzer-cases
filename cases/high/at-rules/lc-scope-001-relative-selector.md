# LC-SCOPE-001: lightningcss rejects a relative selector inside `@scope`

## Minimal Reproduction

```css
@scope(a){>b{}}
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Invalid empty selector` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Spec Context

CSS Cascade Level 6 says selectors in scoped style rules are relative selectors by default, and its examples show an explicit child combinator form such as `> p`.
