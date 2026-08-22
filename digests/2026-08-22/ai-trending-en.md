# AI Open Source Trends 2026-08-22

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-08-22 00:29 UTC

---

# AI Open Source Trends Report — 2026-08-22

## 1. Today's Highlights

The AI open-source ecosystem today is dominated by a surge in **agent skill/harness frameworks** — lightweight, local-first systems that augment AI coding agents (Claude Code, Codex, Cursor) with memory, skills, and security layers. Notably, `mattpocock/skills` and `obra/superpowers` are both trending heavily, signaling a shift toward reusable, methodology-driven agent skill packs as a new distribution format. At the same time, **Apache Maka** (Incubating) has entered the scene as a local-first AI agent workspace with append-only logging, reflecting growing demand for observable, auditable agent behavior. The trend also continues toward **self-hosted, privacy-first AI infrastructure**, with vector databases and memory layers (Milvus, Qdrant, Cognee, Mem0) maintaining strong community momentum. Finally, **Rust** is making inroads as a viable language for AI tooling, seen in `AprilNEA/OpenLogi` and `CodeWhale`.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure (Frameworks, SDKs, Inference, Dev Tools)

- **[modular/modular](https://github.com/modular/modular)** — ⭐0 (+913 today) — The Modular Platform (MAX & Mojo) for high-performance AI compute; gaining traction as a Mojo-based alternative stack.
- **[microsoft/onnxruntime](https://github.com/microsoft/onnxruntime)** — ⭐0 (+5 today) — Cross-platform ML inference accelerator; steady background relevance for production deployment.
- **[cursor/plugins](https://github.com/cursor/plugins)** — ⭐0 (+388 today) — Official plugin specification for Cursor, standardizing how AI agents extend IDE capabilities.
- **[PostHog/posthog](https://github.com/PostHog/posthog)** — ⭐0 (+335 today) — AI observability and analytics for self-driving products; increasingly relevant as agent telemetry demand grows.
- **[Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale)** — ⭐40,835 (topic:ai-agent) — Open-source Rust-based coding agent for the terminal; community-driven with active PRs.

### 🤖 AI Agents / Workflows

- **[mattpocock/skills](https://github.com/mattpocock/skills)** — ⭐0 (+3362 today) — Agent skills from a `.agents` directory; today's top trending repo, showcasing the "skill pack" pattern.
- **[obra/superpowers](https://github.com/obra/superpowers)** — ⭐0 (+790 today) — An agentic skills framework & development methodology; complementary to `skills`, emphasizing workflow discipline.
- **[affaan-m/ECC](https://github.com/affaan-m/ECC)** — ⭐0 (+357 today) — Agent harness performance optimization (skills, memory, security) for Claude Code, Codex, Cursor.
- **[ruvnet/ruflo](https://github.com/ruvnet/ruflo)** — ⭐0 (+140 today) — Multi-agent meta-harness for swarms, adaptive memory, self-learning, RAG; supports multiple agent CLIs.
- **[apache/maka](https://github.com/apache/maka)** — ⭐0 (+148 today) — Local-first AI agent workspace with append-only logs; new Apache incubator project worth watching.
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** — ⭐233,995 (topic:ai-agent) — "The agent that grows with you"; high-star foundation model agent from Nous Research.
- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** — ⭐186,727 (topic:llm) — The original autonomous agent vision; still central to the agent ecosystem.

### 📦 AI Applications (Vertical Solutions)

- **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** — ⭐0 (+1201 today) — AI-driven HD short video generation from keywords via automated workflows; strong consumer-facing growth.
- **[santifer/career-ops](https://github.com/santifer/career-ops)** — ⭐0 (+921 today) — Open-source AI job search: scrapes portals, scores listings A–F, tailors CVs, runs locally in agent CLIs.
- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** — ⭐63,580 (topic:ai-agent) — LLM-driven multi-market stock analysis with dashboards and automated notifications.
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** — ⭐48,476 (topic:ai-agent) — AI generates native PowerPoint decks with charts, transitions, and audio narration from any document.
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** — ⭐50,886 (topic:ai-agent) — AI productivity studio with 300+ assistants and unified access to frontier LLMs.

### 🧠 LLMs / Training

- **[jingyaogong/minimind](https://github.com/jingyaogong/minimind)** — ⭐54,913 (topic:llm-model) — Train a 64M-parameter LLM from scratch in 2 hours; accessible entry for model training education.
- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** — ⭐4,512 (topic:llm-model) — Learn LLM inference on Apple Silicon by building a tiny vLLM + Qwen; systems-engineering angle.
- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** — ⭐7,325 (topic:llm-model) — LLM evaluation platform supporting 100+ datasets; key for model benchmarking.
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** — ⭐233,995 (topic:ai-agent) — Agent paradigm built on top of Hermes models; dual-infrastructure role.

### 🔍 RAG / Knowledge

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** — ⭐88,999 (topic:rag) — Leading open-source RAG engine that fuses RAG with agent capabilities.
- **[Qdrant/qdrant](https://github.com/qdrant/qdrant)** — ⭐34,117 (topic:vector-db) — High-performance vector database, now a core memory layer in agent stacks.
- **[topoteretes/cognee](https://github.com/topoteretes/cognee)** — ⭐30,173 (topic:vector-db) — Self-hosted AI memory platform with knowledge graph engine for persistent agent memory.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** — ⭐63,772 (topic:rag) — Universal memory layer for AI agents; cross-session context retention.
- **[VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex)** — ⭐35,284 (topic:vector-db) — Vector-less, reasoning-based document indexing for RAG; novel approach.
- **[Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify)** — ⭐109,262 (topic:llm) — Turn codebases into queryable knowledge graphs via local AST parsing; no vector store needed.

---

## 3. Trend Signal Analysis

The most explosive community attention today is on **agent skill packs and harnesses**. The simultaneous rise of `skills` (+3,362 stars) and `superpowers` (+790) signals a new distribution layer for AI coding agents — reusable, versioned skill sets that ship as directories (`.agents/`) and are consumed by tools like Claude Code and Cursor. This is a notable shift from "build an agent from scratch" to "compose agent behavior from skill libraries."

Also emerging: **agent memory and observability as first-class concerns**. Projects like `apache/maka` (append-only logs), `mem0`, and `cognee` reflect a maturing ecosystem where agent trust, auditability, and long-term memory are becoming mandatory infrastructure. PostHog's AI observability pivot reinforces this.

**New tech stacks**: Rust continues its quiet invasion of AI tooling (AprilNEA/OpenLogi, CodeWhale, qdrant, lancedb, rig). Apache Maka's incubation could normalize "agent workspaces" as a distinct product category.

**Industry connections**: The focus on local-first, no-telemetry tools (OpenLogi, career-ops) aligns with growing privacy sentiment post-Cloudflare/AI-regulation debates. The sheer volume of `.agents`-compatible skills suggests agent CLIs are converging on a common skill spec — possibly foreshadowing an open standard.

---

## 4. Community Hot Spots

- **[mattpocock/skills](https://github.com/mattpocock/skills)** — The #1 trending repo today; a must-watch for anyone building or consuming agent skills. The `.agents` directory pattern is quickly becoming a convention.
- **[apache/maka](https://github.com/apache/maka)** — Apache incubator project; local-first agent workspace with append-only logging. Worth tracking for governance and compliance use cases.
- **[santifer/career-ops](https://github.com/santifer/career-ops)** — Applied AI that resonates broadly (job search automation). Demonstrates how agent CLIs + structured rubrics can power vertical apps.
- **[VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex)** — A creative RAG variant (vectorless, reasoning-based indexing) that challenges the vector DB orthodoxy. High potential if efficiency claims hold up.
- **[ruvnet/ruflo](https://github.com/ruvnet/ruflo)** — Early-stage multi-agent meta-harness with self-learning claims; community is hungry for robust swarm orchestration outside research labs.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*