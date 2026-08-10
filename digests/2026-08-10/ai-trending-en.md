# AI Open Source Trends 2026-08-10

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-08-10 00:45 UTC

---

# AI Open Source Trends Report — 2026-08-10

---

## 1. Today's Highlights

Today's trending data reveals a clear **explosion of "Agent Skills"** — a new abstraction layer for equipping AI coding agents with reusable, production-grade capabilities. Google's official `skills` repository and Addy Osmani's `agent-skills` both entered today's trending list with strong early adoption (528 and 680 stars today respectively), signaling platform-level commitment to this pattern. Meanwhile, **self-improving coding agents** are gaining serious traction: PrimeIntellect's `prime-agent` (an RLM agent) surged with 2,356 stars today, making it the single most-starred trending repository. The **evaluation of agent capabilities** is also emerging as a hotspot, with Harvey's legal-LLM benchmark (`harvey-labs`) and Google DeepMind's `weathernext` (physical-science AI) demonstrating a broadening of agentic AI beyond coding into professional verticals. Interestingly, **knowledge-graph-based RAG** continues to challenge the vector-database paradigm, with projects like `code-graph-rag` and Graphify Labs' `graphify` (104k stars) pushing deterministic, structure-aware retrieval.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure

- [affaan-m/ECC](https://github.com/affaan-m/ECC) — ⭐239,028 | The agent harness performance optimization system; systems-level work for skills, instincts, memory, and security across agent CLIs.  *(Active in topic search for llm)*
- [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) — ⭐164,200 | Web context API for AI agents to search, scrape, and interact with web pages at scale.
- [ollama/ollama](https://github.com/ollama/ollama) — ⭐178,139 | The de-facto local LLM runner; now supporting Kimi-K2.6, GLM-5.2, DeepSeek, and more.
- [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) — ⭐65,653 | Token compression proxy/MCP for coding agents; 20% fewer tokens for code, 60–95% fewer for JSON.
- [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) — ⭐8,220 | Modular Rust LLM application framework; the strongest Rust-native agent infrastructure option.
- [Elastic/elasticsearch](https://github.com/elastic/elasticsearch) — ⭐73,404 (stars from the ML topic context) — Notable in the ML topic dataset for vector search, though not a new entry today.

### 🤖 AI Agents / Workflows

- [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) — ⭐186,462 | The seminal general-purpose agent framework; still the benchmark name in autonomous workflows.
- [langchain-ai/langchain](https://github.com/langchain-ai/langchain) — ⭐143,811 | The agent engineering platform; now the anchor for agent/RAG orchestration in Python and JS.
- [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) — ⭐39,313 | Resilient agent-state machines; the graph-based execution layer for production agents.
- [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) — ⭐227,936 | "The agent that grows with you" — a self-evolving agent framework from Nous Research.
- [browser-use/browser-use](https://github.com/browser-use/browser-use) — ⭐108,484 | Makes websites accessible to AI agents; critical infrastructure for web automation agents.
- [HKUDS/nanobot](https://github.com/HKUDS/nanobot) — ⭐46,794 | Ultra-lightweight, self-hosted personal AI agent framework with WebUI, tools, memory, MCP, and multi-agent workflows.
- [PrimeIntellect-ai/prime-agent](https://github.com/PrimeIntellect-ai/prime-agent) — ⭐0 (+2,356 today) | **Trending highlight**: A self-improving RLM (Reinforcement Learning from Machines) agent for coding workflows and long-running autonomous tasks. The fastest-growing repo today.
- [pcingola/SwarmDebug](https://github.com/pcingola/SwarmDebug) — ⭐113 (from community signal) | Orchestrates autonomous debugging as a swarm.

### 📦 AI Applications

- [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) — ⭐102,335 | Generates 1080p short videos from a keyword/topic via LLM pipelines and automations.
- [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) — ⭐61,187 (+306 today) | LLM-driven multi-market stock analysis with multi-source market data, news, decision dashboards, and automated notifications.
- [Comfy-Org/ComfyUI](https://github.com/Comfy-Org/ComfyUI) — ⭐(+365 today) | The most modular diffusion-model GUI and backend; the standard for node-based image/video workflows.
- [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) — ⭐50,181 | AI productivity studio with smart chat, autonomous agents, and 300+ assistants unifying frontier LLM access.
- [DeepWiki/deepwiki-anything](https://github.com/DeepWiki/deepwiki-anything) — ⭐532 | Auto-generates documentation for any public GitHub repo.
- [harveyai/harvey-labs](https://github.com/harveyai/harvey-labs) — ⭐(+47 today) | **Trending**: A benchmark for evaluating and improving agent capabilities for legal work; a signal of AI agents moving into professional-service verticals.
- [google-deepmind/weathernext](https://github.com/google-deepmind/weathernext) — ⭐(+86 today) | **Trending**: DeepMind's weather modeling (likely diffusion/ML-based), applying AI to physical-science prediction at scale.
- [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) — ⭐44,095 | AI converts documents into native PowerPoint decks with shapes, charts, transitions, and audio narration.

### 🧠 LLMs / Training

- [huggingface/transformers](https://github.com/huggingface/transformers) — ⭐163,505 | The model-definition framework powering the open-source ML ecosystem.
- [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) — ⭐102,049 | Step-by-step ChatGPT-like LLM implementation from scratch in PyTorch.
- [jingyaogong/minimind](https://github.com/jingyaogong/minimind) — ⭐54,498 | Train a 64M-parameter LLM from scratch in 2 hours; essential for understanding training from the ground up.
- [esengine/DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix) — ⭐33,442 | DeepSeek-native coding agent for the terminal, engineered around prefix-cache stability.
- [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) — ⭐4,456 | Build a tiny vLLM + Qwen to learn LLM inference on Apple Silicon for systems engineers.
- [open-compass/opencompass](https://github.com/open-compass/opencompass) — ⭐7,287 | Open-source evaluation platform for LLMs across 100+ datasets.
- [picollm](https://github.com/Picovoice/picollm) — ⭐316 | On-device LLM inference powered by X-bit quantization (edge deployment focus).

### 🔍 RAG / Knowledge

- [infiniflow/ragflow](https://github.com/infiniflow/ragflow) — ⭐87,125 | Leading open-source RAG engine fusing RAG with agent capabilities for a superior LLM context layer.
- [Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) — ⭐131,758 | 100+ AI agents, agent skills, and RAG apps — free and open source.
- [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) — ⭐90,216 | Persistent context across sessions for every agent; compresses and injects relevant memory back into future sessions.
- [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) — ⭐104,620 | Deterministic AST-based knowledge graphs from any codebase; no vector store, every edge explained.
- [vitali87/code-graph-rag](https://github.com/vitali87/code-graph-rag) — ⭐(+96 today) | **Trending**: "The ultimate RAG for your monorepo" — knowledge graphs over multi-language codebases.
- [milvus-io/milvus](https://github.com/milvus-io/milvus) — ⭐45,573 | Cloud-native vector database for scalable ANN search; backbone of production RAG.
- [qdrant/qdrant](https://github.com/qdrant/qdrant) — ⭐33,889 | High-performance vector database and search engine for next-gen AI applications.
- [topoteretes/cognee](https://github.com/topoteretes/cognee) — ⭐29,892 | Open-source AI memory platform (knowledge-graph engine) for persistent agent memory.

---

## 3. Trend Signal Analysis

The strongest signal today is the **emergence of "Agent Skills" as a formal ecosystem layer**. Google's `skills` repo and Addy Osmani's `agent-skills` (both trending with +528 and +680 stars today) confirm that skills — portable, declarative capability packages injected into coding agents — are becoming the standard unit of agent augmentation. This has implications: the future of agent capability is less about the agent core and more about the skill ecosystem surrounding it.

Second, **self-improving and RL-trained agents** are gaining serious momentum: PrimeIntellect's `prime-agent` (+2,356 today) is the most-starred trending repository, and NousResearch's `hermes-agent` (227k stars) continues to demonstrate the appetite for agents that grow and learn from usage.

Third, there is an accelerating shift toward **knowledge-graph-based RAG over vector databases**. Projects like `code-graph-rag` and `graphify` offer deterministic, structure-aware retrieval — a direct answer to the hallucination and "surface-level" retrieval limits of pure vector search. Expect further convergence of GQL and LLM contexts.

Fourth, **agent evaluation** is a rising subcategory: Harvey's `harvey-labs` benchmark, OpenCompass, and even legal-LLM work signal a maturation of the Agent Era — from "build it" to "prove it works and measure it."

Finally, the **"local-first" model continues to dominate**: Ollama now supports Kimi-K2.6, GLM-5.2, and MiniMax by default, and self-hosted agent frameworks like `nanobot`, `anything-llm`, and `claude-mem` reinforce the trend toward privacy-friendly, memory-preserving, offline-capable AI stacks.

---

## 4. Community Hot Spots

- **[Agent Skills ecosystem](https://github.com/google/skills) + [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)** — If Google and the V8 performance lead are both building skill packs for coding agents, this is the new reality. The "skill" is the new "plugin."
- **[Graph-based RAG: Graphify](https://github.com/Graphify-Labs/graphify) + [code-graph-rag](https://github.com/vitali87/code-graph-rag)** — Deterministic, explainable retrieval over massive monorepos. For engineering teams, this may become the preferred retrieval layer over vector DBs.
- **[Self-improving agents: PrimeIntellect/prime-agent](https://github.com/PrimeIntellect-ai/prime-agent) + [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** — The idea of agents that train themselves during use is catalyzing serious developer mindshare and venture attention.
- **[Agent memory: claude-mem](https://github.com/thedotmack/claude-mem) + [mem0ai/mem0](https://github.com/mem0ai/mem0)** — Persistent, injectable context is the missing piece for production agents; both are in the top RAG/Agent conversation today.
- **[Agent benchmarking: harvey-labs](https://github.com/harveyai/harvey-labs) + [open-compass](https://github.com/open-compass/opencompass)** — As agents move into legal, stock, video, and beyond, measurement and accountability become essential for enterprise adoption.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*