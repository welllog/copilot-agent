## github copilot agent
这些agent定义仅适用于vscode中的github copilot,规范和约束都需要遵循copilot相关文档


## 同步规则

每次修改根目录下的任何 `.agent.md` 文件后，必须同步更新 `zh/` 目录下对应的中文版本。

同步要求：

- `name` 字段保留英文原样
- `description` 字段翻译为中文
- 正文内容翻译为中文
- 输出格式中的结构化字段名（如 `Status`、`Severity`、`Coverage`）保留英文
- 保持文件结构和 frontmatter 格式一致

## zh 目录隔离

`zh/` 目录下的文件仅作为翻译副本存在。除同步更新中文版本外，不要读取、引用或将其纳入代码审查、修改和评审范围。根目录的 `.agent.md` 文件是唯一权威来源。
