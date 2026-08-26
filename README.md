# mobile-app-kinder

A cross-platform collection tracker for people who collect the toy figures from
chocolate surprise eggs. See [idea.md](idea.md) for the product concept and the
planned MVP scope.

Working name: **Surprise Collector**. The app deliberately avoids the Kinder and
Ferrero trademarks in its name and visual identity.

## Design system

The design system lives in Figma and is the source of truth for anything visual:

**[Surprise Collector — Design System](https://www.figma.com/design/kbZ39m2G2qM7misMz37XF6)**

It covers foundations and base components — no product screens yet.

| | |
|---|---|
| Themes | Light and dark, designed together |
| Breakpoints | 375 (mobile) · 768 (tablet) · 1440 (wide) |
| Platforms | One component set for iOS, Android and web |
| Typeface | Inter |
| Icons | [Lucide](https://lucide.dev) (ISC) |
| Accessibility | WCAG 2.1 AA — every foreground/background pair verified |

The Figma file is organised as: cover, four foundations pages (colour, typography,
scale and layout, elevation), an icon page, then one page per component, and a
changelog.

## tokens.json

[`tokens.json`](tokens.json) is the exported machine-readable copy of the Figma
variables, in [W3C Design Tokens](https://tr.designtokens.org/format/) draft format.
334 tokens.

```
primitive/     raw colour ramps — never referenced directly by UI code
color/         light and dark semantic colours, aliased to primitives
spacing/       4px-grid spacing scale
radius/        corner radii — buttons and other controls use radius.sm (8px)
size/          icon, avatar and control sizes (touch-min = 44px)
stroke/        border widths
layout/        responsive values, one group per breakpoint
font/          families, weights, sizes, line heights
typography/    composite text styles
shadow/        elevation levels
```

### Corner radii

| Token | Value | Used for |
|---|---|---|
| `radius.none` | 0px | Full-bleed surfaces, dividers |
| `radius.sm` | 8px | Buttons, inputs, selects, segmented controls |
| `radius.md` | 12px | Cards, list rows |
| `radius.lg` | 16px | Sheets, modals |
| `radius.xl` | 24px | Large containers, onboarding panels |
| `radius.2xl` | 32px | Hero and cover surfaces |
| `radius.full` | 9999px | Pills (Chip, Badge), avatars, progress tracks |

Buttons share a single radius across all sizes, so a small and a large button read as
the same family. The focus ring sits 4px outside the button and uses `radius.md` (12px)
to stay concentric with it. Chip and Badge are the only fully pill-shaped controls.

Semantic colours are aliases, so a theme is a single lookup table:

```json
"color": {
  "light": { "bg": { "canvas": { "$type": "color", "$value": "{primitive.neutral.50}" } } },
  "dark":  { "bg": { "canvas": { "$type": "color", "$value": "{primitive.neutral.950}" } } }
}
```

Consume it with Style Dictionary or any DTCG-compatible transformer to produce CSS
custom properties, Kotlin, or Swift. Regenerate it from Figma rather than editing it
by hand — Figma is the source of truth.
