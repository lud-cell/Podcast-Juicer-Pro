# Podcast-Juicer-Pro
基于 OpenClaw 的全自动、零幻觉、阅后即焚的播客硬核提炼工作流（Groq API 加持）

## 🌟 核心痛点与解决方案 (Why this exists?)
听完播客后总是啥都没记住，因此我设计了以下内容总结工作流，帮助回忆要点，加强理解

## 🛠️ 环境依赖与配置 (Prerequisites & Setup)

1. **基础环境**：[OpenClaw](https://github.com/OpenClaw/OpenClaw) 运行实例。
2. **必备 Skills（插件）**：
   * `agent-browser`：用于解析网页和抓取真实音频流。
   * `openai-whisper-api`：用于对接云端语音大模型。

3. **关键配置**：
   前往 [GroqCloud](https://console.groq.com/) 申请免费 API Key，并在 OpenClaw 的 `openai-whisper-api` 插件中填入以下参数：
   * **API Key**: `gsk_xxxxxxx` (你的 Groq 密钥)
   * **Base URL**: `https://api.groq.com/openai/v1` (⚠️ 必须修改以重定向至 Groq)
   * **Model**: `whisper-large-v3`

---

## 🚀 核心工作流指令 (The Workflow Prompt)

将以下指令完整复制，存入你的 OpenClaw System Prompt 或作为快捷指令触发：

```text
【工作流代号】：Podcast-Juicer-Pro (全自动无痕提炼 - 云端极速版)

【执行协议】：
当我向你发送一个小宇宙或播客链接，并让你执行本工作流时，你必须严格按顺序、全自动调用以下技能，中途不需要向我请示：

Step 1: 网页解析与获取
调用 agent-browser 技能，访问我提供的 URL，提取网页中的音频真实下载地址和基础 Meta 信息。

Step 2: 音频转录 (Audio Transcribe)
将音频文件下载到本地临时目录。立即调用 openai-whisper-api 技能（调用 Groq 云端算力），对该音频进行高精度的全文极速转录，并临时保存为 txt 逐字稿。

Step 3: 物理销毁一（删音频）
确认文本转录 100% 完成后，立即执行文件删除操作，将刚才下载的**音频源文件（.mp3/m4a等）**从服务器中彻底删除。

Step 4: 硬核提炼与防幻觉总结
读取生成的临时 txt 逐字稿，严格按照以下模板进行总结，严禁任何形式的常识脑补或数据编造：

🎯 终极结论 (The Bottom Line)
用精炼的语言（50-100字），概括这期播客到底解决了一个什么核心问题，或者传达了什么最核心的理念？

✨ 高光时刻 (Top 3-5 Highlights)
（挑选全篇最反常识、最硬核的 3-5 个点。必须按以下格式输出：）
* [核心观点简述]
  * 🎙️ 原音重现：“（在此填入原文中支撑该观点的精确语句，必须带双引号）”
  * 💡 为什么重要：结合商业模式或壁垒，用一句话解释这个观点有何启发。如果原文没提，必须写“原文未提及”。

🔍 贝壳扫雷 (Quality Check)
* 一句话点评这期播客的“水分”大不大。
* 指出嘉宾逻辑不够闭环或没讲透的一个痛点。

Step 5: 最终交付与物理销毁二（删文本）
将 Step 4 生成的总结排版美观后，发送到对话框。
强制清场动作： 确认消息发送成功后，立即将生成的 txt 逐字稿文件彻底删除。确保整个工作流结束后，服务器上不留存任何原始音频和过程文本。
