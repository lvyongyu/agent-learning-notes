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
| 输入规格 | **Input Schema** | 工具参数的格式约定 / the spec of a tool's arguments |
| 工具结果 | **Tool Result** | 工具执行后回传给模型的内容 / what a tool returns to the model |
| 幻觉 | **Hallucination** | 模型一本正经编造的假内容 / confident but false output |
| 提示词注入 | **Prompt Injection** | 把坏指令藏进数据里冒充命令 / hidden malicious instructions in data |
| 提示词工程 | **Prompt Engineering** | 把提示词写好的手艺 / the craft of writing good prompts |
| 规划/拆解 | **Planning / Decomposition** | 把大任务拆成步骤再执行 / break a big task into steps |
| 评估集 | **Eval** | 用题目集给 Agent 打分 / a test set to score an Agent |
| AI 当裁判 | **LLM-as-judge** | 用另一个模型给输出打分 / use a model to grade output |
| 人在环中 | **Human in the Loop** | 关键操作让人确认 / a human confirms key actions |
| 最小权限 | **Least Privilege** | 只给必需的权限 / grant only what's needed |
| 向量 | **Embedding** | 把文字变成一串表示"意思"的数字 / text turned into meaning-numbers |
| 向量数据库 | **Vector DB** | 按"意思"存取片段的库 / store & search by meaning |
| 模型上下文协议 | **MCP** (Model Context Protocol) | 接外部工具的统一标准 / a universal tool-plug standard |
| 思维链 | **CoT** (Chain-of-Thought) | 让模型一步步想出声 / reason step by step |
| 反思 | **Reflection** | 做完自我审查再改 / self-critique then revise |
| 先规划后执行 | **Plan-and-Execute** | 先列完整计划再逐项做 / plan all, then do |
| 路由 | **Router** | 先判断类型再分派 / classify then dispatch |
| 零样本 | **Zero-shot** | 不给例子直接问 / ask with no examples |
| 少样本 | **Few-shot** | 给几个例子让它照学 / show a few examples |
| 结构化输出 | **Structured Output** | 输出程序可读的格式(JSON)/ machine-readable output |
| 预训练 | **Pre-training** | 海量文本学"猜下一个词" / learn next-token on huge text |
| 微调 | **Fine-tuning / SFT** | 用范例教它好好回答 / teach it to answer well |
| 人类反馈强化学习 | **RLHF** | 用人的偏好对齐模型 / align via human preference |
| 对齐 | **Alignment** | 让行为符合人类期望 / match human expectations |
| 知识截止日期 | **Knowledge Cutoff** | 训练数据的时间上限 / when its knowledge stops |
| 温度 | **Temperature** | 控制随机/创意程度 / randomness dial |
| 核采样 | **Top-p** | 只在高概率候选里抽词 / sample from top probability mass |
| 幻觉(根因) | **Next-token Prediction** | 模型本质:按概率猜下一个词 / its essence |

---

← 回目录 / Back to [README](../README.md)
