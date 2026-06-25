## GitHub Copilot agent
这些 agent 定义仅适用于 VS Code 中的 GitHub Copilot，规范和约束都需要遵循 Copilot 相关文档


## 通用技能（skill/）

`skill/` 目录下的 `.skill.md` 文件是与具体 coding agent 无关的通用工作流技能，不绑定任何工具集、框架或委托模型。根目录的 `.agent.md` 是 Copilot 专属流程定义，`skill/` 则是可被任意 coding agent 复用的流程沉淀。


## 同步规则

每次修改根目录下的任何 `.agent.md` 或 `skill/` 下的任何 `.skill.md` 文件后，必须同步更新 `zh/` 目录下对应的中文版本。

同步要求：

- `name` 字段保留英文原样
- `description` 字段翻译为中文
- 正文内容翻译为中文
- 输出格式中的结构化字段名（如 `Status`、`Severity`、`Coverage`）保留英文
- 保持文件结构和 frontmatter 格式一致

## zh 目录隔离

`zh/` 目录下的文件仅作为翻译副本存在。除同步更新中文版本外，不要读取、引用或将其纳入代码审查、修改和评审范围。根目录的 `.agent.md` 与 `skill/` 下的 `.skill.md` 文件是唯一权威来源。
