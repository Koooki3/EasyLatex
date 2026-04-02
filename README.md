# EasyLatex

EasyLatex is a general-purpose toolkit for turning structured source documents into maintainable LaTeX projects.

EasyLatex 是一套通用的结构化文档转 LaTeX 工具包，用于将原始写作材料稳定整理为可维护、可复用、可审查的 LaTeX 项目。

## Introduction | 简介

EasyLatex focuses on a practical document production path:

- collect source material with a constrained template
- normalize structure before formatting
- map content into a predictable LaTeX file layout
- run a review pass before delivery

EasyLatex 聚焦一条可落地的文档生产路径：

- 用受约束的源文件模板收集内容
- 在排版前先完成结构归一化
- 将内容映射到稳定的 LaTeX 文件布局
- 在交付前执行一次审查与修正

It is especially suitable for:

- theses and dissertations
- long academic reports
- proposal documents
- structured technical manuscripts

它尤其适用于：

- 学位论文
- 长篇学术报告
- 开题或中期文档
- 结构清晰的技术文稿

## Design Goals | 设计目标

- General, not school-branded
- Template-driven source intake
- Reproducible conversion workflow
- Reviewable intermediate structure
- Easy extension from `.txt` to `.docx`
- Compatible with repository-specific rules when needed
- Able to absorb official standards or example-based checks from the target project

- 通用化，而不是绑定某个学校标识
- 模板驱动的源文件采集
- 可复现的转换流程
- 可审查的中间结构
- 便于从 `.txt` 扩展到 `.docx`
- 需要时可叠加具体仓库规则

## Core Capabilities | 核心能力

- Standard source templates for structured writing
- A canonical `.txt -> LaTeX` workflow
- Reusable generation and review skills
- A reserved adapter boundary for `.docx`
- A clear separation between generic workflow and project-specific constraints

- 标准化结构源文件模板
- 规范的 `.txt -> LaTeX` 工作流
- 可复用的生成与复核 skills
- 预留 `.docx` 适配边界
- 明确区分通用流程与项目特定约束

## Directory Layout | 目录结构

```text
EasyLatex/
  README.md
  adapters/
    docx-adapter-spec.md
  skills/
    thesis-generate/
      SKILL.md
    thesis-review/
      SKILL.md
  templates/
    conversion-source-guide.txt
    conversion-source-bachelor-template.txt
    conversion-source-master-template.txt
    conversion-source-doctor-template.txt
  workflows/
    txt-to-latex-workflow.md
```

## Requirements | 环境要求

EasyLatex itself is lightweight. The minimum requirement is a workspace that can host:

- source templates
- target `.tex` files
- optional bibliography files
- optional images and appendix materials

EasyLatex 本身很轻量，最低要求只是一个能承载下列内容的工作目录：

- 源文件模板
- 目标 `.tex` 文件
- 可选的参考文献文件
- 可选的图片与附录材料

Recommended runtime assumptions:

- UTF-8 text encoding
- a LaTeX-capable workspace
- a repeatable folder layout
- an agent or script that can follow the documented workflow

建议具备以下运行前提：

- UTF-8 文本编码
- 支持 LaTeX 的工作目录
- 可重复使用的目录布局
- 能执行文档化工作流的 agent 或脚本

## Supported Inputs | 当前支持输入

- `.txt` is the primary production input
- `.docx` is planned through an adapter layer
- source content should be text-first and structure-first

- `.txt` 是当前主输入格式
- `.docx` 通过适配层进行后续扩展
- 源材料应以文本结构为主，而不是版式为主

## Deployment | 部署方式

### Option A: Drop-in Folder Deployment

Use this when you want to copy EasyLatex into an existing LaTeX project or workspace.

1. Create an `EasyLatex/` folder in your workspace.
2. Copy the full directory structure shown above.
3. Keep `templates/`, `workflows/`, `skills/`, and `adapters/` together.
4. Point your generation process to the files inside `EasyLatex/`.
5. Keep project-specific rules outside EasyLatex when possible.

### 方案 A：直接拷贝部署

适用于你要把 EasyLatex 作为一个子工具包放进现有 LaTeX 项目。

1. 在工作区中创建 `EasyLatex/` 目录。
2. 完整复制上面的目录结构。
3. 保持 `templates/`、`workflows/`、`skills/`、`adapters/` 同时存在。
4. 让生成流程引用 `EasyLatex/` 内的文档与模板。
5. 项目专属规则尽量放在 EasyLatex 之外维护。

### Option B: Standalone Toolkit Deployment

Use this when you want EasyLatex to serve multiple document projects.

1. Place `EasyLatex/` at a stable shared location.
2. Treat it as the canonical source of templates and workflow docs.
3. Let each document project maintain only:
   - manuscript content
   - project-specific LaTeX layout rules
   - project-specific output files
4. Reuse the same EasyLatex folder across projects.

### 方案 B：独立工具包部署

适用于你希望 EasyLatex 服务多个文档项目。

1. 将 `EasyLatex/` 放在一个稳定的共享位置。
2. 将其视为模板和工作流文档的统一来源。
3. 每个文档项目只维护：
   - 原始稿件内容
   - 项目特定 LaTeX 规则
   - 项目特定输出文件
4. 多个项目复用同一套 EasyLatex。

## Reproducible Workflow | 可复现工作流

The recommended workflow is deterministic and review-friendly.

1. Choose the source template that matches the document type.
2. Fill the template using plain text and LaTeX math.
3. Preserve all required top-level sections.
4. Mark intentional gaps with `【留空】`.
5. Keep figure/table placeholders on standalone lines.
6. Write references in `[n] full entry text` format.
7. Parse the filled source into structured content blocks.
8. Generate the target LaTeX project files.
9. Run the review pass.
10. Fix structure before adjusting wording or style.
11. If the target project references official standards or sample deliverables, run those checks before sign-off.

推荐工作流是可重复、可审查的：

1. 选择与文档类型匹配的源模板。
2. 用纯文本和 LaTeX 公式填写模板。
3. 保留所有必需的一级结构块。
4. 用 `【留空】` 标记有意保留但暂无内容的部分。
5. 图表占位文字必须单独成行。
6. 参考文献统一使用 `[序号] 完整条目文本`。
7. 将填好的源文件解析为结构化内容块。
8. 生成目标 LaTeX 项目文件。
9. 执行复核流程。
10. 先修结构，再修措辞与样式。

## Step-by-Step Reproduction | 复现步骤

This section describes how to reproduce the same conversion result from scratch.

### 1. Prepare the workspace

Create a document workspace containing:

- `EasyLatex/`
- your source manuscript file
- your target LaTeX project folder

### 2. Prepare the source file

Pick one template from `templates/` and fill it.

Rules:

- use UTF-8
- use heading markers exactly as required
- keep formulas in LaTeX syntax
- do not paste screenshots, tables, or rich-text formatting residue

### 3. Parse the source into structure

Split the manuscript into:

- metadata
- abstract blocks
- chapter hierarchy
- appendix
- references

### 4. Normalize content

Before generation:

- preserve explicit placeholders
- normalize copied entities such as `&amp;`
- identify standalone caption placeholders
- reject fake numbering embedded in titles

### 5. Generate LaTeX files

Map normalized content into your target LaTeX layout, for example:

- one root entry file
- separate chapter files
- separate abstract files
- a dedicated bibliography file

### 6. Review the output

Check:

- structure completeness
- bibliography integrity
- title hierarchy
- placeholder preservation
- compatibility with the target class or template
- any official style or standard constraints adopted by the target project

### 7. Re-run if needed

If the source changes, repeat the same pipeline rather than editing generated output ad hoc.

复现时建议按以下顺序执行：

### 1. 准备工作区

建立一个包含下列内容的文档工作区：

- `EasyLatex/`
- 源稿件文件
- 目标 LaTeX 项目目录

### 2. 准备源文件

从 `templates/` 中选择一份模板并填写。

要求：

- 使用 UTF-8
- 严格使用规定的标题层级标记
- 公式必须是 LaTeX 语法
- 不要粘贴截图、表格或富文本残留

### 3. 解析源文件结构

将稿件拆为：

- 元数据
- 摘要块
- 章节层级
- 附录
- 参考文献

### 4. 归一化内容

生成前先处理：

- 保留显式留空标记
- 归一化 `&amp;` 等复制残留
- 识别单独成行的图表标题占位
- 排除标题里的伪编号

### 5. 生成 LaTeX 文件

把归一化结果映射到目标 LaTeX 结构中，例如：

- 一个根入口文件
- 分离的章节文件
- 分离的摘要文件
- 独立参考文献文件

### 6. 执行复核

重点检查：

- 结构是否完整
- 文献是否可追溯
- 标题层级是否正确
- 占位符是否被保留
- 是否兼容目标模板或类文件

### 7. 需要时重新生成

如果源文件变化，优先重复同一条生成链路，而不是直接临时手改生成结果。

## How to Use the Included Files | 内置文件如何使用

- [txt-to-latex-workflow.md](/D:/whuthesis/EasyLatex/workflows/txt-to-latex-workflow.md)
  Canonical conversion flow for `.txt` input.

- [docx-adapter-spec.md](/D:/whuthesis/EasyLatex/adapters/docx-adapter-spec.md)
  Extension contract for `.docx`.

- [conversion-source-guide.txt](/D:/whuthesis/EasyLatex/templates/conversion-source-guide.txt)
  Human-facing authoring guide for source preparation.

- [conversion-source-bachelor-template.txt](/D:/whuthesis/EasyLatex/templates/conversion-source-bachelor-template.txt)
  Source template for bachelor-level thesis material.

- [conversion-source-master-template.txt](/D:/whuthesis/EasyLatex/templates/conversion-source-master-template.txt)
  Source template for master-level thesis material.

- [conversion-source-doctor-template.txt](/D:/whuthesis/EasyLatex/templates/conversion-source-doctor-template.txt)
  Source template for doctor-level thesis material.

- [thesis-generate/SKILL.md](/D:/whuthesis/EasyLatex/skills/thesis-generate/SKILL.md)
  Reusable generation skill.

- [thesis-review/SKILL.md](/D:/whuthesis/EasyLatex/skills/thesis-review/SKILL.md)
  Reusable review skill.

## Extension Strategy | 扩展策略

EasyLatex should evolve by layering, not by mixing concerns.

- put general source-format rules in `templates/`
- put process rules in `workflows/`
- put agent behavior in `skills/`
- put format-specific extraction contracts in `adapters/`
- keep project-specific policies outside the core toolkit

EasyLatex 应按分层方式扩展，而不是把不同职责混写在一起：

- 通用源格式规则放在 `templates/`
- 流程规则放在 `workflows/`
- agent 行为放在 `skills/`
- 格式适配契约放在 `adapters/`
- 项目特定政策放在工具包核心之外

## What EasyLatex Does Not Try to Solve | 非目标

- pixel-perfect migration of Word layout
- automatic recovery of missing citation facts
- automatic insertion of final figures and tables
- replacing the target LaTeX class or institutional template itself

- 不追求 Word 版式的像素级迁移
- 不自动补全缺失的文献信息
- 不自动完成最终图表插入
- 不替代目标 LaTeX 模板或类文件本身

## Recommended Tags | 推荐标签

- `latex`
- `thesis`
- `dissertation`
- `document-conversion`
- `txt-to-latex`
- `docx-to-latex`
- `academic-writing`
- `workflow`
- `automation`

## Maintenance | 维护建议

- update templates when the source collection contract changes
- update workflow docs before changing automation behavior
- keep adapter contracts explicit
- prefer regeneration over manual patching of generated output

- 当源文件采集规范变化时，先更新模板
- 修改自动化行为前，先更新工作流文档
- 适配层契约必须保持明确
- 优先重新生成，而不是手工零散修补生成结果
