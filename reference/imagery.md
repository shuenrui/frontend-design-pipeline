## Generated imagery

When the committed direction needs an image that does not exist and cannot be
sourced, generate it.

### How generation actually works here

A skill is instructions. It has no runtime, no process, and no credentials, so
it cannot generate an image. The agent executing this pipeline does the
generating, through whatever the host exposes.

**Preferred route: delegate to Codex.** On this setup the user has chosen Codex
for image quality, so use it for imagery assets even when the host also has a
native image tool. Native tools stay the fallback when Codex is absent,
unauthorized, or the request is a trivial one-off where the latency and token
cost are not justified.

```bash
codex exec --skip-git-repo-check --sandbox workspace-write -C <project-dir> \
  -o /tmp/codex-img.txt \
  "Generate an image with your built-in image_gen tool: <brief>. \
   Save it as <name>.png in the working directory and report the filename."
```

Verified interface details, each of which caused a failed attempt before it was
written down:

- **Interaction is a subprocess, not a session.** The agent shells out to
  `codex exec`, Codex runs headless with its own context and its own sandbox,
  and the agent gets stdout back. There is no MCP server involved and no chat
  handoff. The artifact crosses the boundary as a **file path**, never as bytes.
- **Global options precede the `resume`/`fork` subcommands.** `codex exec resume
  --last ...` fails on argument parsing; `codex exec --skip-git-repo-check
  resume --last "..."` works. Options placed after the prompt are read as extra
  positionals and error out.
- **Always pass `-o <file>`** and read that file, rather than letting the
  transcript stream into the session. It writes only the agent's final message,
  which keeps the ~18k-token generation out of the orchestrating context.
- **`-C <dir>` sets the working root**, so the image can be saved by relative
  name; it also keeps Codex out of unrelated project files.
- **Iterate with `resume --last`.** It retains the session, so a follow-up can
  be one sentence ("warmer light, no text in the image") instead of re-sending
  the entire brief. For a fresh branch of the same idea use `fork`.
- **`-i/--image` attaches a reference image** to a new prompt — useful for
  keeping a shot list visually consistent once one image in the series is
  approved. It is input only; it is not how generation happens.
- Sandbox choices are `read-only`, `workspace-write`, `danger-full-access`.
  Use `workspace-write` for saving files. `danger-full-access` and
  `--dangerously-bypass-approvals-and-sandbox` are not needed for image work and
  should not be used to get around a failure — the failure is almost always the
  read-only default or a missing destination.
- Expect a call to run minutes, not milliseconds. Do not fire generations
  one-after-another inside a turn while waiting on each; when several are
  independent, batch the shot list, run them, then continue once results land.

```bash
# cheap follow-up on an approved image, same session
codex exec --skip-git-repo-check --sandbox workspace-write -C <project-dir> \
  -o /tmp/codex-img2.txt resume --last \
  "Regenerate with warmer afternoon light. Keep composition identical."
```

Three things break if skipped. The default sandbox is read-only, so the image
generates and then cannot be saved — pass `--sandbox workspace-write`. Codex
writes originals to `~/.codex/generated_images/<session-id>/<call-id>.png`
before placing them, so name the destination in the request rather than hunting
for the file after. And budget for it: one verified generation cost ~18k tokens
and produced a 1254x1254 PNG, so a page needing six images is a real cost, not a
rounding error — confirm the shot list at Stage 3 before generating any of them.

Codex authorizes through a ChatGPT plan login (`auth_mode = chatgpt` in
`~/.codex/auth.json`), so **no API key is required and an absent
`OPENAI_API_KEY` is not evidence that generation is unavailable.** It also has
an API-key fallback mode; prefer the built-in `image_gen` tool on a subscription.
Check entitlement with `codex login status` or by reading the auth mode, never by
probing shell variables.

Write the brief to Codex the way you would write it to any generator: scene and
backdrop, then subject, then details, then constraints, with the intended use
stated so it picks the right polish level. Quote exact text verbatim and specify
typography and placement, since rendered text is the usual failure. Ask for the
aspect ratio and crop the layout will actually consume. Iterate with
single-change follow-ups rather than regenerating from scratch.

If the delegation route is unavailable, resolve in this order instead:

1. **A native image tool from the host.** Check the current tool list for an
   image generator (names vary by harness: `ImageGen`, `generate_image`,
   `text_to_image`). Call it directly with the same brief; it returns a local
   file path or URL.
2. **A configured MCP server or plugin that exposes image generation.**
   Available only when the user has set one up. Present only if it appears in
   the tool list; never assume one exists or claim availability because a
   provider supports images.
3. **A shell route with credentials already present.** An API call needs a key
   and an endpoint the user has configured. Test for the credential without
   printing it, e.g. `[ -n "$OPENAI_API_KEY" ] && echo SET`. If unset, this
   route does not exist — do not ask the user for a key mid-design and do not
   write one into a file. Remember a subscription login is a different
   credential path and grants generation without any key.
4. **Nothing.** Generate no image. Ship the layout with a defined image slot,
   explicit replacement notes, and the exact prompt you would have used, so the
   user can run it later. A missing image is a documented gap, never a reason
   to stop the build.

Do not confuse a CLI's image *input* flag with generation. `-i, --image <FILE>`
attaches images to a prompt. Whether a CLI can also produce images is a separate
capability, and some can — establish it by checking the tool's own feature
surface (`codex features list`) rather than by reading `--help` and concluding a
flag is absent.

Probe quietly and once. Do not enumerate the user's environment out loud, and
never echo a credential value, length included only when it helps debug.

When the direction depends on imagery the environment cannot produce, surface
that at Stage 3 while the direction is still cheap to change — a typography-led
or CSS-textured route may be the better plan anyway, and choosing it is a design
decision rather than a consolation.

Imagery is a direction decision, so request it during Stage 3, before code.
Decide what the image must carry — subject, framing, light, aspect ratio,
palette relationship, where it sits in the layout — then generate toward that
brief, rather than generating first and finding a use for the result. Generate
at the aspect ratio and crop the layout will actually consume; a regenerated
image is a new composition decision, not a re-run.

Before generating, classify the image's truth claim:

- **Safe to generate.** Original and decorative material: texture, paper grain,
  ambient light, abstractions of the subject's own world, illustrative motifs,
  iconography, patterns, empty states, backgrounds, and clearly stylized
  non-representational art. These express the direction without asserting facts.
- **Never generate as fact.** Anything that impersonates commercial or product
  truth: the actual premises, products, food, staff, or customers of a named
  real business; screenshots of a real interface; real artwork or a live
  brand's identity; testimonials, press logos, awards, or client work. A
  convincing generated photograph of a real cafe is a claim that the cafe looks
  like that, which is fabrication regardless of how well it renders. Reach for
  supplied assets, or leave an explicit replacement note.
- **Generate only when labeled.** Placeholders that will ship in view of users
  as stand-ins for real photography. Label them in the file or the markup, and
  in the handoff.

A synthetic image inherits this pipeline's existing content rule: real supplied
content always wins, synthetic must be labeled, and a missing asset is a
replacement note rather than an invention. Generated imagery never substitutes
for a product's actual claims.

Technical duties after generating:

- Save into the project's real asset location and reference it by relative
  path. Never leave a generated file outside the deliverable or reference an
  absolute scratch path.
- Provide meaningful `alt`, explicit `width`/`height` or an aspect-ratio box,
  `loading="lazy"` below the fold, and a `decoding` hint so the image cannot
  cause layout shift.
- Preserve the direction's palette relationship. A generated image that fights
  the token system is a defect in the composition, not a reason to repaint the
  page.
- Keep it in budget. For a single-file artifact, an embedded raster inflates the
  payload; prefer CSS-drawn texture there, and say why when you choose one.
- Disclose in the handoff which images were generated, by what, and which are
  awaiting real assets, so a later pass can replace rather than re-generate.

Routing stays as follows: `imagegen-frontend-web` and `imagegen-frontend-mobile`
own *design-direction comps* — images to review a layout or screen concept.
`brandkit` owns identity boards and logo systems. Plain asset generation for
placement inside a page is this section, which needs no aesthetic specialist
loaded and is not a competing direction.
