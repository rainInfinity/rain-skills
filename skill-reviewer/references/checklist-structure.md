# B. 结构层 Checklist

结构层审查 SKILL 文件组织是否支持渐进式 context 加载，避免不必要的 token 消耗。

---

## B1: SKILL.md 存在

**检查位置**：SKILL 目录根目录
**通过条件**：SKILL.md 文件存在
**不通过 → Critical**
**改进建议**：创建 SKILL.md，这是 SKILL 的唯一必须文件，Agent 通过它识别并加载该 SKILL

---

## B2: SKILL.md 体积合理

**检查位置**：SKILL.md 总行数
**通过条件**：纯指令内容 ≤ 300 行；若超过，检查是否有大量参考内容/规则/示例应移入 references/
**不通过 → Major**（300–500 行），**Critical**（> 500 行）
**改进建议**：将参考内容、规则表格、示例数据移入 references/，SKILL.md 只保留协议、工作流和指令

---

## B3: 参考内容放在 references/ 而非内联于 SKILL.md

**检查位置**：SKILL.md 正文中是否有大块规则表格、数据清单、参考手册
**通过条件**：SKILL.md 不包含超过 50 行的规则或数据内容；此类内容应在 references/ 下独立文件中存放
**不通过 → Major**
**改进建议**：将规则/数据内容提取到 references/ 目录，SKILL.md 中写路径引用，如 "read references/xxx.md"

---

## B4: 输出模板放在 assets/ 而非内联于 SKILL.md

**检查位置**：SKILL.md 中是否有大段输出模板或示例格式
**通过条件**：如有固定输出格式，以独立文件存在于 assets/ 中，SKILL.md 中只写路径引用
**不通过 → Minor**
**改进建议**：将输出模板移至 assets/，SKILL.md 中写 "read assets/xxx.md for output format"

---

## B5: references/ 中各文件职责不重叠

**检查位置**：references/ 目录下的所有文件名及其内容
**通过条件**：每个文件有清晰的语义命名，文件间功能不重叠
**不通过 → Minor**
**改进建议**：按职责拆分文件，避免一个 references 文件承担多个不相关职责

---

## B6: 无孤立文件

**检查位置**：references/、assets/、scripts/、data/ 中的所有文件
**通过条件**：每个文件都能在 SKILL.md 或其他已引用文件中找到使用说明；不存在从未被引用的文件
**不通过 → Minor**
**改进建议**：删除无引用的孤立文件，或在 SKILL.md 中补充对应引用说明

---

## B7: 目录分工符合约定

**检查位置**：整体目录结构
**通过条件**：references/（知识/规则）、assets/（输出模板）、scripts/（可执行工具）、data/（数据文件）各司其职，没有混放
**不通过 → Minor**
**改进建议**：按约定重组文件到对应目录；如有混放，移动到正确位置并更新 SKILL.md 中的引用路径
