# AI Open Source Trends 2026-08-23

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-08-23 00:32 UTC

---

# AI Open Source Trends Report — 2026-08-23

---

## 1. Today's Highlights

Today's GitHub trending list is dominated by an unprecedented surge in **agent skill frameworks and harness optimization tools** — the ecosystem is moving rapidly beyond raw agent scaffolding to the *craft* of making agents performant, context-efficient, and behaviorally refined. Notable developments include open-source "skills" packages like `mattpocock/skills` and `obra/superpowers` that codify engineering methodology for Claude Code and Codex, while `affaan-m/ECC` repositions itself as a full "agent harness performance optimization system" — signaling the commoditization of agent infrastructure and a focus on operational excellence. Anthropic's `claude-code` and OpenAI's `codex` remain reference points in terminal-based coding agents, but the Chinese open-source ecosystem is also maturing rapidly with subscription-sharing gateways and AI security tooling from Tencent. Notably absent from today's top trending were traditional training frameworks — the energy has shifted to **applied agentic workflows**.

---

## 2. Top Projects by Category

### 🤖 AI Agents / Workflows

| Project | Stars (Total / Today) | Why it matters |
|---|---|---|
| [mattpocock/skills](https://github.com/mattpocock/skills) | 0 / +2,683 | A collection of reusable "skills" from `.agents` directories — the hottest repo today, showing a demand for battle-tested agent capabilities. |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | 242,172 / +411 (trending) | Positions itself as a full agent harness optimization stack (skills, memory, security) for Claude Code, Codex, Cursor, and more. |
| [obra/superpowers](https://github.com/obra/superpowers) | 0 / +592 | An "agentic skills framework" with an opinionated software dev methodology — example of codifying best practices into agent instructions. |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 234,393 / — | The flagship from Nous Research — an agent that "grows with you"; one of the most-starred AI agent repos today. |
| [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | 74,955 / — | A nano "agent harness" teaching you to build a Claude Code–like agent from scratch — educational and practical. |
| [HKUDS/nanobot](https://github.com/HKUDS/nanobot) | 47,286 / — | Ultra-lightweight, self-hosted personal AI agent framework in Python — strong option for local-first agent control. |
| [zhayujie/CowAgent](https://github.com/zhayujie/CowAgent) | 46,634 / — | Open-source AI assistant & agent harness (formerly chatgpt-on-wechat) — Chinese ecosystem favorite supporting multi-model/multi-channel. |

### 🔧 AI Infrastructure (Frameworks, SDKs, CLI Tools)

| Project | Stars (Total / Today) | Why it matters |
|---|---|---|
| [openai/codex](https://github.com/openai/codex) | 0 / +1,544 | OpenAI's lightweight terminal coding agent — the reference point for open-weights/local agent CLIs. |
| [anthropics/claude-code](https://github.com/anthropics/claude-code) | 0 / +127 | Anthropic's agentic coding tool, now with Python core — daily driver for many developers. |
| [modular/modular](https://github.com/modular/modular) | 0 / +395 | The Modular Platform (MAX & Mojo) — a single stack for inference, compilation, and model deployment; Mojo gaining steam. |
| [n8n-io/n8n](https://github.com/n8n-io/n8n) | 0 / +149 | Fair-code workflow automation with native AI capabilities — important bridge between traditional automation and agentic workflows. |
| [Tencent/AI-Infra-Guard](https://github.com/Tencent/AI-Infra-Guard) | 0 / +150 | Full-stack AI Red Teaming platform — scanning agents, skills, MCP, and LLMs — security is becoming a first-class concern. |
| [Cursor/plugins](https://github.com/cursor/plugins) | 0 / +286 | Official Cursor plugin spec — signal that IDEs are formalizing the agent plugin ecosystem with standards. |

### 🔍 RAG / Knowledge

| Project | Stars (Total / Today) | Why it matters |
|---|---|---|
| [langgenius/dify](https://github.com/langgenius/dify) | 153,218 / — | The leading open-source platform for agentic workflows + RAG — de-facto standard for production LLM apps. |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 149,596 / — | The go-to user-friendly local AI interface (Ollama, OpenAI API) — critical front-end for self-hosted stacks. |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 89,043 / — | High-performance RAG engine with agent capabilities — a major player for production knowledge systems. |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 63,833 / — | Universal memory layer for AI agents — solving a key limitation of stateless conversational systems. |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 45,737 / — | High-performance cloud-native vector database — one of the most widely-adopted infrastructure components. |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 34,128 / — | Massive-scale vector search engine — resilient, efficient, and developer-friendly. |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | 12,829 / — | MLsys 2026 paper: "RAG on Everything" — 97% storage savings on-device; a standout research contribution with practical payoff. |

### 🧠 LLMs / Training

| Project | Stars (Total / Today) | Why it matters |
|---|---|---|
| [huggingface/transformers](https://github.com/huggingface/transformers) | 164,345 / — | The universal model framework — the center of gravity for research and deployment. |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 89,723 / — | High-throughput inference engine — the production workhorse behind most LLM serving. |
| [ollama/ollama](https://github.com/ollama/ollama) | 179,206 / — | Local LLM runner — now supports Kimi-K2.6, GLM-5.2, MiniMax, and more; gateway to local-first AI computing. |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | 54,926 / — | Train a 64M-parameter LLM from scratch in 2 hours — the best practical starting point for learning LLM pre-training. |
| [AarambhDevHub/aarambh-studio](https://github.com/AarambhDevHub/aarambh-studio) | 82 / — | LLM built from scratch in pure Rust (Candle, Gated DeltaNet, MoE) — small but technically valuable for the Rust-AI niche. |

### 📦 AI Applications (Vertical Solutions)

| Project | Stars (Total / Today) | Why it matters |
|---|---|---|
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 48,629 / — | AI generates native PowerPoint decks with shapes, charts, and narration — a polished vertical application. |
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | 114,646 / — | One-click AI short video generation — very popular in Chinese-speaking communities. |
| [Wei-Shaw/sub2api](https://github.com/Wei-Shaw/sub2api) | 0 / +278 | Subscription sharing gateway for Claude, OpenAI, Gemini, Grok — an interesting "consumer utility" for cost sharing. |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 50,924 / — | AI productivity studio with 300+ assistants and unified access to frontier LLMs. |
| [santifer/career-ops](https://github.com/santifer/career-ops) | 67,789 / — | Open-source AI job search: scans portals, scores companies, tailors CV — practical agent application in recruiting. |

---

## 3. Trend Signal Analysis

The single most explosive development today is the **"skills" ecosystem** — a Cambrian explosion of directories, frameworks, and standards around agent skills (`.agents`, `CLAUDE.md`, skill packs). Repos like `mattpocock/skills`, `obra/superpowers`, and `multica-ai/andrej-karpathy-skills` (a CLAUDE.md distilled from Karpathy's observations on LLM coding pitfalls) signal a shift from “can agents code?” to “**how do we make agents excellent**?”. The community is codifying behavioral rules, prompt discipline, and tool-calling habits into reusable, version-controlled skill packs.

A second signal is **the comoditization of agent harnesses**: `affaan-m/ECC` reframes itself as a “performance optimization system” for agent harnesses (Claude Code, Codex, Cursor, Opencode), `shareAI-lab/learn-claude-code` deconstructs a harness from first principles, and `HKUDS/nanobot` offers a lightweight self-hosted alternative. The takeaway: building agents is now *table stakes*; **making them fast, cheap, and behaviorally aligned is the new frontier**.

Third is the growing importance of **AI security**: Tencent’s `AI-Infra-Guard` adds agent/skills/MCP scanning and LLM jailbreak evaluation — a signal that enterprises are taking agentic ecosystems seriously, and the security stack around MCP and skills must mature.

Finally, **local-first and cost-control** themes persist: `ollama` shipping support for Kimi-K2.6, `headroomlabs-ai/headroom` (20–95% token reduction for coding agents), and `JuliusBrussee/caveman` (a Claude Code skill that cuts 65% of tokens) all attack the economics of agent inference.

---

## 4. Community Hot Spots

- **Agent "Skills" as a distributable artifact** — Watch `mattpocock/skills`, `obra/superpowers`, and `multica-ai/andrej-karpathy-skills`. This pattern will likely become the "npm of agents," and IDEs/CLIs that embrace a skill spec (Cursor, Claude Code, Codex) will win ecosystem mindshare.
- **Agent Harness Optimization** — `affaan-m/ECC` and `shareAI-lab/learn-claude-code` are worth studying if you want to build or improve your own agent harnesses; token efficiency and memory management are the moats.
- **Model-agnostic local gateways** — `Wei-Shaw/sub2api` (subscription sharing) and `Mirrowel/LLM-API-Key-Proxy` (unified API gateway) highlight a demand for cost pooling and multi-provider abstraction; expect consolidation in "LLM gateway" tooling.
- **AI Security & Red Teaming for Agents** — `Tencent/AI-Infra-Guard` is one to watch for enterprise adoption; security scanning of agents, MCP servers, and skills will become mandatory in production deployments.
- **Self-hosted AI workspaces** — `siyuan-note/siyuan` (privacy-first knowledge workspace with agents), `n8n`, and `open-webui` continue to converge toward a "personal AI OS" stack; the integrations between note-taking, memory, and agent workflows are where long-term value accrues.

---

*Report generated from GitHub trending + topic data on 2026-08-23.*

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*