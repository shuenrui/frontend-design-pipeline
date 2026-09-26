## Reading skill references

Loaded instructions are a budget, not a bonus. Measured cost of a new-build
landing page as this pipeline routes it, before a single line of code:

| Load | Bytes | ≈Tokens |
| --- | --- | --- |
| `design-taste-frontend/SKILL.md` | 87,253 | 21,813 |
| `impeccable/reference/new-work.md` | 52,769 | 13,192 |
| `ui-ux-pro-max/SKILL.md` | 28,066 | 7,017 |
| this router (`SKILL.md`) | 21,250 | 5,313 |
| `impeccable/SKILL.md` | 11,658 | 2,915 |
| `frontend-design/SKILL.md` | 9,390 | 2,348 |
| `impeccable` `context` output | ~3,000 | 750 |
| `impeccable/reference/craft-floor.md` | 5,500 | 1,375 |
| **total** | **218,886** | **≈54,700** |

Two files are 64% of that. A raw detector pass can add ~17,000 more on top,
which is why projection below is not a micro-optimization. Spend the budget
knowing these numbers.

- **The Taste skill is 87 KB, and it is monolithic by design.** Upstream ships
  it as one file with no `reference/` split, so loading the skill loads all of
  it. Do not invoke it as a skill when you need one part of it. Read the
  numbered section you need by path and range instead — locate it first, because
  line numbers move between versions:

  ```bash
  grep -n '^## ' ~/.agents/skills/design-taste-frontend/SKILL.md
  ```

  A direction decision needs §1 dials and §2 brief→system map. An anti-slop
  pass needs §9 AI TELLS and §14 pre-flight. Neither needs the appendices or the
  block library. Targeted sections typically cost a few KB against 87.
- Never ingest raw `detect --json`. Project it — see
  [detector-trust.md](detector-trust.md). 53% of that payload is the same
  `description` boilerplate repeated per finding.
- `wc -l` is not a size estimate. A 322-line file can hold ~68 KB because a
  handful of lines are very long. Check bytes, not lines.
- Load the reference a stage actually needs, and only that one. Impeccable owns
  one playbook at a time; `craft-floor.md` is not needed during planning, and
  loading it early is pure cost.
- A whole-file read that exceeds the tool output cap returns truncated and
  forces extra round trips — the expensive failure is the re-read, not the read.
- Prefer `ui-ux-pro-max` script queries to reading its data files. The search
  script returns matched rows; a CSV read loads thousands you will not use.
- Never load two aesthetic specialists to compare their prose. Route per the
  tables in the router and load one.
- After intake, do not re-read a skill's flow documents to confirm what you are
  about to do. One pass per owning document per session.
- **Scale the load to the task.** A narrow refinement, a single component, or a
  single-file artifact does not need the new-world surface: `new-work.md` and the
  full Taste skill are 65 KB of ceremony for a button fix. Classify first, then
  load only what that classification can change.
- Offload heavy generative work rather than doing it inline. Delegating an image
  to `codex exec` runs the ~18k-token generation in *its* context and returns a
  path, so the orchestrating session stays lean. That is a real efficiency, not
  just a capability fallback.
