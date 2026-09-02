# A. 激活层 Checklist

激活层审查 SKILL 能否在正确时机被 Agent 识别并调用。

---

## A1: description 字段存在且非空

**检查位置**：SKILL.md frontmatter（`---` 之间的 YAML）
**通过条件**：`description:` 字段存在，且值不为空字符串
**不通过 → Critical**
**改进建议**：在 frontmatter 中添加 `description: "..."` 字段，这是 Agent 激活 SKILL 的首要依据

---

## A2: description 包含动作动词

**检查位置**：description 字段值
**通过条件**：包含至少 3 个描述该 SKILL 能做什么的动词（如 create、review、generate、analyze、build、manage、audit 等）
**不通过 → Major**
**改进建议**：在 description 中补充动作动词，覆盖该 SKILL 的核心操作场景，Agent 通过动词匹配用户意图

---

## A3: description 包含用户视角的触发词

**检查位置**：description 字段值
**通过条件**：包含用户可能实际说出的词语，如产品类型、任务对象、操作场景，而不只是技术术语
**不通过 → Major**
**改进建议**：加入用户视角的触发词，如 "landing page, dashboard, form, chart" 而非只有 "UI component system"

---

## A4: description 长度与可读性合理

**检查位置**：description 字段值
**通过条件**：总长度 ≤ 600 字符；不存在 10 个以上近义词连排的词语堆砌
**不通过 → Minor**
**改进建议**：精简 description，优先覆盖高频触发场景，删除低价值的近义词堆砌

---

## A5: 存在激活边界说明章节

**检查位置**：SKILL.md 正文
**通过条件**：存在"When to Apply"或等价章节（When to Use、适用场景等），说明何时应使用该 SKILL
**不通过 → Critical**
**改进建议**：添加 When to Apply 章节，至少包含 Must Use 场景列表

---

## A6: Must / Recommended / Skip 三段式完整

**检查位置**：When to Apply 或等价章节
**通过条件**：包含三类情形的说明：必须使用、推荐使用、不需要/跳过
**不通过 → Major**（仅缺少 Skip），**Critical**（完全只有一段，无任何分级）
**改进建议**：补充 Skip 条件，明确 SKILL 的边界，防止被误用于不适合的场景

---

## A7: Must Use 场景足够具体

**检查位置**：Must Use 列表
**通过条件**：每个 Must Use 条目描述具体（包含触发条件而非泛化描述），至少 3 条
**不通过 → Major**
**改进建议**：将"用于所有 UI 工作"改为"新建 Landing Page、Dashboard、Admin Panel 等页面时"；每条说明具体触发情境

---

## A8: Skip 条件能排除相邻误触发场景

**检查位置**：Skip 列表
**通过条件**：Skip 条件能排除与该 SKILL 高度相邻但不适用的场景，防止被误触发
**不通过 → Minor**
**改进建议**：对每个 Must Use 场景，思考"什么情况看起来相似但实际不应使用该 SKILL"，加入 Skip 列表
