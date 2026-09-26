## Optional component-library reference

When the project uses shadcn/ui, `ui-styling` is the owner and its
`references/upstream-shadcn/` tree (a vendored copy of the official
`shadcn-ui/ui` skill) is authoritative over any summary in this pipeline or in
`ui-ux-pro-max`'s stack data. Read the project's primitive base with
`npx shadcn@latest info` before writing component code; it may be Base UI,
Radix, or React Aria, and custom triggers differ between them (`asChild` vs
`render`). Do not assume Radix.

Other Taste helpers:

- `ui-ux-pro-max` is a core data engine, not an aesthetic specialist, so it
  stays available alongside any one specialist above. When a specialist is
  loaded, the specialist owns the look; use `ui-ux-pro-max` for data,
  UX/accessibility rules, charts, icons, and stack guidance, and let its
  generated palette/type yield to the committed direction.
- Load `redesign-existing-projects` only as a diagnostic checklist for a
  targeted modernization that preserves stack and function. Impeccable remains
  the redesign owner.
- Load `full-output-enforcement` only when the user requests exhaustive inline
  files or a finite complete set. Normal shared-workspace edits do not need it.
- Never load `design-taste-frontend-v1` alongside the current Taste skill.

If no specialist's trigger is satisfied, load none. More design skills do not
mean better design.
