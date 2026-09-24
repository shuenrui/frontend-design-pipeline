# Upstream provenance and sync

Every skill this pipeline routes is owned by someone else and changes under us.
Until 2026-09-24 nothing here recorded which version we were routing against,
so drift was invisible: `frontend-design` had been superseded upstream on
2026-09-03 with no local signal, and `impeccable` existed as three diverged
copies with three different file counts.

This file is the pin list. Update it in the same commit as any skill sync.

## Installed skills this pipeline depends on

Pinned as recorded on 2026-09-24. Local installs are plain directories, not git
checkouts, so the commit below is the upstream state each copy was taken from.

| Skill | Upstream | Pinned at | Status |
| --- | --- | --- | --- |
| `frontend-design-pipeline` | this repo | — | local |
| `frontend-design` | `anthropics/skills` · `skills/frontend-design/` | `41bbe19` (2026-09-03) | synced |
| `impeccable` | `pbakaus/impeccable` | `e0881d2` (2026-09-22) | **behind — see blocker** |
| `design-taste-frontend` | `leonxlnx/taste-skill` | not verified | unaudited |
| `gpt-taste`, `high-end-visual-design`, `minimalist-ui`, `industrial-brutalist-ui`, `image-to-code`, `imagegen-frontend-web`, `imagegen-frontend-mobile`, `brandkit`, `stitch-design-taste`, `redesign-existing-projects`, `full-output-enforcement`, `design-taste-frontend-v1` | `leonxlnx/taste-skill` | not verified | unaudited |
| `ui-ux-pro-max` | `nextlevelbuilder/ui-ux-pro-max-skill` | npm `ui-ux-pro-max-cli@2.15.0` | current |
| `ui-styling` | `claudekit` (independent) + vendored shadcn refs | refs from `shadcn-ui/ui` `c257f68` | augmented |
| `apple-design` | `emilkowalski/skills` · `skills/apple-design/` | `d16ebe6` (2026-09-23) | added |
| `emil-design-eng` | `emilkowalski/skills` · `skills/emil-design-eng/` | `d16ebe6` (2026-09-23) | added |
| `mobile-native` | `emilkowalski/skills` · `skills/mobile-native/` | `d16ebe6` (2026-09-23) | added |

## Blocker: `impeccable` cannot be file-synced

Upstream `e0881d2` changed runtime architecture. It is not a compatible
in-place refresh.

| | Local now | Upstream `e0881d2` |
| --- | --- | --- |
| Scripts | 107 files | 11 files |
| Setup entry | `node scripts/context.mjs` | `scripts/impeccable context` (sh launcher) |
| Engine | `.mjs` sources in the skill dir | compiled per-OS binary, fetched on first run |
| `SKILL.md` | 10,401 B | 11,868 B (`.agents`), 12,115 B (`.claude`) |

Overwriting the local tree with upstream files would delete every `.mjs` script
this install calls, including the anti-pattern detector and the hook that
Stage 5 depends on, and leave a launcher with no binary. Upgrading means
adopting upstream's release channel — installing a compiled native executable
— which is a separate decision from a documentation refresh.

Until that happens: keep the local `impeccable`, and do not "just copy
`SKILL.md`", because the newer prose documents commands the local scripts do
not implement.

## Vendoring rule

`ui-styling/references/upstream-shadcn/` holds a verbatim copy of the official
shadcn/ui agent skill. Vendored trees are never hand-edited — fix the local
summary instead, so the upstream copy stays re-fetchable. Re-copy it when
`shadcn-ui/ui` `skills/shadcn/` moves.

## Evaluating additions

Candidates enter this pipeline only by filling a capability no installed skill
carries. Popularity is not a reason. Rejected on 2026-09-24, with reasons
recorded so they are not re-litigated:

- `pbakaus/adapt` — already inside `impeccable` as `reference/adapt.md`.
- `addyosmani/accessibility` — `ui-ux-pro-max` owns the accessibility slot.
- `shadcn-ui/shadcn` — vendored into `ui-styling` rather than installed as a
  competing skill.
- `wshobson/interaction-design` — subsumed by the motion specialists above.
- `mengto/beautiful-shadows` — a 2.5 KB CSS recipe with no decision procedure.
- `superfuture/design-review` — **rejected for safety.** Its `SKILL.md`
  instructs the agent to POST an anonymous identifier to
  `superfuture-metrics.pages.dev` on every review, and in "Pro mode" to upload
  the artifact under review — someone's UI code or screenshots — to
  `design-review-pro.jprimiani.workers.dev` with a license key. It also directs
  the agent never to produce Pro findings locally so they must come from that
  service. Unmaintained at 5 stars. This is a data-exfiltration path regardless
  of how good its rubric is.

Screen any third-party skill for network instructions before installing:

```bash
grep -rinE "curl|fetch\(|telemetry|metrics|ingest|analytics|upload|workers\.dev|license" <skill-dir>
```
