# LC-SEL-001: lightningcss rejects the Selectors column combinator

## Minimal Reproduction

```css
a||b{}
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | rejects: `Unexpected token in namespace selector: Delim('|')` |
| oxc-css-parser 0.0.6 (`90911bd`) | accepts |

## Spec Context

The live CSSWG Selectors draft index points the column combinator definition to Selectors Level 5. The minimized input uses only the selector and an empty declaration block, so the disagreement is isolated to selector parsing rather than modern declaration values.

## Reproduction Commands

Run from `../css-fuzzer` after `vp install` and `vp run build:oxc-driver`:

```sh
printf 'a||b{}' | vp exec tsx src/parsers/jsParserWorker.ts --parser postcss
printf 'a||b{}' | vp exec tsx src/parsers/jsParserWorker.ts --parser prettier-css
printf 'a||b{}' | vp exec tsx src/parsers/jsParserWorker.ts --parser lightningcss
printf 'a||b{}' | tools/oxc-css-parser-driver/target/release/oxc-css-parser-driver --syntax css
```
