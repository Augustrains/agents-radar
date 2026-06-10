# AI Open Source Trends 2026-06-10

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-10 02:03 UTC

---

# AI Open Source Trends Report — 2026-06-10

## 1. Today's Highlights

Three major themes dominate today's AI open-source landscape: **agent skill ecosystems** are exploding, with multiple projects crossing 1,000+ daily stars by packaging reusable capabilities for Claude Code and other coding agents; **local-first AI tooling** is gaining massive traction, as seen in surge of projects that benchmark, optimize, and deploy LLMs on consumer hardware; and **memory & knowledge infrastructure** for agents is maturing rapidly, with new vectorless RAG and persistent context solutions drawing significant community attention. The convergence of agent frameworks with skill marketplaces and memory layers signals a shift from building single agents to ecosystems of composable agent capabilities.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure

| Project | Stars | Description |
|---------|-------|-------------|
| [turbovec](https://github.com/RyanCodrai/turbovec) | +1,801 today | Rust-based vector index with Python bindings, built on TurboQuant — targeting high-performance local embedding search |
| [supervision](https://github.com/roboflow/supervision) | 43k+ total, +733 today | Reusable computer vision tools library; continues steady growth as the go-to CV utility layer |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 82,363 total | High-throughput LLM inference engine; remains the standard for production serving |
| [ollama/ollama](https://github.com/ollama/ollama) | 173,717 total | Local LLM runner, now supporting Kimi-K2.6, GLM-5.1, DeepSeek, and more — the de facto local inference entry point |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 47,134 total | AI productivity studio unifying 300+ LLM assistants with autonomous agents; strong multi-model support |

### 🤖 AI Agents / Workflows

| Project | Stars | Description |
|---------|-------|-------------|
| [aaif-goose/goose](https://github.com/aaif-goose/goose) | +489 today | Extensible AI agent in Rust that goes beyond code suggestions — installs, executes, edits, and tests with any LLM |
| [santifer/career-ops](https://github.com/santifer/career-ops) | +1,110 today, 51,737 total | AI-powered job search system with 14 skill modes, built on Claude Code — demonstrates agent-as-application pattern |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 188,891 total | The "agent that grows with you" — leading open-source agent framework with huge community |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 138,902 total | The agent engineering platform; remains foundational for building LLM-powered workflows |
| [bytedance/deer-flow](https://github.com/bytedance/deer-flow) | 70,832 total | Long-horizon SuperAgent harness with sandboxes, memories, tools, and subagents for complex tasks |
| [langgenius/dify](https://github.com/langgenius/dify) | 144,595 total | Production-ready agentic workflow development platform; strong momentum in enterprise adoption |

### 📦 AI Applications

| Project | Stars | Description |
|---------|-------|-------------|
| [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill) | +3,191 today | AI agent skill that researches topics across Reddit, X, YouTube, HN, Polymarket — synthesizes grounded summaries; **#1 trending** |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | +443 today | Production-grade engineering skills for AI coding agents — curated by Chrome team veteran |
| [phuryn/pm-skills](https://github.com/phuryn/pm-skills) | +806 today | PM Skills Marketplace with 100+ agentic skills for product management workflows |
| [career-ops](https://github.com/santifer/career-ops) | +1,110 today, 51,737 total | AI job search application with PDF generation and batch processing |
| [openai/plugins](https://github.com/openai/plugins) | +284 today | Official OpenAI Plugins repo — resurgence of interest in plugin ecosystem |
| [maziyarpanahi/openmed](https://github.com/maziyarpanahi/openmed) | +191 today | Open-source healthcare AI toolkit |

### 🧠 LLMs / Training

| Project | Stars | Description |
|---------|-------|-------------|
| [huggingface/transformers](https://github.com/huggingface/transformers) | 161,459 total | The standard model-definition framework; continuous updates for new architectures |
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | 72,034 total | Unified fine-tuning for 100+ LLMs and VLMs; essential tool for model customization |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,075 total | LLM evaluation platform supporting 100+ datasets and major models |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | +251 today | Minimal and scalable library for pretraining foundation and world models — early but notable |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4,263 total | Educational LLM inference serving on Apple Silicon; systems engineer's guide |

### 🔍 RAG / Knowledge

| Project | Stars | Description |
|---------|-------|-------------|
| [anything-llm](https://github.com/Mintplex-Labs/anything-llm) | 61,327 total | Local-first agent experience with everything needed for RAG; "stop renting your intelligence" |
| [ragflow](https://github.com/infiniflow/ragflow) | 82,320 total | Leading open-source RAG engine combining cutting-edge RAG with agent capabilities |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 58,205 total | Universal memory layer for AI agents — persistent context across sessions |
| [claude-mem](https://github.com/thedotmack/claude-mem) | 81,494 total | Captures agent sessions, compresses with AI, injects relevant context into future sessions |
| [graphify](https://github.com/safishamsi/graphify) | 64,270 total | Turn code folders, schemas, and docs into queryable knowledge graphs for AI coding agents |
| [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | 81,651 total | Bridge between images/PDFs and LLMs; supports 100+ languages |
| [whichllm](https://github.com/Andyyyy64/whichllm) | +633 today | Find the best local LLM for your hardware with recency-aware benchmarks — one command |

---

## 3. Trend Signal Analysis

**Agent skill ecosystems are experiencing explosive growth.** Today's #1 trending repo (`last30days-skill`) gained 3,191 stars in a single day by packaging a focused research agent skill. It's part of a broader pattern: `pm-skills` (+806), `agent-skills` (+443), and the resurgence of `openai/plugins` (+284) all point to a market forming around **composable, reusable agent capabilities**. The success of `career-ops` (+1,110 today, 51,737 total) demonstrates that full application-level agents are also resonating when they solve concrete user problems.

**Local-first AI tooling is surging.** `turbovec` (+1,801) provides high-performance vector indexing in Rust with Python bindings — optimized for local deployment. `whichllm` (+633) solves the practical problem of finding the best LLM for your specific hardware. This aligns with the continued dominance of `ollama` (173k stars) and the "own your intelligence" messaging from `anything-llm`. The community is actively seeking tools that reduce dependency on cloud APIs.

**Memory and persistence for agents is becoming infrastructure.** Projects like `mem0` (58k stars), `claude-mem` (81k stars), and `cognee` (17k stars) are building the "long-term memory" layer for AI agents. Notably, `graphify` (64k stars) turns any codebase into a queryable knowledge graph — a concrete bridge between RAG and agent workflows. The emergence of `VectifyAI/PageIndex` (32k stars) for "vectorless, reasoning-based RAG" suggests the community is exploring alternatives to pure vector search for retrieval.

**Rust is gaining as an AI infrastructure language.** Beyond `turbovec`, the `rig` framework (7.5k stars) for modular LLM applications and `qonqr` for vector databases point to Rust's growing role in performance-critical AI tooling, complementing Python's dominance in model development.

---

## 4. Community Hot Spots

- **🔗 [last30days-skill](https://github.com/mvanhorn/last30days-skill)** — The #1 trending repo demonstrates that focused, single-purpose agent skills (not just frameworks) can achieve viral adoption. Expect a wave of similar "agent skill" projects.

- **🔗 [turbovec](https://github.com/RyanCodrai/turbovec)** — Rust-based vector indexing with Python bindings is a pattern we'll see more of: high-performance infrastructure wrapped in Python-friendly APIs for local-first AI.

- **🔗 [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)** — Production-grade engineering skills from a Chrome team veteran. Signals that even browser/infrastructure engineers are building for the agent ecosystem.

- **🔗 [claude-mem](https://github.com/thedotmack/claude-mem)** — 81k stars for persistent agent context across sessions. Memory/infrastructure for agents is becoming a must-have category; this project shows the demand.

- **🔗 [whichllm](https://github.com/Andyyyy64/whichllm)** — As local LLM adoption grows, benchmarking tools that consider real performance (not just parameter count) will be essential infrastructure. This fills that gap with zero friction.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*