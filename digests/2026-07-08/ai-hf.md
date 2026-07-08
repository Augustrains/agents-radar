# Hugging Face 热门模型日报 2026-07-08

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-08 01:21 UTC

---

好的，这是基于您提供的数据生成的《Hugging Face 热门模型日报》。

---

# Hugging Face 热门模型日报 | 2026年7月8日

## 今日速览

本周 Hugging Face 生态迎来两大核心趋势：一是 **Qwen 3.5/3.6 家族成为绝对主导**，周榜中有超过 12 个模型以其为基座，覆盖从量化版到多模态变体，社区微调热度极高；二是 **超大参数的 MoE (混合专家) 模型进入主流视野**，如 `mistralai/Leanstral-1.5-119B-A6B` 与 `zai-org/GLM-5.2` 凭借极致参数效率成为焦点。此外，**GGUF 量化版本**继续霸榜下载量，体现了社区对本地化部署的强烈需求。

---

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**
  - 作者: zai-org | 点赞: 3,591 | 下载: 281,584
  - 说明：一款极具潜力的 MoE 模型，凭借高点赞成为本周最受关注的对话式模型，其 5.2 版本采用了新型 DSA 架构。

- **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)**
  - 作者: mistralai | 点赞: 157 | 下载: 157
  - 说明：Mistral 推出的极致稀疏 MoE 模型，总参数量 119B 但每次推理仅激活 6B，是“大力出奇迹”与“效率优先”理念的结合。

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)**
  - 作者: deepseek-ai | 点赞: 424 | 下载: 15,538
  - 说明：DeepSeek V4 Pro 版本，带有专用推理框架 DSpark，作为头部闭源厂商的开放权重模型，备受开发者关注。

- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)**
  - 作者: meituan-longcat | 点赞: 139 | 下载: 385
  - 说明：美团推出的长上下文对话模型，聚焦于解决长文本场景下的对话连贯性问题。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
  - 作者: nvidia | 点赞: 2,657 | 下载: 1,424,958
  - 说明：NVIDIA 发布的通用目标定位模型，仅 3B 参数就能完成零样本下的图像中任意物体定位，是视觉理解领域的新星。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
  - 作者: HauhauCS | 点赞: 2,551 | 下载: 2,823,988
  - 说明：基于 Qwen 3.6 的大型 MoE 模型，以“无审查”和更激进的回复风格为特色，下载量遥遥领先。

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**
  - 作者: baidu | 点赞: 1,833 | 下载: 1,084,945
  - 说明：百度推出的通用 OCR 模型，宣称能处理无限长文本的识别任务，实用价值极高。

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)**
  - 作者: krea | 点赞: 540 | 下载: 123,729
  - 说明：Krea 公司推出的文生图加速版模型，基于 Krea-2 优化，主打快速生成。

### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**
  - 作者: yuxinlu1 | 点赞: 2,638 | 下载: 674,977
  - 说明：基于 Google Gemma 4 的代码专用模型，融合了 Fable5 与 Composer2.5 技术，在代码生成与推理任务上表现突出。

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)**
  - 作者: google | 点赞: 287 | 下载: 9,458
  - 说明：谷歌推出的表格数据基础模型，支持零样本的表格分类与回归，正推动 AI 在结构化数据分析中的应用。

- **[nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16](https://huggingface.co/nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16)**
  - 作者: nvidia | 点赞: 131 | 下载: 10,936
  - 说明：NVIDIA 发布的“双塔”架构基础模型，专为在检索增强生成（RAG）和特征提取场景进行优化。

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**
  - 作者: empero-ai | 点赞: 1,758 | 下载: 1,683,711
  - 说明：社区微调标杆，将 Qwen 3.5 与 Claude 风格融合，提供 GGUF 量化版，下载量超 168 万，适合本地部署。

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**
  - 作者: unsloth | 点赞: 991 | 下载: 2,842,118
  - 说明：知名量化团队 Unsloth 出品的 Qwen3.6 量化版，下载量接近 300 万，是性价比最高的 27B 级本地模型之一。

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)**
  - 作者: deepreinforce-ai | 点赞: 779 | 下载: 502,663
  - 说明：Ornith 系列的 35B GGUF 版，在性能和资源占用间取得了不错的平衡，社区下载量活跃。

- **[Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF)**
  - 作者: Jackrong | 点赞: 161 | 下载: 159,871
  - 说明：结合了 Qwen 3.6 MoE 与代码能力的量化版，轻量级多模态代码助手。

---

## 生态信号

1.  **Qwen 家族势不可挡**：无论是官方发布的 `Qwen-AgentWorld-35B`，还是社区量化的各种变体（Unsloth、HauhauCS、Jackrong），Qwen 3.5/3.6 已成为本周的“空气”模型，覆盖了从代码到对话到视觉的各个细分赛道的微调与量化。
2.  **MoE 架构成为主流**：本周榜单上出现了多个 MoE 模型（GLM-5.2、Leanstral、Ornith、Agents-A1）。这表明社区正在迅速拥抱“大参数、小激活”的设计哲学，以更低的推理成本换取更强的能力。
3.  **开源权重与闭源的拉扯**：`DeepSeek-V4-Pro` 和 `GLM-5.2` 等模型的出现，表明头部闭源厂商（DeepSeek、智谱）依然在强力贡献开源权重。同时，NVIDIA 与 Google 持续通过开放权重模型（如 LocateAnything、TabFM）巩固其生态影响力。

---

## 值得探索

1.  **`nvidia/LocateAnything-3B`**：如果你对视觉 AI 感兴趣，这是本周必试模型。3B 参数就能实现强大的零样本定位能力，为图像理解和机器人视觉提供了新的基线。
2.  **`mistralai/Leanstral-1.5-119B-A6B`**：对于关注模型效率的研究者，这是极佳的研究对象。它是当前“超大参数、极小激活”流派的代表，有望推动高效推理领域的发展。
3.  **`zai-org/GLM-5.2`**：作为本周点赞最高的模型，它代表了智谱在 MoE 方向的最新探索。如果你是中文社区模型的使用者或开发者，值得深入体验其对话与推理能力。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*