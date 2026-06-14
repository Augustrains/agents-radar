# AI Open Source Trends 2026-06-14

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-14 02:13 UTC

---

# AI Open Source Trends Report — 2026-06-14

## 1. Today's Highlights

The AI open-source ecosystem is experiencing an **explosive surge in agent skill security and optimization tooling**. NVIDIA's *SkillSpector* (+804 stars today) enters the scene as a dedicated security scanner for AI agent skills — reflecting growing community concern about supply-chain risks in agent ecosystems. Meanwhile, *LMCache* (+238 stars) pushes LLM inference performance with a specialized KV cache layer, and the rapid rise of *agent-skills* (+1,514 stars) by Addy Osmani and *superpowers* (+924 stars) signals a new paradigm: the formalization of "agent skills" as a reusable, production-grade engineering primitive. Cross-agent session analytics tools like *agentsview* (+190 stars) are also gaining traction, pointing to an emerging **observability layer for coding agents**.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure
- **[LMCache](https://github.com/LMCache/LMCache)** ⭐ — +238 today  
  A high-performance KV cache layer that supercharges LLM inference throughput and reduces latency for production deployments.

- **[andrewyng/aisuite](https://github.com/andrewyng/aisuite)** ⭐ — +127 today  
  Provides a simple, unified Python interface across multiple generative AI providers — reducing vendor lock-in friction for developers.

- **[swc-project/swc](https://github.com/swc-project/swc)** ⭐ — +20 today  
  While primarily a Rust-based web platform, its compilation speed increasingly powers AI-assisted code generation toolchains.

- **[Picovoice/picollm](https://github.com/Picovoice/picollm)** ⭐312  
  On-device LLM inference engine using X-Bit quantization — enabling private, offline AI on edge devices.

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐82,783  
  High-throughput LLM inference serving engine — the de-facto standard for production deployments.

### 🤖 AI Agents / Workflows
- **[addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)** ⭐ — +1,514 today  
  Production-grade engineering skills for AI coding agents — a curated library turning agent capabilities into modular, tested primitives.

- **[obra/superpowers](https://github.com/obra/superpowers)** ⭐ — +924 today  
  An agentic skills framework + software development methodology that combines agent autonomy with human oversight in a structured workflow.

- **[NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector)** ⭐ — +804 today  
  Security scanner for AI agent skills — detects vulnerabilities, malicious patterns, and security risks before deployment.

- **[kenn-io/agentsview](https://github.com/kenn-io/agentsview)** ⭐ — +190 today  
  Local-first session intelligence and analytics for coding agents — supports Claude Code, Codex, and 20+ agents; 100x faster than ccusage.

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐192,802  
  A growing, agent-architecture framework that adapts to user interactions over time — "the agent that grows with you."

- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐184,931  
  The original autonomous AI agent platform — still a primary reference for multi-step task decomposition.

### 📦 AI Applications
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐47,281  
  AI productivity studio with smart chat, autonomous agents, and 300+ pre-built assistants — unified access to frontier LLMs.

- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐42,424  
  LLM-powered stock analysis for A/H/US markets — integrates multi-source data, LLM decision dashboards, and zero-cost scheduled runs.

- **[OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB)** ⭐69,067  
  Financial data platform designed for analysts, quants, and AI agents — enabling automated financial research pipelines.

- **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)** ⭐85,847  
  Multi-agent LLM financial trading framework — coordinating specialized agents for market analysis, execution, and risk management.

### 🧠 LLMs / Training
- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐174,072  
  Get up and running with local LLMs — now supporting Kimi-K2.6, GLM-5.1, MiniMax, DeepSeek, gpt-oss, Qwen, Gemma, and more.

- **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐161,570  
  The model-definition framework for state-of-the-art ML models — text, vision, audio, and multimodal.

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,082  
  Comprehensive LLM evaluation platform supporting 100+ datasets and models including Llama3, GPT-4, Qwen, GLM.

- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** ⭐4,274  
  Educational course on LLM inference serving for Apple Silicon — build a tiny vLLM + Qwen from scratch.

### 🔍 RAG / Knowledge
- **[Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm)** ⭐61,542  
  "Stop renting your intelligence" — local-first RAG platform turning any document into queryable AI knowledge.

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐82,658  
  Leading open-source RAG engine fusing advanced retrieval with agent capabilities for superior LLM context layers.

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐58,495  
  Universal memory layer for AI agents — enabling persistent, cross-session recall without fine-tuning.

- **[topoteretes/cognee](https://github.com/topoteretes/cognee)** ⭐17,815  
  Open-source AI memory platform using knowledge graphs — gives agents persistent long-term memory across sessions.

- **[StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN)** ⭐11,918  
  [MLsys2026] Achieves 97% storage savings for RAG while running fast, accurate, 100% private RAG on personal devices.

- **[zilliztech/claude-context](https://github.com/zilliztech/claude-context)** ⭐11,839  
  Code search MCP for Claude Code — makes entire codebase the context for any coding agent.

---

## 3. Trend Signal Analysis

### Agent Skills Standardization Is the Dominant Narrative
The most explosive growth today is in the **agent skills** ecosystem. *agent-skills* (+1,514) and *superpowers* (+924) represent a shift from ad-hoc agent prompts to **version-controlled, security-audited, reusable skill libraries**. This mirrors the early DevOps movement where scripts became modules became packages. NVIDIA's *SkillSpector* (+804) confirms this is now a security priority — the first dedicated vulnerability scanner for AI agent skills.

### Observability Becomes Agent Infrastructure
*agentsview* (+190) signals a new category: **coding agent analytics and session intelligence**. As developers run multiple AI coding agents (Claude Code, Codex, Gemini CLI, etc.), the need for cross-agent telemetry and performance metrics is emerging. The emphasis on "local-first" suggests privacy-conscious agent monitoring is a key requirement.

### Memory and Context Systems Deepen
Two parallel memory trends are accelerating: **persistent agent memory** (mem0, cognee) and **codebase-as-context** (claude-context, safishamsi/graphify). Both aim to solve the context-window bottleneck — one via long-term storage, the other via intelligent retrieval. The *graphify* project (⭐66,740) turns code, schemas, and docs into queryable knowledge graphs, representing a hybrid of RAG and agent memory.

### Inference Optimization Continues to Specialize
*LMCache* (+238) focuses specifically on KV cache optimization — a narrow but critical performance bottleneck in LLM serving. This follows the broader trend of **infrastructure tooling becoming more granular**: instead of general "LLM frameworks," we now see dedicated cache layers, security scanners, session analytics, and skill managers.

---

## 4. Community Hot Spots

- **🔐 Agent Skill Security** — *SkillSpector* by NVIDIA: As agent skills become reusable modules, supply-chain security is the next big problem to solve. Developers should track this for tooling that scans skills before deployment.

- **🧩 Cross-Agent Session Analytics** — *agentsview*: With 20+ coding agents in the wild, a unified analytics layer is becoming essential for teams managing agent-driven workflows.

- **📦 Multi-Provider Unified Interfaces** — *aisuite* by Andrew Ng: The trend toward abstraction layers that let teams switch between LLM providers without code changes is accelerating — important for cost optimization and resilience.

- **🏗️ Agent Methodology** — *superpowers*: This project treats agentic development as a formal methodology with defined skills, reviews, and iteration cycles — a potential blueprint for how teams structure AI-augmented software development.

- **🧠 Persistent Memory for Agents** — *mem0* and *cognee*: Solving the "groundhog day" problem where agents forget everything after each session. These are becoming foundational for any production agent system that requires stateful interactions.

---

*Report generated from GitHub trending data (2026-06-14) and AI topic search results. Stars reflect approximate counts at time of analysis.*

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*