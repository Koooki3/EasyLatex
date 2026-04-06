---
name: thesis-figure-layout
description: Format thesis figures and subfigures with repository-compatible LaTeX layouts. Use when drafting, converting, reviewing, or fixing single figures, side-by-side figures, four-panel subfigures, figure captions, labels, and chapter-scoped figure asset paths such as `chapter3-figs/`.
---

# Thesis Figure Layout

## Use This Skill When

- the task adds or edits figures in thesis chapters
- the task converts figure placeholders into LaTeX figure blocks
- the task needs subfigure layouts without introducing new package dependencies
- the task reviews caption placement, labels, asset paths, or figure references

## First Read

1. Read the active project rule file first.
2. Inspect one existing figure example from the target project.
3. Open only the chapter files and figure directories relevant to the task.

## Preferred Layout Pattern

- Use repository-compatible patterns first:
  - single figure: `center` + `\includegraphics` + `\captionof{figure}`
  - multi-panel figure: `minipage` blocks inside a centered container, then one shared `\captionof{figure}`
- Do not introduce `subcaption` or `subfigure` unless the target project already depends on them.

## Workflow

1. Put assets under a chapter-scoped directory such as `chapter3-figs/`.
2. Reference each figure in the body before it appears, for example `如图~\ref{fig:paper-ch3-yolo-evolution}所示`.
3. Place the caption below the image block.
4. Add a stable label after the caption.
5. For subfigures, mark panels as `(a)`, `(b)`, `(c)`, `(d)` below each panel.
6. Keep panel sizes visually balanced. Use `width=\linewidth` inside `minipage` blocks and control height with `keepaspectratio` when needed.

## Hard Constraints

- Do not put the figure caption above the figure.
- Do not mix multiple unrelated figures into one caption block.
- Do not use absolute filesystem paths in LaTeX image references.
- Do not leave a figure in the chapter without a corresponding body reference.

## Label Style

- Prefer labels like:
  - `fig:paper-ch3-yolo-evolution`
  - `fig:paper-ch3-nwd-compare`
  - `fig:paper-ch3-dino-fusion`

## Example

```tex
如图~\ref{fig:paper-ch3-segmentdata-examples}所示，四类缺陷样本在局部纹理与边界形态上存在明显差异。
\begin{center}
  \begin{minipage}[b]{0.45\textwidth}
    \centering
    \includegraphics[width=\linewidth,height=0.18\textheight,keepaspectratio]{chapter3-figs/example-a.png}

    \small (a) 类型 A
  \end{minipage}
  \hfill
  \begin{minipage}[b]{0.45\textwidth}
    \centering
    \includegraphics[width=\linewidth,height=0.18\textheight,keepaspectratio]{chapter3-figs/example-b.png}

    \small (b) 类型 B
  \end{minipage}
  \captionof{figure}{示例子图布局}
  \label{fig:paper-ch3-segmentdata-examples}
\end{center}
```
