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
