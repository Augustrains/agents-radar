# AI Open Source Trends 2026-08-14

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-08-14 00:54 UTC

---

# AI Open Source Trends Report — 2026-08-14

---

## 1. Today's Highlights

Today's trending list reveals a decisive pivot toward **agent-native infrastructure**: the #1 trending repo is a diagram/design system purpose-built for Claude Code, while Anthropics officially opened its **Agent Skills** repository (anthropics/skills), signaling that "skills" — modular, installable agent capabilities — are becoming the new package format for the AI ecosystem. On the compute edge, **cactus-compute/needle** (a 14MB foundation model for tiny devices) demonstrates that on-device AI is moving from wearables to smart home and robotics. Unsloth's new local UI for training LLMs and diffusion models, plus NVIDIA's **Switchyard** for cross-provider model routing, both point to a maturing "model ops" layer. Finally, **macro-inc/macro** (+1,239 today) shows that AI memory is now being embedded directly into collaborative workspaces, not just chatbot UIs.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure

| Project | Stars (Total / Today) | Why it matters |
|---|---|---|
| [unslothai/unsloth](https://github.com/unslothai/unsloth) | — / +328 | Local UI to run and train LLMs and diffusion models; brings Qwen3.8, Kimi K3, DeepSeek-V4, FLUX to consumer GPUs. |
| [NVIDIA-NeMo/Switchyard](https://github.com/NVIDIA-NeMo/Switchyard) | — / +408 | Rust-based traffic router for LLM apps across models/providers; preserves native OpenAI/Anthropic API compatibility — a new "model ops" layer. |
| [semantica-agi/semantica](https://github.com/semantica-agi/semantica) | — / +713 | Graph-native infrastructure for context and accountable AI — a new take on structured memory. |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 88,013 / +465 | Leading open-source RAG engine fusing retrieval with agent capabilities as a context layer for LLMs. |

### 🤖 AI Agents / Workflows

| Project | Stars (Total / Today) | Why it matters |
|---|---|---|
| [anthropics/skills](https://github.com/anthropics/skills) | — / +312 | Official public repo for **Agent Skills** — the emerging standard for modular, installable agent capabilities. |
| [cathrynlavery/diagram-design](https://github.com/cathrynlavery/diagram-design) | — / +4,475 | 29 editorial diagram types for Claude Code; self-contained HTML+SVG, no shadows, no Mermaid-slop — today's #1 trending repo. |
| [holaboss-ai/holaOS](https://github.com/holaboss-ai/holaOS) | — / +241 | Open-source "all-in-one" AI agent workspace; runs any agent (Claude Code, Codex) across 100+ integrations with shared memory. |
| [macro-inc/macro](https://github.com/macro-inc/macro) | — / +1,239 | Unified workspace (email, chat, docs, tasks, CRM) with shared AI memory; agents embedded into the collaboration layer. |
| [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents) | — / +778 | A complete "AI agency" as a set of specialized agents — from frontend to Reddit community management. |
| [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) | — / +292 | Agent skills for Obsidian — teaches agents to use Obsidian CLI and open formats including Markdown, Bases, JSON Canvas. |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 230,134 / — | "The agent that grows with you" — highly starred general-purpose agent. |
| [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | 74,141 / — | Nano Claude Code-like agent harness built from scratch; the "learn by doing" approach to agent engineering. |

### 📦 AI Applications

| Project | Stars (Total / Today) | Why it matters |
|---|---|---|
| [altic-dev/FluidVoice](https://github.com/altic-dev/FluidVoice) | — / +76 | Fastest macOS dictation app with on-device STT + custom trained AI enhancement; local Wispr Flow alternative. |
| [lightningpixel/modly](https://github.com/lightningpixel/modly) | — / +118 | Desktop app to generate 3D models from images using local AI, entirely on GPU. |
| [Lightricks/LTX-2](https://github.com/Lightricks/LTX-2) | — / +205 | Official inference + LoRA trainer for LTX-2 audio–video generative model. |
| [3b1b/manim](https://github.com/3b1b/manim) | — / +176 | Animation engine for explanatory math videos — classic tool, still actively relevant for AI-generated educational content. |

### 🧠 LLMs / Training

| Project | Stars (Total / Today) | Why it matters |
|---|---|---|
| [cactus-compute/needle](https://github.com/cactus-compute/needle) | — / +769 | **14MB foundation model** for phones, wearables, smart home, robots — edge AI is shrinking fast. |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4,483 / — | Build a tiny vLLM + Qwen inference system on Apple Silicon — a hands-on systems-engineering path to LLM inference. |
| [AarambhDevHub/aarambh-studio](https://github.com/AarambhDevHub/aarambh-studio) | 76 / — | Decoder-only LLM built from scratch in pure Rust (Candle) — Gated DeltaNet + sparse attention + MoE, from 25M to 1.3B params. |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 102,359 / — | The foundational deep learning framework; still the backbone of most AI OSS. |
| [huggingface/transformers](https://github.com/huggingface/transformers) | 164,079 / — | The model-definition framework for state-of-the-art ML models in text, vision, audio, and multimodal. |

### 🔍 RAG / Knowledge

| Project | Stars (Total / Today) | Why it matters |
|---|---|---|
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 106,041 / — | Turns codebases, docs, schemas into queryable knowledge graphs; local, deterministic, no vector store. |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 90,653 / — | Persistent context across sessions for every agent; compresses and injects relevant context back into future sessions. |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 63,209 / — | Universal memory layer for AI agents. |
| [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) | 66,232 / — | Compress tool outputs, logs, and RAG chunks before they reach the LLM — 20–95% fewer tokens with same answers. |
| [langgenius/dify](https://github.com/langgenius/dify) | 152,373 / — | Build agentic workflows and RAG pipelines with rich model/tool support; deploy on cloud, VPC, or self-hosted. |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 45,628 / — | High-performance cloud-native vector database for scalable ANN search. |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 33,967 / — | High-performance vector database + search engine for next-gen AI. |

---

## 3. Trend Signal Analysis

**Agent Skills are the new package format.** Today's #1 trending repo (diagram-design, +4,475 stars) is not a model or a framework — it's a **skill pack for Claude Code**. Combined with anthropics/skills official repo, obsidian-skills, and graphify's "/graphify skill" for multiple CLIs, it's clear that the community is converging on "skills" as the distribution unit for agent capabilities. This is analogous to the plugin/tool ecosystem that emerged around early IDEs — expect skill marketplaces next.

**Edge AI is going sub-100MB.** needle's 14MB foundation model targeting phones, wearables, smart home, and robots is a significant data point. Combined with FluidVoice (on-device STT for macOS) and modly (local GPU 3D generation), the "local-first AI" movement is maturing beyond chatbots into ambient intelligence for everyday devices.

**Model Ops is becoming a distinct layer.** NVIDIA's Switchyard (cross-provider routing preserving native API compatibility) and unsloth's new local training/run UI both point to a new abstraction layer: managing models as deployable, routable, benchmarkable units — independent of any single provider. This mirrors what Kubernetes did for containers.

**AI memory is moving into the workspace.** macro-inc (+1,239 today) embeds shared AI memory into email/chat/docs/CRM, while claude-mem, mem0, and cognee all focus on persistent cross-session memory. The "memory layer" is no longer a niche research topic — it's becoming table stakes for any serious agent platform.

**First-time signal:** Rust is emerging in the AI infra layer (Switchyard, rig, aarambh-studio's pure-Rust LLM). Also noteworthy: "test-time scaling" survey repo and Agentic RL awesome-list — research directions are formalizing fast.

---

## 4. Community Hot Spots

- **⚡ Claude Code ecosystem**: The explosive growth of diagram-design (+4,475 today), obsidian-skills, and graphify confirms that Claude Code skills are the most active developer surface right now. If you build AI dev tools, target this CLI first.
- **🧠 Persistent agent memory**: claude-mem (90k stars), mem0 (63k stars), and semantica (+713 today) show that "memory for AI agents" is a solved-problem-in-progress — everyone is racing to build the universal memory layer.
- **📉 Local / edge inference**: needle (14MB model) + modly (GPU 3D gen) + FluidVoice (on-device STT) — the "run everything locally" movement is expanding from text to voice, vision, and 3D.
- **🔀 Model routing / provider abstraction**: NVIDIA's Switchyard is a strong signal that enterprises want provider-agnostic routing with native API compatibility — watch for this to become a standard infra component.
- **📚 Agent engineering education**: hello-agents (72k stars), ai-agent-book (37k stars), tiny-llm (4.5k stars) — the community is systematically teaching itself how to build agents and inference systems from scratch, indicating a maturing discipline.

---

*Report compiled from 2026-08-14 GitHub trending and AI topic search data. All star counts as listed in source data.*

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*