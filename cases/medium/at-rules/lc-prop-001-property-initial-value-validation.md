# LC-PROP-001: lightningcss validates `@property initial-value` against `syntax`

## Minimal Reproduction

```css
@property --x{syntax:"<color>";inherits:false;initial-value:calc()}
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token Function("calc")` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Spec Context

CSS Properties and Values API Level 1 says an `@property` rule with a non-universal syntax must have an `initial-value` that parses successfully against the registered syntax and is computationally independent. This case intentionally uses `syntax: "<color>"` with a length `calc()`, so the disagreement is mostly about whether a parser adapter validates descriptors or only parses rule structure.

## Reproduction Commands

Run from `../css-fuzzer` after `vp install` and `vp run build:oxc-driver`:

```sh
printf '@property --x{syntax:"<color>";inherits:false;initial-value:calc()}' | vp exec tsx src/parsers/jsParserWorker.ts --parser postcss
printf '@property --x{syntax:"<color>";inherits:false;initial-value:calc()}' | vp exec tsx src/parsers/jsParserWorker.ts --parser prettier-css
printf '@property --x{syntax:"<color>";inherits:false;initial-value:calc()}' | vp exec tsx src/parsers/jsParserWorker.ts --parser lightningcss
printf '@property --x{syntax:"<color>";inherits:false;initial-value:calc()}' | tools/oxc-css-parser-driver/target/release/oxc-css-parser-driver --syntax css
```
