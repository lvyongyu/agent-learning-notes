# 27 · 多模态:让 Agent 看图听声 / Multimodal Agents

> 实战篇 · 第 2 篇 / Hands-on track · Note 2

前面的 Agent 只会处理**文字**。但真实世界有图片、截图、语音、视频——能处理这些的模型叫**多模态 (Multimodal)**。
Our Agent so far handles only *text*. But the real world has images, screenshots, audio, video — models that handle these are **multimodal**.

## 一句话 / In One Sentence

> 多模态 = 模型的"输入/输出"不只是文字,还能是**图、声、视频**。模态(modality)就是"信息的种类"。
> Multimodal = the model's inputs/outputs aren't just text but also *images, audio, video*. A "modality" is a *kind* of information.

```
单模态(纯文字)/ text-only:
   文字 ──▶ 模型 ──▶ 文字

多模态 / multimodal:
   文字 ┐
   图片 ┼─▶ 模型 ──▶ 文字 (或图/语音)
   语音 ┘            text (or image / speech)
```

## 它解锁了哪些新能力 / What It Unlocks

| 能力 / Ability | 例子 / Example |
|----------------|----------------|
| 👀 **看图说话** | 上传一张报错截图,问"这是什么错误?" |
| 📄 **读文档/表格图** | 把一张发票拍下来,提取金额 |
| 🖥️ **看屏幕操作** | 看着界面截图,决定点哪个按钮(电脑操作 Agent) |
| 🎙️ **听语音** | 把会议录音转成纪要 |
| 🎨 **生成图像** | 根据文字描述画图(输出端的多模态) |

## 对 Agent 意味着什么 / Why It Matters for Agents

> 多模态让 Agent 的"[眼睛和耳朵](04-components.md)"打开了。它能处理的任务从"纯文本"扩展到"**任何能拍下来/录下来的东西**"。
> Multimodality opens the Agent's "eyes and ears". Its tasks expand from text to *anything you can photograph or record*.

最典型的就是 **计算机操作 Agent(Computer Use)**:
The classic case is a **computer-use Agent**:

```
循环和 [26 篇] 一样,只是"看"的部分变了:
Same loop as Note 26, but the "Observe" changes:

🧠 想:我要点"提交"按钮
🛠️ 做:调用工具【截屏】
👀 看:拿到一张界面图片(不是文字!)
🧠 想:从图里找到按钮在 (820, 540)
🛠️ 做:调用工具【点击 820,540】
……
```

这正是 [ReAct 循环](17-react.md),只是 Observation 从"文字结果"变成了"一张图"。
It's the same [ReAct loop](17-react.md), with the Observation now an image instead of text.

## 实战注意点 / Practical Gotchas

| 注意 / Gotcha | 说明 / Note |
|---------------|-------------|
| 💸 **图片很费 token** | 一张图可能顶上千字,[成本/窗口](07-context-memory.md) 压力大 / images cost lots of tokens |
| 🔍 **细节会看漏** | 小字、密集表格可能识别不准,要验证 / fine print can be misread |
| 🧩 **不是所有模型都支持** | 选模型时要确认它支持你要的模态 / check the model supports your modality |
| 🎭 **图里也能藏攻击** | 图片里的文字也可能是 [提示词注入](13-safety.md) / images can carry injections too |

> 小知识 / Note:多模态没有改变 Agent 的骨架——还是 [那个循环](26-build-minimal-agent.md)。变的只是"喂进去的东西"和"工具返回的东西"可以是图片/声音了。
> Multimodality doesn't change the Agent's skeleton — still [the same loop](26-build-minimal-agent.md). Only the *inputs* and *tool results* can now be images/audio.

➡️ 下一篇 / Next: [上线工程](28-production.md)
