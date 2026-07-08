# OXC-SCROLL-001: OXC rejects scroll-driven keyframe range selectors

## Minimal Reproduction

```css
@keyframes k { entry 0% { opacity: 0; } }
```

## Parser Results

| Parser | Result |
| --- | --- |
| postcss 8.5.16 | accepts |
| prettier CSS parser 3.9.4 | accepts |
| lightningcss 1.32.0 | accepts |
| oxc-css-parser 0.0.5 (`e4c405e`) | rejects: `expect token :, but found <percentage>` |

## Spec Context

This came from the downloaded Scroll-driven Animations Level 1 corpus. The `entry 0%` keyframe selector uses a timeline range name followed by a percentage.
