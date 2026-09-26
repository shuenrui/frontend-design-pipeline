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
