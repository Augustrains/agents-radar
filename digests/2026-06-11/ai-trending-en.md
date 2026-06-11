# AI Open Source Trends 2026-06-11

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-11 02:14 UTC

---

Here is the structured AI Open Source Trends Report for **2026-06-11**, based on the provided GitHub data.

---

## 1. Today's Highlights

Today marks a clear inflection point in the open-source AI ecosystem: **"Agent Skills" have become the dominant primitives of software development.** Repositories like `addyosmani/agent-skills` and `phuryn/pm-skills` are exploding in popularity, signaling a shift from building agents to *packaging reusable capabilities* for them. The rise of `google/skills` and `obra/superpowers` further validates this trend, with major tech players and community frameworks standardizing how agents acquire domain-specific expertise. Meanwhile, projects like `mvanhorn/last30days-skill` demonstrate the demand for **grounded, real-time data synthesis** by agents, moving beyond static knowledge bases.

## 2. Top Projects by Category

### 🔧 AI Infrastructure
- [**apple/container**](https://github.com/apple/container) — ⭐0 (+1611 today)  
  Apple's new Swift tool for running Linux containers via lightweight VMs on Mac Silicon; essential infrastructure for local AI agent sandboxing.
- [**vllm-project/vllm**](https://github.com/vllm-project/vllm) — ⭐82,463 [topic:llm]  
  High-throughput LLM inference engine; remains the backbone for serving open models in production.
- [**activeloopai/hivemind**](https://github.com/activeloopai/hivemind) — ⭐0 (+64 today)  
  Centralized "brain" that coordinates multiple agents, enabling shared memory and orchestration across agent ecosystems.

### 🤖 AI Agents / Workflows
- [**addyosmani/agent-skills**](https://github.com/addyosmani/agent-skills) — ⭐0 (+821 today)  
  A library of production-grade engineering skills for AI coding agents; today's most representative example of the "skills" paradigm.
- [**google/skills**](https://github.com/google/skills) — ⭐0 (+211 today)  
  Google's own agent skills for its products; legitimizes and standardizes the "skill as a package" concept across the industry.
- [**shareAI-lab/learn-claude-code**](https://github.com/shareAI-lab/learn-claude-code) — ⭐65,917 [topic:ai-agent]  
  A minimalist "agent harness" built from scratch that teaches the core mechanics of Claude Code-like tool-use agents.
- [**CherryHQ/cherry-studio**](https://github.com/CherryHQ/cherry-studio) — ⭐47,175 [topic:ai-agent]  
  Unified frontend for 300+ AI assistants and autonomous agents; a rapidly growing productivity hub for multi-model workflows.
- [**HKUDS/nanobot**](https://github.com/HKUDS/nanobot) — ⭐44,009 [topic:ai-agent]  
  Ultralightweight open-source AI agent designed for embedding into tools and chat workflows; emphasizes extensibility.

### 📦 AI Applications
- [**harry0703/MoneyPrinterTurbo**](https://github.com/harry0703/MoneyPrinterTurbo) — ⭐0 (+1389 today)  
  One-click AI short video generation using LLMs; a viral application for content creation.
- [**maziyarpanahi/openmed**](https://github.com/maziyarpanahi/openmed) — ⭐0 (+527 today)  
  Open-source healthcare AI stack, including clinical NLP and diagnostic support; shows expanding vertical AI adoption.
- [**soxoj/maigret**](https://github.com/soxoj/maigret) — ⭐0 (+318 today)  
  OSINT tool that uses AI to build dossiers from 3000+ sites; a powerful application of multi-source information gathering.
- [**ruvnet/RuView**](https://github.com/ruvnet/RuView) — ⭐0 (+420 today)  
  AI that turns WiFi signals into spatial intelligence and vital sign monitoring; novel application of non-video sensing.

### 🧠 LLMs / Training
- [**hiyouga/LlamaFactory**](https://github.com/hiyouga/LlamaFactory) — ⭐72,056 [topic:llm]  
  The go-to unified fine-tuning framework for 100+ LLMs and VLMs; essential for adapting open models.
- [**skyzh/tiny-llm**](https://github.com/skyzh/tiny-llm) — ⭐4,267 [topic:llm-model]  
  Educational course on building a tiny vLLM + Qwen inference server on Apple Silicon; excellent for learning LLM systems.
- [**FareedKhan-dev/train-llm-from-scratch**](https://github.com/FareedKhan-dev/train-llm-from-scratch) — ⭐0 (+247 today)  
  Straightforward end-to-end pipeline for training your own LLM from data download to text generation; lowers the barrier to entry.

### 🔍 RAG / Knowledge
- [**infiniflow/ragflow**](https://github.com/infiniflow/ragflow) — ⭐82,419 [topic:rag]  
  Leading open-source RAG engine that combines retrieval with agent capabilities for a superior context layer.
- [**mem0ai/mem0**](https://github.com/mem0ai/mem0) — ⭐58,285 [topic:rag]  
  Universal memory layer for AI agents, providing persistent, long-term context across sessions.
- [**thedotmack/claude-mem**](https://github.com/thedotmack/claude-mem) — ⭐81,659 [topic:rag]  
  Captures, compresses, and re-injects agent session context; solves the "blank context" problem for coding agents.
- [**refactoringhq/tolaria**](https://github.com/refactoringhq/tolaria) — ⭐0 (+612 today)  
  Desktop app for managing markdown knowledge bases; a lightweight tool for personal RAG and note-taking.

## 3. Trend Signal Analysis

The most explosive community attention today is squarely on **Agent Skills and Skill Marketplaces**. The "agent-skills" repositories by `addyosmani`, `phuryn`, and `obra` are not just accumulating stars—they represent a fundamental shift in how the open-source community thinks about AI software. Instead of building monolithic agents, developers are now packaging **reusable, composable capabilities** (skills) that can be plugged into any agent framework (Claude Code, OpenClaw, Gemini CLI, etc.). This is the open-source analogue of a "skill store" for agents.

A new tech stack direction appears in the form of **"Agent Harnesses"** — lightweight shells that orchestrate skills, tools, memory, and sub-agents. `shareAI-lab/learn-claude-code` and `bytedance/deer-flow` exemplify this, abstracting away the complexity of tool calling and context management. The appearance of `google/skills` is a major validation signal: when Google releases an official skill pack for its products (Workspace, Cloud), it confirms that "skills" are now a first-class packaging format.

This surge correlates with the maturation of coding agents (Claude Code, Codex, OpenCode). As these agents become capable of executing complex tasks, the bottleneck has shifted from "can the agent code?" to **"what domain knowledge and API integrations does the agent have?"** — which skills directly solve.

## 4. Community Hot Spots

- **`addyosmani/agent-skills` and `obra/superpowers`**: The two main skill frameworks currently competing for developer mindshare. Watch for ecosystem lock-in and interoperability standards (e.g., MCP vs. native skills).
- **`mvanhorn/last30days-skill`**: Demonstrates the pinnacle of grounded, real-time research agents. Its pattern (multi-source scrape + synthesis) is being replicated across verticals.
- **`zilliztech/claude-context`**: A vector-database-backed MCP for codebase search. This is the template for "knowledge augmentation" for agents that need deep understanding of existing codebases.
- **`thedotmack/claude-mem`**: Solving the persistent memory problem for agents. Memory is the next frontier after skills—agents without long-term context are forgetful tools.
- **`ruvnet/RuView`**: A dark horse. Non-video sensing (WiFi-based spatial awareness) is an entirely new modality for AI agents, opening up ambient computing use cases beyond cameras and microphones.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*