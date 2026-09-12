# frontend-design-pipeline

A **coordinator skill** for [opencode](https://opencode.ai) that acts as the
traffic controller for frontend design work. It does not add another aesthetic —
it gives each installed design skill one job, selects only the relevant
specialists, and prevents competing recipes from steering the same decision.

It orchestrates four skill families into a single pipeline:

| Role | Skill(s) | Source |
| --- | --- | --- |
| Lifecycle owner | `impeccable` | [pbakaus/impeccable](https://github.com/pbakaus/impeccable) |
| Art director | `frontend-design` | [anthropics/claude-code](https://github.com/anthropics/claude-code) |
| Aesthetics / anti-slop | `design-taste-frontend`, `gpt-taste`, `minimalist-ui`, `industrial-brutalist-ui`, `high-end-visual-design`, `image-to-code`, `imagegen-frontend-web` / `-mobile`, `brandkit`, `stitch-design-taste`, `redesign-existing-projects`, `full-output-enforcement` | [leonxlnx/taste-skill](https://github.com/leonxlnx/taste-skill) |
| Design-system data engine | `ui-ux-pro-max` | [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) |

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
