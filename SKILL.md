---
name: frontend-design-pipeline
description: Mandatory coordinator for frontend design work. Use before creating, redesigning, reviewing, polishing, or visually changing websites, landing pages, product UI, dashboards, data viz, components, forms, responsive layouts, native/mobile/desktop UI, motion, generated imagery, or design systems. Owns one consolidated intake so downstream flows do not re-ask, orchestrates Impeccable, Anthropic frontend-design, the Leonxlnx Taste skills and the ui-ux-pro-max data engine, routes optional motion, mobile-feel and shadcn specialists, scales ceremony to the delivery shape, and calibrates detector findings against known false-positive classes.
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
   Taste, motion, or mobile-feel specialist as implementation guidance or
   anti-slop lint.
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

**A user-pinned look overrides every skill's anti-slop list.** When the brief
names a direction that a skill's banned-defaults list also names — warm cream
with a serif display and a terracotta accent, near-black with one acid accent,
broadsheet hairlines, SaaS cards, or anything else a skill treats as a tell —
the direction stands, and rung 1 is the reason. Escape the cliché in the
rendition, not the direction: earn it through the subject's own materials, real
content, spacing, and detail rather than by substituting a different palette the
skills find more original. Do not silently re-interpret an approved look into a
less recognizable one, and do not report the pinned direction as a defect. This
holds whether or not you have read the skill that bans it.

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

When this pipeline's consolidated intake already captured product truth, treat
Impeccable's `init` interview as satisfied: write `PRODUCT.md` from the intake
answers and continue into the owning playbook. `init` is a place to put answers
you already have, not a reason to ask the user again.

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

This skill is 87 KB and ships monolithic — invoking it loads all of it, which is
the single largest cost in a run. When one part is what the stage needs, grep its
numbered headings and read that range by file path instead of loading the skill.
Reserve the full load for genuinely design-led work: a new visual world, a
redesign, or a landing or portfolio page where the whole directive set can
change the output.

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

## Loading discipline

Loaded instructions are a budget, not a bonus. A fully-loaded new-build run
costs ~55k tokens before any code, and two files account for 64% of it. Read
[reference/loading-budget.md](reference/loading-budget.md) for the measured
table, for the rule against loading the 87 KB Taste skill whole when one
numbered section is what you need, and for scaling load to the task. Project
detector JSON rather than reading it raw — over half that payload is the same
boilerplate repeated per finding.

## Stage 1: classify

Before editing, classify the request on four axes:

- Work type: new visual world, new surface in an established world, explicit
  redesign, narrow refinement, audit/review, or visual bug fix.
- Surface mode: Persuade, Operate, Read, or Experience, using Impeccable's
  definitions.
- Output: runnable code, design/reference images, mobile images, brand board,
  Stitch artifact, or review only.
- Delivery shape: repository work in an existing project, or a self-contained
  single-file artifact. See Single-file artifacts.
- Preservation level: preserve, evolve within the system, or replace with
  explicit approval.

Ask one compact question only when the answer changes scope, product truth, or
the preserve/replace decision. Otherwise infer from the code and brief.

## Intake and delivery shape

One pipeline-owned question round, then never ask again. Load
[reference/intake.md](reference/intake.md) at Stage 1 whenever the brief lacks
product truth, a pinned look, or the delivery shape, and always before choosing
single-file versus repository work. It defines the consolidated intake, writing
answers into `PRODUCT.md` so Impeccable's `init` interview is already satisfied,
and the single-file mode that drops build, lint, and dev-server ceremony.

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

Load at most one motion/interaction specialist:

| Skill | Load only when |
| --- | --- |
| `apple-design` | The surface has gesture-driven or physics-bearing interaction: drag, swipe, sheets, carousels, pull-to-refresh, momentum dismissal, interruptible transitions, spring settle, or translucent-material depth. It supplies spring parameters (damping/response), velocity handoff, momentum projection, and rubber-banding that no other skill carries. Not for static or content-only surfaces. |
| `emil-design-eng` | A component needs interaction polish at the CSS level: enter/exit easing choice, duration, `:active` feedback, origin-aware popovers, tooltip timing, `@starting-style`, or masking a weak transition. It owns the concrete motion-implementation rules and the Before/After review table. Not for direction selection. |
| `mobile-native` | The deliverable runs in a mobile browser and must feel installed: sticky hover after tap, tap-highlight flash, `100vh` height bug, input zoom, tap latency, pull-to-refresh hijack, safe-area/notch content, long-press text selection, horizontal carousels. Its symptom table is the owner for these; `ui-ux-pro-max --domain ux` stays the source for accessibility targets and safe-area rules generally. |

These three address different layers and are not mutually exclusive with each
other: choose the one matching the dominant risk, or none. `apple-design` is
about interaction behavior over time, `emil-design-eng` about per-component CSS
craft, `mobile-native` about platform defects. A surface needing all three is
rare; if genuinely required, load the one for the current pass and finish
before moving on.

All three are subordinate to Impeccable's `animate.md` motion thesis. They
supply implementation rules and parameters; they never authorize motion the
locked direction and budget did not earn, and they never override a
project's existing motion library or reduced-motion handling.

`emil-design-eng` mandates a Before/After markdown table when reviewing UI code.
Adopt that format for motion and polish findings, but it does not create a
separate review pass — fold the table into Impeccable's single finish pass.

## Component libraries

When the project uses shadcn/ui, load
[reference/component-library.md](reference/component-library.md). Read the
primitive base with `npx shadcn@latest info`; it may be Base UI, Radix, or
React Aria, and custom triggers differ. Never assume Radix.

## Imagery

When the direction needs an image, generate it through **Codex** — that is the
preferred route on this setup for quality, via its built-in `image_gen` tool on
a ChatGPT plan login, with `--sandbox workspace-write` and the destination path
named in the request. Load
[reference/imagery.md](reference/imagery.md) before Stage 3 closes: it has the
exact invocation, the fallbacks when Codex is unavailable, the truth
classification that keeps decorative generation allowed and fabricated product
imagery not, and the alt/size/lazy duties for whatever ships. Confirm the shot
list before generating anything — each image runs ~18k tokens in Codex's own
context, which is why delegating is cheaper than generating inline.

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
  state, or story. Where the surface has gesture-driven or physics-bearing
  interaction, or a component needs motion/easing/duration craft, pull the
  concrete parameters from the one routed motion specialist instead of
  inventing curves; see Optional Taste routing.
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

### Detector findings are evidence, not verdicts

The detector resolves declarations statically and does not evaluate your theme
system. Load [reference/detector-trust.md](reference/detector-trust.md) before
acting on any `cramped-padding` or `low-contrast` finding; both have reproduced
or plausible false-positive classes, and bulk-fixing them costs more than the
pass saves.

## Common conflict decisions

Read [reference/conflicts.md](reference/conflicts.md) when two skills want the
same call. These are the ones that can block a release on their own:

- A user-pinned look beats every skill's anti-slop list; escape the cliche in
  the rendition, not the direction.
- Motion: Impeccable's `animate.md` owns whether motion exists and its budget;
  a routed specialist owns the curve and parameters inside that budget.
- Generated palette, type, and tokens are candidates. Existing brand tokens and
  the approved direction win.
- Dashboards, data tables, charts, and native/mobile/desktop detail belong to
  `ui-ux-pro-max` plus Impeccable's Operate/native guidance, not to the Taste
  specialists, which disclaim them.
- Generated imagery may be decorative or clearly stylized; it may never assert
  what a real business, product, or person looks like.
- A skipped check is reported as skipped, never as passing.
