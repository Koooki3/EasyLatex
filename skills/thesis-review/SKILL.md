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
3. Read the active root `.tex` file.

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
10. Target-environment compatibility risks

## Conversion Checks

- standalone figure/table placeholders remain identifiable
- `【留空】` was not expanded into fabricated prose
- reference input stayed traceable to the original numbered entries
- task-specific content lives in task-specific files
- if the project rules define abstract-length, keyword-count, layout, or standard-transition checks, those checks were run explicitly

## Fix Strategy

- prefer the smallest patch that restores compliance
- preserve user manuscript content whenever possible
- change structure before changing prose

## Maintenance Sync Rule

- When the parent `whuthesis` workspace gains new generic conversion capabilities, workflow improvements, template conventions, or reusable review logic, update the corresponding generic parts in `EasyLatex/` in the same task whenever feasible.
- Sync only the generic layer into `EasyLatex/`. Keep repository-specific rules, file contracts, and school-specific template constraints outside the generic toolkit unless they have been explicitly generalized.
