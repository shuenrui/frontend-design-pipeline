---
name: frontend-design-pipeline
description: Mandatory coordinator for frontend design work. Use before creating, redesigning, reviewing, polishing, or visually changing websites, landing pages, product UI, dashboards, data viz, components, forms, responsive layouts, native/mobile/desktop UI, or design systems. Orchestrates Impeccable, Anthropic frontend-design, the Leonxlnx Taste skills, and the ui-ux-pro-max design-system data engine without conflicting aesthetics or duplicate workflows.
compatibility: opencode
metadata:
  audience: frontend-engineers
  workflow: design-orchestration
---

# Frontend Design Pipeline

This skill is the traffic controller for frontend design work. It does not add a
fourth aesthetic. It gives each installed design skill one job, selects only the
relevant specialist skills, and prevents competing recipes from steering the
same decision.

Use it for any task where layout, visual hierarchy, UX, responsive behavior,
interaction design, accessibility, copy, theming, motion, or design-system
coherence can change. Skip it for backend-only work and purely mechanical
frontend changes with no visible or UX effect.

## Authority order

Resolve every conflict in this order:

1. The user's latest explicit brief, supplied content, approvals, references,
   exclusions, and requested scope.
2. Product truth, functional correctness, accessibility, security, legal
   requirements, and data integrity.
3. Existing project architecture, dependencies, platform conventions, brand
   assets, tokens, behavior, routes, analytics, localization, and browser
   support.
4. An approved visual source of truth: brand guide, Figma design, supplied
   reference, approved comp, or coherent neighboring surface.
5. The owning Impeccable playbook and the committed direction for this surface.
6. Anthropic `frontend-design` as the art-direction and self-critique lens.
7. The applicable parts of `design-taste-frontend` and any explicitly routed
   Taste specialist as implementation guidance or anti-slop lint.
8. `ui-ux-pro-max` generated systems and looked-up data (palettes, type
   pairings, tokens, chart picks, UX/accessibility rules, stack guidance) as
   structured recommendations.
9. Generic defaults, randomizers, font lists, palette bans, and aesthetic
   preferences from any skill.

Specific evidence beats a general rule. Preservation beats invention during a
refinement. Never average two conflicting styles into a compromise. Choose one
owner for each decision. Within `ui-ux-pro-max`, its accessibility, UX, chart,
and stack data are evidence and rank accordingly; its generated palettes, type
pairings, and tokens are only candidates and yield to rungs 1-7.

## Core skill roles

Load the core skills through the skill tool, not by copying their files into the
prompt.

### Impeccable: lifecycle owner

Always load `impeccable` first for substantial design work. It owns task
classification, product/design context, surface mode, new-work versus
refinement routing, implementation quality, inspection, and finish. Follow its
setup once per session and load exactly one owning playbook at a time.

Do not run several Impeccable commands as competing passes. An explicit audit
is report-only unless the user also asks for fixes.

### Anthropic frontend-design: art director

Load `frontend-design` for new UI, a replacement visual world, or meaningful
visual reshaping. Use it to ground the work in the subject, audience, and page
job; sharpen typography and copy; identify one memorable signature; and
challenge generic choices before code.

It advises the direction but does not replace Impeccable's new-work flow,
concept seed, project context, or finish process. During an Impeccable new-work
flow, feed its subject-grounded ideas into that one flow rather than presenting
a second plan or running another randomizer.

For narrow refinements, use this skill only as a critique lens. Do not let it
invent a new identity.

### Taste: scoped anti-slop reviewer

Load the current `design-taste-frontend` for landing pages, marketing sites,
portfolios, editorial pages, and design-led web redesigns. Use its design read,
responsive and copy checks, state coverage, and anti-tell guidance after the
direction is known.

It does not own dashboards, data tables, multi-step product UI, native UI, stack
selection, or dependency migration. On those surfaces, mark it not applicable:
Impeccable's Operate/native flow owns the work and `ui-ux-pro-max` supplies the
concrete data, charts, accessibility rules, and stack guidance. Never load
`design-taste-frontend-v1` unless the user explicitly requires exact v1
behavior.

Taste rules are contextual lint under this pipeline. Aesthetic bans do not
override the brief, an existing design system, an approved comp, accessibility,
or correctness. Do not fabricate metrics, dates, customers, testimonials,
prices, capabilities, or social proof to make a design look realistic.

### ui-ux-pro-max: design-system data engine

`ui-ux-pro-max` is not a fourth aesthetic; it is a deterministic, queryable data
engine. Use it to generate concrete candidates and to look up evidence the prose
skills do not carry: palettes with semantic CSS tokens, font pairings, spacing
scales, chart and data-viz selection, the 119-rule UX/accessibility catalog,
icon guidance, and stack-specific implementation rules across 22 web, native,
and desktop stacks. It owns the surfaces the Taste skills explicitly disclaim —
dashboards, data tables, charts, multi-step product UI, and native/mobile/
desktop detail.

Run its script directly; load the `ui-ux-pro-max` skill for the full query
contract and reference docs when you need deeper guidance. The universal install
path is `~/.agents/skills/ui-ux-pro-max/scripts/search.py` (confirm against the
loaded skill if it differs):

```bash
python3 ~/.agents/skills/ui-ux-pro-max/scripts/search.py "<product industry keywords>" --design-system -p "Name"
python3 ~/.agents/skills/ui-ux-pro-max/scripts/search.py "<concern>" --domain <ux|style|color|typography|chart|icons|gsap|landing|product|react|web|google-fonts>
python3 ~/.agents/skills/ui-ux-pro-max/scripts/search.py "<concern>" --stack <react|nextjs|html-tailwind|swiftui|flutter|...>
```

Treat every result as a recommendation, never as an instruction that overrides
the brief, the committed direction, an existing design system, or accessibility
truth. Its generated palette, type, and token values are candidates that feed
the one Impeccable-owned concept decision; they do not start a competing
direction and never overwrite approved brand tokens. Do not run `--design-system`
as a second randomizer alongside `frontend-design`: generate once, then
art-direct. Use `--persist` only when the user wants a reusable data-driven
system, always pass `--output-dir <project-root>`, and never `--force` over an
existing `MASTER.md` or an Impeccable-owned `DESIGN.md` without explicit
authorization.

## Stage 1: classify

Before editing, classify the request on four axes:

- Work type: new visual world, new surface in an established world, explicit
  redesign, narrow refinement, audit/review, or visual bug fix.
- Surface mode: Persuade, Operate, Read, or Experience, using Impeccable's
  definitions.
- Output: runnable code, design/reference images, mobile images, brand board,
  Stitch artifact, or review only.
- Preservation level: preserve, evolve within the system, or replace with
  explicit approval.

Ask one compact question only when the answer changes scope, product truth, or
the preserve/replace decision. Otherwise infer from the code and brief.

## Stage 2: establish truth

Inspect before choosing an aesthetic:

- Read project instructions, dependency files, the target route/component, and
  at least one neighboring implementation.
- Read PRODUCT.md, DESIGN.md, surface briefs, tokens, themes, shared components,
  and real brand assets when present.
- Identify the actual user, surface job, primary action or task, required
  states, supplied proof/content, and unsupported claims.
- Record the existing framework and styling approach. Do not migrate or install
  a design system merely because a skill prefers one.
- Detect the stack (package.json, pubspec.yaml, *.xcodeproj/Package.swift,
  composer.json, React Native markers). When the work needs concrete
  palette/type/token candidates, chart selection, accessibility rules, or
  guidance for a native, desktop, or data-heavy surface, query `ui-ux-pro-max`
  (`--stack`, `--domain`) for evidence instead of guessing. Never assume a
  stack: a wrong default silently misroutes every recommendation.
- For redesigns, establish a before baseline for behavior, routes, content,
  accessibility, responsive states, SEO, and tracked interactions.

## Stage 3: choose one direction

For an open new or replacement world, follow Impeccable new-work. Use
`frontend-design` to make the candidates subject-specific and to critique the
selected direction for generic defaults. Use Taste only after selection to flag
relevant anti-patterns. One concept process, one approved direction, one source
of visual truth. You may seed candidates with a single `ui-ux-pro-max
--design-system` run (pattern, palette, type, anti-patterns), but feed them into
that one Impeccable concept decision; it must not auto-commit a direction or run
as a second generator next to `frontend-design`.

For a new surface inside an established world, inherit the world and explore
structure only. For a component or narrow refinement, skip concept generation
and preserve the incumbent identity.

Before implementation, lock a compact contract:

- Audience and single surface job.
- Mode and preservation level.
- Palette and typography roles derived from the chosen world.
- Layout/composition principle.
- One signature element or interaction, if the task warrants one.
- Content and claims that are real, synthetic and labeled, or still missing.
- Mobile behavior and reduced-motion behavior.

Spend boldness in one place. Do not add motion, imagery, glass, cards, serif
type, asymmetric composition, or dark mode solely because a skill lists it.

## Optional Taste routing

Load at most one aesthetic specialist. A specialist refines the committed
direction; it never starts another direction-selection process.

| Skill | Load only when |
| --- | --- |
| `gpt-taste` | The user explicitly wants an Awwwards-style, GSAP-heavy marketing or portfolio experience and the project supports the motion budget. Its RNG, mandatory AIDA, and GSAP-everywhere rules remain advisory under the locked direction. |
| `high-end-visual-design` | The approved direction specifically calls for cinematic agency craft, haptic glass, nested bezels, or floating-island materiality. "Premium" alone is not enough. |
| `minimalist-ui` | The brief or approved reference explicitly calls for warm monochrome, editorial/workspace minimalism, flat surfaces, and restrained motion. "Simple" alone is not enough. |
| `industrial-brutalist-ui` | The user explicitly requests industrial brutalism, Swiss machinery print, tactical telemetry, CRT, or declassified-blueprint aesthetics. Choose one of its two modes, never both. |

The four aesthetic specialists above are mutually exclusive.

Load at most one output/workflow specialist:

| Skill | Load only when |
| --- | --- |
| `image-to-code` | The user explicitly wants generated-comp-first runnable web code, or an approved generated comp is the implementation source. Do not duplicate Impeccable's visualization flow. |
| `imagegen-frontend-web` | The deliverable is website section reference images, not code. |
| `imagegen-frontend-mobile` | The deliverable is mobile app screen or flow images, not code. |
| `brandkit` | The deliverable is a logo system, identity board, or brand-guidelines image. Missing branding alone does not trigger it. |
| `stitch-design-taste` | The user explicitly requests Google Stitch output or a Stitch-oriented semantic design document. Do not overwrite an Impeccable-owned DESIGN.md without explicit migration intent. |

The five output/workflow specialists above are mutually exclusive.

Other Taste helpers:

- `ui-ux-pro-max` is a core data engine, not an aesthetic specialist, so it
  stays available alongside any one specialist above. When a specialist is
  loaded, the specialist owns the look; use `ui-ux-pro-max` for data,
  UX/accessibility rules, charts, icons, and stack guidance, and let its
  generated palette/type yield to the committed direction.
- Load `redesign-existing-projects` only as a diagnostic checklist for a
  targeted modernization that preserves stack and function. Impeccable remains
  the redesign owner.
- Load `full-output-enforcement` only when the user requests exhaustive inline
  files or a finite complete set. Normal shared-workspace edits do not need it.
- Never load `design-taste-frontend-v1` alongside the current Taste skill.

If no specialist's trigger is satisfied, load none. More design skills do not
mean better design.

## Stage 4: implement

Immediately before UI edits, load Impeccable's craft-floor reference as its
playbook directs. Then:

- Work in the existing stack and styling system unless migration is explicitly
  requested.
- Verify dependencies before imports. Prefer existing components and tokens.
- Preserve functionality, routes, analytics, copy, and out-of-scope areas.
- Implement the full requested path, including relevant loading, empty, error,
  success, disabled, permission, long-content, and missing-content states.
- Make controls semantic, keyboard accessible, visibly focused, and adequately
  sized. Meet the project's contrast target and honor reduced motion.
- Use real supplied content and assets. Label synthetic demonstrations. Leave
  explicit replacement notes for missing commercial truth.
- Build responsive behavior intentionally for mobile, intermediate, and wide
  viewports; do not assume desktop CSS will collapse correctly.
- Keep motion purposeful and bounded. It must communicate hierarchy, feedback,
  state, or story.
- Pull concrete implementation guidance from `ui-ux-pro-max` as needed:
  `--domain ux` for accessibility and interaction rules, `--domain chart` for
  data-viz selection, `--domain icons` for accessible icon usage, `--domain
  gsap` for motion presets, and `--stack <x>` for framework- or platform-
  specific patterns. It is the owner for dashboard, data-table, and
  native/mobile/desktop implementation detail the Taste skills disclaim.

## Stage 5: verify and finish

Use bounded, evidence-based passes:

1. Run the project's relevant build, typecheck, lint, and tests.
2. Exercise the real interaction path and inspect browser/runtime errors.
3. Inspect desktop and mobile together in one screenshot round. Fix findings in
   one batch, confirm once, then stop open-ended polishing.
4. Run one anti-slop pass: use the active Impeccable hook or detector, not both.
   Apply the relevant Taste checks to the rendered result and distinguish true
   defects from aesthetic preferences.
5. Verify keyboard flow, focus, semantics, labels, contrast, zoom/reflow,
   reduced motion, touch targets, long content, and relevant UI states.
6. Review the source diff for accidental churn, debug output, dead code,
   temporary assets, duplicated styles, and unauthorized content or route
   changes.
7. For a new or replacement world, complete Impeccable's finish review and
   document the built system. A narrow extension or polish pass must not rewrite
   DESIGN.md.

For native/mobile or data-heavy surfaces, cross-check the relevant
`ui-ux-pro-max --domain ux` outcomes (touch targets, safe areas, dynamic type,
contrast parity, color-not-sole-indicator) rather than the web-only Taste
checklist. Fold this into one Impeccable finish pass; do not stack a second
pre-delivery checklist on top of it.

Release blockers are failed requirements, correctness, accessibility, product
truth, security, or project budgets. An aesthetic detector finding blocks only
when it violates the brief, approved direction, or established system.

## Common conflict decisions

- Centered versus asymmetric hero: the brief, content, and committed
  composition decide.
- One accent versus a full palette: the committed color strategy decides.
- Inter or another commonly banned font: existing brand, licensing, language
  coverage, readability, and performance decide.
- Imagery required versus typography-led: the surface's content and approved
  direction decide.
- Motion everywhere versus restraint: user value, performance, and reduced
  motion decide. Never animate to satisfy a dial.
- Double-bezel containers versus no nested cards: the committed material system
  and real hierarchy decide; blanket enclosure recipes lose.
- Dual theme versus one locked theme: project requirements and actual use scene
  decide.
- Icon library versus authored SVG: preserve the incumbent family; use an
  accessible authored SVG for product-specific geometry when justified.
- Official design-system package versus current stack: platform contract or an
  explicit brief can require it; visual resemblance cannot.
- `ui-ux-pro-max` generated palette/type/tokens versus existing brand or
  approved comp: the committed direction and existing tokens win; generated
  values are candidates, not overrides.
- Dashboards, data tables, charts, and native/mobile/desktop detail: owned by
  `ui-ux-pro-max` plus Impeccable's Operate/native guidance, not by the Taste
  specialists, which disclaim these surfaces.

At handoff, state which core skills (Impeccable, frontend-design, Taste,
ui-ux-pro-max) and optional specialist were used, what each contributed, and
which conflicting rules were deliberately suppressed. Keep the report concise.
