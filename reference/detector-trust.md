### Detector findings are evidence, not verdicts

The Impeccable detector resolves declarations statically. It does not evaluate
your theme system, and some findings are unreliable enough that acting on them
uncritically costs more time than skipping the pass.

### Never read raw detector JSON into context

`detect --json` spends 53% of its payload repeating the same `description`
boilerplate for every finding — measured at 628 bytes per finding, so a 111-
finding pass costs ~17,400 tokens to say what 2,100 tokens would carry. Project
first, then read details only for the specific rule you are about to act on:

```bash
<skill>/scripts/impeccable detect --json <targets> 2>/dev/null \
  | jq -r '.[] | "\(.antipattern)|\(.severity)|L\(.line)|\(.snippet[0:60])"'
```

Measured on a 9-finding page: 5,685 B raw against 670 B projected — 12% of the
size for the same triage value. `--quiet` collapses further still, to a count
plus one line per rule, which is usually enough to decide whether a deeper look
is warranted at all. Group repeated identical findings rather than listing them:
four identical `cramped-padding` hits are one defect with four instances.

`--scope <domain>`, `--no-advisory`, and `--viewport` reduce work only when they
actually exclude something. On a themed test page both `--scope type` and
`--no-advisory` returned the identical 9 findings, so do not treat them as
noise controls by reflex — measure the count, then claim the saving.

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
