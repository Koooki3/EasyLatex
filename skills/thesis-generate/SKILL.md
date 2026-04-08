---
name: thesis-generate
description: Generate or update thesis LaTeX sources from structured user material. Use EasyLatex templates and workflow first, then enforce the active project's rules.
---

# Thesis Generate

## Use This Skill When

- the user provides thesis material, source text, metadata, references, or chapter content
- the target is repository-ready `.tex` and `.bib`
- the input is already in `.txt` form or can be normalized into the same structure

## First Read

1. Read the active project rule file first.
2. Read `D:/whuthesis/EasyLatex/workflows/txt-to-latex-workflow.md`.
3. If the task touches `.docx`, `.xlsx`, `.csv`, `.json`, `.yaml`, or other exchange files, read `D:/whuthesis/EasyLatex/workflows/file-encoding-policy.md`.
4. Open only the specific project files needed for the current task.
5. If the task writes or fixes displayed equations, read `D:/whuthesis/EasyLatex/skills/thesis-equation-format/SKILL.md`.
6. If the task writes or fixes figures or subfigures, read `D:/whuthesis/EasyLatex/skills/thesis-figure-layout/SKILL.md`.
7. If the task writes or fixes data tables, read `D:/whuthesis/EasyLatex/skills/thesis-three-line-table/SKILL.md`.

## Canonical EasyLatex Inputs

- `D:/whuthesis/EasyLatex/templates/conversion-source-guide.txt`
- `D:/whuthesis/EasyLatex/templates/conversion-source-bachelor-template.txt`
- `D:/whuthesis/EasyLatex/templates/conversion-source-master-template.txt`
- `D:/whuthesis/EasyLatex/templates/conversion-source-doctor-template.txt`

## Workflow

1. Determine `type`.
2. Determine `class` when applicable.
3. Choose a stable task slug.
4. Declare the canonical editable source when multiple file types coexist.
5. Parse source content into metadata, abstracts, chapters, appendix, and references.
6. Start from the target project's entry-file structure rather than an empty file.
7. Bind task-specific body files from the root entry file.
8. Keep shared wrapper files generic.
9. Generate `pages/*.tex` and `ref/*.bib`.
10. Prefer portable compile defaults unless the project explicitly requires something else.
11. Delegate equation, figure, and table formatting details to the companion formatting skills instead of duplicating local ad hoc patterns.

## Source-Specific Rules

- Treat LaTeX math as source, not prose.
- Treat standalone `图x.x.x ...` and `表x.x.x ...` lines as centered placeholders.
- When the active project is `whu-thesis`, structured **Markdown pipe tables** in `.txt` should become `table` floats with **`booktabs` 三线表** (`\toprule`/`\midrule`/`\bottomrule`), `\caption` above `tabular`, per `doc/rules.md` §12.1 and §15.1.
- Preserve `【留空】` as an intentional empty block.
- Normalize copied artifacts such as `&amp;`.
- Apply `D:/whuthesis/EasyLatex/workflows/file-encoding-policy.md` when the task reads from or writes to exchange files such as `.docx`, `.csv`, `.json`, or `.yaml`.
- Do not invent missing bibliography facts.
- If the active project rules reference official standards, manuals, or example deliverables, fold those constraints into the final validation pass.

## Hard Constraints

- Do not handwrite frontmatter pages.
- Do not overwrite shared wrapper files with task content.
- Do not use raw `\bibliography`.
- Do not move the root thesis entry file into a subdirectory unless the target project is explicitly designed that way.
- Do not switch to a newer citation or bibliography standard before the active project rules explicitly adopt it.
- Do not rely on platform-default encodings for text serialization.
- Do not treat `.docx` or `.xlsx` as plain-text files.

## Maintenance Sync Rule

- When the parent `whuthesis` workspace gains new generic conversion capabilities, workflow improvements, template conventions, or reusable review logic, update the corresponding generic parts in `EasyLatex/` in the same task whenever feasible.
- Sync only the generic layer into `EasyLatex/`. Keep repository-specific rules, file contracts, and school-specific template constraints outside the generic toolkit unless they have been explicitly generalized.
