# CSS Parser Fuzzer Cases

This repository collects minimized parser disagreement cases found by `css-fuzzer`.

Current verified parser versions:

- postcss: 8.5.16
- prettier CSS parser: prettier 3.9.4, `__debug.parse(..., { parser: "css" })`
- lightningcss: 1.32.0
- oxc-css-parser: 0.0.6 at `oxc-project/oxc-css-parser@90911bd`

## Parser Symbols

✅ = clean parse. ❌ = not a clean parse: rejected, crashed, timed out, unsupported, or accepted with recoverable parser errors.

Only cases where `oxc-css-parser` is ❌ are listed below. OXC clean-accept cases stay under `cases/` with full sidecar notes, but are not listed in this human triage table.

## High Priority

| ID | Area | Minimal case | Why it matters | oxc-css-parser | postcss | prettier CSS parser | lightningcss | Parser notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ANCHOR-CONTAINER-001 | Anchor Position 2 anchored query | [`cases/high/at-rules/anchor-container-001-anchored-query.css`](./cases/high/at-rules/anchor-container-001-anchored-query.css) | CSS Anchor Position 2 includes `@container anchored(fallback: ...)`; OXC rejects the condition even though parser-only tools accept the rule shape. | ❌ | ✅ | ✅ | ❌ | OXC rejects: `expect token ), but found <ident>`. lightningcss rejects: `Unexpected token Function("anchored")`. |
| LC-SCOPE-002 | CSS Cascade 6 empty scope roundtrip | [`cases/high/at-rules/lc-scope-002-empty-scope-roundtrip.css`](./cases/high/at-rules/lc-scope-002-empty-scope-roundtrip.css) | lightningcss accepts `@scope (.x || a)` and emits `@scope ()`; OXC rejects that emitted CSS, so the accepted-input roundtrip produces parser disagreement. | ❌ | ✅ | ✅ | ✅ | OXC rejects: `simple selector is expected`. |
| OXC-CONTAINER-001 | Container query by name only | [`cases/high/at-rules/oxc-container-001-name-only-query.css`](./cases/high/at-rules/oxc-container-001-name-only-query.css) | CSS Conditional 5 says a stylesheet can query for a container only by name; OXC rejects the name-only `@container` form while the other parsers accept it. | ❌ | ✅ | ✅ | ✅ | OXC rejects: `expect token <ident>, but found {`. |
| OXC-SCROLL-001 | Scroll-driven keyframe range selector | [`cases/high/at-rules/oxc-scroll-001-keyframes-entry-range.css`](./cases/high/at-rules/oxc-scroll-001-keyframes-entry-range.css) | Scroll-driven animations allow timeline range names such as `entry` in keyframe selectors; OXC rejects `entry 0%` while the other parsers accept it. | ❌ | ✅ | ✅ | ✅ | OXC rejects: `expect token :, but found <percentage>`. |
| OXC-SHADOW-PARTS-001 | CSS Shadow Parts multi-ident `::part()` | [`cases/high/selectors/oxc-shadow-parts-001-multiple-part-ident.css`](./cases/high/selectors/oxc-shadow-parts-001-multiple-part-ident.css) | CSS Shadow Parts allows multiple idents inside `::part()`; OXC rejects the second ident while the other parsers accept the selector. | ❌ | ✅ | ✅ | ✅ | OXC rejects: `expect token ), but found <ident>`. |
| OXC-COLOR-001 | CSS Color 5 `device-cmyk` color profile | [`cases/high/at-rules/oxc-color-001-device-cmyk-profile.css`](./cases/high/at-rules/oxc-color-001-device-cmyk-profile.css) | CSS Color 5 includes `@color-profile` and `device-cmyk`; OXC reports a recoverable parser error for the predefined profile name while the other parsers accept it cleanly. | ❌ | ✅ | ✅ | ✅ | OXC accepts with recoverable error: `dashed identifier is expected`. |

## Medium Priority

| ID | Area | Minimal case | Why it matters | oxc-css-parser | postcss | prettier CSS parser | lightningcss | Parser notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DRAFT-TEMPLATE-001 | CSS Template `@page::slot()` syntax | [`cases/medium/at-rules/draft-template-001-page-slot-pseudo.css`](./cases/medium/at-rules/draft-template-001-page-slot-pseudo.css) | CSS Template Layout 1 includes `@page::slot(g)` examples; OXC rejects the pseudo syntax while parser-only tools accept it. | ❌ | ✅ | ✅ | ❌ | OXC rejects: `expect token ;, but found ::`. lightningcss rejects: `Unexpected token Colon`. |

## Low Priority

| ID | Area | Minimal case | Why it matters | oxc-css-parser | postcss | prettier CSS parser | lightningcss | Parser notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STRICT-SEL-001 | Invalid selector recovery | [`cases/low/selectors/strict-sel-001-double-class-dot.css`](./cases/low/selectors/strict-sel-001-double-class-dot.css) | `.a..b` is invalid selector syntax. This is a recovery/leniency reference, not a likely strict-parser bug. | ❌ | ✅ | ✅ | ❌ | OXC rejects: `expect token <ident>, but found .`. lightningcss rejects: `Expected identifier in class selector, got Delim('.')`. |
| STRICT-VAR-001 | Dynamic property name recovery | [`cases/low/declarations/strict-var-001-dynamic-property-name.css`](./cases/low/declarations/strict-var-001-dynamic-property-name.css) | CSS Values 5 shows that `var()` cannot be used as a property name and the declaration should be thrown away as a syntax error. | ❌ | ✅ | ✅ | ❌ | OXC rejects: `expect token :, but found (`. lightningcss rejects: `Unexpected token Semicolon`. |
| STRICT-MQ-002 | Invalid media query list recovery | [`cases/low/media-queries/strict-mq-002-invalid-query-list-recovery.css`](./cases/low/media-queries/strict-mq-002-invalid-query-list-recovery.css) | Media Queries 5 says a grammar mismatch in one media query is replaced by `not all`; strict parsers reject this malformed-list example. | ❌ | ✅ | ✅ | ❌ | OXC rejects: `expect token <ident>, but found &`. lightningcss rejects: `Unexpected token Comma`. |
| STRICT-MQ-003 | Invalid media at-rule semicolon recovery | [`cases/low/media-queries/strict-mq-003-invalid-media-semicolon.css`](./cases/low/media-queries/strict-mq-003-invalid-media-semicolon.css) | `@media test;` is invalid media at-rule syntax. postcss and Prettier recover from the semicolon form, while strict parsers reject it. | ❌ | ✅ | ✅ | ❌ | OXC rejects: `expect token {, but found ;`. lightningcss rejects: `Unexpected token Semicolon`. |

## Verification

Run the fuzzer verifier after changing cases:

```sh
vp run verify-cases -- --dir ../css-parser-fuzzer-cases/cases --readme ../css-parser-fuzzer-cases/README.md --timeout-ms 1500 --check-minimized --minimize-attempts 80
```

The verifier checks sidecar note coverage, sidecar reproduction blocks, sidecar required headings with non-empty `Spec Context` or `Triage Note` explanatory text, sidecar title IDs for README-listed OXC issue cases, README coverage for every current OXC non-clean-accept case, stale links, unique case listing, case ID filename prefixes, High/Medium/Low priority grouping, priority folder consistency, complete human-readable README parser emoji rows with parser notes, complete sidecar parser matrix coverage, README emoji drift, sidecar parser matrix drift, continued parser disagreement, and whether the current structure-level reducer can still produce a shorter case with the same parser-result fingerprint. For recognized issue families, the reducer must preserve that family as well as the parser fingerprint.

## Triage Rules

- High priority: current or near-current CSS syntax where at least two parsers accept the input and one production parser rejects it, or any parser crashes or times out.
- Medium priority: draft syntax with unclear implementation status, recovery-mode differences that may still affect formatter output, or parser-specific extensions.
- Low priority: likely-invalid syntax, duplicate findings, or behavior that needs a stronger spec citation before escalation.
