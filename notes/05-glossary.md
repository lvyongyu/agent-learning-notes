# 05 · 术语表 / Glossary（中英对照）

面试 / 看英文资料时常遇到的词，先混个眼熟。
Common terms you'll meet in interviews and English docs.

| 中文 | English | 一句话解释 / TL;DR |
|------|---------|--------------------|
| 智能体 | **Agent** | 会用工具、能循环干活的 LLM / an LLM that uses tools in a loop |
| 大语言模型 | **LLM** (Large Language Model) | Agent 的"大脑" / the Agent's brain |
| 工具 | **Tool** | Agent 能调用的功能（读文件、搜索…）/ a callable capability |
| 工具调用 | **Tool Call / Function Call** | Agent 决定使用某个工具的动作 / the act of invoking a tool |
| 上下文 | **Context** | Agent 当前"记得"的所有信息 / everything the Agent currently "remembers" |
| 上下文窗口 | **Context Window** | 记忆的容量上限（按 token 算）/ the memory size limit |
| 词元 | **Token** | 文本的最小计费单位 / the billing unit of text |
| 提示词 | **Prompt** | 你给模型的输入/指令 / the input you give the model |
| 系统提示词 | **System Prompt** | 设定 Agent 角色和规则的"开场说明" / sets the Agent's role & rules |
| 思考-行动-观察 | **Think-Act-Observe** | Agent 的核心循环 / the core loop |
| ReAct | **ReAct** | "推理+行动"的经典 Agent 模式 / Reasoning + Acting pattern |
| 子智能体 | **Sub-agent** | 主 Agent 派出去做子任务的小 Agent / a helper Agent for subtasks |
| 检索增强 | **RAG** (Retrieval-Augmented Generation) | 先查资料再回答 / look things up before answering |

---

← 回目录 / Back to [README](../README.md)
