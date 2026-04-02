# TXT to LaTeX Workflow

## Goal

Turn a structured `.txt` source file into repository-ready LaTeX sources without hand-building frontmatter or breaking the target project's template contract.

## Scope

- Active input: `.txt`
- Planned extension: `.docx` through a normalization adapter
- Output targets:
  - root thesis entry `.tex`
  - `pages/<task>-abstract-body.tex`
  - `pages/<task>-enabstract-body.tex`
  - `pages/<task>-innovation-body.tex` when needed
  - `pages/<task>-chapterN.tex`
  - `pages/<task>-appendix.tex`
  - `ref/<task>.bib`

## Workflow

1. Choose thesis profile.
   - `type = bachelor | master | doctor`
   - `class = academic | professional` for master or doctor when needed
2. Choose a stable task slug.
   - Example: `proposal`, `thesis-v1`, `midterm-report`
3. Collect source content with the matching template.
4. Parse the source into blocks.
   - metadata
   - abstracts
   - notation
   - chapters
   - acknowledgements
   - appendix
   - references
5. Normalize text.
   - keep LaTeX math as source
   - preserve explicit `【留空】`
   - normalize copied HTML entities such as `&amp;`
6. Detect structural markers.
   - heading levels `#`, `##`, `###`, `####`
   - standalone `图x.x.x ...` or `表x.x.x ...` placeholders
7. Generate repository files.
   - start from the demo structure
   - bind task-specific abstract body files from the root entry file
   - keep shared wrapper files unchanged
8. Generate bibliography.
   - prefer a dedicated `ref/<task>.bib`
   - do not invent missing metadata
9. Review project compliance.
   - check `\whusetup`
   - check `bib-backend`
   - check `bib-resource`
   - check auto frontmatter rules
   - check any official standards, example documents, or style constraints surfaced by the target project rules

## Input Rules

- Source must be plain text.
- Do not paste images, tables, screenshots, or Word layout artifacts.
- Titles should not include manual numbering like `第一章` or `1.1`.
- References should use `[n] full entry text`.
- Figure and table placeholders must be on their own lines.
- If the target project references official standards or example files, treat them as validation inputs rather than optional reading.

## Output Rules

- Do not handwrite `\frontmatter`.
- Do not handwrite covers, originality statements, or license pages.
- Do not replace shared wrapper files with task-specific manuscript text.
- Use `\printbibliography` rather than raw bibliography commands.
- Do not switch citation or bibliography standards early unless the target project has explicitly adopted the newer standard.
- If the target project adds official abstract, keyword, or layout checks, run them before delivery.

## Extension Boundary for DOCX

The `.docx` path should only add a source adapter. It should not fork the downstream LaTeX generation flow. After extraction and normalization, the data model should match the `.txt` workflow exactly.
