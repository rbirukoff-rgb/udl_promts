# udl_promts (public registry)

Public registry of readymade UDL prompt templates, organised by role/layer
(top-level folders are stable layers; subfolders express nesting when needed).

## Layout

Each layer is a top-level folder:

- core/     Always-included ground rules (architecture, concurrency, errors, style, formats, diff rules, glossary).
- roles/    Per-role instructions (architect, coder, reviewer).
- formats/  Output-format standards (code, diff, text, markdown, multi-file).
- contracts/ Inter-role baton-passing rules.
- tasks/    Operational prompts (plan, implement, refactor, debug, tests).
- presets/  Composed prompts = core + roles/<x> + formats. Real files maintained by hand.

Nested layouts inside a layer are fine - the manager walks recursively
and reports them as <domain>/<sub>/<name>.

## Usage

./udl4
:prompts init https://github.com/rbirukoff-rgb/udl_promts.git
:prompts pull
:p list

## MVP contribution model

Edit / add files, git add -A && git commit && git push origin main.
Once the user count grows past a handful, switch to fork + PR.
