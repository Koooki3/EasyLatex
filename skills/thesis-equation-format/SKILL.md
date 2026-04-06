---
name: thesis-equation-format
description: Format thesis equations in LaTeX with consistent numbering, lead-in text, and symbol explanations. Use when drafting, converting, reviewing, or fixing displayed equations in thesis chapters, especially when the target project requires equation references like “如式~\\ref{...}所示”, right-side “式 x.x” numbering, and post-equation “式中” explanations.
---

# Thesis Equation Format

## Use This Skill When

- the task adds or edits displayed equations in a thesis
- the task converts math from notes, `.txt`, or reference summaries into thesis-ready LaTeX
- the task reviews equation numbering, references, labels, or symbol explanations

## First Read

1. Read the active project rule file first.
2. Read the active root `.tex` file if equation tag formatting may need project-level setup.
3. Open only the chapter files that actually contain equations.

## Workflow

1. Verify each formula against a primary source before writing it into the manuscript.
2. Use LaTeX math environments only:
   - `equation` for a single displayed formula
   - `align` for aligned multi-line formulas
   - `aligned` or `split` inside `equation` when one equation number should cover multiple lines
3. Add a lead-in sentence before each displayed formula, for example `如式~\ref{eq:paper-ch3-yolo-loss}所示，...`.
4. Add a label to every displayed formula that may be referenced later.
5. Follow the displayed formula with a short explanation. Use `式中，` when symbols need definition.
6. Reuse existing symbol meanings within the same chapter. Do not silently rename symbols mid-chapter.

## Hard Constraints

- Do not use `$$ ... $$`.
- Do not handwrite equation numbers in prose.
- Do not leave a displayed formula without either a lead-in sentence or a nearby explanatory sentence.
- Do not rely on secondary notes such as `参考文献/formulas.md` as the final authority for a formula.

## Label and Reference Style

- Prefer labels like:
  - `eq:paper-ch3-yolo-loss`
  - `eq:paper-ch3-nwd-distance`
  - `eq:paper-ch4-exp-alias`
- Reference formulas with `式~\ref{...}` or in a lead-in sentence `如式~\ref{...}所示`.
- Keep label prefixes stable across the manuscript.

## Output Expectations

- Displayed equations are centered by the environment itself.
- Equation numbers stay on the right.
- If the target project requires the visual style `式 x.x`, implement that once in the root entry file instead of patching formulas individually.
- Symbol explanations remain concise and thesis-style, not textbook-style lists unless the formula is dense.

## Example

```tex
如式~\ref{eq:paper-ch3-nwd-sim}所示，归一化 Wasserstein 距离可写为
\begin{equation}
  \label{eq:paper-ch3-nwd-sim}
  \mathrm{NWD}(B_p,B_g)=\exp\left(-\frac{\sqrt{W_2^2(B_p,B_g)}}{C}\right).
\end{equation}
式中，$B_p$ 和 $B_g$ 分别表示预测框与真实框，$W_2^2(\cdot)$ 表示二阶 Wasserstein 距离平方，$C$ 为数据集尺度归一化常数。
```
