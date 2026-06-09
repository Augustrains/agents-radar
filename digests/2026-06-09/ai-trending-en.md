# AI Open Source Trends 2026-06-09

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-09 01:52 UTC

---

# AI Open Source Trends Report — 2026-06-09

## 1. Today's Highlights

Today marks a clear **agentic explosion** across the open-source ecosystem, with **skill-based AI agents** dominating the trending list. Three of the top four trending repos are agent skill frameworks: `mvanhorn/last30days-skill` (3,558 stars today), `Panniantong/Agent-Reach` (679), and `phuryn/pm-skills` (164). Google's official entry into this space with `google/skills` (461 stars) signals enterprise validation of the "skill-as-a-plugin" paradigm. The Rust–Python hybrid vector store `turbovec` (1,729 stars) also emerged, showing growing appetite for performance-optimized vector infrastructure.

## 2. Top Projects by Category

### 🔧 AI Infrastructure (Frameworks, SDKs, Inference Engines, Dev Tools)

- **[turbovec](https://github.com/RyanCodrai/turbovec)** ⭐0 (+1,729 today) — Rust-native vector index with Python bindings, leveraging TurboQuant for high-performance nearest-neighbor search.
- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐82,255 — High-throughput LLM inference engine, now the standard for production-grade serving.
- **[samchon/nestia](https://github.com/samchon/nestia)** ⭐2,160 — NestJS helper library enabling AI chatbot development with TypeScript.
- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐173,628 — Local LLM runner supporting Kimi, GLM, DeepSeek, Qwen, and many models.

### 🤖 AI Agents / Workflows (Agent Frameworks, Automation, Multi-Agent Systems)

- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** ⭐0 (+3,558 today) — Autonomous agent skill that researches topics across Reddit, X, YouTube, HN, Polymarket, and synthesizes grounded summaries.
- **[Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach)** ⭐0 (+679 today) — CLI tool giving agents visual access to Twitter, Reddit, YouTube, GitHub, Bilibili, and XiaoHongShu with zero API fees.
- **[google/skills](https://github.com/google/skills)** ⭐0 (+461 today) — Official Google agent skills framework for Google products and technologies.
- **[CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)** ⭐34,162 (+378 today) — Frontend stack for building agents & generative UI across React, Angular, Mobile, Slack.
- **[aaif-goose/goose](https://github.com/aaif-goose/goose)** ⭐0 (+699 today) — Open-source extensible AI agent that installs, executes, edits, and tests with any LLM.
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐187,468 — The "agent that grows with you," a popular autonomous agent framework.
- **[bytedance/deer-flow](https://github.com/bytedance/deer-flow)** ⭐70,755 — Long-horizon SuperAgent harness for coding, research, and automated workflows.
- **[ShareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code)** ⭐65,473 — Nano agent harness built from scratch to teach Claude Code fundamentals.

### 📦 AI Applications (Specific Apps, Vertical Solutions)

- **[santifer/career-ops](https://github.com/santifer/career-ops)** ⭐50,567 (+308 today) — AI-powered job search system with 14 skill modes, Go dashboard, and PDF batch processing.
- **[phuryn/pm-skills](https://github.com/phuryn/pm-skills)** ⭐0 (+164 today) — Marketplace of 100+ agentic skills for product management: discovery, strategy, execution, launch, growth.
- **[danielmiessler/Personal_AI_Infrastructure](https://github.com/danielmiessler/Personal_AI_Infrastructure)** ⭐0 (+62 today) — Agentic AI infrastructure designed to augment human capabilities.
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐47,078 — AI productivity studio with 300+ assistants, autonomous agents, and unified LLM access.
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐25,305 — AI generates editable PowerPoints from any document with native shapes and audio narration.

### 🧠 LLMs / Training (Model Weights, Training Frameworks, Fine-Tuning Tools)

- **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)** ⭐72,002 — Unified efficient fine-tuning for 100+ LLMs and VLMs (ACL 2024).
- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** ⭐4,258 — Educational course on building LLM inference serving from scratch for Apple Silicon.
- **[Andyyyy64/whichllm](https://github.com/Andyyyy64/whichllm)** ⭐0 (+143 today) — One-command tool finding the best local LLM for your hardware, ranked by recency-aware benchmarks.
- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐251 — Minimal, scalable library for pretraining foundation and world models.

### 🔍 RAG / Knowledge (Vector Databases, Retrieval-Augmented Generation, Knowledge Management)

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐82,225 — Leading open-source RAG engine combining cutting-edge retrieval with agent capabilities.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐58,080 — Universal memory layer for AI agents, enabling persistent context across sessions.
- **[MemPalace/mempalace](https://github.com/MemPalace/mempalace)** ⭐0 (+170 today) — Best-benchmarked open-source AI memory system.
- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** ⭐81,310 — Persistent context across sessions for every agent, compressing session data and injecting relevant context.
- **[StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN)** ⭐11,894 — [MLsys2026] 97% storage savings for private, on-device RAG applications.
- **[lancedb/lancedb](https://github.com/lancedb/lancedb)** ⭐10,538 — Developer-friendly embedded retrieval library for multimodal AI.
- **[microsoft/synthetic-rag-index](https://github.com/microsoft/synthetic-rag-index)** ⭐37 — Service to import data and index into AI Search, reducing data size by 90%+ for RAG scenarios.

## 3. Trend Signal Analysis

### Agent Skills Market Is Exploding
The single strongest signal today is the **commoditization of agent "skills"** as modular, reusable plugins. `last30days-skill` (3,558 stars today) demonstrates that the community craves pre-built, domain-specific capabilities—research synthesis, social media scraping, job search automation—rather than building from scratch. Google's official `skills` repo validates this as a platform play.

### Rust–Python Hybrids Gain Traction
`turbovec` (1,729 stars today) continues a trend of writing performance-critical AI infrastructure in Rust while exposing Python bindings. This mirrors the success of `lancedb` and `qdrant` in vector search, and signals that developers want **fast, memory-safe backends** with convenient Python APIs.

### Memory and Context Persistence Are the New Frontier
Three of the top topic-search repos by star count (`claude-mem`, `mem0`, `mempalace`) focus on giving agents long-term, persistent memory. This addresses a fundamental limitation of current LLMs: stateless, context-window-limited interactions. The ecosystem is converging on **memory as a first-class infrastructure layer**.

### Personal AI Infrastructure Emerges as a Category
`danielmiessler/Personal_AI_Infrastructure` and `CherryHQ/cherry-studio` represent a new wave: individuals setting up their own **self-hosted, agentic AI stacks**. This parallels the 2024 "local-first" movement but adds autonomous agent orchestration on top.

### Connection to Industry Events
The surge in agent skills coincides with Claude Code's growing ecosystem (`claude-howto` at 312 stars today) and Anthropic's MCP protocol adoption. The "learn-claude-code" repo (65,473 stars) and `claude-mem` (81,310) indicate that Claude's developer tools have become a major platform for building and distributing agent capabilities.

## 4. Community Hot Spots

- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** — The #1 trending repo today. Watch for "skill-as-a-service" becoming a distribution model for AI agent capabilities. Builders should explore skill composition patterns.

- **[turbovec](https://github.com/RyanCodrai/turbovec)** — Rust-powered vector indexing with Python bindings. Worth watching for developers needing high-throughput, low-latency vector search without abandoning the Python ecosystem.

- **[claude-mem](https://github.com/thedotmack/claude-mem)** (81,310 stars) — Persistent context across sessions for any agent. The memory layer is becoming as essential as the LLM itself for production agents.

- **[StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN)** — 97% storage savings for private RAG. Critical for edge deployments and organizations with strict data residency requirements.

- **[CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)** — AG-UI Protocol for embedding agents into any frontend. As agents move from CLI to UI, this pattern will define how users interact with AI in everyday applications.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*