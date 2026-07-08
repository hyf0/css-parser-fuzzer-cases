# LC-SCOPE-002: OXC rejects a lightningcss-emitted empty `@scope` root

## Minimal Reproduction

```css
@scope(){a{color:red}}
```

## Roundtrip Trigger

lightningcss 1.32.0 accepts this input:

```css
@scope (.x || a) { a { color: red; } }
```

It emits the minimal reproduction above. The emitted stylesheet is then accepted by postcss, Prettier CSS, and lightningcss, but rejected by OXC.

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | accepts |
| oxc-css-parser 0.0.6 (`90911bd`) | rejects: `simple selector is expected` |

## Spec Context

CSS Cascade Level 6 `@scope` roots are selector lists. An empty root `()` is not a useful selector root, and this case matters because it is emitted by lightningcss from an input that the full parser matrix accepts.
