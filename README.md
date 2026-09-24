# frontend-design-pipeline

A **coordinator skill** for [opencode](https://opencode.ai) that acts as the
traffic controller for frontend design work. It does not add another aesthetic —
it gives each installed design skill one job, selects only the relevant
specialists, and prevents competing recipes from steering the same decision.

It orchestrates six skill families into a single pipeline:

| Role | Skill(s) | Source |
| --- | --- | --- |
| Lifecycle owner | `impeccable` | [pbakaus/impeccable](https://github.com/pbakaus/impeccable) |
| Art director | `frontend-design` | [anthropics/skills](https://github.com/anthropics/skills) |
| Aesthetics / anti-slop | `design-taste-frontend`, `gpt-taste`, `minimalist-ui`, `industrial-brutalist-ui`, `high-end-visual-design`, `image-to-code`, `imagegen-frontend-web` / `-mobile`, `brandkit`, `stitch-design-taste`, `redesign-existing-projects`, `full-output-enforcement` | [leonxlnx/taste-skill](https://github.com/leonxlnx/taste-skill) |
| Design-system data engine | `ui-ux-pro-max` | [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) |
| Motion / interaction specialists | `apple-design` (spring and gesture physics), `emil-design-eng` (easing, duration, component polish) | [emilkowalski/skills](https://github.com/emilkowalski/skills) |
| Mobile-web feel | `mobile-native` | [emilkowalski/skills](https://github.com/emilkowalski/skills) |
| Component-library reference | `ui-styling` + vendored official shadcn skill | [shadcn-ui/ui](https://github.com/shadcn-ui/ui) |

Which upstream commit each of these is routed against is pinned in
[`PROVENANCE.md`](PROVENANCE.md).

## What it does

`frontend-design-pipeline` defines an **authority order**, **one job per skill**,
and a **5-stage flow** (classify → establish truth → choose one direction →
implement → verify/finish), plus routing tables and conflict-resolution rules so
the skills above cooperate instead of fighting.

`ui-ux-pro-max` fills the gaps the prose aesthetic skills explicitly disclaim —
dashboards, data tables, charts, and native/mobile/desktop detail — with
deterministic, queryable data: palettes with semantic tokens, font pairings, a
119-rule UX/accessibility catalog, 25 chart types, and 22 stacks. Its generated
values are treated as **candidates** that yield to the brief and any existing
design system, never as overrides.

## Install

This skill is a folder containing `SKILL.md`. Clone it into your opencode skills
directory:

```bash
git clone https://github.com/shuenrui/frontend-design-pipeline.git \
  ~/.config/opencode/skills/frontend-design-pipeline
```

### Dependency: ui-ux-pro-max

The data-engine role requires `ui-ux-pro-max` (Python 3 + Node). Install it
globally so the pipeline can call its `search.py`:

```bash
npm install -g ui-ux-pro-max-cli
uipro init --ai universal --global   # installs to ~/.agents/skills/ui-ux-pro-max
```

The pipeline calls it at `~/.agents/skills/ui-ux-pro-max/scripts/search.py`. If
your install location differs, the coordinator confirms the path from the loaded
skill.

The other three families (`impeccable`, `frontend-design`, the Taste skills)
should also be installed for full coverage; the pipeline degrades gracefully
when a specialist is absent.

### Optional: motion, mobile-feel, and shadcn specialists

These fill gaps the four core families do not cover — `impeccable`'s
`animate.md` has no spring/gesture model, and `ui-ux-pro-max` ships zero spring
rows in its motion data.

```bash
git clone --depth 1 https://github.com/emilkowalski/skills.git /tmp/emil
for s in apple-design emil-design-eng mobile-native; do
  cp -R /tmp/emil/skills/$s ~/.agents/skills/$s
done
```

Install only the ones you need. Each is routed by a specific trigger in
`SKILL.md`; an unused specialist is dead weight in the prompt, not a bonus.

For shadcn/ui projects, vendor the official skill into `ui-styling` so its
current CLI, registry, MCP, and Base UI vs Radix rules win over any summary:

```bash
mkdir -p ~/.agents/skills/ui-styling/references/upstream-shadcn/rules
B=https://raw.githubusercontent.com/shadcn-ui/ui/main/skills/shadcn
cd ~/.agents/skills/ui-styling/references/upstream-shadcn
for f in SKILL.md cli.md registry.md customization.md mcp.md; do curl -fso $f $B/$f; done
for f in base-vs-radix chat composition forms icons styling; do curl -fso rules/$f.md $B/rules/$f.md; done
```

## Usage

opencode loads the skill automatically for frontend design work. Optionally drop
`bootstrap.md` into your project or agent instructions to force-load the
pipeline before any other design skill.

Restart opencode after installing so this skill (and `ui-ux-pro-max`) are
discovered.

## Files

- `SKILL.md` — the coordinator (authority order, skill roles, 5 stages, routing,
  conflict rules).
- `bootstrap.md` — optional instruction snippet that forces the pipeline to load
  first.
- `PROVENANCE.md` — upstream pin list, the `impeccable` sync blocker, vendoring
  rule, and the criteria (and rejections) used when evaluating new skills.
