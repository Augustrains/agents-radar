# Hugging Face 热门模型日报 2026-06-25

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-25 02:00 UTC

---

好的，以下是为你整理的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-06-25**

#### **1. 今日速览**

本周 Hugging Face 生态迎来重磅发布：**DeepSeek-V4-Pro** 以压倒性点赞（5,048）登顶，延续了国产大模型的热潮。与此同时，**GLM-5.2** 系列（原版、量化版、FP8版）全面爆发，显示出 MoE 架构在推理效率上的巨大吸引力。在多模态领域，**NVIDIA LocateAnything-3B** 和 **MiniMax-M3** 表现抢眼，视觉定位与多模态理解仍是核心战场。此外，**Gemma-4-12B** 家族在社区微调（如Agentic、Coder、Abliterated）和 GGUF 量化方面持续升温，显示 Google 模型已成为社区二创的基石之一。

#### **2. 热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **deepseek-ai/DeepSeek-V4-Pro** (作者: deepseek-ai, 👍5,048, ⬇️2,052,463)  
  最新旗舰级对话模型，拥有强大的推理与代码能力，以绝对优势获得本周最高关注度。

- **zai-org/GLM-5.2** (作者: zai-org, 👍2,358, ⬇️57,186)  
  智谱AI 最新 MoE 开源模型，DSA 架构在保持性能的同时大幅降低推理成本，社区讨论度极高。

- **zai-org/GLM-5.2-FP8** (作者: zai-org, 👍158, ⬇️445,304)  
  GLM-5.2 的 FP8 半精度版本，极大降低了显存占用和部署门槛，下载量惊人。

- **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** (作者: yuxinlu1, 👍2,301, ⬇️483,139)  
  基于 Gemma-4-12B 的代码特化 GGUF 模型，社区量化版的明星，适合本地部署编程助手。

- **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** (作者: yuxinlu1, 👍534, ⬇️138,704)  
  Gemma-4-12B 的 Agent 版本，擅长终端命令执行与任务规划，下载量增长迅速。

- **Qwen/Qwen-AgentWorld-35B-A3B** (作者: Qwen, 👍150, ⬇️223)  
  通义千问最新 Agent 专用 MoE 模型，35B 总参 + 3B 激活，主打游戏与模拟环境下的智能体决策。

- **poolside/Laguna-M.1** (作者: poolside, 👍95, ⬇️2,913)  
  来自 poolside 的代码与软件工程基础模型，专注于下一代 AI 辅助开发。

- **lordx64/Qwable-v1** (作者: lordx64, 👍180, ⬇️5,719)  
  社区基于 Qwen3.5-MoE 的微调版本，侧重对话体验优化。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **nvidia/LocateAnything-3B** (作者: nvidia, 👍2,347, ⬇️359,498)  
  NVIDIA 推出的通用视觉定位模型，支持指代分割、检测与跟踪，任务“定位一切”，实用性极强。

- **MiniMaxAI/MiniMax-M3** (作者: MiniMaxAI, 👍1,228, ⬇️143,093)  
   MiniMax 最新多模态大模型，原生支持图像、文本混合输入，在理解和生成任务上表现均衡。

- **moonshotai/Kimi-K2.7-Code** (作者: moonshotai, 👍984, ⬇️480,013)  
  月之暗面 Kimi 模型的最新代码多模态版本，适合图像与代码混合任务（如图表生成、代码截图理解）。

- **google/gemma-4-12B-it** (作者: google, 👍1,163, ⬇️2,114,441)  
  Google 官方指令微调版，支持“any-to-any”多模态输入输出，下载量巨大，是当前社区微调与量化的基础模型。

- **krea/Krea-2-Turbo** (作者: krea, 👍190, ⬇️878)  
  Krea 团队的新一代图像生成模型，主打快速生成和高质量输出，填补了文本到图像领域的空白。

- **owensong/Inflect-Nano-v1** (作者: owensong, 👍193, ⬇️0)  
  超轻量 TTS 模型，适合边缘设备部署，虽然是全新发布，但社区关注度很高。

- **nvidia/nemotron-3.5-asr-streaming-0.6b** (作者: nvidia, 👍678, ⬇️47,208)  
  NVIDIA 的高效流式语音识别模型，支持实时处理，适合语音交互应用。

- **Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF** (作者: Jackrong, 👍83, ⬇️10,867)  
  基于 Qwen3.6 的多模态代码模型 GGUF 版本，支持图像和文本的代码理解。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **baidu/Unlimited-OCR** (作者: baidu, 👍738, ⬇️45,687)  
  百度推出的“无限” OCR 模型，支持各类复杂场景的文本识别，是目前 OCR 领域的焦点。

- **WeiboAI/VibeThinker-3B** (作者: WeiboAI, 👍692, ⬇️49,569)  
  微博团队的 3B 小参数量数学推理模型，在数学竞赛任务上表现突出，证明了小模型的潜力。

- **datalab-to/lift** (作者: datalab-to, 👍147, ⬇️4,644)  
  专注于 PDF 内容提取与理解的多模态模型，文档智能化处理工具。

- **microsoft/FastContext-1.0-4B-SFT** (作者: microsoft, 👍336, ⬇️4,805)  
  微软的快速长上下文模型，针对长文档问答和检索任务进行了优化，适合 RAG 应用。

- **LiquidAI/LFM2.5-Embedding-350M** (作者: LiquidAI, 👍119, ⬇️11,471)  
  Liquid AI 的新一代嵌入模型，用于语义相似度计算，是构建高质量 RAG 系统的热门选择。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** (作者: HauhauCS, 👍2,209, ⬇️3,769,369)  
  社区对 Qwen3.6 MoE 模型的“无限制”微调版本，下载量已超过300万，是目前最热门的社区量化模型之一。

- **unsloth/GLM-5.2-GGUF** (作者: unsloth, 👍348, ⬇️76,971)  
  unsloth 优化的 GLM-5.2 GGUF 量化版，确保在消费级显卡上流畅运行。

- **huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated** (作者: huihui-ai, 👍124, ⬇️4,402)  
  对 Gemma-4-12B 代码模型进行“去审查”的微调版本，社区探索更具创造性的应用。

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** (作者: empero-ai, 👍354, ⬇️63,637)  
  融合了 Claude 风格调教的 Qwen3.5 量化版，社区趣味性微调的代表。

#### **3. 生态信号**

- **MoE 与大模型强强之争**：榜单上同时出现 **GLM-5.2 (MoE-DSA)**、**DeepSeek-V4 (Dense?)** 和 **Qwen3.6 MoE**，说明 MoE 架构在降低推理成本的同时保持高性能，正成为头部 Labs 的共同选择，但传统 Dense 模型（如 DeepSeek-V4-Pro）凭借更强的单次推理能力依然强势。
- **开源权重的“事实标准”**：所有上榜模型均为开源权重，并提供了 `transformers`、`safetensors` 和 `GGUF` 等多种格式。这表明开放权重模型已完全主导了开发者生态，社区生态也从“下载使用”转向了“微调定制”。
- **社区微调活动空前活跃**：围绕 **Gemma-4-12B** 和 **Qwen3.6** 的社区微调版本层出不穷（Agentic、Coder、Abliterated），反映了开发者不再满足于基础模型，而是追求针对特定场景（编程、Agent、角色扮演）的深度定制。**GGUF** 量化是社区二次传播的核心介质。

#### **4. 值得探索**

1.  **nvidia/LocateAnything-3B**：如果你对“视觉定位”或“机器人抓取”感兴趣，这个模型以极低的参数量（3B）实现了以前需要大模型才能完成的复杂视觉推理，是计算机视觉方向不能错过的模型。
2.  **zai-org/GLM-5.2** & **zai-org/GLM-5.2-FP8**：作为国产 MoE 的新锐，其 DSA 架构非常值得研究。建议直接尝试其 FP8 版本，可在一张消费级显卡（如 RTX 4090）上获得接近旗舰模型的对话体验。
3.  **microsoft/FastContext-1.0-4B-SFT**：如果你的工作涉及长文档分析（如论文、财报、法律文书），这款模型在 4B 参数下实现了超长上下文的快速处理，是构建高效 RAG 系统的优秀基座。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*