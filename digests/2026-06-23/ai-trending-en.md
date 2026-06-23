# AI Open Source Trends 2026-06-23

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-23 01:58 UTC

---

Here is the structured **AI Open Source Trends Report** for 2026-06-23.

---

## 1. Today's Highlights

The open-source AI ecosystem today is dominated by a massive pivot toward **agentic video and content production**, led by **OpenMontage** (+2,938 stars today) and **Hyperframes** (+395). Simultaneously, the **agent skills/CLI configuration market** has exploded, with **palmier-pro** (+2,463), **mattpocock/skills** (+2,051), and **garrytan/gstack** (+573) reflecting a new trend: developers are selling and open-sourcing their exact agent setups (`.claude` directories, toolchains) as starter kits. ByteDance’s **deer-flow** (+738) signals continued major corporate investment in long-horizon agent harnesses, while **DeusData/codebase-memory-mcp** (+1,185) reveals that persistent code knowledge graphs (via MCP) are becoming the default architecture for coding agents.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure (Frameworks, SDKs, Inference Engines, CLI Tools)
- **[DeusData/codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp)** ⭐+1,185 today — High-performance MCP server that indexes entire codebases into a persistent knowledge graph in milliseconds; 158 languages, sub-ms queries.
- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐174,754 total — The de facto local LLM runner; now supporting Kimi-K2.6, GLM-5.1, and Gemma out of the box.
- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐83,585 total — High-throughput LLM inference engine, the backbone of most self-hosted AI deployments.
- **[lyogavin/airllm](https://github.com/lyogavin/airllm)** ⭐+193 today — Enables 70B parameter inference on a single 4GB GPU; critical for edge deployment.
- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐+1,557 today — LLM-powered multi-market stock analysis with zero-cost scheduled runs; a strong example of AI + financial infrastructure.

### 🤖 AI Agents / Workflows (Agent Frameworks, Automation, Multi-Agent)
- **[calesthio/OpenMontage](https://github.com/calesthio/OpenMontage)** ⭐+2,938 today — World's first open-source agentic video production system: 12 pipelines, 52 tools, 500+ agent skills. The top trending repo overall.
- **[bytedance/deer-flow](https://github.com/bytedance/deer-flow)** ⭐+738 today — ByteDance's open-source long-horizon SuperAgent harness; researches, codes, and creates with sandboxes, memories, and subagents.
- **[mattpocock/skills](https://github.com/mattpocock/skills)** ⭐+2,051 today — Straight from the `.claude` directory: skills for "real engineers." A new category of agent starter kits.
- **[garrytan/gstack](https://github.com/garrytan/gstack)** ⭐+573 today — Garry Tan's exact Claude Code setup: 23 opinionated tools serving as CEO, Designer, Eng Manager, etc.
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐199,996 total — "The agent that grows with you." Highly modular, growing agent framework.
- **[langgenius/dify](https://github.com/langgenius/dify)** ⭐146,178 total — Production-ready platform for agentic workflow development, now the flagship of the RAG + Agent cross-section.

### 📦 AI Applications (Specific Vertical Solutions, End-User Tools)
- **[jamiepine/voicebox](https://github.com/jamiepine/voicebox)** ⭐+529 today — Open-source AI voice studio: clone, dictate, and create. Competing with ElevenLabs.
- **[heygen-com/hyperframes](https://github.com/heygen-com/hyperframes)** ⭐+395 today — Write HTML, render video. Built specifically for AI agents to generate video content.
- **[mukul975/Anthropic-Cybersecurity-Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)** ⭐+956 today — 817 structured cybersecurity skills mapped to 6 frameworks (MITRE ATT&CK, NIST CSF, etc.). A domain-specific agent skillset.
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐47,670 total — AI productivity studio with 300+ assistant personas and autonomous agents.
- **[santifer/career-ops](https://github.com/santifer/career-ops)** ⭐55,240 total — AI-powered job search system built on Claude Code; 14 skill modes.

### 🧠 LLMs / Training (Model Weights, Training Frameworks, Fine-Tuning)
- **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐161,819 total — The standard model-definition framework; continues to define how models are built and shared.
- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐185,088 total — The original autonomous agent project; still a massive reference for agent research.
- **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)** ⭐78,037 total — AI-driven development framework; one of the most active in the code-generation agent space.
- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐+266 today — New pretraining library for foundation/world models, gaining traction for reliability and minimalism.
- **[zjunlp/LightThinker](https://github.com/zjunlp/LightThinker)** ⭐+164 today — EMNLP 2025 paper implementing step-by-step compression during reasoning (thinking tokens compression).

### 🔍 RAG / Knowledge (Vector Databases, Retrieval-Augmented Generation, KM)
- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** ⭐+615 today, 137,351 total — The API to search, scrape, and interact with the web at scale; now the standard web connector for RAG pipelines.
- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐83,374 total — Leading open-source RAG engine with agent capabilities; the most starred dedicated RAG system.
- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** ⭐83,767 total — Persistent context across sessions; captures, compresses, and injects memories for Claude Code, OpenClaw, and more.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐59,151 total — Universal memory layer for AI agents; the standard for persistent agent memory.
- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐44,896 total — Cloud-native vector database; the most battle-tested infrastructure for production RAG.
- **[VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex)** ⭐33,296 total — "Vectorless, reasoning-based RAG" — a new approach to retrieval without traditional vector embeddings.
- **[StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN)** ⭐12,508 total — MLsys2026 paper: 97% storage savings while running fast, accurate, private RAG on personal devices.

---

## 3. Trend Signal Analysis

**Video generation enters the agent stack.** The most explosive signal today is **OpenMontage** (+2,938 stars). It’s the first open-source system that frames video production as an agentic pipeline (12 pipelines, 52 tools, 500 skills). This, combined with **HeyGen's Hyperframes** (HTML-to-video for agents) and **palmier-pro** (macOS AI video editor), suggests a major inflection point: **video is becoming a first-class output modality for AI agents**, not just a separate generative model.

**The "agent skills marketplace" is born.** Three of the top 10 trending repos today — **mattpocock/skills**, **garrytan/gstack**, and **mukul975/Anthropic-Cybersecurity-Skills** — are not tools themselves, but **exported Claude Code configurations, skill directories, and `.claude` setups**. Developers are treating their CLI agent setups as shareable, marketable artifacts. This signals a new distribution model: "bring your own agent setup" is replacing "buy the tool."

**MCP (Model Context Protocol) becomes the universal glue.** **DeusData/codebase-memory-mcp** (+1,185) and **zilliztech/claude-context** (+11,927 total) are both MCP servers that index codebases into persistent knowledge graphs. The trend: **MCP is standardizing how agents access long-term memory** — not just databases, but entire codebases, conversation histories, and tool outputs. The `codebase-memory-mcp` repo’s claim of "99% fewer tokens" is a breakthrough claim for agent efficiency.

**Corporate AI open-source is accelerating.** ByteDance’s **deer-flow** (+738) and Alibaba’s **zvec** (lightweight vector DB) represent major Chinese tech companies doubling down on open-source agent infrastructure. The connection to recent LLM releases (e.g., Kimi-K2.6 in Ollama) suggests these companies see open-source retention as a competitive moat.

**Edge inference hits a new low point.** **airllm** (+193) running 70B models on a 4GB GPU, combined with **LEANN** (97% storage savings for on-device RAG), points to a strong push toward **practical on-device AI** — not just small models, but efficient inference of large models on commodity hardware.

---

## 4. Community Hot Spots

- **[calesthio/OpenMontage](https://github.com/calesthio/OpenMontage)** — The #1 trending repo overall. If you work on agentic content generation, this is the reference architecture to watch today.
- **[mattpocock/skills](https://github.com/mattpocock/skills)** — A new category: "developer skills as open-source artifacts." If you have a well-tuned Claude Code setup, consider sharing it as a repo — this format is exploding.
- **[DeusData/codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp)** — The fastest path to giving your coding agent persistent, token-efficient memory. 158 languages, sub-ms queries, zero-dependency binary.
- **[mukul975/Anthropic-Cybersecurity-Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)** — The most comprehensive structured skill set for AI agents in cybersecurity. 817 skills across 6 frameworks. A model for domain-specific agent skills.
- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** — The leading example of a zero-cost, LLM-driven financial analysis pipeline. If you want to see how LLMs can run scheduled, agentic workflows for free, study this repo.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*