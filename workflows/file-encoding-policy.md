# File Encoding and Serialization Policy

## Goal

Prevent mojibake, parser breakage, and application-specific incompatibilities when a thesis task touches multiple file types.

## Core Rule

Choose a **canonical editable source** for the current task and treat other formats as derived artifacts whenever feasible.

- If `.txt`, `.tex`, and `.docx` coexist, do not hand-edit all three independently unless the task explicitly requires it.
- When a delivery file is suspected to be corrupted, regenerate it from a clean canonical source instead of trying ad hoc re-encoding first.

## File-Type Policy Matrix

### Plain text source files

- `.txt`, `.md`
- Canonical encoding: `UTF-8` preferred, no BOM by default
- Safe tools: explicit-encoding text editors, repository patches, parser-aware scripts
- Required checks:
  - reopen the file with explicit `UTF-8`
  - verify representative Chinese, English, punctuation, and math text survived round-trip

### LaTeX and bibliography files

- `.tex`, `.bib`, `.cls`, `.sty`
- Canonical encoding: `UTF-8` preferred, no BOM by default
- Safe tools: repository patches, LaTeX-aware or plain-text editors with explicit encoding
- Required checks:
  - do not rely on platform-default ANSI/GBK code pages
  - preserve ASCII control syntax such as `\`, `{}`, `%`, `_`
  - reopen after write and inspect escaped characters and Chinese text

### Structured config and data files

- `.json`, `.yaml`, `.yml`, `.toml`
- Canonical encoding: `UTF-8` preferred, no BOM by default
- Safe tools: parser-aware libraries first, explicit-encoding editors second
- Required checks:
  - parse the file after writing
  - do not depend on shell-default encodings

### Delimited tables

- `.csv`, `.tsv`
- Canonical encoding: pick based on the target software and record the choice in the task notes
- Preferred rule:
  - if the file is for repository scripts, Python, or cross-platform processing, use `UTF-8`
  - if the file is primarily for Windows Excel double-click opening, prefer `UTF-8 with BOM` or deliver `.xlsx` instead
- Required checks:
  - reopen with the target software or parser
  - verify Chinese headers and delimiters

### Office word-processing documents

- `.docx`
- This is **not** a plain-text encoding problem; it is an Open XML package serialization problem
- Safe tools:
  - Microsoft Word
  - LibreOffice
  - `python-docx`
  - other Open XML aware tooling
- Unsafe patterns:
  - treating `.docx` as a plain text file
  - writing document content through shell redirection or default code-page conversions
  - editing package XML without understanding the ZIP package structure and explicit XML encoding
- Required checks:
  - keep a backup before modification
  - reopen the output in the target application, preferably Word when Word is the delivery path
  - verify there are no unexpected `?` or replacement characters in body text
  - if corruption is widespread, rebuild from a clean source instead of trying repeated re-encoding

### Office spreadsheets

- `.xlsx`
- This is a structured container, not a plain-text file
- Safe tools:
  - Excel
  - LibreOffice Calc
  - spreadsheet-aware libraries
- Required checks:
  - reopen in the target spreadsheet application when formulas, merged cells, or Chinese text matter

### Binary assets

- `.pdf`, `.png`, `.jpg`, `.jpeg`, model weights, archives
- Treat as binary
- Never rewrite through text encoders

## Windows Write-Path Rules

- Do not rely on PowerShell or shell default encodings when writing text files.
- If shell output must be written to disk, specify the encoding explicitly.
- Prefer parser-aware libraries over text concatenation for structured formats.
- Prefer application-native libraries over ZIP/XML hand-editing for Office files.

## Round-Trip Validation

After any meaningful write:

1. Reopen the file with the same class of tool that will consume it.
2. Check representative multilingual content, not only ASCII.
3. Check for mojibake markers such as unexpected `?` or `�`.
4. For delivery artifacts, verify with the actual delivery application when feasible.

## Workflow Integration

- `thesis-generate` should decide the canonical source before writing derived artifacts.
- `thesis-review` should audit both structure and serialization safety, not only visible formatting.
- The `.docx` adapter should normalize content into UTF-8 text after Open XML aware extraction, rather than mixing Word-specific serialization with downstream LaTeX generation.
