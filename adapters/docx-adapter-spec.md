# DOCX Adapter Specification

## Purpose

Define how `.docx` input can later plug into the same EasyLatex workflow used by `.txt`.

## Design Rule

`.docx` support is an adapter problem, not a generation-logic rewrite.

The adapter must follow `D:/whuthesis/EasyLatex/workflows/file-encoding-policy.md`.

## Required Adapter Output

The adapter should normalize a `.docx` document into the same logical structure expected from `.txt`:

- thesis profile
- metadata fields
- abstract blocks
- notation block
- chapter hierarchy
- acknowledgements
- appendix
- reference list
- standalone figure/table placeholder lines

## Minimum Behavioral Contract

1. Preserve heading hierarchy.
2. Preserve plain paragraphs.
3. Convert equations into LaTeX-ready text when possible.
4. Keep unsupported rich objects as explicit placeholders rather than silently dropping them.
5. Remove Word-only styling noise.
6. Normalize full-width punctuation or copied HTML artifacts when needed.
7. Use Open XML aware tooling for read/write rather than treating `.docx` as plain text.
8. Emit normalized `UTF-8` text into the downstream intermediate representation.

## Recommended Mapping

- Heading 1 -> `#`
- Heading 2 -> `##`
- Heading 3 -> `###`
- Heading 4 -> `####`
- Body paragraph -> paragraph text
- Equation paragraph -> LaTeX equation block
- Caption-only line -> standalone placeholder line

## Non-Goals

- Pixel-perfect Word layout migration
- Automatic import of embedded figures into final thesis placement
- Automatic recovery of incomplete citation metadata

## Validation

After normalization, the resulting intermediate text should be reviewable with the same checks used for `.txt` input.

If the task also outputs a `.docx` delivery artifact:

- keep a backup before overwriting
- reopen the result in Word or an equivalent target application
- verify that representative Chinese and English text survived without mojibake
