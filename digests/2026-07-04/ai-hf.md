# Hugging Face 热门模型日报 2026-07-04

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-04 01:30 UTC

---

好的，作为AI模型生态分析师，以下是基于您提供的2026-07-04数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-04**

#### **今日速览**

本周Hugging Face生态呈现三大核心趋势：首先，**大模型家族化竞争白热化**，以Qwen 3.5/3.6、GLM 5.2和DeepSeek V4为代表的旗舰模型及其衍生品占据半壁江山，尤其在MoE架构上竞争激烈。其次，**量化与社区微调极度活跃**，多个权重模型在发布后迅速跟上GGUF量化版，如“Ornith”系列和“Huihui-GLM”，且“Uncensored”（无审查）版本获得极高下载量，反映出社区对模型自由度的高度需求。最后，**“Agentic”（智能体）与“Coder”（代码）方向成为微调热点**，Google的Gemma 4系列凭借在此领域的针对性优化，涌现出多个高人气变体。

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** (作者: zai-org | 👍 3,343 | ⬇️ 191,462)  
  智谱AI的旗舰MoE模型，凭借高点赞数成为本周最受关注的对话模型，代表了国产开源大模型的一线实力。

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** (作者: deepseek-ai | 👍 343 | ⬇️ 9,388)  
  深度求索的V4系列高端Pro版本，标志着DeepSeek生态的正式迭代，对标顶级闭源模型，备受技术社区关注。

- **[deepreinforce-ai/Ornith-1.0-397B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)** (作者: deepreinforce-ai | 👍 200 | ⬇️ 8,079)  
  基于Qwen 3.5 MoE的巨型模型（约397B总参数量），展示了社区在超大模型上的探索野心，是规模竞赛的缩影。

- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LiquidAI/LFM2.5-230M)** (作者: LiquidAI | 👍 197 | ⬇️ 29,645)  
  Liquid AI出品的小参数甜蜜点模型，以极低成本实现高效文本生成，适合资源受限的推理场景。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** (作者: nvidia | 👍 2,589 | ⬇️ 1,108,586)  
  NVIDIA的视觉定位模型，能够无预设类别地定位图像中任何物体，以超高下载量成为本周现象级的多模态模型。

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** (作者: baidu | 👍 1,692 | ⬇️ 885,040)  
  百度的通用OCR模型，支持无限类别识别，在文档处理、票据识别等场景极具实用价值，下载量惊人。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** (作者: empero-ai | 👍 1,371 | ⬇️ 1,366,360)  
  融合“Claude Mythos”风格的视觉语言模型量化版，在保持高性能的同时大幅降低部署门槛，下载量突破百万。

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** (作者: krea | 👍 480 | ⬇️ 84,006)  
  Krea公司推出的新一代图像生成模型Turbo版，主打高速度和高质量，代表了文生图领域的快速迭代趋势。

- **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)** (作者: fal | 👍 150 | ⬇️ 0)  
  用于LTX视频模型的LoRA适配器，专攻3D写实风格文生视频，虽然刚发布暂无下载，但代表了视频生成精细化的发展方向。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** (作者: yuxinlu1 | 👍 2,585 | ⬇️ 628,225)  
  基于Google Gemma 4的代码专用模型，经过“Fable5”和“Composer2.5”等高级技术优化，在编程任务上表现出色。

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** (作者: yuxinlu1 | 👍 992 | ⬇️ 329,391)  
  同样是Gemma 4的变体，但这版专注于“Agentic”能力，专为自主规划和工具调用优化，是智能体生态的关键模型。

- **[BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6](https://huggingface.co/BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6)** (作者: BugTraceAI | 👍 125 | ⬇️ 11,444)  
  一款专注于网络安全和攻防的专用模型，填补了“Offensive Security”领域的空白，体现了AI在垂直安全领域的应用。

- **[nationaldesignstudio/rampart](https://huggingface.co/nationaldesignstudio/rampart)** (作者: nationaldesignstudio | 👍 115 | ⬇️ 1,149)  
  基于ONNX/BERT的PII（个人身份信息）识别模型，专注于数据脱敏和隐私保护，是企业级应用的实用工具。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** (作者: HauhauCS | 👍 2,432 | ⬇️ 3,029,679)  
  Qwen 3.6的“无审查”+“激进”风格社区量化版，以惊人的300万周下载量登顶，体现了社区对模型自由度的极致追求。

- **[yuuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** (作者: yuuxinlu1 | 👍 992 | ⬇️ 329,391)  
  Gemma 4的Agent变体量化版，证明了针对特定任务（代码/Agent）的量化模型同样能获得极高人气。

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** (作者: unsloth | 👍 938 | ⬇️ 1,774,298)  
  Unsloth团队出品的Qwen 3.6 27B MTP量化版，以高效的量化工具和庞大的用户基础，成为Qwen生态中最受欢迎的量化模型之一。

- **[huihui-ai/Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)** (作者: huihui-ai | 👍 144 | ⬇️ 3,683)  
  对GLM 5.2进行“abliterated”（消除对齐限制）的社区版本，反映了社区对模型控制权的追求，是“Uncensored”运动的变体。

- **[nvidia/GLM-5.2-NVFP4](https://huggingface.co/nvidia/GLM-5.2-NVFP4)** (作者: nvidia | 👍 214 | ⬇️ 189,970)  
  英伟达为GLM 5.2提供的NVFP4 4-bit量化版，结合硬件厂商的优化，展示了软硬件协同的量化降本路径。

#### **生态信号**

本周生态信号非常明确：**“开放”与“可控”是社区主旋律**。模型家族方面，**Qwen 3.x**系列（含3.5、3.6）凭借其强大的MoE架构和开放的许可，成为社区二次创作（量化、微调、Uncensored）最大的基石。**GLM与DeepSeek**作为国内顶级玩家，竞争正从单模型转向模型家族生态。

在开源与闭源的博弈中，**开源权重模型几乎主导了榜单**，其丰富的社区衍生品（GGUF、LoRA）形成了强大的飞轮效应。值得注意的是，**“Uncensored”和“Abliterated”模型的流行**，表明开发者群体对模型输出的自主权和探索边界有强烈需求，这将是未来模型发布和社区治理的重要议题。量化活动上，GGUF依然是绝对主流，而NVIDIA等硬件厂商的参与（如NVFP4）则预示着专用硬件的量化格式将获得增长。

#### **值得探索**

1.  **尝试：`nvidia/LocateAnything-3B`** ([链接](https://huggingface.co/nvidia/LocateAnything-3B))  
    **理由**：作为视觉定位的SOTA模型，它在“任何物体”上的零样本定位能力颠覆了传统目标检测的范式。高下载量和点赞数证明了其强大的实用性，是探索多模态AI应用的理想起点。

2.  **研究：`yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF`** ([链接](https://huggingface.co/yuuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF))  
    **理由**：该模型代表了将中小型模型（12B）通过精细微调（Fable5, Composer2.5）适配到“Agent”这一前沿方向的成果。研究其微调策略和量化后的效果，对于如何在有限算力下构建高效智能体具有极高的参考价值。

3.  **部署：`unsloth/Qwen3.6-27B-MTP-GGUF`** ([链接](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF))  
    **理由**：Qwen 3.6是当前生态的明星基座模型之一，而Unsloth团队在量化效率和易用性上极具口碑。此模型提供了性能与资源消耗的极佳平衡点（27B总参，MTP架构），是个人开发者和中小企业本地部署高性能大语言模型的首选方案之一。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*