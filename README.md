# AI Agent Global Prompt ZH

一份面向中文用户和源码项目的 AI 编码助手全局提示词模板。

它综合了 MiMo Code、Codex 等编码代理的常见使用经验，目标是让 AI 助手在日常工程任务中更稳定、更克制、更可验证：少空话，多推进；少猜测，多核实；少炫技，多贴合现有代码库。

## 适合谁

- 主要使用中文和国内开发环境的用户。
- 希望统一多种 AI 编码工具行为的人。
- 希望 AI 写代码时更重视最小改动、SQL 性能、代码可读性和验证闭环的人。
- 同时使用 Codex、MiMo Code、Claude Code 或其他支持 `AGENTS.md` / 全局提示词机制的工具的人。

## 快速使用

复制根目录的 [`AGENTS.md`](./AGENTS.md) 到你的工具全局提示词位置。

常见位置示例：

```text
Codex:      ~/.codex/AGENTS.md
MiMo Code:  ~/.config/mimocode/AGENTS.md
项目级:     <project>/AGENTS.md
```

Windows 示例：

```powershell
Copy-Item .\AGENTS.md C:\Users\<你的用户名>\.codex\AGENTS.md
Copy-Item .\AGENTS.md C:\Users\<你的用户名>\.config\mimocode\AGENTS.md
```

建议先备份原文件：

```powershell
Copy-Item C:\Users\<你的用户名>\.codex\AGENTS.md C:\Users\<你的用户名>\.codex\AGENTS.md.bak
```

## 包含哪些规则

- 中文优先和国内用户语境。
- 少问但不乱猜：能合理假设就推进，高风险或会返工时再确认。
- 先明确成功标准，再做最小必要改动。
- 写代码时保持逻辑清晰，避免绕来绕去、深嵌套和过度抽象。
- 写 SQL 和数据访问代码时默认考虑性能，避免隐式全表扫描、无边界查询和 N+1 查询。
- 保留用户已有代码和项目风格，不顺手重构无关内容。
- 使用 `.wolf/` 作为源码项目的跨工具记忆层。
- 只在源码任务中使用 CodeGraph，并明确 CodeGraph 与 `rg` 的分工。
- 当前信息主动检索，稳定知识直接回答。
- 对版权、高风险、安全和隐私问题保持边界。

## 文件结构

```text
.
├── AGENTS.md              # 通用全局提示词模板
├── README.md              # 项目说明
├── LICENSE                # MIT License
├── docs/
│   └── design-notes.md    # 设计取舍说明
└── templates/
    └── minimal.md         # 更短的最小版模板
```

## 定制建议

如果你只想保留最核心行为，可以从 [`templates/minimal.md`](./templates/minimal.md) 开始。

如果你的工具不支持 CodeGraph 或 `.wolf/`，可以删除对应章节。  
如果你的团队有固定数据库规范、测试策略或代码风格，建议把这些规则追加到 `编码准则` 后面。

## 设计原则

这份提示词刻意避免“神奇咒语”和过度人格化，重点放在可执行的工程行为上：

- 让 AI 先理解上下文，而不是直接改代码。
- 让 AI 少做无关改动，降低 diff 噪音。
- 让 AI 主动关注 SQL 和数据访问性能。
- 让 AI 交付前做验证，而不是只说“应该可以”。
- 让 AI 对当前信息、法律金融医疗等高风险问题保持谨慎。

## License

MIT

