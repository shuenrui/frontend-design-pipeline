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

## Reading skill references

Loaded instructions are a budget, not a bonus. Reading three reference files
before writing any code can cost more than the design work itself, and these
files are written for humans: line counts lie.

- `wc -l` is not a size estimate. A 322-line reference file can hold ~68 KB
  because a handful of lines are very long. Check bytes, not lines, before
  opening a reference wholesale.
- Load the reference a stage actually needs, and only that one. Impeccable
  owns one playbook at a time; this pipeline's stages do not need
  `craft-floor.md` during planning, and loading it early is pure cost.
- For a long file, read a targeted range or grep for the section you need
  rather than reading it end to end. A whole-file read that exceeds the tool
  output cap comes back truncated and forces extra round trips — the
  expensive failure mode is the re-read, not the read.
- Prefer `ui-ux-pro-max` script queries over reading its data files: the search
  script returns the rows you asked for, while reading a CSV loads thousands of
  lines you will not use.
- Never load two aesthetic specialists to compare their prose. Route per the
  tables below and load one.
- After intake, do not re-read a skill's flow documents to confirm what you are
  about to do. One pass per owning document per session.

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

## One consolidated intake

The pipeline owns exactly one question round per task, at this point, before
Impeccable's flows run. Impeccable `init` and `new-work` each carry their own
interview, and `context` blocks until `PRODUCT.md` exists, so an uncoordinated
run can ask the same product truth two or three times over.

Collect everything the downstream flows will want in one pass, then never ask
for it again:

- subject, audience, and the single job of the surface;
- product truth: real names, hours, prices, places, claims, and supplied copy
  or assets;
- brand, references, existing tokens, and any look the user explicitly pinned;
- delivery shape, preservation level, and platform/browser constraints;
- content that is real, synthetic-but-labelled, or still missing;
- performance, motion budget, and accessibility target where they matter.

Ask it as one compact grouped question, not a sequence. Then write the answers
down where the owning flow reads them — `PRODUCT.md` for Impeccable context —
so the downstream interview is satisfied by the artifact rather than re-run.

When an answer is genuinely unknown, record the inference and label it, then
continue; do not stop to confirm an assumption the brief already constrains.
Only re-open intake when new information changes scope, product truth, or the
preserve/replace decision — that is an escalation, not a second round.

Treat a downstream "run the interview" instruction as already satisfied when
this stage produced the answers it wanted. Announce that in one line, for
example: product truth captured at intake; `init` proceeds without re-asking.

## Single-file artifacts

Not every task is a repository. When the deliverable is one self-contained
file, or a page a user will paste into a sandbox, classify the delivery shape
as single-file and drop the ceremony that cannot change its output: no build
tooling, no dev server, no dependency install, no lint/typecheck pass, no
framework migration, no repo-wide search for a design system that does not
exist. Inline the styles, keep the file renderable on its own, and record
tokens at the top so the artifact remains the source of truth.

Verify it by opening the file and exercising the interaction path, not by
running project pipelines. Stage 5's build/typecheck/lint steps and any
detector pass are skipped when there is no project for them to run against;
state that plainly rather than reporting them as passing.

Scale the rest of the flow the same way. For a narrow refinement or a single
component, concept generation, a design system lookup, and a full finish review
are cost without leverage — classify in Stage 1 decides. Run the stages that can
change this task's output and mark the rest not applicable in one line.

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

## Optional component-library reference

When the project uses shadcn/ui, `ui-styling` is the owner and its
`references/upstream-shadcn/` tree (a vendored copy of the official
`shadcn-ui/ui` skill) is authoritative over any summary in this pipeline or in
`ui-ux-pro-max`'s stack data. Read the project's primitive base with
`npx shadcn@latest info` before writing component code; it may be Base UI,
Radix, or React Aria, and custom triggers differ between them (`asChild` vs
`render`). Do not assume Radix.

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

## Generated imagery

When the committed direction needs an image that does not exist and cannot be
sourced, generate it. Use whatever image capability the runtime provides — the
host's image tool, a Codex or other model-backed generator, or a local
diffusion CLI — and treat the specific model as an environment detail, not a
pipeline step. Detect what exists; do not assume a generator is available and
do not fail the task when one is absent.

Imagery is a direction decision, so request it during Stage 3, before code.
Decide what the image must carry — subject, framing, light, aspect ratio,
palette relationship, where it sits in the layout — then generate toward that
brief, rather than generating first and finding a use for the result. Generate
at the aspect ratio and crop the layout will actually consume; a regenerated
image is a new composition decision, not a re-run.

Before generating, classify the image's truth claim:

- **Safe to generate.** Original and decorative material: texture, paper grain,
  ambient light, abstractions of the subject's own world, illustrative motifs,
  iconography, patterns, empty states, backgrounds, and clearly stylized
  non-representational art. These express the direction without asserting facts.
- **Never generate as fact.** Anything that impersonates commercial or product
  truth: the actual premises, products, food, staff, or customers of a named
  real business; screenshots of a real interface; real artwork or a live
  brand's identity; testimonials, press logos, awards, or client work. A
  convincing generated photograph of a real cafe is a claim that the cafe looks
  like that, which is fabrication regardless of how well it renders. Reach for
  supplied assets, or leave an explicit replacement note.
- **Generate only when labeled.** Placeholders that will ship in view of users
  as stand-ins for real photography. Label them in the file or the markup, and
  in the handoff.

A synthetic image inherits this pipeline's existing content rule: real supplied
content always wins, synthetic must be labeled, and a missing asset is a
replacement note rather than an invention. Generated imagery never substitutes
for a product's actual claims.

Technical duties after generating:

- Save into the project's real asset location and reference it by relative
  path. Never leave a generated file outside the deliverable or reference an
  absolute scratch path.
- Provide meaningful `alt`, explicit `width`/`height` or an aspect-ratio box,
  `loading="lazy"` below the fold, and a `decoding` hint so the image cannot
  cause layout shift.
- Preserve the direction's palette relationship. A generated image that fights
  the token system is a defect in the composition, not a reason to repaint the
  page.
- Keep it in budget. For a single-file artifact, an embedded raster inflates the
  payload; prefer CSS-drawn texture there, and say why when you choose one.
- Disclose in the handoff which images were generated, by what, and which are
  awaiting real assets, so a later pass can replace rather than re-generate.

Routing stays as follows: `imagegen-frontend-web` and `imagegen-frontend-mobile`
own *design-direction comps* — images to review a layout or screen concept.
`brandkit` owns identity boards and logo systems. Plain asset generation for
placement inside a page is this section, which needs no aesthetic specialist
loaded and is not a competing direction.

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

The Impeccable detector resolves declarations statically. It does not evaluate
your theme system, and some findings are unreliable enough that acting on them
uncritically costs more time than skipping the pass.

Trust tiers, from a v0.1.5 reproduction pass:

- **Reproduce before acting — `cramped-padding`.** The detector cannot resolve
  `clamp()`, `min()`, or `max()`. A container with
  `padding: clamp(20px, 3vw, 30px)` and a visible border reports *"children
  flush against border on all sides (no inset)"* even though it is correctly
  padded at every viewport. Confirmed reproducible. Treat it as a false positive
  unless the rendered result shows real collision, and say so rather than
  "fixing" it.
- **Re-resolve before acting — `low-contrast`.** A reported ratio pairs a
  foreground and background the detector found, which is not necessarily the
  pair a user sees. In a themed project, a dark-theme token can be measured
  against the light ground, or an unused pairing reported while the live one
  passes. Recompute the ratio for the actual rendered element in the theme the
  user will see, for both themes when the project ships both, and act only on
  the pairs that genuinely fail. Do not bulk-fix a contrast list.
- **Generally sound** — semantics, missing labels, focus-visible absence,
  duplicated utility patterns, and structural tells.

Cheap ways to cut noise before you triage anything:

```bash
# scope to the domain you are actually reviewing
<skill>/scripts/impeccable detect --scope type,layout <targets>
# suppress advisory-only findings
<skill>/scripts/impeccable detect --no-advisory <targets>
# scan the rendered page rather than the source, when a dev server exists
<skill>/scripts/impeccable detect --viewport 390x844 http://localhost:PORT/
```

Inline ignore comments (`impeccable-disable`) and project ignore rules are the
durable way to retire a recurring false positive class; use them instead of
re-litigating the same finding every run. When a detector category is mostly
noise on your token setup, verify contrast by measuring computed styles in the
browser and say which method produced the result.

Report findings in three buckets — true defects fixed, false positives rejected
with reason, real issues left out of scope — so a future run can calibrate
against the pass instead of repeating it.

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
- Motion duration and easing when Impeccable's `animate.md` and a motion
  specialist disagree: `animate.md` owns the budget and whether motion exists
  at all; the specialist owns the specific curve, spring parameters, and
  component-level timings inside that budget. A specialist's faster or slower
  default never expands Impeccable's budget.
- Spring versus duration-based transition: springs for anything the user can
  touch, drag, or interrupt; CSS transitions/keyframes for bounded state changes
  with no interruption risk, and where the project's motion library cannot
  express springs. Follow the existing stack first.
- Primitive base for shadcn/ui components: `npx shadcn@latest info` and
  `references/upstream-shadcn/rules/base-vs-radix.md` decide. Assuming Radix
  because shadcn historically shipped on it is wrong; the current default is
  Base UI.
- Double-bezel containers versus no nested cards: the committed material system
  and real hierarchy decide; blanket enclosure recipes lose.
- Dual theme versus one locked theme: project requirements and actual use scene
  decide.
- Icon library versus authored SVG: preserve the incumbent family; use an
  accessible authored SVG for product-specific geometry when justified.
- Official design-system package versus current stack: platform contract or an
  explicit brief can require it; visual resemblance cannot.
- Generated imagery versus product truth: supplied assets win; decorative and
  abstract original imagery may be generated; an image asserting that a real
  business, product, or person looks a specific way is fabrication and needs a
  replacement note, not a render.
- Ceremony versus delivery shape: a single-file artifact has no build, lint,
  dev server, or design system to consult. Skipping those checks is correct,
  reporting them as satisfied is not.
- `ui-ux-pro-max` generated palette/type/tokens versus existing brand or
  approved comp: the committed direction and existing tokens win; generated
  values are candidates, not overrides.
- Dashboards, data tables, charts, and native/mobile/desktop detail: owned by
  `ui-ux-pro-max` plus Impeccable's Operate/native guidance, not by the Taste
  specialists, which disclaim these surfaces.

At handoff, state which core skills (Impeccable, frontend-design, Taste,
ui-ux-pro-max) and which optional specialist — aesthetic, output/workflow,
motion, or mobile-feel — were used, what each contributed, and which
conflicting rules were deliberately suppressed. Keep the report concise.
