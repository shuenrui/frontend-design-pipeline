# Upstream provenance and sync

Every skill this pipeline routes is owned by someone else and changes under us.
Until 2026-09-24 nothing here recorded which version we were routing against,
so drift was invisible: `frontend-design` had been superseded upstream on
2026-09-03 with no local signal, and `impeccable` existed as three diverged
copies with three different file counts.

This file is the pin list. Update it in the same commit as any skill sync.

## Installed skills this pipeline depends on

Pinned as recorded on 2026-09-24. Local installs are plain directories, not git
checkouts, so each entry is the upstream commit, or the npm/engine release for
installed artifacts, that the local copy was taken from.

| Skill | Upstream | Pinned at | Status |
| --- | --- | --- | --- |
| `frontend-design-pipeline` | this repo | — | local |
| `frontend-design` | `anthropics/skills` · `skills/frontend-design/` | `41bbe19` (2026-09-03) | synced |
| `impeccable` | `pbakaus/impeccable` | engine `0.1.5`, CLI `impeccable@4.1.0` (2026-09-24) | synced via installer |
| `design-taste-frontend` | `leonxlnx/taste-skill` | not verified | unaudited |
| `gpt-taste`, `high-end-visual-design`, `minimalist-ui`, `industrial-brutalist-ui`, `image-to-code`, `imagegen-frontend-web`, `imagegen-frontend-mobile`, `brandkit`, `stitch-design-taste`, `redesign-existing-projects`, `full-output-enforcement`, `design-taste-frontend-v1` | `leonxlnx/taste-skill` | not verified | unaudited |
| `ui-ux-pro-max` | `nextlevelbuilder/ui-ux-pro-max-skill` | npm `ui-ux-pro-max-cli@2.15.0` | current |
| `ui-styling` | `claudekit` (independent) + vendored shadcn refs | refs from `shadcn-ui/ui` `c257f68` | augmented |
| `apple-design` | `emilkowalski/skills` · `skills/apple-design/` | `d16ebe6` (2026-09-23) | added |
| `emil-design-eng` | `emilkowalski/skills` · `skills/emil-design-eng/` | `d16ebe6` (2026-09-23) | added |
| `mobile-native` | `emilkowalski/skills` · `skills/mobile-native/` | `d16ebe6` (2026-09-23) | added |

## Updating impeccable

Do not copy files into an impeccable install. Upstream ships an installer that
writes provider-specific builds and fetches a matching engine binary; a manual
copy produces a tree the launcher cannot run.

```bash
npx impeccable@latest update
# or re-install for specific harnesses:
npx impeccable@latest install --providers=claude,agents,qoder --scope=global --force
```

`--providers` accepts the harness folders this pipeline assumes: `claude` →
`~/.claude/skills`, `agents` → `~/.agents/skills`, `qoder` → `~/.qoder/skills`.
Each receives a different build (57 files for `.agents`, 52 for `.claude` and
`.qoder`) — those counts differing is correct, not drift. Confirm after any
update that the engine answers and the detector runs:

```bash
~/.agents/skills/impeccable/scripts/impeccable engine-probe   # -> impeccable-engine <version>
~/.agents/skills/impeccable/scripts/impeccable detect --json <some-file>
```

### History: the 2026-09-24 architecture break

Before this pipeline pinned anything, `impeccable` was a Node skill: it ran
`node scripts/context.mjs` and carried a 107-file `.mjs` tree including the
anti-pattern detector. Upstream replaced that with a compiled engine.

| | before | after |
| --- | --- | --- |
| Scripts | 107 `.mjs` files | 11 files + per-OS binary |
| Setup entry | `node scripts/context.mjs` | `scripts/impeccable context` |
| Detector | `.mjs` sources in the skill dir | engine binary, `…/scripts/bin/<os>-arch/` |
| Copies | 3 diverged trees (152 / 147 / 147 files) | 3 provider builds from one command |

The local copies had also silently diverged from each other, with no
provenance file to reveal it. A hand-copy of upstream `SKILL.md` at that point
would have documented commands the local scripts did not implement, and a
recursive copy of the upstream tree would have deleted the detector. Both were
avoided only because the file counts were compared first — which is the reason
this section exists.

The install ran with `--no-hooks`, so the detector is not wired to fire
automatically on UI edits; the skill falls back to a manual `detect` pass, which
it announces via `MANUAL_DETECTOR_REQUIRED`. Add hook manifests later with
`npx impeccable@latest install` without `--no-hooks` if you want it automatic.
The engine binary is fetched from GitHub releases and verified against a
`.sha256` sidecar, failing closed when the sidecar or a hasher is unavailable.

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
