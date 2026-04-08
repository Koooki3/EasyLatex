---
name: thesis-three-line-table
description: Format thesis data tables as booktabs three-line tables with caption-above layout and repository-compatible longtable patterns. Use when drafting, converting, reviewing, or fixing thesis tables, especially when turning Markdown pipe tables or experiment summaries into formal LaTeX tables.
---

# Thesis Three-Line Table

## Use This Skill When

- the task adds or edits data tables in a thesis
- the task converts Markdown pipe tables into LaTeX
- the task reviews caption placement, column specs, longtable pagination, or table notes

## First Read

1. Read the active project rule file first.
2. Inspect one existing compliant table from the target project.
3. Open only the chapter files that actually contain tables.

## Preferred Table Pattern

- Use `booktabs` three-line tables for正文数据表:
  - `\toprule`
  - `\midrule`
  - `\bottomrule`
- Use `table` or `longtable` depending on expected length.
- Place the caption above the table body.
- Prefer column specs like `@{}lcc@{}` or paragraph columns without vertical rules.
- When a table is width-sensitive, prefer `xltabular` with a mix of:
  - one natural-width non-wrapping column for short labels such as `类别` or `参数项`
  - one or more `X` columns for the remaining width so descriptive cells can wrap naturally
- Avoid forcing all columns into narrow fixed-width `p{}` columns when the table contains long identifiers, configuration keys, file names, or mixed Chinese/ASCII content.

## Workflow

1. Decide whether the table is short or multipage.
2. Write the caption first.
3. Keep the table semantically compact. Merge repeated wording in prose when that reduces column width pressure.
4. Normalize units, abbreviations, and naming before finalizing the table.
5. Rebalance column widths using the longest cell in each column rather than header text alone.
6. If the table contains long ASCII tokens, configuration enums, or underscore-heavy keys, give the code-heavy column more width and let explanatory columns wrap.
7. For dense engineering tables, prefer a slightly smaller body size such as `\zihao{-5}`, moderate `\tabcolsep` such as `4pt`, and `\arraystretch` around `1.1` to `1.2`.
8. Add a body reference before the table, for example `各数据集训练设置如表~\ref{tab:paper-ch4-train-origin}所示`.

## Hard Constraints

- Do not use vertical rules.
- Do not use dense `\hline` grids for正文数据表.
- Do not place the caption below the table.
- Do not leave unexplained abbreviations in headers when the same table can stay readable with expanded wording.
- Do not leave obvious visual crowding unresolved when a different column allocation would fix it.
- Do not force a long identifier column to wrap awkwardly if the same table can stay readable by giving that column natural width and reallocating the remaining width.

## Label Style

- Prefer labels like:
  - `tab:paper-ch4-train-origin`
  - `tab:paper-ch4-ablation-ex`
  - `tab:paper-ch5-dependencies`

## Example

```tex
各数据集训练设置如表~\ref{tab:paper-ch4-train-origin}所示。
\begin{table}[htbp]
  \centering
  \caption{PKU-Market-PCB 数据集训练设置}
  \label{tab:paper-ch4-train-origin}
  \begin{tabular}{@{}lll@{}}
    \toprule
    项目 & 参数 & 说明 \\
    \midrule
    输入尺寸 & 960 & 检测训练统一输入分辨率 \\
    优化器 & AdamW & 与其余检测实验保持一致 \\
    \bottomrule
  \end{tabular}
\end{table}
```

For width-sensitive engineering tables, prefer a pattern like:

```tex
{\zihao{-5}\setlength{\tabcolsep}{4pt}\renewcommand{\arraystretch}{1.12}
\begin{xltabular}{\textwidth}{@{}l>{\hsize=1.15\hsize\linewidth=\hsize\raggedright\arraybackslash}X>{\hsize=0.85\hsize\linewidth=\hsize\raggedright\arraybackslash}X@{}}
  \caption{默认 ORT 会话参数}
  \label{tab:paper-ch5-ort} \\
  \toprule
  参数项 & 取值 & 备注 \\
  \midrule
  graph\_optimization\_level & ORT\_ENABLE\_EXTENDED & 图优化级别 \\
  execution\_mode & ORT\_SEQUENTIAL & 顺序执行模式 \\
  \bottomrule
\end{xltabular}
}
```

This pattern keeps the first column on one line, gives the value column slightly more width than the note column, and avoids the crowded look common in fixed-width three-column tables.
