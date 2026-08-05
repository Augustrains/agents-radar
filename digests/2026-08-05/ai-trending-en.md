# AI Open Source Trends 2026-08-05

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-08-05 01:18 UTC

---

# AI Open Source Trends Report — 2026-08-05

---

## 1. Today's Highlights

Today's AI open-source landscape is dominated by **AI agent memory and skills infrastructure** — from TencentDB's team-level memory hub for agents to the explosive rise of `reverse-skill` bringing structured security research skills to AI coding clients. Meanwhile, **PDF intelligence** is emerging as a hot niche, with Firecrawl's Rust-based PDF inspector gaining 2,540 stars in a day for its smart routing between scanned and text-based documents. The agent ecosystem continues to consolidate around **skill/memory architectures**, with projects like `superpowers`, `claude-mem`, and `thedotmack` reinforcing persistent context and reusable capability layers. We also see **edge inference and efficiency** remaining critical — AirLLM's single-4GB-GPU 70B inference gained 1,711 stars, underscoring demand for democratized LLM deployment. Notably, **security for AI agents** (Uber's ADR) and **compound engineering plugins** (EveryInc) signal the maturation of enterprise AI agent governance.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure

| Project | Stars | Today | Why It Matters |
|---|---|---|---|
| [firecrawl/pdf-inspector](https://github.com/firecrawl/pdf-inspector) | 0 | ▲2,540 | Rust-based PDF intelligence engine for detecting scanned vs. text-based PDFs, enabling smarter RAG routing |
| [lyogavin/airllm](https://github.com/lyogavin/airllm) | 0 | ▲1,711 | 70B LLM inference on a single 4GB GPU — democratizing large-model deployment |
| [esengine/DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix) | 30.8k | ▲922 | DeepSeek-native terminal coding agent with prefix-cache stability for long-running sessions |
| [livekit/agents](https://github.com/livekit/agents) | 0 | ▲432 | Framework for building realtime voice AI agents with audio/video support |
| [obra/superpowers](https://github.com/obra/superpowers) | 0 | ▲653 | Agentic skills framework and software development methodology — a structured approach to agent capabilities |
| [browser-use/video-use](https://github.com/browser-use/video-use) | 0 | ▲320 | Edit videos programmatically with coding agents — merging video tooling with agent workflows |

### 🤖 AI Agents / Workflows

| Project | Stars | Today | Why It Matters |
|---|---|---|---|
| [zhaoxuya520/reverse-skill](https://github.com/zhaoxuya520/reverse-skill) | 0 | ▲2,297 | AI-powered skill router for security research — auto-routing, toolchain bootstrapping, self-evolving knowledge base for Claude Code, Cursor, Cline |
| [TencentCloud/TencentDB-Agent-Memory](https://github.com/TencentCloud/TencentDB-Agent-Memory) | 0 | ▲1,111 | Team-level memory hub converting conversations/docs/code into governed, reusable agent memory assets |
| [EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin) | 0 | ▲40 | Official Compound Engineering plugin for Claude Code, Codex, Cursor — codifying cross-agent workflows |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | 237.7k | — | Agent harness performance optimization: skills, instincts, memory, security for multiple AI coding CLIs |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 225.5k | — | "The agent that grows with you" — adaptive personal AI agent framework |
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | 66.5k | — | Give AI agents eyes to the entire internet — read/search Twitter, Reddit, YouTube, GitHub with zero API fees |

### 📦 AI Applications

| Project | Stars | Today | Why It Matters |
|---|---|---|---|
| [uber/ADR](https://github.com/uber/ADR) | 0 | ▲148 | Uber's AI agent security: observability, security benchmarking, threat detection — enterprise-grade agent governance |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 49.4k | — | AI productivity studio with 300+ assistants and unified frontier LLM access |
| [zhayujie/CowAgent](https://github.com/zhayujie/CowAgent) | 46.3k | — | Open-source super AI assistant & agent harness with multi-model, multi-channel support |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 43.0k | — | AI turns documents into native PowerPoint decks with animations, charts, and narration |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | 60.1k | — | LLM-powered multi-market stock analysis with dashboards and automated notifications |
| [googleworkspace/cli](https://github.com/googleworkspace/cli) | 30.2k | — | Google Workspace CLI with AI agent skills — drive, Gmail, Calendar via one tool |

### 🧠 LLMs / Training

| Project | Stars | Today | Why It Matters |
|---|---|---|---|
| [microsoft/generative-ai-for-beginners](https://github.com/microsoft/generative-ai-for-beginners) | 0 | ▲783 | 21-lesson generative AI course — the go-to educational resource tracking latest practices |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 88.2k | — | High-throughput LLM inference & serving engine — the industry standard |
| [ollama/ollama](https://github.com/ollama/ollama) | 177.8k | — | Get up and running with Kimi-K2.6, GLM-5.2, MiniMax, DeepSeek, gpt-oss, Qwen, Gemma — includes latest model releases |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7.3k | — | Comprehensive LLM evaluation platform across 100+ datasets |
| [AarambhDevHub/aarambh-studio](https://github.com/AarambhDevHub/aarambh-studio) | 62 | — | Decoder-only LLM built from scratch in pure Rust using Candle — Gated DeltaNet + sparse attention, fine-grained MoE |

### 🔍 RAG / Knowledge

| Project | Stars | Today | Why It Matters |
|---|---|---|---|
| [cognee](https://github.com/topoteretes/cognee) | 29.8k | — | Open-source AI memory platform — self-hosted knowledge graph engine for persistent agent memory |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | 12.8k | — | RAG on everything with 97% storage savings — private, fast, accurate on personal devices |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 102.5k | — | Turn codebases/docs/schemas into queryable knowledge graphs — deterministic AST parsing, no vector store |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 89.6k | — | Persistent context across sessions for every agent — captures, compresses, and injects relevant context |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 62.5k | — | Universal memory layer for AI agents |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 86.8k | — | Leading open-source RAG engine fusing retrieval with agent capabilities |
| [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) | 64.8k | — | Compress tool outputs and RAG chunks 60-95% before reaching LLM — same answers, fewer tokens |
| [VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex) | 35.0k | — | Vectorless, reasoning-based RAG document indexing |

---

## 3. Trend Signal Analysis

**Agent memory and skills infrastructure** is receiving explosive community attention — TencentDB's Agent-Memory (▲1,111 today) and `reverse-skill` (▲2,297 today) represent a shift from building agents to **equipping and governing them**. The pattern is clear: as agent frameworks mature, the battleground moves to persistent memory, reusable skills, and security/observability.

**Security for AI agents is becoming first-class** — Uber's ADR deployment demonstrates that enterprise AI adoption requires dedicated threat detection and security benchmarking. This is a new category that didn't exist at this scale a year ago.

**PDF et al. document intelligence via Rust** is a fresh technical direction — Firecrawl's pdf-inspector shows specialized media intelligibility gaining momentum, likely feeding into more intelligent RAG pipelines.

**Edge inference efficiency** continues its pull — AirLLM's single-4GB-GPU 70B inference (▲1,711) signals persistent demand for democratized LLM deployment, likely amplified by recent quantized model releases from Kimi, GLM, and DeepSeek mentioned in Ollama's model list update.

**The "skill" ecosystem is consolidating around coding CLI agents** — Claude Code, Codex, Cursor, Cline compatibility is now table stakes for new agent tooling (reverse-skill, superpowers, compound-engineering-plugin, ECC, caveman). This mirrors the MCP protocol's standardization push but at the skills/capability layer.

**Compiler-level agent performance** (ECC's "agent harness performance optimization," headroom's 60-95% token compression) points to a maturing focus on token economics — as LLM costs accumulate in production, tooling for token reduction becomes critical infrastructure.

---

## 4. Community Hot Spots

- **`reverse-skill`** — Security research skill router pack for AI coding clients; ▲2,297/day shows massive demand for domain-specialized agent skills
- **Memory layer wars** — `claude-mem` (89.6k★), `cognee`, `mem0`, and TencentDB's Agent-Memory all competing for the "agent memory" standard; expect consolidation
- **Rust-powered AI tooling** — Firecrawl's pdf-inspector and AarambhDevHub's pure-Rust LLM signal growing Rust adoption in AI infrastructure for performance-critical paths
- **GraphRAG without vectors** — Graphify's 102.5k★ for deterministic AST-based knowledge graphs challenges vector-database hegemony, especially for code intelligence
- **Agent security/observability** — Uber's ADR at only ▲148 today but with enterprise backing signals a gap most OSS projects haven't addressed yet — early movers will win this space

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*