# udl_promts (public registry)

Public registry of readymade UDL **prompt templates**, organised by
**role / layer** (top-level folders are stable layers; subfolders
express nesting when needed).

This README describes the **planned layout as a sample**. The actual
folder set in `main` may be smaller at any moment — folders and
prompts here are added deliberately, one at a time, by maintainers.

## Planned layout (sample — feel free to deviate when needed)

```
core/                  # ground rules, always-on in any prompt
  architecture.md
  concurrency.md
  error_handling.md
  code_style.md
  file_formats.md
  diff_rules.md
  output_format.md
  glossary.md

roles/
  architect/
    responsibilities.md
    plan_structure.md
    constraints.md
  coder/
    responsibilities.md
    coding_protocol.md
    testing_protocol.md
  reviewer/
    responsibilities.md
    review_checklist.md
    diff_validation.md

formats/               # output-format standards
  code_output.md
  diff_output.md
  text_output.md
  markdown_output.md
  multi_file_output.md

contracts/             # how roles pass the baton to each other
  architect_to_coder.md
  coder_to_reviewer.md
  reviewer_to_architect.md

tasks/                 # action-specific prompts
  generate_arch_plan.md
  implement_feature.md
  refactor.md
  debug.md
  write_tests.md

presets/               # composed prompts (real files, hand-assembled)
  architect_prompt.md   # = core + roles/architect + formats
  coder_prompt.md       # = core + roles/coder + formats
  reviewer_prompt.md    # = core + roles/reviewer + formats
  system_prompt.md      # global rules
```

### What each layer does

- **`core/`** — fundamental rules. Always included.
- **`roles/<role>/`** — per-role instructions.
- **`formats/`** — output-format standards (ensures diffs and files
  are emitted correctly).
- **`contracts/`** — inter-role hand-off rules.
- **`tasks/`** — operational prompts for specific actions.
- **`presets/`** — ready-to-use assembled prompts. Each preset is a
  real `.md` file with the content inlined. UDL treats them like any
  other prompt; no include-magic.

### Nesting inside a layer

Nested layouts are allowed. UDL's prompt manager walks recursively and
reports them as `<domain>/<sub>/<name>` (e.g.
`roles/architect/responsibilities`).

## Usage in a UDL workspace

```bash
./udl4
:prompts init https://github.com/rbirukoff-rgb/udl_promts.git
:prompts pull
:p list
```

Then reference prompts by `domain.name`:

```json
{ "role": "coder", "prompt": "core.architecture + roles.coder.coding_protocol" }
```

(The `+` notation is descriptive — concrete composition lives in
`presets/<role>_prompt.md`.)

## MVP contribution model

Edit / add files, `git add -A && git commit && git push origin main`.

Once the user count grows past a handful, we switch to fork + PR.
