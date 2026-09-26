## Generated imagery

When the committed direction needs an image that does not exist and cannot be
sourced, generate it.

### How generation actually works here

A skill is instructions. It has no runtime, no process, and no credentials, so
it cannot generate an image and cannot drive another CLI into generating one.
The agent executing this pipeline does the generating, through whatever the
host exposes. Resolve the capability in this order and use the first that
exists:

1. **A native image tool from the host.** This is the normal path. Check the
   current tool list for an image generator (names vary by harness: `ImageGen`,
   `generate_image`, `text_to_image`, a drawing tool). Call it directly with a
   written brief; it returns a local file path or URL.
2. **A configured MCP server or plugin that exposes image generation.**
   Available only when the user has set one up. Present only if it appears in
   the tool list; never assume one exists or claim availability because a
   provider supports images.
3. **A shell route with credentials already present.** An API call needs a key
   and an endpoint the user has configured. Test for the credential without
   printing it, e.g. `[ -n "$OPENAI_API_KEY" ] && echo SET`. If unset, this
   route does not exist — do not ask the user for a key mid-design and do not
   write one into a file. A subscription login is not an API key: an agent
   authorized through a plan login can generate without any key in the
   environment, so an absent key proves nothing about whether generation is
   available. Check the agent's own auth, not only the shell.
4. **A second agent CLI that has generation built in.** When the host executing
   this pipeline has no image tool but the user has a coding-agent CLI installed
   that does, delegate to it. Codex is a concrete, verified case: its built-in
   `image_gen` tool works on a ChatGPT plan login with no `OPENAI_API_KEY` set.

   ```bash
   codex exec --skip-git-repo-check --sandbox workspace-write \
     "Generate an image with image_gen: <brief>. Save it to <project path>/<file>.png"
   ```

   Two things break if you skip them. The default sandbox is read-only, so the
   image is generated but the copy into the project fails — pass
   `--sandbox workspace-write`. And Codex writes originals into
   `~/.codex/generated_images/<session-id>/<call-id>.png` before placing them,
   so name the destination path in the request rather than hunting for the file
   afterward. Codex also carries an API-key fallback mode; prefer the built-in
   tool when the user's entitlement is a subscription. Budget for it: a single
   delegated generation ran ~18k tokens.
5. **Nothing.** Generate no image. Ship the layout with a defined image slot,
   explicit replacement notes, and the exact prompt you would have used, so the
   user can run it later. A missing image is a documented gap, never a reason
   to stop the build.

Do not confuse a CLI's image *input* flag with generation. `-i, --image <FILE>`
attaches images to a prompt. Whether a CLI can also produce images is a separate
capability, and some can — establish it by checking the tool's own feature
surface rather than by reading `--help` and concluding a flag is absent.

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
