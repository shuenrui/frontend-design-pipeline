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
