# AI Agent Global Prompt ZH

一份面向中文用户和工程项目的 AI 编码助手全局工作规范。

它综合了 MiMo Code、Codex 等编码代理的常见使用经验，目标是统一 AI 的规则层级、执行边界、工程质量、任务续接和文件管理习惯：少空话，多推进；少猜测，多核实；少炫技，多贴合现有项目。

## 适合谁

- 主要使用中文和国内开发环境的用户。
- 希望统一多种 AI 编码工具行为的人。
- 希望 AI 写代码时更重视最小改动、SQL 性能、代码可读性和验证闭环的人。
- 希望长任务能够跨会话继续，并避免 AI 工作资料散落在项目中的人。
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

## 可选依赖

这份仓库本质上是一份提示词模板，复制 `AGENTS.md` 不会自动安装任何命令行工具或 MCP 工具。

模板中提到的 CodeGraph 是可选的外部代码分析能力，需要单独安装。可以用下面的命令做最小检查：

```powershell
codegraph --version
codegraph status
```

完整模板只会在 CodeGraph 已安装且项目已经初始化时优先使用它；不可用时继续使用 `rg` 和现有工具，不会把安装或初始化当成任务前置条件。

`.ai-work/` 不是软件依赖，而是默认的项目级 AI 工作空间。它仅在任务确有需要时创建，用于统一保存 AI 内部工作资料；长任务可在其中使用 `state.md` 保存续接状态。该目录默认不提交版本库。

## 包含哪些规则

- 中文优先和国内用户语境。
- 明确规则优先级、任务类型、授权边界和外部副作用。
- 少问但不乱猜：低风险假设可以推进，高风险或会返工时再确认。
- 先明确成功标准，再做最小必要改动。
- 写代码时保持逻辑清晰，避免绕来绕去、深嵌套和过度抽象。
- 写 SQL 和数据访问代码时默认考虑性能，避免隐式全表扫描、无边界查询和 N+1 查询。
- 保留用户已有代码和项目风格，不顺手重构无关内容。
- 长任务在唯一 AI 工作空间维护精简的续接状态，便于跨会话继续。
- 所有 AI 内部工作资料统一放入唯一工作空间，避免在项目中散落文件和目录。
- 条件化使用 CodeGraph 做源码结构分析，并明确它与 `rg` 的分工。
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

如果项目已有唯一的 AI 工作目录约定，可以把默认的 `.ai-work/` 改成现有目录。没有使用 CodeGraph 时可以保留其条件化规则，也可以删除对应章节。

如果你的团队有固定数据库规范、测试策略或代码风格，建议把这些规则追加到 `工程质量` 后面。

## 设计原则

这份提示词刻意避免“神奇咒语”和过度人格化，重点放在可执行的工程行为上：

- 让 AI 先理解上下文，而不是直接改代码。
- 让 AI 少做无关改动，降低 diff 噪音。
- 让 AI 主动关注 SQL 和数据访问性能。
- 让长任务能够恢复，并把 AI 工作资料集中在唯一位置。
- 让专业工具在确有价值且满足条件时使用，而不是成为固定仪式。
- 让 AI 交付前做验证，而不是只说“应该可以”。
- 让 AI 对当前信息、法律金融医疗等高风险问题保持谨慎。

## License

MIT
