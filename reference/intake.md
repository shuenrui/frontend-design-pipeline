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
