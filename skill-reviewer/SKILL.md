---
name: skill-reviewer
description: "Review, audit, evaluate, assess, diagnose, or check a SKILL directory for design quality. Use when someone asks to review a skill, audit skill design, evaluate a SKILL.md, check skill quality, or improve a skill. Analyzes: activation clarity (description and When-to-Apply), file structure and context loading efficiency, instruction precision and gate conditions, tooling safety and prerequisites, output predictability and persistence strategy, maintainability and portability. Produces a structured report with Critical/Major/Minor severity findings grouped by dimension, plus top improvement priorities and positive highlights."
---

# Skill Reviewer

对一个 SKILL 目录进行全面审查，输出按维度分组、按严重程度分级的结构化报告，并附带可操作的改进建议。

## When to Apply

### Must Use

- 用户要求审查、评估、诊断某个 SKILL 的质量
- 用户反映某 SKILL 激活不准确或 Agent 执行不稳定
- 用户在发布或分享 SKILL 前做最终质检

### Recommended

- 设计完一个新 SKILL 后的自审
- 修改现有 SKILL 后验证未引入新问题

### Skip

- 用户只想了解某个 SKILL 的功能（不是审查）
- 用户要求直接修改 SKILL 内容（执行修改，不走审查流程）
- 目标不是 SKILL 目录（如普通代码项目、文档目录）

---

## 严重程度定义

| 级别 | 标志 | 含义 |
|------|------|------|
| Critical | 🔴 | 直接导致 SKILL 无法被激活或无法正确执行 |
| Major | 🟡 | 显著降低 SKILL 质量或可靠性，但不会完全失效 |
| Minor | ⚪ | 不影响核心功能，但降低专业度或可维护性 |

## 整体健康度判断规则

| 结果 | 条件 |
|------|------|
| 🟢 良好 | Critical = 0 且 Major ≤ 2 |
| 🟡 需改进 | Critical = 0 且 Major > 2，或 Critical = 1 |
| 🔴 需重构 | Critical ≥ 2 |

---

## 审查流程

### Phase 0: 定位目标

1. 从对话上下文中提取 SKILL 目录路径
2. 如果未提供路径，使用 AskUserQuestion 询问目标路径

> ⛔ GATE: SKILL 目录路径已确认。DO NOT proceed to Phase 1 until the skill directory path is known.

---

### Phase 1: 文件扫描

1. 使用 Glob 扫描整个 SKILL 目录树，获取所有文件列表
2. 检查以下条目是否存在，记录到文件清单：
   - `SKILL.md`（必须）
   - `references/`（可选）
   - `assets/`（可选）
   - `scripts/`（可选）
   - `data/`（可选）
3. 使用 Read 读取 SKILL.md 全文
4. 使用 Read 依次读取 references/、assets/、scripts/、data/ 下所有文件

> ⛔ GATE: SKILL.md 已读取。If SKILL.md does not exist, record one Critical finding "SKILL.md 缺失" under dimension B and stop — output a partial report with only this finding.

---

### Phase 2: 逐维审查

对维度 A → F 依次执行：

1. **读取**对应 checklist 文件（路径见下表）
2. 逐条对照已扫描的文件内容进行评估
3. 对每条不符合项，记录：
   - 维度代码 + 条目 ID（如 A3）
   - 严重程度（Critical / Major / Minor）
   - 具体证据（引用原文片段，或标注"文件缺失"）
   - 改进建议（具体可操作的修改方向）
4. 通过的条目无需记录

| 维度 | Checklist 文件 |
|------|----------------|
| A. 激活层 | `references/checklist-activation.md` |
| B. 结构层 | `references/checklist-structure.md` |
| C. 指令层 | `references/checklist-instruction.md` |
| D. 工具使用层 | `references/checklist-tooling.md` |
| E. 输出层 | `references/checklist-output.md` |
| F. 可维护性层 | `references/checklist-maintainability.md` |

> ⛔ GATE: 全部 6 个维度评估完毕。DO NOT proceed to Phase 3 until every dimension has been evaluated against its checklist.

---

### Phase 3: 生成报告

1. 读取 `references/report-template.md`
2. 按模板结构填入所有 findings
3. 直接输出完整报告

DO NOT summarize, abbreviate, or omit any findings. Output the complete report in full.
