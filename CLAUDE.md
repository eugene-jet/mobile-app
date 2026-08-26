# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this repository is

**Surprise Collector** — a planned cross-platform collection tracker for people
who collect the toy figures from chocolate surprise eggs.

Right now the repository contains **no application code**. It holds the product
concept and the design system output:

| File | What it is |
|---|---|
| `README.md` | Design system overview — token groups, the corner radius map, how to consume `tokens.json` |
| `idea.md` | Product concept and planned MVP scope (written in Ukrainian) |
| `tokens.json` | 334 design tokens exported from Figma, W3C Design Tokens (DTCG) draft format |

MVP scope, per `idea.md`: catalogue + my collection + wishlist. Trading,
selling and community features are explicitly out of scope for the first stage.

## Hard rules

**Never edit `tokens.json` by hand.** Figma is the source of truth. The file is
a machine export; a hand edit is silently lost on the next regeneration. If a
token value needs to change, change it in Figma and re-export.

Design system Figma file:
<https://www.figma.com/design/kbZ39m2G2qM7misMz37XF6>

**Never use the Kinder or Ferrero trademarks** in the app name, visual
identity, copy, or any user-facing string. The neutral working name is
deliberate — `idea.md` flags the trademark question as an open legal item.
Referring to the real-world product descriptively in internal docs is fine;
branding the app with it is not.

**Never reference `primitive/*` tokens from UI code.** Primitives are raw
colour ramps. UI consumes the semantic aliases under `color/light` and
`color/dark`, so that a theme stays a single lookup table.

## tokens.json structure

```
primitive/     raw colour ramps (alpha, amber, blue, gold, green, indigo, neutral, purple)
color/         light and dark semantic colours, aliased to primitives
spacing/       4px-grid scale (none, 3xs … xl)
radius/        none, sm, md, lg, xl, 2xl, full
size/          icon, avatar and control sizes — touch-min is 44px
stroke/        thin, default, thick, focus
layout/        responsive values, one group per breakpoint
font/          family, weight, size, line height
typography/    composite text styles (display, heading, body, label, caption)
shadow/        elevation levels
```

Consume via Style Dictionary or any DTCG-compatible transformer to produce CSS
custom properties, Kotlin, or Swift.

### Radius mapping

The Figma component library is the source of truth for which radius a component
uses, not intent or intuition. The table in `README.md` mirrors what the library
actually binds — check the Figma components before changing a row in it. Three
deliberate levels: controls 8px, fields 12px, containers 16px, so nesting reads
as distinct steps. Buttons share one radius across all sizes.

## Design constraints

- Light and dark themes are designed together — a change to one needs its pair.
- Breakpoints: 375 mobile, 768 tablet, 1440 wide.
- One component set covers iOS, Android and web.
- Typeface Inter; icons from Lucide (ISC).
- WCAG 2.1 AA: every foreground/background pair must be verified, and touch
  targets stay at or above the 44px `size/touch-min` token.

## Stack

Not chosen yet. `idea.md` names React Native and Flutter as the candidates for
cross-platform. Don't assume one — ask before scaffolding application code.

## Conventions

- Commit messages follow Conventional Commits (`feat:`, `docs:`, …), subject in
  the imperative mood, as in the existing history.
- Work happens on a branch; `main` is merged through pull requests.
  Remote: <https://github.com/eugene-jet/mobile-app.git>
- Documentation prose is English. `idea.md` stays Ukrainian — it is the
  author's own concept note; don't translate it as a side effect of an edit.
- `.claude/worktrees/` is agent scratch space. Never commit it.
