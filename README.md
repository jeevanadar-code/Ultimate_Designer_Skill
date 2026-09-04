# Ultimate Designer

A Claude Skill that makes AI design work look designed rather than generated.

> *"Reading this as: B2B SaaS landing for technical buyers, Bauhaus-adjacent — geometric, restrained, Inter + a single accent."*

Every build starts with that line. That's the whole idea.

<sub>Claude Skill · 9 files · 1,472 lines · MIT</sub>

---

## The problem

Ask any model to design something and you get the same page back. Purple-to-blue gradient. Centred hero on a dark mesh. Three equal feature cards with rounded-square icons. A pill badge reading "✨ Introducing". Inter on slate-900.

This isn't a lack of capability. It's an ordering problem: **the model picks an aesthetic before it understands the brief.** With nothing to go on, it reaches for the average of everything it has ever seen — and the average is never right for a specific job.

Adding more instructions doesn't fix that. Adding a decision does.

## What it does

Five stages, in order. Skipping the first two is what produces slop.

```
1. READ       what is this, who is it for, what must it do
2. CHOOSE     commit to a named style — out loud, before any code
3. STRUCTURE  hierarchy, layout, spacing
4. BUILD      components with real rules
5. CHECK      anti-slop pass before shipping
```

The out-loud part in stage 2 matters more than it looks. A wrong read costs one line to correct at that point. Discovered after a full build, it costs the build.

## The core idea: style latitude is set by the surface

Not by preference, and not by what sounds exciting.

| Surface | Latitude |
|---|---|
| Marketing, campaign | Wide — expression is the job |
| Portfolio, editorial | Wide — voice is the point |
| Product UI | **Narrow** — legibility beats expression |
| Transactional | **Very narrow** — trust and clarity only |

Baroque on a healthcare dashboard isn't bold, it's negligent. Vaporwave on a checkout flow loses money.

So every one of the 50 styles in the catalogue carries a viability rating:

| Rating | Count | Meaning |
|---|---|---|
| **UI** | 5 | Safe for product interfaces, including dense ones |
| **MKT** | 32 | Marketing and editorial. Too expressive for product UI |
| **ACCENT** | 8 | Detailing only — a border treatment, one section |
| **PRINT** | 5 | Illustration and packaging. Never a live interface |

**Only five of fifty are safe for product UI** — Bauhaus, Utilitarian, Japandi, Bento Box, Neo-Brutalism. They share one property: all five were built around systems. The ornamental styles were built for surfaces nobody has to operate.

That's not a reason to avoid the other 45. It's a reason to know which surface you're on before picking.

## What's inside

```
ultimate-designer/
├── SKILL.md                          the five-stage pipeline
├── references/
│   ├── style-catalogue.md            50 styles, each rated for viability
│   ├── style-selection.md            choosing, combining, vibe-word translation
│   ├── layout-and-hierarchy.md       type, space, colour, grid, dark mode
│   ├── components.md                 buttons, cards, nav, forms (Material 3)
│   ├── responsive.md                 breakpoints and component swapping
│   ├── anti-slop.md                  the failure catalogue + pre-flight
│   └── accessibility.md              contrast, targets, motion, focus
└── assets/
    └── page-archetypes.md            10 page types and what each needs
```

Progressive disclosure: only `SKILL.md` loads on every trigger. The rest loads when the task needs it, so the colour section isn't sitting in context while you're picking components.

## Install

Settings → Capabilities → Skills → Upload, then select `ultimate-designer.skill`.

It triggers on its own description — no prompting needed. Ask for a landing page, a dashboard, a colour palette, or say "this looks like AI made it," and it fires.

## Examples

**It commits instead of defaulting.**

> **You:** build me a landing page for a wellness app
>
> **It:** Reading this as: consumer wellness landing for people seeking calm, Japandi language — light wood neutrals, generous space, Instrument Serif over Inter, 12px radius, no shadows.

**It converts style names into buildable specs.** "Japandi" isn't a design. This is:

```
Palette   #FAF9F7 base · #FFFFFF surface · #2C2A27 text · #8B7355 accent
Type      Instrument Serif display / Inter body
Scale     1.25 type ratio · 8px spacing unit
Shape     12px radius — soft but not childlike
Depth     Flat with hairline borders. No shadows.
Density   Generous — 96px section padding
Motion    Restrained — 200ms fades, no parallax
```

**It pushes back when the style fights the surface.**

> **You:** make our banking dashboard vaporwave
>
> **It:** Vaporwave on a banking dashboard will fight the job — the palette is low-contrast and the nostalgia reads as unserious where people are checking balances. What works: run it on the marketing site where expression is the point, keep the product surface restrained, and tie them together with a shared accent and typeface.

Say you still want it and it builds it. Your product, and the concern only needs saying once.

## Style combination

Hybrids work, but under rules. **One style leads at ~80%. The second contributes exactly one thing** — palette, type, texture, ornament, or motion. Not several.

| Pair | Lead | Second contributes |
|---|---|---|
| Japandi + Wabi Sabi | Japandi structure | Texture, asymmetric imagery |
| Bauhaus + Memphis | Bauhaus grid | Palette and accent shapes |
| Utilitarian + Neo-Brutalism | Utilitarian density | Borders and type weight |
| Bento + Aurora | Bento structure | Background gradient only |

**What doesn't work:** two ornamental styles (Baroque + Victorian is mud, not richness), two loud palettes, or three-plus styles — which isn't a hybrid, it's an absence of decision.

## The three tests

Run before shipping.

**Substitution** — could this have been made for a different client in a different industry? If yes, it isn't designed. Something must be true only of this brief.

**Greyscale** — remove all colour. Does hierarchy survive? Are states distinguishable? If it collapses, colour was carrying structural work it can't be trusted with.

**40-character** — replace every string with the longest realistic version. Most generated designs break instantly, because they were built around content that fits.

## On "make it less generic"

That complaint is almost always one of three things, and they need different fixes:

| They mean | Fix |
|---|---|
| "It has no point of view" | Style wasn't chosen. Go back and commit harder. |
| "It's flat" | Hierarchy is timid. Triple the size contrast. |
| "I've seen this before" | Forbidden defaults present. Replace them. |

**Adding decoration never fixes generic.** Generic is an absence of decision — more ornament just makes it a busier undecided design.

## Sources

Built from four inputs, synthesised rather than concatenated:

- [**taste-skill**](https://github.com/Leonxlnx/taste-skill) — the anti-slop discipline and the design-read-out-loud pattern
- [**50 Design Styles Every Designer Should Know**](https://medium.com/ux-planet/50-design-styles-every-designer-should-know-for-better-prompting-56c09d55db62) by Himanshu Bhardwaj — the style vocabulary
- **Material Design 3** — component rules, hierarchy, breakpoints
- **Dribbble / Awwwards** — page archetypes and what each needs

The viability ratings, the surface-latitude rule, the 80/20 combination rule, and the style→spec converter are additions. None of the sources connect a style vocabulary to the question of whether a given style is safe to build.

## Limitations

**Web and product UI.** Not print production, motion graphics, 3D, or full brand identity systems.

**Opinionated, on purpose.** It will tell you Baroque doesn't belong on a dashboard. If you want a tool that builds whatever you name without comment, this isn't it.

**Material-leaning components.** The component rules follow Material 3. If you're building to Apple HIG or a house design system, `components.md` needs adapting.

**Style names aren't magic.** "Japandi" gets you a coherent direction, not a finished design. The converter exists precisely because the name alone isn't buildable.

## License

MIT
