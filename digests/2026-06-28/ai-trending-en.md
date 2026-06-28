# AI Open Source Trends 2026-06-28

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-28 02:07 UTC

---

# AI Open Source Trends Report — 2026-06-28

## Step 1: Filter (AI/ML Relevant Projects)

**Excluded (non-AI):**
- simplex-chat (private messaging)
- CasaOS (personal cloud OS)
- free-for-dev (SaaS list)
- microsoft/PowerToys (Windows utilities)
- dbt-core (data transformation)
- keycloak (IAM)
- open-seo (SEO tool)
- JuliaLang/julia (general language)
- Developer-Y/cs-video-courses (education list)
- netdata (monitoring, though has AI features, primarily infra)
- tesseract-ocr (OCR, included as AI-adjacent)

**Included AI/ML projects from trending + topic search (deduplicated):**

From Trending (20 repos): ai-berkshire, openpilot, design.md, ppt-master, ai-website-cloner-template, gstack, MediaCrawler, Open-Generative-AI, cognee, claude-howto, opencode, OpenSpec, Vibe-Trading → **13 AI projects**

From Topic Search (81 repos): All topic-tagged repos are AI-related → **81 projects**

**Final filtered set: 94 unique AI projects**

---

## Step 2: Categorization

### 🤖 AI Agents / Workflows (30 projects)
Core agent frameworks, coding agents, automation tools, multi-agent systems

### 🔧 AI Infrastructure (25 projects)
Frameworks, SDKs, inference engines, development tools, CLI tools

### 🔍 RAG / Knowledge (18 projects)
Vector databases, retrieval-augmented generation, knowledge management, memory

### 📦 AI Applications (14 projects)
Vertical applications, specific use-case solutions, trading, content generation

### 🧠 LLMs / Training (7 projects)
Model weights, training frameworks, fine-tuning, evaluation

---

## Step 3: Report

### 1. Today's Highlights

The AI open-source ecosystem is experiencing an unprecedented **agent harness explosion**, led by Claude Code ecosystem tooling. **NousResearch/hermes-agent** (⭐204k) and **affaan-m/ECC** (⭐222k) dominate as the most-starred agent performance systems, while **topoteretes/cognee** (+780 today) surges as the go-to memory layer for persistent agent context. A notable new direction is **spec-driven development (SDD)**, with **Fission-AI/OpenSpec** gaining traction for structuring AI coding workflows. Financial AI continues to heat up — **xbtlin/ai-berkshire** (+685 today) applies multi-agent value investing, and **HKUDS/Vibe-Trading** targets personal trading agents. The **coding agent arms race** is intensifying, with **anomalyco/opencode** (+392 today) emerging as a major open-source alternative to Claude Code and Codex.

---

### 2. Top Projects by Category

#### 🤖 AI Agents / Workflows

| Project | Stars | Today | Description |
|---------|-------|-------|-------------|
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 204,381 | — | The fastest-growing modular agent harness; "the agent that grows with you" with skill, memory, and research-first design |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 185,186 | — | Pioneer autonomous agent framework, still central to the agent ecosystem |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 78,516 | — | AI-driven development platform competing directly with Claude Code and Cursor |
| [bytedance/deer-flow](https://github.com/bytedance/deer-flow) | 75,061 | — | ByteDance's long-horizon SuperAgent harness with sandboxes, tools, and multi-agent orchestration |
| [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | 68,679 | — | "Bash is all you need" — minimalist Claude Code clone built from scratch, highly educational |
| [anomalyco/opencode](https://github.com/anomalyco/opencode) | — | +392 | Open-source coding agent alternative to Claude Code, gaining rapid adoption |
| [garrytan/gstack](https://github.com/garrytan/gstack) | — | +674 | Opinionated Claude Code tool set (CEO, Designer, Eng Manager personas) — shows trend of **role-specific agent configs** |

#### 🔧 AI Infrastructure

| Project | Stars | Today | Description |
|---------|-------|-------|-------------|
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 140,348 | — | The foundational agent engineering platform; now "the agent engineering platform" rebranded |
| [langgenius/dify](https://github.com/langgenius/dify) | 146,782 | — | Production-grade agentic workflow platform — dominant for enterprise LLM apps |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 143,249 | — | User-friendly LLM interface supporting Ollama and all major APIs — the de facto local AI frontend |
| [ollama/ollama](https://github.com/ollama/ollama) | 175,004 | — | Updated to support Kimi-K2.6, GLM-5.1, MiniMax — adding more Chinese LLMs |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 84,587 | — | High-throughput LLM inference engine — essential for self-hosting production LLMs |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 100,982 | — | Makes websites accessible to AI agents — critical infrastructure for web automation agents |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | 140,049 | — | Web scraping API for AI agents — explosive growth as LLM web access layer |

#### 🔍 RAG / Knowledge

| Project | Stars | Today | Description |
|---------|-------|-------|-------------|
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | 24,034 | +780 | **Hot project today**: open-source AI memory platform with knowledge graph engine for persistent agent memory |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 84,754 | — | Persistent context across sessions for every agent — compresses and injects relevant history |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 59,599 | — | Universal memory layer for AI agents — becoming standard for long-term agent memory |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 83,749 | — | Leading open-source RAG engine with agent capabilities — enterprise-grade retrieval |
| [VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex) | 33,474 | — | Vectorless, reasoning-based RAG — alternative approach without vector embeddings |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | 12,597 | — | MLsys2026 paper: 97% storage savings for private RAG — significant cost reduction breakthrough |
| [zilliztech/claude-context](https://github.com/zilliztech/claude-context) | 11,982 | — | Code search MCP for Claude Code — makes entire codebase agent-accessible |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,983 | — | Cloud-native vector database — stable backbone for production RAG |

#### 📦 AI Applications

| Project | Stars | Today | Description |
|---------|-------|-------|-------------|
| [xbtlin/ai-berkshire](https://github.com/xbtlin/ai-berkshire) | — | +685 | **Hot project today**: Multi-agent value investing framework using Claude Code — Buffett/Munger methodology |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 33,114 | +589 | AI generates editable PowerPoints from documents with native shapes, animations, and audio narration |
| [Anil-matcha/Open-Generative-AI](https://github.com/Anil-matcha/Open-Generative-AI) | — | +255 | Unrestricted alternative to AI video platforms — 200+ models including Flux, Kling, Sora |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 89,165 | — | Multi-agent LLM financial trading framework — biggest financial AI agent project |
| [JCodesMore/ai-website-cloner-template](https://github.com/JCodesMore/ai-website-cloner-template) | — | +750 | **Hot project today**: Clone any website with one command using AI coding agents |
| [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading) | — | +92 | Personal trading agent — new entrant in AI-powered automated trading |
| [commaai/openpilot](https://github.com/commaai/openpilot) | — | +322 | Robotics OS upgrading driver assistance on 300+ cars — stable AI robotics application |

#### 🧠 LLMs / Training

| Project | Stars | Today | Description |
|---------|-------|-------|-------------|
| [huggingface/transformers](https://github.com/huggingface/transformers) | 161,976 | — | The universal model framework — continues as the standard for all LLM work |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 101,066 | — | Tensors and neural networks — core ML framework powering most AI projects |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 84,587 | — | High-throughput LLM inference — critical for self-hosting production models |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | 269 | — | New pretraining library for foundation models — minimal, scalable approach |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,126 | — | LLM evaluation platform supporting 100+ datasets — essential for model benchmarking |
| [zjunlp/LightThinker](https://github.com/zjunlp/LightThinker) | 164 | — | EMNLP 2025: Step-by-step compression for LLM reasoning — cutting-edge efficiency research |

---

### 3. Trend Signal Analysis

The dominant theme today is the **professionalization of AI coding agents**. Three distinct sub-trends are converging:

**Agent Harness Ecosystem Explosion**: The most-starred projects on GitHub today are no longer LLM models or frameworks — they're **agent harnesses** that orchestrate Claude Code, Codex, Gemini CLI, and open-source alternatives. **ECC** (⭐222k) and **hermes-agent** (⭐204k) dwarf even foundational frameworks like LangChain. This signals a shift from "how do I call an LLM?" to "how do I make an LLM reliably complete multi-step tasks?"

**Spec-Driven Development (SDD)**: A new paradigm is emerging where AI agents are guided by structured specifications. **Fission-AI/OpenSpec** (+177 today) and **google-labs-code/design.md** (+1541 today) represent a shift from prompt engineering to **specification engineering** — giving agents formal, machine-readable instructions rather than free-text prompts. This is the first major methodological innovation in AI-assisted coding since agent frameworks emerged.

**Vertical Financial AI**: The convergence of multi-agent systems with quantitative finance is accelerating. **ai-berkshire** (+685), **TradingAgents** (89k), and **Vibe-Trading** (+92) span from value investing to algorithmic trading. The methodology of "multi-agent adversarial analysis" (agents debating investment theses) is novel and gaining traction.

**Memory as First-Class Infrastructure**: The success of **cognee** (+780) and **claude-mem** (84k) signals that **persistent memory** has become the critical missing piece for production AI agents. The industry is moving beyond stateless LLM calls to stateful agent systems that remember past interactions, compress them, and selectively inject context.

**Chinese Ecosystem Integration**: ollama now supports Kimi, GLM, MiniMax alongside DeepSeek, Qwen — the Chinese LLM ecosystem is becoming globally accessible through standard interfaces.

---

### 4. Community Hot Spots

- 🔥 **cognee** (topoteretes/cognee) — +780 stars today, the most active new repo. It's positioning as "the memory platform for agents" with knowledge graph backing. If you're building stateful agents, this is the project to watch.

- 🚀 **ai-berkshire** (xbtlin/ai-berkshire) — +685 stars, multi-agent value investing. Represents the intersection of two hot trends: financial AI and adversarial multi-agent systems. Its methodology (4 masters + multi-agent debate) is novel.

- ⚡ **opencode** (anomalyco/opencode) — +392 stars, the open-source coding agent. With Claude Code and Codex being proprietary, opencode is the most viable open alternative. Watch for it to become the default in open-source workflows.

- 🎨 **design.md** (google-labs-code/design.md) — +1541 stars, a specification format for design systems to AI agents. This could become the standard for "design-to-code" pipelines, bridging the gap between designers and AI coders.

- 🧠 **claude-mem** (thedotmack/claude-mem) — 84k stars, persistent context across sessions. For anyone building agents, this solves the "cold start" problem — agents remember past sessions, compress them, and inject relevant context automatically.

---

*Report generated 2026-06-28. Data sources: GitHub Trending, GitHub Topic Search API. Focus: AI open-source ecosystem analysis.*

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*