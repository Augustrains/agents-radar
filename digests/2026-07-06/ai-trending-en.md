# AI Open Source Trends 2026-07-06

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-07-06 01:53 UTC

---

Here is the **AI Open Source Trends Report** for **2026-07-06**, based on the provided GitHub trending and topic search data.

---

## 1. Today's Highlights

Today’s open-source landscape is defined by a massive, community-driven standardization around **AI coding agents**, particularly **Claude Code** and its ecosystem of “Skills.” A new meta-pattern has emerged: developers are creating and sharing libraries of modular, reusable agent skills (marketing, compliance, token optimization) that plug directly into CLI-based agents like Claude Code, Codex, and Gemini CLI. Simultaneously, privacy-first, local-first AI tools—from meeting assistants using Whisper to WiFi-based spatial sensing—are seeing explosive growth, signaling a strong user backlash against cloud-dependent AI. Finally, the **system prompt leak** phenomenon (e.g., extracting prompts from Claude, ChatGPT, and Gemini) has become a viral sub-trend, driven by the competitive need to understand how frontier models are being instructed.

## 2. Top Projects by Category

### 🔧 AI Infrastructure (Frameworks, SDKs, Inference Engines, CLI Tools)

| Project | Stars (Total / Today) | Why It Matters Today |
|---|---|---|
| [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc) | +1532 today | OpenAI's official bridge allowing Claude Code to call Codex for code review/delegation – a major interoperability signal. |
| [ogulcancelik/herdr](https://github.com/ogulcancelik/herdr) | +651 today | An "agent multiplexer" that lives in your terminal, enabling seamless multi-agent orchestration from a single CLI. |
| [googleworkspace/cli](https://github.com/googleworkspace/cli) | 29,423 total | Google’s official CLI for Workspace, now with built-in AI agent skills for Drive, Gmail, and Calendar – a new vector for enterprise automation. |
| [usestrix/strix](https://github.com/usestrix/strix) | +1114 today | An open-source AI penetration testing tool that uses LLM agents to find and fix app vulnerabilities – agent-native security tooling. |

### 🤖 AI Agents / Workflows

| Project | Stars (Total / Today) | Why It Matters Today |
|---|---|---|
| [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills) | +392 today | A huge (337 skills) marketplace of reusable agent skills for Claude Code, Codex, and 8 other agents – the "npm" of agentic behavior. |
| [gastownhall/gastown](https://github.com/gastownhall/gastown) | +51 today | A multi-agent workspace manager, hinting at the growing need for orchestrating multiple agents in production environments. |
| [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) | +145 today | Domain-specific agent skills (CRO, SEO, copywriting) for marketing teams – vertical AI agent specialization. |
| [OthmanAdi/planning-with-files](https://github.com/OthmanAdi/planning-with-files) | +66 today | Crash-proof, file-based planning for long-running agentic tasks, solving the critical "context loss" problem in agent workflows. |
| [dotnet/skills](https://github.com/dotnet/skills) | +246 today | Microsoft’s official repo for .NET/C# skills for AI coding agents – a sign that enterprise frameworks are embracing the agent skill standard. |

### 📦 AI Applications (Vertical Solutions, Specific Tools)

| Project | Stars (Total / Today) | Why It Matters Today |
|---|---|---|
| [Zackriya-Solutions/meetily](https://github.com/Zackriya-Solutions/meetily) | +1409 today | A privacy-first, 100% local AI meeting assistant using Whisper + Ollama – riding the "local-first" wave. |
| [ruvnet/RuView](https://github.com/ruvnet/RuView) | +161 today | Turns commodity WiFi into spatial intelligence and vital sign monitoring – a novel sensor fusion AI application. |
| [CoplayDev/unity-mcp](https://github.com/CoplayDev/unity-mcp) | +414 today | A bridge between LLMs and the Unity Editor, enabling AI to control game assets and scenes – a new frontier for generative game dev. |
| [asgeirtj/system_prompts_leaks](https://github.com/asgeirtj/system_prompts_leaks) | +981 today | Viral repository of extracted system prompts from Claude, ChatGPT, Gemini, Grok, and Copilot – becoming a standard reference for prompt engineering. |

### 🧠 LLMs / Training & Fine-Tuning

| Project | Stars (Total / Today) | Why It Matters Today |
|---|---|---|
| [AarambhDevHub/aarambh-ai](https://github.com/AarambhDevHub/aarambh-ai) | +8 today | A decoder-only LLM built from scratch in pure Rust (Candle), supporting LoRA/QLoRA and GRPO – a notable step toward Rust-native training. |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | 313 total | On-device LLM inference using X-Bit quantization – critical for edge AI and privacy-preserving applications. |
| [R-D-BioTech-Alaska/Qelm](https://github.com/R-D-BioTech-Alaska/Qelm) | +27 today | "Quantum Enhanced Language Model" – experimental research bridging quantum computing and LLMs (very early stage, but trending). |

### 🔍 RAG / Knowledge & Vector Databases

| Project | Stars (Total / Today) | Why It Matters Today |
|---|---|---|
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 85,993 total | Persistent context across sessions for any agent – compresses and re-injects historical context into future sessions. |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 78,187 total | Turns any codebase, docs, or images into a queryable knowledge graph – bridging RAG with knowledge graph structures. |
| [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) | 56,833 total | Compresses tool outputs and RAG chunks by 60-95% before reaching the LLM – solving the "token waste" problem in RAG pipelines. |
| [alibaba/zvec](https://github.com/alibaba/zvec) | 12,988 total | Alibaba's lightweight, in-process vector database – a potential disruptor for embedded/local RAG scenarios. |

## 3. Trend Signal Analysis

The most explosive community attention today is directed toward **agent skill standardization** and **agent interoperability**. Projects like `claude-skills`, `awesome-claude-code`, `dotnet/skills`, and `planning-with-files` are not just repositories; they are de facto “package managers” for agentic behavior. This suggests the ecosystem is maturing past single-agent experiments toward a "composable agent" paradigm where skills are shared, versioned, and cross-compatible between Claude Code, Codex, Gemini CLI, and Cursor.

A new direction appearing for the first time is **WiFi-based spatial AI** (`RuView`), which uses commodity hardware for non-video sensing. This signals a move away from camera-dependent AI toward more privacy-preserving sensor fusion. Similarly, **Unity MCP** opens the door for AI-driven game development, a previously untapped vertical for LLM agents.

These trends align with the recent releases of **Claude Code** (Anthropic) and **Codex CLI** (OpenAI) as mature coding agents. The viral `system_prompts_leaks` repository is a direct reaction to the "prompt arms race" between frontier labs, as developers race to understand the exact instructions behind these powerful agents. The “caveman” skill (`JuliusBrussee/caveman`) is a playful but telling signal: token optimization is now a first-class UX concern, driven by rising API costs and context window pressure.

## 4. Community Hot Spots

- **Agent Skill Marketplaces (`claude-skills`, `planning-with-files`)**: The standardization of reusable, cross-agent skills is the single most important trend for developers to watch. It lowers the barrier to building complex agent workflows.
- **System Prompt Leaks (`system_prompts_leaks`)**: The demand to understand "how to prompt the prompts" is surging. Developers should study these leaks to reverse-engineer effective AI agent behaviors.
- **Local-First AI (`meetily`, `Picovoice/picollm`)**: Privacy and cost concerns are driving a renaissance in offline AI. Tools that run fully on-device (Whisper, Ollama, quantized LLMs) are becoming mandatory for sensitive enterprise use cases.
- **Knowledge Graph + RAG Convergence (`Graphify-Labs/graphify`, `thedotmack/claude-mem`)**: The next generation of RAG is not just retrieval but structured memory and graph-based reasoning. These projects point to a future where agents maintain persistent, queryable world models.
- **AI Penetration Testing (`strix`)**: Security is becoming the killer app for agentic AI. Automated, agent-driven security scanning (`strix`) is a high-growth niche with immediate enterprise demand.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*