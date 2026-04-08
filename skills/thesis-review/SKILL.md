---
name: thesis-review
description: Review, audit, or repair thesis LaTeX sources against the EasyLatex workflow and the active project's exact rules.
---

# Thesis Review

## Use This Skill When

- the user asks for an audit, repair, compliance check, or structural review
- the project already contains `.tex` sources that may violate the template contract

## First Read

1. Read the active project rule file first.
2. Read `D:/whuthesis/EasyLatex/workflows/txt-to-latex-workflow.md`.
3. If the task touches `.docx`, `.xlsx`, `.csv`, `.json`, `.yaml`, or other exchange files, read `D:/whuthesis/EasyLatex/workflows/file-encoding-policy.md`.
4. Read the active root `.tex` file.
5. If equations are in scope, read `D:/whuthesis/EasyLatex/skills/thesis-equation-format/SKILL.md`.
6. If figures are in scope, read `D:/whuthesis/EasyLatex/skills/thesis-figure-layout/SKILL.md`.
7. If tables are in scope, read `D:/whuthesis/EasyLatex/skills/thesis-three-line-table/SKILL.md`.

## Review Priorities

1. Wrong thesis profile or class options
2. Broken repository structure
3. Missing `\whusetup` fields
4. Missing `bib-backend` or `bib-resource`
5. Missing checks against any official standards, examples, or style constraints referenced by the active project rules
6. Citation-standard transitions applied too early
7. Shared wrapper files overwritten with task content
8. Manual frontmatter or bibliography hacks
9. Placeholder handling regressions from source conversion
10. Unsafe encoding or serialization paths for exchange files
11. Target-environment compatibility risks
12. Equation, figure, and table formatting regressions against the companion formatting skills

## Conversion Checks

- standalone figure/table placeholders remain identifiable
- `【留空】` was not expanded into fabricated prose
- reference input stayed traceable to the original numbered entries
- task-specific content lives in task-specific files
- if the project rules define abstract-length, keyword-count, layout, or standard-transition checks, those checks were run explicitly
- displayed equations use LaTeX environments rather than `$$`
- figure captions remain below figures and table captions remain above tables
- 正文数据表 remain three-line tables unless the project rules explicitly justify another pattern
- exchange files were reopened with the target parser or application after writing
- no new mojibake markers such as unexpected `?` or `�` were introduced into user-visible content
- `.docx` and `.xlsx` were handled with structure-aware tooling rather than plain-text writes

## Fix Strategy

- prefer the smallest patch that restores compliance
- preserve user manuscript content whenever possible
- change structure before changing prose
- if a delivery artifact is heavily corrupted, rebuild it from a clean canonical source instead of retrying ad hoc re-encoding

## Maintenance Sync Rule

- When the parent `whuthesis` workspace gains new generic conversion capabilities, workflow improvements, template conventions, or reusable review logic, update the corresponding generic parts in `EasyLatex/` in the same task whenever feasible.
- Sync only the generic layer into `EasyLatex/`. Keep repository-specific rules, file contracts, and school-specific template constraints outside the generic toolkit unless they have been explicitly generalized.
