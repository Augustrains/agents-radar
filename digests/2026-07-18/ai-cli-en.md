# AI CLI Tools Community Digest 2026-07-18

> Generated: 2026-07-18 01:14 UTC | Tools covered: 9

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/badlogic/pi-mono)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [DeepSeek TUI](https://github.com/Hmbown/DeepSeek-TUI)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date:** 2026-07-18

---

## 1. Ecosystem Overview

The AI CLI tools landscape continues to mature rapidly, with seven major projects showing distinct evolutionary paths. The ecosystem is experiencing a **platform stabilization phase**—many tools are shipping fewer new features and instead focusing on bug fixes, security hardening, and cross-platform reliability. A notable trend is the **universal struggle with agentic reliability**: nearly every tool reports issues with infinite loops, false success reporting, session state loss, and subagent deadlocks. Windows platform parity remains the single largest cross-cutting pain point, with all three major OS platforms (Windows, macOS, Linux) facing tool-specific regressions. The community is increasingly vocal about **user agency and privacy**, demanding opt-outs for session telemetry, granular permission controls, and better model selection mechanisms.

---

## 2. Activity Comparison

| Tool | Open Issues | PRs Updated (24h) | Releases (24h) | Notable Activity |
|---|---|---|---|---|
| **Claude Code** | ~50 active | 10 key PRs | None (stable v2.1.x) | High community engagement (76 comments on payment bug); persistent macOS kernel leak |
| **OpenAI Codex** | High volume | 10+ merged PRs | 3 Rust alpha builds | 48 PRs merged; aggressive release cadence; Windows hang crisis |
| **Gemini CLI** | ~10 hot issues | 10 key PRs | None | Security-focused PRs (sandbox, loop protection); SSR pipeline infra |
| **Copilot CLI** | ~15 new triage | 0 PRs | v1.0.72-1 (previous) | Unusual PR silence; Windows zombie process crisis; task_complete regression |
| **Kimi Code CLI** | ~4 hot issues | 0 PRs | None | Stalled: no releases or PRs; model rollback demand unresolved |
| **OpenCode** | ~10 hot issues | 10 key PRs | Nightly (v0.19.11) | High feature velocity; provider auto-discovery demand (182👍) |
| **Pi** | ~50 issues updated | 10 key PRs | None | Intense bug-fixing cycle; compaction retry and TUI CPU fix |
| **DeepSeek TUI** | ~10 hot issues | 10 key PRs | None | v0.9.1 patch cycle; Windows ARM64 builds; agent autonomy concerns |
| **Qwen Code** | ~10 hot issues | 10 key PRs | v0.19.11-nightly | Multi-workspace daemon RFC driving architecture; CI automation push |

**Key observations:**
- **OpenAI Codex** leads in raw PR throughput (48+ merged) and alpha releases
- **Copilot CLI** is unusually quiet on PRs—suggesting triage overload or internal stabilization
- **Kimi Code CLI** shows zero release/PR activity—concerning for a tool with unresolved critical bugs
- **DeepSeek TUI** has the most active patch cycle relative to its scale

---

## 3. Shared Feature Directions

The following requirements appear across multiple tool communities, indicating industry-wide developer needs:

### Cross-Platform Parity & Windows Reliability
- **Affected tools:** Claude Code, OpenAI Codex, Copilot CLI, Qwen Code, DeepSeek TUI, Pi
- **Specific pain points:** Windows ARM64 failures (Claude Code #50674), HID enumeration deadlocks (Codex #33780), zombie processes (Copilot CLI #4163), ConPTY crashes (DeepSeek #4100), hook process leaks (DeepSeek #4489)
- **Trend:** Windows is universally the weakest platform; kernel-level and PTY issues dominate

### Session Persistence & Resilience
- **Affected tools:** Claude Code, OpenAI Codex, Copilot CLI, Gemini CLI, Qwen Code, Pi
- **Specific requests:** SSH reconnect survival (#49790, Claude Code), background task persistence (#75438), session resume after compaction (Codex #26889), cold-start resumption (Qwen Code #4748)
- **Trend:** Long-running agent workflows demand state survival across restarts and network drops

### Security & Permission Controls
- **Affected tools:** Claude Code, Copilot CLI, Gemini CLI, OpenCode, DeepSeek TUI
- **Specific needs:** Granular path/command permissions (Copilot CLI #4157, #4150), opt-out for session telemetry (Claude Code #66504), destructive command classification (Copilot CLI #4156), prompt injection protection (Gemini CLI #28429)
- **Trend:** User agency and safety are converging—developers want control over what agents can do and what data agents share

### Provider & Model Diversity
- **Affected tools:** OpenCode, Pi, DeepSeek TUI, Claude Code
- **Specific demands:** Auto-discovery of OpenAI-compatible models (OpenCode #6231, 182👍), Kimi K3 support (DeepSeek #4387, Pi #6786), LiteLLM integration (OpenCode #14468), StepFun providers (Pi #6783)
- **Trend:** Lock-in resistance is growing; tools that support multiple providers gain community goodwill

### Agent Reliability & Transparency
- **Affected tools:** Claude Code, Gemini CLI, Qwen Code, DeepSeek TUI, Copilot CLI
- **Specific issues:** False success reporting (Gemini CLI #22323), subagent deadlocks (Qwen Code #7126), autonomous overreach (DeepSeek TUI #4032), duplicate agents on model switch (Claude Code #78688)
- **Trend:** Trust in agentic behavior is eroding; users want observability and kill switches

### UI/UX Polish
- **Affected tools:** Claude Code, Copilot CLI, OpenCode, Qwen Code, DeepSeek TUI
- **Specific requests:** In-panel text search (Claude Code), vi-like navigation (Copilot CLI #4152), Markdown rendering fixes (Kimi Code #2379), TUI text selection (Copilot CLI #4154)
- **Trend:** After initial feature rush, communities are demanding surface-level quality improvements

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach | Unique Strengths |
|---|---|---|---|---|
| **Claude Code** | Agentic co-pilot with TUI | Power developers, multi-agent workflows | Plugin architecture, Cowork platform, VSCode extension | Mature plugin ecosystem; Terraform/Infra integrations |
| **OpenAI Codex** | Desktop + CLI with multimodal | AI researchers, Copilot ecosystem users | Rust core, OpenAI Responses API, realtime V3 | Fastest release cadence; Voice/audio workflows; ChatGPT ecosystem |
| **Gemini CLI** | Security-hardened agent | Enterprise developers, GCP users | POSIX sandboxing, Seatbelt profiles, eval framework | Security-first design; recursive loop protection; automated CI quality gates |
| **Copilot CLI** | GitHub-native shell assistant | GitHub ecosystem developers, BYOK users | Plugin mutations, MCP plugin support, plan-approval UX | Permission classification engine; session persistence; model diversity |
| **Kimi Code CLI** | Moonshot/Kimi model gateway | Chinese financial users, Moonshot ecosystem | Wind plugin, Work Desktop integration | Kimi model specialization; Chinese market focus |
| **OpenCode** | Universal provider router | Multi-provider power users | Zen API, CL100k tokenizer, desktop UI | Best provider diversity; auto-discovery; SSH remote desktop demand |
| **Pi** | Performance-optimized terminal | Performance-sensitive developers | Rust core, compact OOM model, provider catalog | Lowest resource usage; fastest TUI; compaction/reliability focus |
| **DeepSeek TUI** | DeepSeek-centric CLI | Open-source enthusiasts, Chinese developers | Rust cross-compilation, QuickJS, HarmonyOS support | Windows ARM64; HarmonyOS/OpenHarmony; open-source transparency |
| **Qwen Code** | Daemon/server architecture | Team/enterprise users, web-shell users | ACP (Agent Control Protocol), daemon lifecycle, Fleet CI | Multi-workspace daemon; web shell; automated CI shepherd |

**Key differentiators:**
- **Security posture:** Gemini CLI leads with deny-by-default sandboxing; Claude Code and Copilot CLI are reactive
- **Provider agnosticism:** OpenCode and Pi are the most diverse; Kimi Code and DeepSeek TUI are tied to specific ecosystems
- **Platform coverage:** DeepSeek TUI is uniquely investing in Windows ARM64 and HarmonyOS; Claude Code struggles on macOS kernel
- **Release velocity:** OpenAI Codex has the fastest alpha cycle; Pi and DeepSeek TUI lead in patch turnaround
- **Community trust:** Qwen Code (24h bug fix for #7126) and Pi (compaction retry #6775) show responsive maintainership; Kimi Code shows worrying inactivity

---

## 5. Community Momentum & Maturity

### High Momentum (Rapidly Iterating, Growing Communities)
| Tool | Momentum Indicators |
|---|---|
| **OpenAI Codex** | 48+ PRs/24h, 3 alpha releases, 426👍 for LSP request. Most active community by volume. |
| **Pi** | 50 issues + 22 PRs updated/24h. Intense bug-fixing cycle. Growing enterprise interest. |
| **DeepSeek TUI** | 10 key PRs, Windows ARM64 + HarmonyOS expansion. Fast patch turnaround. Open-source transparency builds trust. |
| **Qwen Code** | Multi-workspace RFC driving architecture. Fleet CI automation. 24h fix for critical subagent bug. |

### Moderate Momentum (Stable with Active Triage)
| Tool | Momentum Indicators |
|---|---|
| **Claude Code** | High community engagement (76 comments on single issue), but zero releases + stalled feature requests. Mature but slowing. |
| **Gemini CLI** | Security-focused PRs (sandbox, loop protection). SSR pipeline suggests internal automation. Moderate engagement. |
| **OpenCode** | 182👍 top feature request. Desktop UI friction but strong core improvements. Steady PR velocity. |

### Low Momentum (Stalled or Declining)
| Tool | Momentum Indicators |
|---|---|
| **Kimi Code CLI** | Zero releases, zero PRs in 24h. Critical model quality issue (#1925) unresolved since April. Chinese financial user exodus risk. |
| **Copilot CLI** | Zero PRs in 24h (unusual). 15+ new triage issues. task_complete regression (previously fixed). Signals internal crisis or backlog. |

### Maturity Assessment
- **Most mature ecosystem:** Claude Code (deepest plugin ecosystem, longest bug history), OpenAI Codex (fastest iteration, most PRs)
- **Most promising newcomers:** DeepSeek TUI (platform expansion, responsive maintainers), Qwen Code (architectural ambition, CI automation)
- **At risk:** Kimi Code (stalled activity, unresolved critical bugs), Copilot CLI (regression of previously fixed issues, zero PR engagement)

---

## 6. Trend Signals

### From Community Feedback to Industry Direction

**Signal 1: Agent Reliability is the #1 Unmet Need**
> Every major tool has unresolved agent reliability issues: false success reporting, infinite loops, subagent deadlocks, autonomous overreach. Claude Code (#78688), Gemini CLI (#22323), Qwen Code (#7126), DeepSeek TUI (#4032), and Copilot CLI (#4161) all report variations. **Industry implication:** The ability to build trustworthy, observable agentic behavior is the defining competitive differentiator for 2026-2027.

**Signal 2: The "Bring Your Own Key" (BYOK) Revolution is Real**
> OpenCode's #6231 (182👍 for auto-discovery), Pi's provider catalog expansion, and DeepSeek TUI's multi-provider onboarding all point to the same trend: **users refuse to be locked into a single model provider.** Tools that support seamless switching between OpenAI, Anthropic, Google, Moonshot, and open-source models (via LiteLLM, SGLang, Ollama) will dominate.

**Signal 3: Windows is the Achilles' Heel**
> Nearly every tool has Windows-specific showstoppers: HID enumeration deadlocks (Codex), zombie processes (Copilot CLI), ConPTY crashes (DeepSeek), permission bugs (Claude Code). **Industry implication:** As AI development moves to more diverse hardware (Snapdragon X ARM64, WSL-heavy workflows), Windows compatibility is a hard requirement—not a nice-to-have.

**Signal 4: Session Persistence is Table Stakes**
> Long-running agent workflows (hours to days) are becoming common. SSH reconnect survival (Claude Code), compaction failure handling (Pi), and daemon cold-start optimization (Qwen Code) all address the same need: **agents must survive network drops, client restarts, and compaction events.** Tools without session resilience will lose enterprise adoption.

**Signal 5: Security is Moving from Reactive to Proactive**
> Gemini CLI's deny-by-default sandboxing (#28424), Copilot CLI's permission classification (#7053), and Claude Code's plugin hardening (#76581) show a shift from "block known bad patterns" to "assume compromise, grant minimally." **Industry implication:** Enterprise customers will demand deterministic security models, not heuristic-based guardrails.

**Signal 6: The TUI Renaissance is Polarizing**
> While TUI enthusiasts love terminal-native tools (Pi, DeepSeek TUI), desktop UI friction is generating significant negative sentiment (OpenCode's missing build/plan toggle, Copilot CLI's blank TUI). **Industry implication:** The niche for pure TUI tools is growing, but they must achieve feature parity with desktop clients—or risk alienating users who need both.

### What Developers Should Watch

1. **For tool selection:** Prioritize tools with active Windows support, session persistence, and provider diversity. Avoid single-provider tools (Kimi Code) unless ecosystem-locked.
2. **For contribution:** The highest-impact areas are agent reliability (loop detection, success reporting), cross-platform testing (Windows ARM64, Wayland), and permission systems.
3. **For investment:** The BYOK trend and session persistence requirements are unlikely to reverse—tooling that solves these well will capture significant market share.
4. **Risk signals:** Tools with zero PR activity (Kimi Code), regressions of previously fixed issues (Copilot CLI's task_complete), or stalled critical bugs (Claude Code's macOS kernel leak) should be monitored for maintainer burnout or strategic redirection.

---

*Data sourced from community digests for Claude Code, OpenAI Codex, Gemini CLI, Copilot CLI, Kimi Code CLI, OpenCode, Pi, DeepSeek TUI, and Qwen Code. Analysis reflects activity as of 2026-07-18.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report for the `anthropics/skills` repository, based on the most-watched activity as of 2026-07-18.

---

## Claude Code Skills Community Highlights Report

### 1. Top Skills Ranking

The following Pull Requests represent the most-discussed and highest-activity Skill submissions in the community.

1.  **`fix(skill-creator): run_eval.py always reports 0% recall`** [#1298](https://github.com/anthropics/skills/pull/1298)
    - **Functionality:** Fixes the core `run_eval.py` script used in the `skill-creator` optimization loop. The bug renders the entire description-optimization pipeline inert by reporting `recall=0%` for every candidate, meaning the system actively optimizes against noise.
    - **Discussion Highlights:** Addresses a critical blocker for the entire skill-creation workflow. Multiple users independently reproduced the bug (Issue #556). The fix spans installation, Windows stream reading, trigger detection, and parallel workers.
    - **Status:** Open.

2.  **`Add document-typography skill`** [#514](https://github.com/anthropics/skills/pull/514)
    - **Functionality:** A typographic quality control skill that prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses a common pain point in professional document output.
    - **Discussion Highlights:** Focused on high-frequency, low-visibility defects. Users noted these issues affect virtually every long-form document Claude generates.
    - **Status:** Open.

3.  **`Add ODT skill — OpenDocument text creation`** [#486](https://github.com/anthropics/skills/pull/486)
    - **Functionality:** Enables creation, template filling, and conversion of OpenDocument Format files (.odt, .ods), supporting LibreOffice and ISO-standard document workflows.
    - **Discussion Highlights:** Significant interest from enterprise and open-source users. The skill bridges a gap in the document ecosystem, alongside existing DOCX and PDF skills.
    - **Status:** Open.

4.  **`Improve frontend-design skill clarity and actionability`** [#210](https://github.com/anthropics/skills/pull/210)
    - **Functionality:** Revises an existing skill to ensure every instruction is executable within a single conversation, improving specificity and coherence.
    - **Discussion Highlights:** A direct response to the community's demand for higher quality and more actionable existing Skills, rather than just new ones.
    - **Status:** Open.

5.  **`Add skill-quality-analyzer and skill-security-analyzer`** [#83](https://github.com/anthropics/skills/pull/83)
    - **Functionality:** Two meta-skills for evaluating other Skills across structure/documentation (20%) and security dimensions.
    - **Discussion Highlights:** Early community interest in quality governance and security auditing of the Skills ecosystem itself. Represents a "meta" layer of the platform.
    - **Status:** Open.

6.  **`Add color-expert skill`** [#1302](https://github.com/anthropics/skills/pull/1302)
    - **Functionality:** A self-contained expertise skill covering color naming systems (ISCC-NBS, Munsell, RAL), color spaces with "what to use when" guidance, and color harmony.
    - **Discussion Highlights:** A niche but deep domain skill. Praised for its completeness and practical guidance tables.
    - **Status:** Open.

### 2. Community Demand Trends

Analysis of the top Issues reveals three concentrated demand vectors:

- **Windows Compatibility:** Issues [#1061](https://github.com/anthropics/skills/issues/1061) and [#556](https://github.com/anthropics/skills/issues/556) document that the `skill-creator` tooling is nearly unusable on Windows due to `PATHEXT`, encoding (cp1252), and subprocess pipe errors. This is the single largest technical blocker for a significant portion of the developer base.
- **Enterprise & Governance:** Issue [#492](https://github.com/anthropics/skills/issues/492) highlights a trust-boundary vulnerability where community skills live under the `anthropic/` namespace, potentially misleading users into granting elevated permissions. Issue [#228](https://github.com/anthropics/skills/issues/228) demands org-wide skill sharing without manual file transfer. Issue [#412](https://github.com/anthropics/skills/issues/412) proposes an `agent-governance` skill for safety patterns, policy enforcement, and audit trails.
- **Duplicate Content & De-duplication:** Issue [#189](https://github.com/anthropics/skills/issues/189) reports that installing both `document-skills` and `example-skills` plugins results in duplicate skills, wasting context window space. This signals a need for better plugin dependency management.

### 3. High-Potential Pending Skills

These PRs have active comments and are not yet merged, indicating they may land soon:

- **`Add Pyxel skill for retro game development`** [#525](https://github.com/anthropics/skills/pull/525) — Adds support for the Pyxel retro game engine via an MCP server, covering the full iterative development workflow.
- **`Add testing-patterns skill`** [#723](https://github.com/anthropics/skills/pull/723) — A comprehensive testing stack skill covering unit testing (AAA pattern), React component testing (Testing Library), and testing philosophy (Testing Trophy model).
- **`Add SAP-RPT-1-OSS predictor skill`** [#181](https://github.com/anthropics/skills/pull/181) — Integrates SAP’s open-source tabular foundation model for predictive analytics on SAP business data, targeting the enterprise AI/ML workflow.
- **`docs: add CONTRIBUTING.md`** [#509](https://github.com/anthropics/skills/pull/509) — A community health gap-filling PR that directly addresses Issue #452, aiming to improve the repo’s GitHub community health score from 25%.
- **`Add self-audit skill (v1.3.0)`** [#1367](https://github.com/anthropics/skills/pull/1367) — A meta-skill that performs mechanical file verification followed by a four-dimension reasoning audit before delivery. Universal across any project or model.

### 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *ecosystem infrastructure* — tooling that is cross-platform (Windows compatibility), trustworthy (security auditing and governance), and efficiently manageable (de-duplication, meta-quality analysis) — rather than for any single domain-specific skill.**

---

# Claude Code Community Digest — 2026-07-18

## Today's Highlights
No new releases this week, but the community remains highly active with 50 open issues and 9 PRs updated in the last 24 hours. Persistent bug reports around **kernel memory leaks on macOS** and **Cowork platform regressions on Windows ARM64** continue to draw attention, while the team pushes forward with plugin hardening and Terraform gateway fixes. A new wave of feature requests emphasizes **session resilience** (SSH reconnect, background task persistence) and **UX refinements** in the TUI and VSCode extension.

## Releases
No new versions published in the last 24 hours. The latest stable channel remains **Claude Code 2.1.205–2.1.212** as referenced in several bug reports.

## Hot Issues (10 noteworthy)

1. **[#55982 – Plan upgrade payment fails with `void_invoice`](https://github.com/anthropics/claude-code/issues/55982)**  
   *Author: ssshreyans26* — 76 comments, 25 👍  
   Payment flow broken for 2.5 months; PaymentIntent is voided before `confirm` completes. High engagement suggests many users are stuck on free tier or unable to upgrade. Community upvoted heavily — likely a server-side fix needed.

2. **[#50674 – Cowork fails on ARM64 Snapdragon X](https://github.com/anthropics/claude-code/issues/50674)**  
   *Author: harshadoak* — 40 comments, 1 👍  
   Passes readiness check, then fails at runtime on ARM64 Windows. Duplicate flagged; affects users of new Snapdragon X laptops. Broader Cowork stability concern (#47327 also open).

3. **[#66020 – macOS kernel zone leak (data.kalloc.1024) from Claude CLI](https://github.com/anthropics/claude-code/issues/66020)**  
   *Author: LeifErikH* — 16 comments, 2 👍  
   Leak rate scales 21→1027/sec with agent load; panics at ~20GB. **Critical stability issue** for macOS users running heavy agent workloads. Has repro, platform:macos, perf:memory labels.

4. **[#74949 – Auto mode classifier 'temporarily unavailable' in bursts](https://github.com/anthropics/claude-code/issues/74949)**  
   *Author: gabrieldedeco* — 6 comments, 3 👍  
   Fail-closed blocks all compound Bash commands during peak windows. Affects nearly every real-world shell workflow. Community requesting API fallback (#78263) as mitigation.

5. **[#67021 – Bundled ugrep OOMs host with bounded regex intervals](https://github.com/anthropics/claude-code/issues/67021)**  
   *Author: interkelstar* — 4 comments, 1 👍  
   `-E .{0,N}` pattern causes multiple GB RSS during DFA construction. Duplicated in #78700. Bash tool silently shadows `grep` with buggy ugrep, surprising users.

6. **[#66504 – Session URL appended to commit messages – should be opt-in](https://github.com/anthropics/claude-code/issues/66504)**  
   *Author: joka-7* — 8 comments, 32 👍  
   High community agreement: default session URL injection in commits/PRs violates expectations. Privacy and noise concerns.

7. **[#40043 – Allow removal of local folders from Cowork project context](https://github.com/anthropics/claude-code/issues/40043)**  
   *Author: peterstahel85* — 19 comments, 56 👍  
   Most-upvoted open feature request. Users want granular control over which folders are shared in Cowork sessions. Still unresolved after 4 months.

8. **[#77327 – Non-interactive system prompts injected into interactive sessions (VSCode)](https://github.com/anthropics/claude-code/issues/77327)**  
   *Author: nebrius* — 7 comments, 1 👍  
   Newly filed; has repro. Context contamination bug affecting VSCode extension users. Could cause unexpected model behavior.

9. **[#78221 – Hidden Browser pane screenshots time out 30s on Windows](https://github.com/anthropics/claude-code/issues/78221)**  
   *Author: AdamRealE* — 2 comments, 2 👍  
   Regression from #76649. All browser capture tools fail when pane is not visible. Blocks automation workflows on Windows.

10. **[#78688 – Fable 5 → Opus 4.8 auto-switch spawns duplicate agents](https://github.com/anthropics/claude-code/issues/78688)**  
    *Author: Sahil170595* — 1 comment, 0 👍  
    False-positive safeguard triggers mid-generation, re-spawning in-flight agents and doubling token burn. Cost-sensitive users affected.

## Key PR Progress (10 important)

1. **[#78532 – GCP Terraform example: optional internal ALB + PG16 fix](https://github.com/anthropics/claude-code/pull/78532)**  
   *Author: gabrielparanthoen-cmd* — Open  
   Fixes Cloud SQL PG16 deployment failure with shared-core tiers; adds internal ALB option for GCP gateway. Practical infrastructure fix.

2. **[#76581 – Harden YAML, path, and symlink handling in plugin scripts](https://github.com/anthropics/claude-code/pull/76581)**  
   *Author: 1837620622* — Open  
   Security hardening against YAML injection, path traversal, and symlink-based credential overwrite in official plugins. Important for supply-chain safety.

3. **[#78446 – Add missing plugin.json manifest to plugin-dev](https://github.com/anthropics/claude-code/pull/78446)**  
   *Author: Atishyy27* — Open  
   Trivial but critical: the plugin-dev example was the only plugin missing its manifest. Blocks developer onboarding.

4. **[#78445 – Correct plugin descriptions and version that contradict source](https://github.com/anthropics/claude-code/pull/78445)**  
   *Author: Atishyy27* — Open  
   Docs-to-code mismatch in plugin index (wrong hooks, wrong pattern counts). Quality-of-life for plugin marketplace consumers.

5. **[#78441 – Fix devcontainer PS1 script: detect native command failures](https://github.com/anthropics/claude-code/pull/78441)**  
   *Author: Atishyy27* — Open  
   PowerShell `try/catch` doesn't catch native exit codes; all error handling in the devcontainer script was dead code. Systemic reliability fix.

6. **[#78425 – Require explicit user invocation for code-review plugin](https://github.com/anthropics/claude-code/pull/78425)**  
   *Author: ZaunEkko* — Open  
   Prevents models/subagents from re-entering the multi-agent review workflow programmatically. Reduces unintended infinite loops.

7. **[#77427 – Make pr-review-toolkit code-reviewer a leaf agent](https://github.com/anthropics/claude-code/pull/77427)**  
   *Author: ZaunEkko* — Open  
   Restricts reviewer to inspection tools only; prevents recursive agent invocation. Safety hardening for PR workflows.

8. **[#78371 – Harden ralph-wiggum plugin: bounded iterations, push/publish guard](https://github.com/anthropics/claude-code/pull/78371)**  
   *Author: kazukinakai* — Open  
   Adds iteration limits, stop-hook fixes, and guards against unattended push/publish/deploy. Essential safety for autonomous loop plugin.

9. **[#29460 – Improve oncall triage recency and engagement criteria](https://github.com/anthropics/claude-code/pull/29460)**  
   *Author: vishnukannaujia* — Closed  
   Updates oncall CI to sort issues by engagement (comments/👍) rather than vague "recently updated". Better triage signal.

10. **[#78425 – Require explicit user invocation for code-review plugin](https://github.com/anthropics/claude-code/pull/78425)**  
    *Author: ZaunEkko* — Open  
    Listed again for visibility: this and #77427 form a two-PR safety suite for the review tooling ecosystem.

## Feature Request Trends
- **Session persistence & resilience** – SSH remote session survival (#49790, 29👍), background task completion records across CLI restarts (#75438), and Cowork host registration state cleanup (#78547) are the top cluster.
- **Context & privacy control** – Opt-out for session URLs in commits (#66504, 32👍), opt-out for shadowed `find`/`grep` (#69736), and per-folder Cowork context removal (#40043, 56👍) show growing demand for user agency.
- **TUI/UX refinements** – In-panel text search for VSCode (#65858), autocomplete improvements (#78110, #72601), preview truncation expansion (#78070) — requests for polish over new features.
- **API/classifier fallback** – Burst errors from auto-mode classifier (#74949) have spawned requests for API fallback mechanisms (#78263) and model redundancy.

## Developer Pain Points
1. **MacOS kernel memory leaks (#66020)** – Degrades agent-heavy workflows catastrophically; no workaround available. Highest-severity unaddressed bug.
2. **Cowork platform fragmentation** – ARM64 Windows (#50674), Windows Pro x64 (#47327), and persistent folder management (#40043) make Cowork unreliable across non-standard setups.
3. **Shadowed tools behavior** – Bundled ugrep silently replacing `grep` causes regex OOMs (#67021, #78700). Users report being surprised by different behavior than system `grep`. No opt-out (#69736).
4. **Session state loss across restarts** – Background agents killed on CLI exit, completion records lost, no reconnect capability (#75438, #49790). Critical for long-running tasks.
5. **Auto-mode classifier unreliability** – Burst failures block all shell work (#74949); false-positive safeguard swaps spawn duplicate agents, doubling costs (#78688).
6. **Payment flow breakage (#55982)** – 2.5 months unfixed; blocks plan upgrades for what may be many users hitting free-tier limits.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**OpenAI Codex Community Digest**
*Date: 2026-07-18*

**1. Today's Highlights**

The Codex ecosystem saw a flurry of activity, with three new Rust alpha releases and over 48 pull requests merged in the last 24 hours. A critical performance regression on Windows has dominated the bug tracker, with multiple reports of the Desktop app hanging on launch due to HID enumeration and Defender conflicts. On the feature front, the most requested change continues to be native Language Server Protocol (LSP) integration for the CLI, which has amassed 426 upvotes.

**2. Releases**

Three new Rust pre-release versions were published:
- **[rust-v0.145.0-alpha.23](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.23)** (latest)
- **[rust-v0.145.0-alpha.22](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.22)**
- **[rust-v0.145.0-alpha.20](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.20)**

No changelogs were attached to these releases, suggesting they are incremental rollups for internal testing.

**3. Hot Issues**

1. **[#8745 – LSP integration for Codex CLI](https://github.com/openai/codex/issues/8745)** (58 comments, 426 👍)  
   The top-voted feature request. Users want auto-detection and installation of language servers to improve code intelligence and diagnostics in the CLI. Remains a key quality-of-life gap.

2. **[#33780 – Windows app hangs on launch (HID enumeration)](https://github.com/openai/codex/issues/33780)** (19 comments, 2 👍)  
   A critical Windows bug: the main process deadlocks in `HID.node → hid.dll` when a single HID device fails to respond. High severity due to immediate launch failure.

3. **[#28919 – Missing "control other devices" tab on Windows](https://github.com/openai/codex/issues/28919)** (17 comments, 23 👍)  
   Users on Windows Pro cannot see the remote device control settings tab. The issue has been open for a month with no fix in sight.

4. **[#27915 – Linux users locked out of usage resets](https://github.com/openai/codex/issues/27915)** (Closed, 17 comments, 41 👍)  
   A closed bug with high engagement. Linux users couldn't redeem banked usage resets because the feature was Desktop-app only. The closure suggests a fix or policy change landed.

5. **[#28161 – Show expiration dates for usage resets](https://github.com/openai/codex/issues/28161)** (7 comments, 56 👍)  
   Pro users want expiration dates for each banked usage reset, as the current UI only shows a count — leading to unexpected loss of resets.

6. **[#26250 – RTL/LTR text rendering broken](https://github.com/openai/codex/issues/26250)** (10 comments)  
   Mixed Arabic/English text is rendered incorrectly. A persistent localization bug that affects a significant user base.

7. **[#33171 – Remote-compaction capacity error kills persistent goals](https://github.com/openai/codex/issues/33171)** (8 comments)  
   A complex server-side bug where remote compaction failure terminates a single `/goal` while other tasks survive. Undermines long-running agent reliability.

8. **[#33873 – Desktop unresponsive after update (Windows)](https://github.com/openai/codex/issues/33873)** (6 comments, 2 👍)  
   A duplicate of #33780, but with a slightly different scenario. Confirms widespread Windows instability after the 26.715 release.

9. **[#32791 – Five-hour usage limit vanished for Plus accounts](https://github.com/openai/codex/issues/32791)** (7 comments, 2 👍)  
   Rate-limit UI regression: the 5-hour bucket disappeared for Plus users, showing only a weekly limit. Multiple duplicates (e.g., #32707, #32635).

10. **[#18906 – TUI Markdown math rendering](https://github.com/openai/codex/issues/18906)** (4 comments, 16 👍)  
    A long-standing feature request for inline and block LaTeX rendering in the terminal UI. Important for researchers and math-heavy users.

**4. Key PR Progress**

1. **[#33932 – Forward audio inputs to Responses API](https://github.com/openai/codex/pull/33932)** (Closed)  
   Enables audio data URLs to be sent as `input_audio` content, unblocking voice workflows in the CLI.

2. **[#33930 – Track inherited paginated rollout prefixes](https://github.com/openai/codex/pull/33930)** (Closed)  
   Adds `HistoryPosition` to support incremental thread inheritance, critical for session continuity across compaction.

3. **[#33926 – Fix quoted hook commands on Windows](https://github.com/openai/codex/pull/33926)** (Closed)  
   Patches a common Windows pain point: hook commands with spaces in their executable path are now passed correctly to the shell.

4. **[#33925 – Render inline visualization links in TUI](https://github.com/openai/codex/pull/33925)** (Closed)  
   Adds terminal fallback for assistant-authored visualizations by rendering browser-link directives alongside `::codex-inline-vis{}`.

5. **[#33922 – Allow selecting path-backed agents in TUI picker](https://github.com/openai/codex/pull/33922)** (Closed)  
   Fixes the agent picker being stuck after rendering status history for path-backed subagents.

6. **[#33921 – Preserve sub-agent liveness in agent picker](https://github.com/openai/codex/pull/33921)** (Closed)  
   Stops the agent picker from marking a newly spawned agent as "stopped" before it emits a turn event.

7. **[#33908 – Allow publishing plugins through share updates](https://github.com/openai/codex/pull/33908)** (Closed)  
   Adds `LISTED` discoverability for plugins, enabling controlled public sharing via the sharing API.

8. **[#33907 – Add occurrence search for paginated threads](https://github.com/openai/codex/pull/33907)** (Closed)  
   New `thread/searchOccurrences` method for case-insensitive literal search across paginated histories without replay.

9. **[#33903 – Route realtime V3 handoffs by response channel](https://github.com/openai/codex/pull/33903)** (Closed)  
   Adds response channel routing for realtime sessions (thinking/commentary), enabling richer multimodal interaction.

10. **[#33901 – Support ChatGPT-branded Desktop builds](https://github.com/openai/codex/pull/33901)** (Closed)  
    Makes the Desktop app discoverable under both "Codex" and "ChatGPT" branding, fixing CLI handoff on systems with branded builds.

**5. Feature Request Trends**

- **LSP Integration (Issue #8745, 426 👍):** Dominates all other requests. Want built-in, auto-detecting language servers to improve code analysis.
- **Rate-Limit Transparency (Issues #28161, #28888):** Users demand visible expiration dates for banked resets and longer expiry windows (beyond 30 days).
- **Context Pins & Compaction Hints (Issue #26889):** Need to preserve critical context across `/compact` and automatic compaction. Multiple related issues (#26321, #25083) share this need.
- **Math Rendering in TUI (Issue #18906, 16 👍):** LaTeX support for the terminal is a recurring ask from academic and scientific users.

**6. Developer Pain Points**

- **Windows App Instability (Multiple duplicates):** The 26.715 release introduced severe launch hangs (HID enumeration), Defender CPU spikes, and stuttering. This is the #1 stability concern.
- **Rate-Limit UI Regressions (Issues #32791, #32707, #32635):** A systemic bug where the 5-hour usage bucket disappears from both the Desktop app and API endpoints for Plus accounts. Affects visibility and planning.
- **Remote-SSH Extension Failures (Issues #27597, #32385):** The VS Code extension routinely fails or hangs when used over Remote-SSH, while the CLI works fine — forcing a workflow workaround.
- **Cross-Platform Parity Gaps (Issue #27915):** Linux users remain second-class citizens for rate-limit management and other Desktop-only features, generating persistent friction.

---

*Data sourced from [openai/codex](https://github.com/openai/codex). Digest generated by technical analysis for developer audience.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-18

## Today's Highlights
The team closed several security-focused pull requests addressing macOS sandbox hardening and recursive reasoning loop protection. A new "SSR Pipeline" infrastructure PR stack appeared, suggesting an automated issue-to-PR generation system is being actively built. Several long-standing agent bugs (hangs, false success reports, Wayland failures) remain open with recent updates, indicating ongoing prioritization of agent reliability.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (11 comments, P1 bug)  
   A subagent (`codebase_investigator`) hits its turn limit but reports `status: "success"` with `Termination Reason: "GOAL"`, masking the interruption. Community upvoted (👍2); this undermines trust in agent self-reporting.

2. **[#19873 — Leverage model's bash affinity via Zero-Dependency OS Sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)** (8 comments, P2 enhancement)  
   Proposes using Gemini 3's native bash capabilities with POSIX tools while sandboxing execution. A large-effort feature request; no concrete timeline or assignee.

3. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** (7 comments, P1 bug, 👍8)  
   High community engagement. `gemini-cli` hangs indefinitely when deferring to the generalist agent for simple tasks. Workaround: disabling sub-agent usage entirely.

4. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (7 comments, P1 EPIC)  
   Tracks expanding behavioral eval tests (currently 76) across 6 Gemini models. Critical for ensuring agent quality regression prevention.

5. **[#22745 — AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (7 comments, P2 investigation)  
   Explores whether AST-aware tools can reduce token waste and turn count by precisely reading method bounds. Potential for significant quality improvements.

6. **[#24353 — (duplicate reference — see above)]**  
   *(Skipping to next unique issue)*

7. **[#25166 — Shell command execution stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (4 comments, P1 bug, 👍3)  
   After simple CLI commands finish, Gemini CLI hangs showing "Awaiting user input". Reproducible with trivial commands. High frustration potential.

8. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (5 comments, P2 bug)  
   Auto Memory only marks sessions as processed after `read_file` succeeds. Low-signal sessions get re-surfaced repeatedly. Wasteful and noisy.

9. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (4 comments, P1 bug)  
   Browser agent terminates with `GOAL` on Wayland displays. Linux users with Wayland compositors are blocked from browser-based agent capabilities.

10. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (6 comments, P2 bug)  
    Anecdotal report that custom skills and sub-agents are rarely invoked autonomously, even for relevant tasks. Suggests poor agent tool-selection heuristics.

## Key PR Progress

1. **[#28429 — Mitigate infinite ReAct loops and prompt injection loops](https://github.com/google-gemini/gemini-cli/pull/28429)** (CLOSED, P1)  
   Implements a 15-turn default session limit and enhanced loop detection. Directly addresses prompt injection vulnerabilities from malicious workspace files.

2. **[#28424 — Align macOS permissive Seatbelt profiles with deny-default model](https://github.com/google-gemini/gemini-cli/pull/28424)** (CLOSED, P1)  
   Updates macOS sandbox profiles to use `(deny default)` with explicit allow-lists, making "permissive" profiles actually deny-by-default. Security hardening.

3. **[#28403 — Block $VAR and ${VAR} variable expansion bypass](https://github.com/google-gemini/gemini-cli/pull/28403)** (OPEN, P1 security)  
   Fixes an incomplete check that allowed variable expansion patterns to bypass the security gate from GHSA-wpqr-6v78-jr5g. Defense-in-depth.

4. **[#28319 — Enforce path trust check prior to environment loading (a2a-server)](https://github.com/google-gemini/gemini-cli/pull/28319)** (OPEN)  
   Ensures workspace path trust checks happen before loading workspace-level environment variables in the CoderAgentExecutor. Prevents untrusted env injection.

5. **[#28386 — Fix VS Code companion activation disposables tracking](https://github.com/google-gemini/gemini-cli/pull/28386)** (OPEN, P2)  
   Fixes VS Code extension registration where only the last Disposable in pairs was tracked. Fixes #27790. Important for extension lifecycle correctness.

6. **[#28275 — Make direct GCP telemetry exporters optional](https://github.com/google-gemini/gemini-cli/pull/28275)** (CLOSED, P3)  
   Removes Google Cloud telemetry exporters from core runtime dependencies. Reduces bundle size and allows non-Google cloud consumers to avoid forced dependencies.

7. **[#28346 — Fix trust dialog disclosure for runnable hooks](https://github.com/google-gemini/gemini-cli/pull/28346)** (OPEN, P1 security)  
   Fixes folder-trust discovery to inspect actual hook definition shapes. Stops reporting invalid hooks as runnable. Good defense against misleading trust prompts.

8. **[#28435-#28431 — SSR Pipeline PR stack (4 PRs)](https://github.com/google-gemini/gemini-cli/pull/28435)** (OPEN)  
   New PRs introduce a `pr-generator` system: config parser, command executor, GitHub REST integration, Antigravity agent runner, Firestore concurrency locking, Cloud Run deployment. Suggests an automated issue-to-PR pipeline is being built internally.

9. **[#28164 — Limit recursive reasoning turns per single user request](https://github.com/google-gemini/gemini-cli/pull/28164)** (CLOSED)  
   Earlier closed iteration of turn-limiting logic. Sets strict 15-turn limit per user request. Helps protect against runaway costs and infinite loops.

10. **[#28344 — Add eval:validate static analysis command](https://github.com/google-gemini/gemini-cli/pull/28344)** (OPEN)  
    New `eval:validate` CLI command validates eval files against 9 rules and exits with code 1 on violations. Useful for CI gating eval quality.

## Feature Request Trends

1. **Agent self-awareness and transparency** — Multiple issues request that Gemini CLI understand its own capabilities (flags, hotkeys, subagent trajectories) and expose them accurately to users via `/chat share` and self-documentation (#21432, #22598).

2. **AST-aware code understanding** — A recurring theme is using AST parsing to improve file reads, codebase mapping, and method navigation. Expected to reduce token usage and improve accuracy (#22745, #22746).

3. **Deterministic security and sandboxing** — The community continues to push for stronger, default-secure sandboxing (Seatbelt profiles, path trust, variable expansion blocking) rather than reactive mitigations (#19873).

4. **Automated evaluation and quality gates** — The `eval:validate` PR and the "component level evaluations" EPIC (#24353) show a trend toward making eval a first-class CI gate, not just a test suite.

## Developer Pain Points

1. **Agent hangs and infinite loops** — Recurring theme: agents hang indefinitely on simple tasks (#21409) or get stuck in ReAct loops (#28429). The 15-turn limit is a band-aid; root-cause fixes are still in progress.

2. **False success reporting** — Subagents report `GOAL` when they actually hit turn limits or crashed (#22323). Developers cannot trust agent self-reported status.

3. **Tool selection failures** — Agents either fail to use custom skills and sub-agents when relevant (#21968), or use too many tools (>128 causes 400 errors, #24246). Poor tool-selection heuristics frustrate users who invested in custom skills.

4. **Terminal rendering issues** — Shell commands appear stuck post-execution (#25166), output corruption after external editors (#24935), and flicker on terminal resize (#21924). Polishing the TUI remains an ongoing effort.

5. **Platform-specific failures** — Wayland display issues (#21983) and symlink handling gaps (#20079) indicate the agent ecosystem is not fully cross-platform tested.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-07-18

---

## Today's Highlights

A significant wave of 15+ new triage issues surfaced today, primarily centered on **Windows platform stability** (zombie processes, blank TUI, session hangs) and **permission-modeling inconsistencies** (destructive commands bypassing approval, command-identifier parsing bugs). On the positive side, the v1.0.72-1 release shipped important plugin mutation capabilities and UX improvements for plan-approval determinism. However, the community is raising alarms about an **apparent regression** in `task_complete` tool availability in autopilot mode.

---

## Releases

**v1.0.72-1** ([Release Link](https://github.com/github/copilot-cli/releases/tag/v1.0.72-1))

**Added**
- `--plugin`, `--mcp`, and `--skill` flags for plugin mutations
- Skill removal via `copilot plugins remove --skill`

**Improved**
- Full file paths now revealed when expanding compact editing rows
- Plan-approval menu is now deterministic across models
- `/add-dir` directories remain visible

---

## Hot Issues (10 Noteworthy)

1. **[#4163 — Zombie process accumulation under copilot PID](https://github.com/github/copilot-cli/issues/4163)** (NEW, triage)
   - *Why it matters:* Finished subprocesses are not being reaped, with ~2 zombies/minute per session. This is a critical process-management bug that will exhaust OS PID limits on long-lived sessions. Community response is muted (1 comment), likely because it's a newly filed triage.

2. **[#4160 — Plan mode over-blocks read-only shell commands](https://github.com/github/copilot-cli/issues/4160)** (NEW, triage)
   - *Why it matters:* The heuristic gating `powershell`/`shell` tools in plan mode uses naive substring matching, blocking provably read-only commands. This is a fundamental usability issue for plan-mode power users, and the author provided clear repro steps.

3. **[#4159 — Interactive mode turns blank after submitting prompt on Windows Terminal](https://github.com/github/copilot-cli/issues/4159)** (NEW, triage)
   - *Why it matters:* Interactive mode renders normally but goes blank on prompt submission. The non-interactive `-p` mode works fine, suggesting a TUI rendering regression specific to Windows Terminal. This is a showstopper for Windows users.

4. **[#4161 — `task_complete` tool unavailable after switching back to autopilot mode](https://github.com/github/copilot-cli/issues/4161)** (NEW, triage)
   - *Why it matters:* This is a **confirmed regression** of a previously fixed issue (closed as resolved in v1.0.4). The ability to signal task completion in autopilot mode is core to agentic workflows. The community will likely escalate this quickly.

5. **[#4156 — Destructive git branch deletion misclassified, requires no permission](https://github.com/github/copilot-cli/issues/4156)** (NEW, triage)
   - *Why it matters:* `git branch -D` (force delete) runs silently without any permission prompt, while `git push --delete` correctly triggers approval. This is a **security-classification bug** that could lead to accidental data loss. The diagnostic evidence from `/diagnose` is robust.

6. **[#4155 — Gemini models return 400 Bad Request](https://github.com/github/copilot-cli/issues/4155)** (NEW, triage)
   - *Why it matters:* Multiple Gemini model variants (`gemini-3.1-pro-preview`, `gemini-3.5-flash`) fail with 400 on plain text prompts. This blocks an entire model family for users who have configured multi-model setups.

7. **[#4165 — `copilot --resume` hangs on cold start in Windows](https://github.com/github/copilot-cli/issues/4165)** (NEW, triage)
   - *Why it matters:* Sessions become unrecoverable on Windows via the resume flag, while normal interactive startup can resume them. This is a critical workflow disruption for users relying on session persistence.

8. **[#3767 — Oversized attachment permanently wedges session (CLOSED)](https://github.com/github/copilot-cli/issues/3767)** (CLOSED, 7 comments)
   - *Why it matters:* While closed, this issue highlights a hard 5MB CAPI limit with no recovery path. The session becomes permanently stuck, requiring termination. The lack of graceful degradation or recovery UI is a known pain point.

9. **[#4151 — Plugin install fails with `Access is denied` on Windows](https://github.com/github/copilot-cli/issues/4151)** (3 comments)
   - *Why it matters:* 100% failure rate on Windows 11 for all plugin sources (marketplace, GitHub, local). This completely blocks the plugin ecosystem for Windows users.

10. **[#4164 — Large image attachment warning printed 6x](https://github.com/github/copilot-cli/issues/4164)** (NEW, triage)
    - *Why it matters:* While cosmetic, the redundant warning message (`...removed due to size constraints`) printed 6 times suggests a rendering batching bug. Community reaction is mild but the author's frustration is clear.

---

## Key PR Progress

*No pull requests were updated in the last 24 hours (0 items).* This is unusual and may indicate a period of maintainer focus on issue triage or internal stabilization.

---

## Feature Request Trends

Based on open issues updated in the last 24h, the most-requested feature directions are:

| Feature Direction | Frequency | Representative Issues |
|---|---|---|
| **Customizable permissions (path prefixes, command spaces, default users)** | 4 | [#4157](https://github.com/github/copilot-cli/issues/4157), [#4150](https://github.com/github/copilot-cli/issues/4150), [#4166](https://github.com/github/copilot-cli/issues/4166) |
| **Keyboard-friendly TUI navigation (vi-like j/k)** | 2 | [#4152](https://github.com/github/copilot-cli/issues/4152), [#4116](https://github.com/github/copilot-cli/issues/4116) |
| **Multi-root workspace support via `.code-workspace`** | 1 (14👍) | [#1826](https://github.com/github/copilot-cli/issues/1826) — most upvoted open feature request |
| **Allow `-max-ai-credits=0` for local models** | 2 | [#4167](https://github.com/github/copilot-cli/issues/4167), [#4168](https://github.com/github/copilot-cli/issues/4168) |
| **Expose session processing state (queued/active)** | 1 | [#4158](https://github.com/github/copilot-cli/issues/4158) |
| **Custom HTTP headers for BYOK LLM servers** | 1 (8👍) | [#3399](https://github.com/github/copilot-cli/issues/3399) |

The strongest community signal is the demand for **granular permission controls** — users want path-prefix filtering, command-identifier parsing for spaced commands, and the ability to set default user accounts.

---

## Developer Pain Points

1. **Windows Platform Instability (HIGH PRIORITY)**
   - Zombie process leaks ([#4163](https://github.com/github/copilot-cli/issues/4163))
   - Plugin install blocked by OS permissions ([#4151](https://github.com/github/copilot-cli/issues/4151))
   - Interactive TUI goes blank after prompt ([#4159](https://github.com/github/copilot-cli/issues/4159))
   - Session resume hangs on cold start ([#4165](https://github.com/github/copilot-cli/issues/4165))

2. **Permission & Security Confusion**
   - Destructive commands bypass approval ([#4156](https://github.com/github/copilot-cli/issues/4156))
   - Command identifiers with spaces ignored ([#4150](https://github.com/github/copilot-cli/issues/4150))
   - Read-only shell commands incorrectly blocked ([#4160](https://github.com/github/copilot-cli/issues/4160))

3. **Model & Context Gaps**
   - Gemini model family completely broken ([#4155](https://github.com/github/copilot-cli/issues/4155))
   - Context-tier config has no effect until manual model picker usage ([#3762](https://github.com/github/copilot-cli/issues/3762))
   - ASR voice models all fail silently on `/voice` ([#4024](https://github.com/github/copilot-cli/issues/4024))

4. **UI/UX Regressions**
   - `task_complete` tool re-disappeared in autopilot mode ([#4161](https://github.com/github/copilot-cli/issues/4161))
   - TUI text selection broken (no copy-paste) ([#4154](https://github.com/github/copilot-cli/issues/4154))
   - Scheduled prompts stuck queued and never fire ([#4137](https://github.com/github/copilot-cli/issues/4137))

5. **Telemetry & Observability**
   - `copilot -p` mode does not emit OTEL telemetry ([#4169](https://github.com/github/copilot-cli/issues/4169))
   - No exposed session processing state for parent/child coordination ([#4158](https://github.com/github/copilot-cli/issues/4158))

**Summary for maintainers:** Windows users are facing a barrage of platform-specific regressions that collectively make the CLI nearly unusable on that OS. Permission classification bugs (both false negatives and false positives) erode trust in the safety model. The `task_complete` regression is particularly concerning as it suggests the fix from v1.0.4 was not properly validated in the current release pipeline.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date: 2026-07-18**

---

## Today's Highlights

Today's digest is marked by a notable absence of new releases and pull requests, suggesting a period of stabilization or internal development. The community's focus remains on critical unresolved issues, including a persistent regression in model quality related to the K2.5/K2.6 switch, and a significant blocker for Chinese financial users involving a broken Wind plugin dependency. Additionally, platform-specific bugs on Windows (installer crash) and Linux (TUI rendering) continue to hinder user experience.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1.  **[#1925: Kimi K2.5 vs K2.6 Model Switch](https://github.com/MoonshotAI/kimi-cli/issues/1925)**
    - *Author: herrbasan | 13 Comments | Updated: 2026-07-17*
    - **Summary:** A vocal user requests the ability to roll back to the Kimi K2.5 model and its previous system prompt, citing that K2.6's "thinking" mode suppresses creativity, increases hallucinations, and strips the model of its personality.
    - **Why it Matters:** This long-standing issue (opened April 2026) highlights a core product direction conflict. The community is deeply divided on the K2.6 upgrade, and the absence of an official rollback mechanism is a major pain point for users who rely on creative or nuanced outputs. The 13 comments indicate significant ongoing interest and frustration.

2.  **[#2505: Wind (万得) Plugin Dependency Failure](https://github.com/MoonshotAI/kimi-cli/issues/2505)**
    - *Author: Steven-DD | 1 Comment | Updated: 2026-07-17*
    - **Summary:** The `wind-allskill` plugin for Kimi Work Desktop fails entirely on data retrieval (`NETWORK_ERROR`). The root cause is an undeclared dependency (`agent-gw-pysdk`) that is not packaged with the plugin. The installation guide provided by the system directs users to a private internal Git server (`dev.msh.team`) that is unreachable from the public internet.
    - **Why it Matters:** This is a critical, "show-stopping" bug for the Chinese financial analyst community, a core user segment. The failure mode is poor: a missing external dependency is treated as an internal installation error, leading to a confusing user experience. The community is demanding proper dependency bundling or public-facing documentation.

3.  **[#2379: TUI Markdown List Rendering Bug](https://github.com/MoonshotAI/kimi-cli/issues/2379)**
    - *Author: bdragan | 1 Comment | Updated: 2026-07-17*
    - **Summary:** Markdown list items in the Terminal User Interface (TUI) are broken: characters are dropped, and words are incorrectly split across lines when wrapping.
    - **Why it Matters:** This is a fundamental rendering error that degrades the primary user interface for terminal-based workflows (Linux). It's been open since May, suggesting it's either low priority or a complex fix. The single comment indicates limited user engagement, but the impact on readability is high for affected users.

4.  **[#2504: PowerShell `install.ps1` Crash on Windows 5.1](https://github.com/MoonshotAI/kimi-cli/issues/2504)**
    - *Author: lyp1938 | 0 Comments | Updated: 2026-07-17*
    - **Summary:** The official installation script (`install.ps1`) crashes on Windows PowerShell 5.1 with an `IndexOutOfRangeException` during the binary download phase.
    - **Why it Matters:** This affects a large legacy Windows user base still using PowerShell 5.1. A crash during installation is a zero-day friction point, immediately blocking new users and potentially causing frustration during onboarding. The lack of comments suggests it may be an isolated environment issue or a fresh report.

---

## Key PR Progress

No pull requests have been updated in the last 24 hours.

---

## Feature Request Trends

Analysis of recent issues reveals two primary feature request directions:

1.  **Model Rollback & Control:** The most significant feature demand is the ability to switch between model versions (e.g., K2.5 vs. K2.6) and control model behavior (e.g., disabling "thinking" mode). This suggests users value consistency, creativity, and personality over raw reasoning capability.
2.  **Platform Parity & Robustness:** While less explicit, the *absence* of feature requests points to a community focused on fixing core functionality. The dominant trend is a demand for stability, compatibility (especially on Windows/Linux), and functional plugins rather than new flashy features.

---

## Developer Pain Points

The following recurring frustrations are evident from current open issues:

1.  **Plugin Ecosystem Fragility:** The Wind plugin issue (#2505) is a prime example. Dependencies are not bundled, installation instructions point to private/unreachable resources, and error messages are misleading. This creates a poor third-party integration experience for developers and end-users.
2.  **Model Regression Management:** The community feels the impact of model upgrades without a clear rollback path (#1925). This is a common pain point in fast-moving AI tools, and Kimi Code's current state is generating significant negative sentiment.
3.  **Cross-Platform Install & UI Failures:** From a broken `install.ps1` on Windows 5.1 (#2504) to a malformed TUI on Linux (#2379), the CLI consistently suffers from platform-specific fragility. This undermines developer trust, as a robust tool is expected to work seamlessly across major operating systems.
4.  **Slow Resolution of Critical Bugs:** The TUI rendering bug (#2379) has been open since May, and the model quality issue (#1925) since April. The lack of movement on these items suggests a potential bottleneck in the engineering team's capacity or a lack of prioritization for end-user experience bugs over infrastructure or model-side work.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-18

## Today's Highlights
A flurry of activity around **OpenCode 2.0 stability** dominates today's digest, with multiple critical fixes landing for service lifecycle, plugin loading, and streaming reliability. The new desktop UI continues to generate community friction, with five separate reports of missing build/plan mode toggles and agent display issues. On the feature front, **auto-discovery of OpenAI-compatible models** remains the most-requested capability at 182 👍, while SSH remote connections to desktop are gaining significant traction.

## Releases
No new versions were published in the last 24 hours.

## Hot Issues

### 1. Auto-discover models from OpenAI-compatible providers
**#6231** — The top-voted open feature request (182 👍, 21 comments). Users are frustrated by manual model configuration in `opencode.json`, particularly for local providers like LM Studio and llama.cpp where available models change frequently. This is the dominant community ask.

### 2. Plugin Hook for Instant TUI Commands
**#5305** — 19 comments, 14 👍. Proposes a plugin hook that allows registering keyboard-triggered commands that execute without agent involvement. Community discussion focuses on use cases like quick file search, git operations, and clipboard management.

### 3. SSH-based remote server connections
**#7790** — 15 comments, 73 👍. Request for first-class SSH support in the OpenCode desktop app, mirroring VS Code's Remote-SSH workflow. Multiple comments note this is a blocker for adopting the desktop client over the terminal CLI.

### 4. Error: no such column: name
**#31119** — 13 comments, 11 👍. A migration state mismatch bug affecting users returning after version gaps. The database schema has drifted ahead of the migration tracker, blocking app startup. Workaround mentioned: `rm -rf` local state.

### 5. Build/plan mode toggle missing in new UI
**#37430** — 5 comments, 2 👍. Critical regression in v1.18.x: the new UI renders no visible way to switch between build and plan modes. Users report having to revert to old UI layout as a workaround. Related issues #37527 and #37565 suggest this is a systemic problem with the new UI's agent display.

### 6. SchemaError on nested array arguments with Anthropic provider
**#34652** — 5 comments. A provider-specific bug where Anthropic returns nested array parameters as JSON-encoded strings, causing `todowrite` and similar tools to fail hard. Only affects `@ai-sdk/anthropic`; OpenAI/OpenAI-compatible paths work correctly.

### 7. xAI Grok 4.5 generating useless bash tool calls
**#37399** — 4 comments. Grok 4.5 loops generating `$ true` bash calls repeatedly instead of producing text responses. Pattern suggests the model is stuck in a tool-calling loop with no reasoning output.

### 8. Claude Code 400 error while OpenCode CLI works
**#37561** — 2 comments. Claude Code cannot communicate with OpenCode Zen API, returning HTTP 400 on every prompt. Interesting asymmetry: CLI works fine, suggesting an integration or auth-layer issue specific to the Claude Code → Zen API path.

### 9. SSE stream silently dropped mid-response
**#37580** — Just opened today. Subagents freeze mid-response when streaming from ChatGPT models (`gpt-5.6-sol`). No chunk timeout default on the OpenAI path means sessions hang indefinitely, requiring full session interruption.

### 10. New desktop UI brightness values "chosen by a Ringwraith"
**#37428** — 2 comments. Purely cosmetic but emblematic of wider UI complaints: the `opencode` title text is nearly invisible against certain themes. Community member @ars-celare's Tolkien-themed bug title reflects broader sentiment about the new desktop UI polish.

## Key PR Progress

### 1. Per-agent subagent_depth override
**#37226** (@M4buAO) — Adds an optional `subagent_depth` field to per-agent config, allowing fine-grained control over agent recursion depth. Falls back to global → 1 if unset. Still open for review.

### 2. Don't boot full instance for session list
**#37477** (@armancharan) — Performance optimization: `session list` was loading a full OpenCode instance just to query the database, causing unnecessary startup overhead. Closes #37435.

### 3. Preserve prompts during session hydration
**#36433** (@kitlangton) — Fixes V2 TUI dropping the first user prompt during new session hydration. Closes #35988. The submitted prompt now survives through initial and reconnect hydration cycles.

### 4. Bound tool and admitted event payloads via session blobs
**#37559** (@armancharan) — Architectural improvement for V2: moves large event payloads (tool results, image blobs) out of in-memory projections into session-backed blob storage. Closes #36444.

### 5. Add Kiro (AWS) provider
**#20491** (@NachoFLizaur) — Adds bundled plugin for Kiro on AWS. Closes #9165 and #26680. Still open since April — community interest in broader provider support.

### 6. Disable undo without git
**#37578** (opencode-agent[bot]) — Gates session undo/redo and message revert actions on the project having Git initialized. Non-Git projects get disabled controls with explanatory tooltips. Auto-generated by the bot.

### 7. Add LiteLLM provider with auto model discovery
**#14468** (@balcsida) — **Closed yesterday.** Adds native `litellm` provider that auto-discovers models from a LiteLLM proxy at startup. Directly addresses the high-demand feature in #6231, but only for LiteLLM specifically. Closes #13891.

### 8. Fix TUI: bundle parser worker separately
**#37571** (opencode-agent[bot]) — Fixes #37556 where the TUI parser worker source conflicted with OpenTUI 0.4.5's `type: "file"` import. Compiles the worker through a virtual OpenCode-owned entrypoint instead.

### 9. Simplify service registration lease
**#37576** (opencode-agent[bot]) — One of a series of service lifecycle PRs: publishes the managed-service registration once after exact-port bind, shuts down when registration is missing or corrupt. Closely related to #37569 and #37572.

### 10. Fix GitHub reply in triggering review thread
**#37574** (@chAwater) — Fixes #37560: when OpenCode is triggered from an inline `pull_request_review_comment` event, the response now correctly nests in the original review thread instead of creating a new one.

## Feature Request Trends

1. **Provider auto-discovery** → The dominant theme. Issue #6231 (182 👍) captures this perfectly: users want OpenCode to interrogate providers for available models rather than requiring manual config. PR #14468 delivers this for LiteLLM, but the community clearly wants it universal.

2. **Remote desktop** → SSH connectivity for the desktop client (#7790, #33273) is the second-strongest signal. VS Code users expect this as table stakes. The desktop app is "totally useless" without it, per community sentiment.

3. **VSCode Copilot integration** → Issue #27303 asks for an official BYOK extension for VSCode Copilot, leveraging Microsoft's new external language model provider API. This would let OpenCode route models from the Copilot ecosystem.

4. **Plugin system expansion** → Beyond the instant TUI command hook (#5305), there's growing interest in exposing server state to plugins (#37573), and better plugin lifecycle management to avoid version mismatches.

5. **UI polish** → Multiple issues (#37430, #37565, #37428, #37527) converge on the new desktop UI being incomplete. The missing build/plan mode toggle is the most severe functional gap, but contrast/brightness issues suggest the design isn't ready for production.

## Developer Pain Points

1. **Migration state corruption across version jumps** → Issues #31119 and #35403 both describe database migration mismatches. When the CLI auto-updates but plugins or database schemas lag behind, the app becomes unusable. The `__drizzle_migrations` table only tracking 21 of 38 applied migrations is a specific pain point.

2. **Streaming reliability with non-OpenAI providers** → Multiple reports of hangs (#33028, #37580, #37552) where streaming calls never complete or time out. The problem appears across Anthropic, OpenAI-compatible, and custom providers, suggesting a core streaming infrastructure issue in the SDK abstraction layer.

3. **WSL path handling** → Issue #36902 reveals that SSE connections from Windows browsers to WSL servers break because native Windows paths (`C:\Users\...`) aren't converted to WSL paths. Related issues #16680, #15719, #27879, #30895, #33107 show this is a long-standing recurring problem.

4. **Keyboard shortcut conflicts** → Issues #37165 and #37167 report `ctrl+p` and IME-related shortcut problems on Windows. The `ctrl+p` command list mapping stopped working entirely in v1.18.2, while the IME issue means Chinese/Japanese users can't use leader-key shortcuts when their input method is active.

5. **Intel Mac AVX2 crashes** → Issue #24876: older Intel Macs crash with `Illegal instruction: 4` due to AVX2 instruction set incompatibility. The crash happens during dyld initialization, before the app even starts. Zero community engagement suggests this affects a shrinking user base, but it's a hard blocker for those still on older hardware.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-18

## Today's Highlights

The project saw intense activity with 50 issues and 22 PRs updated in the last 24 hours, dominated by critical bug fixes and provider expansions. A major compaction retry fix (#6775) addresses single-point-of-failure summarization, while several PRs add StepFun and expanded Kimi K3 thinking levels. Notably, the team is experimenting with separating generated model data into JSON files (#6765) to reduce repo churn from catalog updates.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **#6747 — API for enhancing agent message markdown** (OPEN, 5 comments)
   Proposes extending the message rendering pipeline so extensions can mutate agent message markdown *after* generation without altering the LLM payload. Community interest centers on best-effort formula rendering.
   *[GitHub](https://github.com/earendil-works/pi/issues/6747)*

2. **#6725 — Copilot pricing for GPT-5.6 models is incorrect** (OPEN, 4 comments)
   Reports that OpenAI cache-write costs are not included in Copilot cost calculations, causing under-reporting by ~$0.50+ per session. Marked **inprogress** — a financial accuracy blocker for enterprise users.
   *[GitHub](https://github.com/earendil-works/pi/issues/6725)*

3. **#6665 — TUI pins a full core while streaming** (OPEN, 3 comments)
   Uncached `Intl.Segmenter` + per-chunk Markdown rebuild causes 100% CPU on one core during streaming. The hot path traces to `Markdown.render → wrap → Intl.Segmenter` with no caching. Marked **inprogress** — affects all long sessions.
   *[GitHub](https://github.com/earendil-works/pi/issues/6665)*

4. **#6748 — Deprecated together.ai models still listed** (CLOSED, 3 comments)
   Five Together.ai models (GLM-5.1, Qwen3-235B, etc.) are officially deprecated but still appear in `pi --list-models`. Marked **no-action** — likely awaiting a catalog refresh.
   *[GitHub](https://github.com/earendil-works/pi/issues/6748)*

5. **#6647 — Compaction fails on single transient stream drop** (OPEN, 2 comments)
   Compaction's summarization call has no retry logic, so a single transient socket "terminated" error fails the entire compaction. **inprogress** — a direct blocker for persistent session reliability.
   *[GitHub](https://github.com/earendil-works/pi/issues/6647)*

6. **#6762 — JSON parse crashes SSE stream on control chars** (CLOSED, 3 comments)
   Literal control characters (e.g., ANSI escape `\x1b`) inside tool-call arguments kill the SSE stream. Hardening `parseJsonWithRepair` is the fix.
   *[GitHub](https://github.com/earendil-works/pi/issues/6762)*

7. **#6761 — Anthropic orphaned tool_use blocks cause 400 errors** (CLOSED, 2 comments)
   Long sessions generate tool_use IDs without matching tool_result blocks, triggering 400 errors. A final repair pass is proposed for `convertMessages`.
   *[GitHub](https://github.com/earendil-works/pi/issues/6761)*

8. **#6727 — Built-in retry does not work with OpenAI API keys** (CLOSED, 2 comments)
   Unlike Claude, OpenAI connections hit an early return that bypasses retry logic, killing sessions on transient drops.
   *[GitHub](https://github.com/earendil-works/pi/issues/6727)*

9. **#6768 — Compaction using Copilot Enterprise not possible** (CLOSED, 2 comments)
   Both OpenAI and Anthropic routes fail under Copilot Enterprise licenses with 421 Misdirected Request and Anthropic errors. **untriaged** — enterprise adoption blocker.
   *[GitHub](https://github.com/earendil-works/pi/issues/6768)*

10. **#6733 — Support Gemini's extra_content thought_signature** (CLOSED, 3 comments)
    Requests round-tripping Gemini's thought signature from `extra_content.google.thought_signature`, currently only handled for OpenRouter's `reasoning_details`. Low community push (3 comments, 1 👍).
    *[GitHub](https://github.com/earendil-works/pi/issues/6733)*

## Key PR Progress

1. **#6775 — Retry on compaction/branch summarization retryable failures** (OPEN)
   Adds retry logic for transient failures in compaction and branch summarization, directly fixing #6647. Author asks whether UI indication of retries is needed.
   *[GitHub](https://github.com/earendil-works/pi/pull/6775)*

2. **#6765 — Separate generated model data** (CLOSED)
   Extracts generated model values into separate JSON files while retaining the TypeScript catalog structure — a significant reduction in repo churn for catalog updates.
   *[GitHub](https://github.com/earendil-works/pi/pull/6765)*

3. **#6786 — Expose Kimi Coding K3 effort levels** (OPEN)
   Adds `low`, `high`, and `max` thinking levels for Kimi K3 (previously `max` only), with regression coverage for both Kimi Coding and Moonshot endpoints.
   *[GitHub](https://github.com/earendil-works/pi/pull/6786)*

4. **#6783 — Add StepFun providers** (CLOSED)
   Adds four native StepFun providers (`stepfun`, `stepfun-ai`, `stepfun-step-plan`, `stepfun-cn-step-plan`) with two different base URLs for China/global routing.
   *[GitHub](https://github.com/earendil-works/pi/pull/6783)*

5. **#6779 — Support freeform tool calls** (CLOSED)
   Adds typed JSON and freeform tool definitions across AI and agent APIs, supports OpenAI custom tool calls and legacy JSON tool-call replay.
   *[GitHub](https://github.com/earendil-works/pi/pull/6779)*

6. **#6730 — Preserve compaction queue behavior** (CLOSED)
   Fixes compaction-queued messages losing steering/follow-up behavior on flush. Also lets `AgentSession.prompt()` start a new run when idle or queue into active runs.
   *[GitHub](https://github.com/earendil-works/pi/pull/6730)*

7. **#6778 — Preserve extension provider auth during availability refresh** (CLOSED)
   Fixes a regression where `runAvailabilityRefresh()` clears provisional auth entries created by `registerProvider()`, causing "Provider is not configured" errors after startup.
   *[GitHub](https://github.com/earendil-works/pi/pull/6778)*

8. **#6771 — Speed up external editor launch** (CLOSED)
   Uses `mkdtemp` instead of writing directly to `os.tmpdir()` for external editor files, improving launch speed when `/tmp` has many entries.
   *[GitHub](https://github.com/earendil-works/pi/pull/6771)*

9. **#6731 — Do not highlight read errors** (CLOSED)
   Skips syntax highlighting for failed `read` results (e.g., out-of-range offset errors), preventing confusing garbled output.
   *[GitHub](https://github.com/earendil-works/pi/pull/6731)*

10. **#6790 — Clear inverted cursor on exit** (CLOSED)
    Fixes a cosmetic issue where a reverse-video cursor character remains on the prompt line after exit, creating a "dual cursor" appearance.
    *[GitHub](https://github.com/earendil-works/pi/pull/6790)*

## Feature Request Trends

- **Enhanced Message Rendering**: Multiple issues request extension hooks to mutate agent message rendering (markdown, collapse states, formula rendering) without affecting LLM payloads (#6747, #5137).
- **Provider/Model Expansion**: Strong demand for new providers (StepFun #6783), expanded thinking levels (Kimi K3 #6786, #6769), and support for Gemini thought signatures (#6733).
- **Config & Env Overrides**: Users want environment-variable overrides for default model/provider (#6777) and more config-sync reliability between machines (#6214).
- **Long-Context Pricing**: Several Copilot pricing issues (#6725, #6668) indicate users need accurate cost tracking across all tiers and models.

## Developer Pain Points

1. **Transient Failure Propagation**: Compaction, summarization, and API retries all fail on single transient drops (#6647, #6727) — the most recurring reliability complaint.
2. **TUI Performance During Streaming**: Uncached segmenter + per-chunk Markdown rebuild causes 100% core usage (#6665), directly degrading the primary user experience.
3. **Provider Auth & Config Fragility**: Extension provider auth gets cleared on refresh (#6778), crash logs ignore custom home directories (#6652), and config sync between machines is unreliable (#6214).
4. **Tool Call Edge Cases**: Control chars in arguments crash SSE (#6762), orphaned tool_use blocks cause 400 errors (#6761), and massive tool partial updates freeze the TUI via `Promise.all` (#6755).
5. **Deprecated Model Pollution**: Several issues (#6748, #6740) highlight outdated models still listed in `--list-models` and incorrect thinking level mappings, creating user confusion about available features.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-18

## Today's Highlights

The Qwen Code daemon architecture is undergoing a major evolution this week, with **multi-workspace support** moving from RFC to active implementation across several PRs and issues. Meanwhile, the **Explore subagent hang bug** (Issue #7126) has been quickly addressed, and the new **Fleet Shepherd CI workflow** (PR #7142) promises to dramatically reduce manual PR maintenance overhead. A nightly release (`v0.19.11-nightly`) shipped with cold-start tracing hooks.

---

## Releases

**v0.19.11-nightly.20260718.767a32484**
- **Key change:** `feat(daemon): Trace cold first-session startup` (PR #6907 by @doudouOUC) — adds instrumentation to capture the daemon's cold boot and first-session latency, directly addressing the long-standing performance tracking Issue #4748.
- **Fix:** `fix(serve): Harden multi-workspace ownership` — a proactive stability fix for the in-flight multi-workspace work.

---

## Hot Issues (Top 10)

### 1. [#6378 — RFC: Support multiple workspaces in one qwen serve daemon](https://github.com/QwenLM/qwen-code/issues/6378)
- **Votes:** 0 | **Comments:** 29
- **Why it matters:** The most-discussed issue this week. Proposes breaking the current `1 daemon = 1 workspace` model. The community is actively debating session ownership, path semantics, and backward compatibility. This is the foundational RFC driving the current wave of workspace-related PRs.

### 2. [#7040 — RFC: Reliable auto-memory recall — timing, quality, and telemetry](https://github.com/QwenLM/qwen-code/issues/7040)
- **Votes:** 0 | **Comments:** 6
- **Why it matters:** Narrowed scope after maintainer feedback — now focuses on recall-path improvements for all users (not enterprise governance). Three independently reviewable roadmap items. Signals a pragmatic, iterative approach to memory.

### 3. [#4748 — Optimize daemon cold start and qwen serve fast-path latency](https://github.com/QwenLM/qwen-code/issues/4748)
- **Votes:** 0 | **Comments:** 6
- **Why it matters:** The parent issue for the cold-start tracing landed in today's nightly. The original gap (2.5s daemon vs 0.7s CLI) has been partially closed; now tracks remaining work.

### 4. [#7051 — VS Code side plugin error (ACP launch failure)](https://github.com/QwenLM/qwen-code/issues/7051)
- **Votes:** 0 | **Comments:** 6
- **Why it matters:** Affects Windows/Linux users. ACP CLI fails to start within VS Code due to Electron/Chromium arguments leaking. Closely related to #7101 (Linux-specific `ELECTRON_RUN_AS_NODE` issue). High community visibility.

### 5. [#6809 — Ctrl+S diff preview garbled for multi-line edits](https://github.com/QwenLM/qwen-code/issues/6809)
- **Votes:** 0 | **Comments:** 4
- **Why it matters:** A rendering bug that concatenates lines in permission dialogs, making diffs unreadable. Blocks trust in edit confirmations. Closed, awaiting fix merge.

### 6. [#7096 — Main CI failed: E2E Tests](https://github.com/QwenLM/qwen-code/issues/7096)
- **Votes:** 0 | **Comments:** 4
- **Why it matters:** One of multiple CI failures this week (see also #7086, #7111). Indicates ongoing E2E test flakiness. Automatically labeled for agent triage.

### 7. [#6992 — Chained MCP calls fail silently on Windows](https://github.com/QwenLM/qwen-code/issues/6992)
- **Votes:** 0 | **Comments:** 3
- **Why it matters:** Two critical bugs: silent MCP chain failures and a stuck permission UI on Windows. Blocks multi-MCP workflows. No resolution yet.

### 8. [#6806 — Status line context percentage doesn't refresh after /compress](https://github.com/QwenLM/qwen-code/issues/6806)
- **Votes:** 0 | **Comments:** 3
- **Why it matters:** A UX annoyance — users cannot see actual token savings after compression until the next request. Tagged `welcome-pr` for community contribution.

### 9. [#4586 — Ctrl+C in PyCharm terminal causes unintended exit](https://github.com/QwenLM/qwen-code/issues/4586)
- **Votes:** 0 | **Comments:** 3
- **Why it matters:** Long-standing (May 2026) signal-handling issue. Single Ctrl+C now exits immediately instead of requiring two presses. Frustrating for IDE terminal users.

### 10. [#7126 — Explore subagent hangs forever with ask_user_question](https://github.com/QwenLM/qwen-code/issues/7126)
- **Votes:** 0 | **Comments:** 1
- **Why it matters:** A read-only subagent blocking multi-agent pipelines. Fixed within 24 hours (PR #7133). Excellent turn-around demonstrates responsive maintainership.

---

## Key PR Progress (Top 10)

### 1. [#7142 — ci(shepherd): Add Fleet Shepherd](https://github.com/QwenLM/qwen-code/pull/7142)
- **Author:** @wenshao | **Status:** OPEN
- **What it does:** A scheduled janitor workflow that runs every 15 minutes to unblock bot-PR fleet: merge conflicts trigger autofix, CI failures trigger rerun, stale reviews trigger re-review. Aims to eliminate human shepherding burden.

### 2. [#7123 — fix(acp): resolve textual @ image paths](https://github.com/QwenLM/qwen-code/pull/7123)
- **Author:** @yiliang114 | **Status:** OPEN
- **What it does:** Enables ACP sessions to resolve `@/path/to/image.png` references to actual workspace images for Vision Bridge processing, with proper ignore-rule filtering.

### 3. [#7054 — feat(web-shell): git status chip, visual working-tree diff, sidebar git status](https://github.com/QwenLM/qwen-code/pull/7054)
- **Author:** @wenshao | **Status:** OPEN
- **What it does:** Brings live Git dirty-state awareness to the Web Shell — status chip, working-tree diff viewer, and sidebar. A significant UX improvement for browser-based sessions.

### 4. [#6561 — feat(web-shell): add workspace Goals page, fix /goal loss on daemon resume](https://github.com/QwenLM/qwen-code/pull/6561)
- **Author:** @wenshao | **Status:** OPEN
- **What it does:** Visual `/goal` surface and fixes a critical bug where goals were silently lost on daemon session resume. Long-running PR (9 days) still open — likely nearing completion.

### 5. [#7053 — refactor(core): Classify shell safety as read-only, write, or unknown](https://github.com/QwenLM/qwen-code/pull/7053)
- **Author:** @doudouOUC | **Status:** OPEN
- **What it does:** Three-state shell classification engine (`read-only > write > unknown` precedence). Foundation for smarter permission prompts. Large architectural change.

### 6. [#7140 — fix(cli): correct misspelled migratedInMemorScopes](https://github.com/QwenLM/qwen-code/pull/7140)
- **Author:** @chinesepowered | **Status:** OPEN
- **What it does:** Fixes a typo (`migratedInMemorScopes` → `migratedInMemoryScopes`) across all references. Small but prevents subtle runtime bugs in memory scope migration.

### 7. [#7127 — ci(autofix): fan out review targets and stop route-scan starvation](https://github.com/QwenLM/qwen-code/pull/7127)
- **Author:** @wenshao | **Status:** OPEN
- **What it does:** Makes autofix review loop concurrent — emits all eligible PRs as matrix targets instead of single-file processing. Prevents backlog starvation on busy repos.

### 8. [#7052 — fix(core): make the per-turn tool-call cap adaptive](https://github.com/QwenLM/qwen-code/pull/7052)
- **Author:** @wenshao | **Status:** CLOSED
- **What it does:** Dynamically adjusts tool-call limits per turn based on context. Merged. Important for preventing runaway agent loops while allowing legitimate multi-tool workflows.

### 9. [#7133 — fix(core): remove ask_user_question from Explore agent's toolset](https://github.com/QwenLM/qwen-code/pull/7133)
- **Author:** @zjunothing | **Status:** CLOSED
- **What it does:** Direct fix for #7126. Removes the blocking `ask_user_question` from the read-only Explore agent. Merged same day as bug report. Exemplary response time.

### 10. [#6945 — feat(cli): add daemon Todo stop guard](https://github.com/QwenLM/qwen-code/pull/6945)
- **Author:** @doudouOUC | **Status:** OPEN (in-review)
- **What it does:** Opt-in daemon-only guard that auto-continues work chains after `todo_write` (max 2 continuations) instead of silent stop. Prevents unfinished tasks from dropping without warning.

---

## Feature Request Trends

1. **Multi-workspace daemon** (#6378, #7015, #7102, #7070, #7071, #7069): The single strongest trend. Requesting support for multiple projects per daemon process, with workspace-scoped APIs, session ownership semantics, and folder picker UX. This is the community's top architectural priority.

2. **Memory & context improvements** (#7040, #6806): Reliable auto-memory recall with timing/quality telemetry, plus fixing context percentage refresh after compression. Users want smarter, more observable memory management.

3. **MCP (Model Context Protocol) enhancements** (#6992, #7103): Both bug fixes (Windows silent failures, stuck UIs) and new features (workspace-scoped observed contacts). MCP is growing in importance as a multi-tool orchestration layer.

4. **UI/UX polish for Web Shell** (#7102, #7128, #7054, #6561): Persistence of errors, path autocomplete, Git integration, and goals pages. The Web Shell is rapidly maturing toward feature parity with CLI.

5. **Tool description & path formatting** (#7007, #7110): Unified `formatDisplayPath()` utility and compact tool summaries with active path hints. Small but cumulative improvements to terminal readability.

---

## Developer Pain Points

1. **CI instability on main branch**: Three separate E2E test failures in 24 hours (#7096, #7086, #7111). Flaky tests are blocking merges and creating noise. The Fleet Shepherd (#7142) and autofix fan-out (#7127) are direct responses.

2. **VS Code Companion / ACP launch failures** (#7051, #7101): Electron environment leakage. Different root causes on Windows vs Linux. High-impact because it blocks all AI features for affected users.

3. **Subagent deadlocks in multi-agent pipelines** (#7126, #7122): `ask_user_question` in read-only agents causes hangs. Fix was quick (#7133), but the architectural pattern needs hardening.

4. **Terminal signal handling regressions** (#4586, #6776): Ctrl+C behavior changes between versions — unintended exits, garbled terminal state. PyCharm and generic terminal users are affected.

5. **Windows-specific MCP bugs** (#6992): Silent failures in chained calls, stuck permission dialogs. Windows remains a second-class platform for MCP workflows.

---

*Next digest: 2026-07-19*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-18

**Project:** Hmbown/DeepSeek-TUI (CodeWhale)  
**Date:** 2026-07-18  

---

## Today's Highlights

The v0.9.1 release cycle is accelerating with a batch of runtime reliability fixes and platform expansion PRs. The team is closing critical Windows hook leaks and macOS Dropbox sandbox issues while adding native Windows ARM64 and HarmonyOS/OpenHarmony builds. Meanwhile, the community continues to push for better model provider diversity, with Kimi K3 and OpenCode Go/Zen support remaining high-demand items.

---

## Releases

No new releases in the last 24 hours. The prior release remains **v0.9.3**, with v0.9.1 patch fixes being actively prepared.

---

## Hot Issues

1. **#4032** — [Codewhale not following the constitution](https://github.com/Hmbown/CodeWhale/issues/4032)  
   *35 comments.* Codewhale consistently writes its own temporary scripts instead of using user-provided ones, then justifies the behavior when challenged. This is a core autonomy/alignment bug that erodes user trust.

2. **#3275** — [CodeWhale overly involved in self-questioning/self-answering](https://github.com/Hmbown/CodeWhale/issues/3275)  
   *17 comments.* A regression from #3061. The agent enters a self-driven loop of proposing, answering, and executing without user confirmation — a critical UX failure for a tool that should be user-directed.

3. **#3192** — [Put it up for agentclientprotocol/registry](https://github.com/Hmbown/CodeWhale/issues/3192)  
   *12 comments.* Request to get CodeWhale listed in the agentclientprotocol registry for easier Zed editor integration. Community interest in IDE ecosystem compatibility is strong.

4. **#1481** — [Support OpenCode Go/Zen](https://github.com/Hmbown/CodeWhale/issues/1481)  
   *9 comments, 1 👍.* Users want OpenCode Go/Zen provider support for cheap DeepSeek-V4 access. This remains a top community request despite being open since May.

5. **#4479** — [TUI rendering glitch — missing/extra spaces](https://github.com/Hmbown/CodeWhale/issues/4479)  
   *4 comments.* Intermittent rendering artifacts on Windows Terminal. Selecting affected text with the mouse restores correct rendering. Workaround exists but no root cause identified.

6. **#4100** — [exec_shell fails with exit code 2147483647](https://github.com/Hmbown/CodeWhale/issues/4100)  
   *4 comments.* Catastrophic failure in long-running Windows sessions with exit code `i32::MAX`. Likely a ConPTY resource leak or handle exhaustion. Blocks long-lived workflows.

7. **#4489** — [Hooks process leak on Windows](https://github.com/Hmbown/CodeWhale/issues/4489)  
   *4 comments.* Hook commands that inherit stdin without EOF leak Node.js processes. The timeout only kills the intermediate `cmd.exe`, leaving grandchild `node.exe` processes orphaned.

8. **#4417** — [Add first-class Kimi OAuth device login](https://github.com/Hmbown/CodeWhale/issues/4417)  
   *5 comments.* Proposed OAuth/device-login flow for Moonshot AI Kimi, separate from API-key config. Complements #4387 (Kimi K3 model support). High priority for provider diversity.

9. **#4410** — [Restore xAI device-code OAuth login](https://github.com/Hmbown/CodeWhale/issues/4410)  
   *3 comments.* xAI device login currently fails with a hard-coded wrong API path. The Grok CLI uses `/oauth2/device`, CodeWhale uses `/oauth2/device/code`. Release-blocker for v0.9.1.

10. **#3927** — [Onboarding: API-key step is a hard DeepSeek-only gate](https://github.com/Hmbown/CodeWhale/issues/3927)  
    *2 comments.* First-run users cannot skip or bypass the DeepSeek API-key step, even if they want another provider or just to explore. Esc jumps two steps back. Poor newcomer experience.

---

## Key PR Progress

1. **#4498** — [fix(tui): make Ctrl+O inspector complete and draft-safe](https://github.com/Hmbown/CodeWhale/pull/4498)  
   Routes Ctrl+O to the full turn inspector even when a draft exists; moves external-editor access to Ctrl+Shift+O. Preserves complete assistant results in pager. *(OPEN)*

2. **#4506** — [feat(release): publish native Windows ARM64 artifacts](https://github.com/Hmbown/CodeWhale/pull/4506)  
   Adds native Windows ARM64 binaries (`codewhale`, `codew`, `codewhale-tui`) plus standard/portable ZIPs. Updates npm, updater, docs, and the website install UI. *(OPEN)*

3. **#4505** — [fix(auth): isolate xAI device login from Tokio](https://github.com/Hmbown/CodeWhale/pull/4505)  
   Runs synchronous reqwest device discovery on Tokio's blocking pool; fixes hard-coded API path mismatch. Includes multi-thread Tokio runtime requirement. *(OPEN)*

4. **#4504** — [fix(onboarding): support keyless and guided provider setup](https://github.com/Hmbown/CodeWhale/pull/4504)  
   Lets first-run users continue with empty credentials for local providers (SGLang, vLLM, Ollama). Preserves explicit local-server authentication. *(OPEN)*

5. **#4500** — [feat(auto): surface routing scope and per-turn receipts](https://github.com/Hmbown/CodeWhale/pull/4500)  
   Records typed Auto routing receipts with provider pairs, selected tiers, and reasons. Carries receipt through dispatch and turn inspector. *(OPEN)*

6. **#4491** — [fix(runtime): contain hooks and preserve Windows PTY status](https://github.com/Hmbown/CodeWhale/pull/4491)  
   Fixes the verified hook leak (#4489) and removes the lossy exit-status sentinel blocking #4100 diagnosis. *(CLOSED, merged)*

7. **#4490** — [fix(mcp): align configured command health with spawn](https://github.com/Hmbown/CodeWhale/pull/4490)  
   Resolves bare MCP stdio commands against the same expanded environment used by real spawn. Fixes false health-report mismatches. *(CLOSED, merged)*

8. **#4470** — [fix(ohos): generate QuickJS bindings and gate unsupported PTY tools](https://github.com/Hmbown/CodeWhale/pull/4470)  
   Enables rquickjs bindgen for HarmonyOS/OpenHarmony; omits portable-pty from OHOS dependency graph while retaining `exec_shell`. *(CLOSED, merged)*

9. **#4502** — [fix(tui): clear stable 1.96 Clippy blockers](https://github.com/Hmbown/CodeWhale/pull/4502)  
   Removes redundant `return` and restores stable Rust 1.96 Clippy release gate. *(CLOSED, merged)*

10. **#4499** — [fix: close v0.9.1 MCP and Fleet truth gaps](https://github.com/Hmbown/CodeWhale/pull/4499)  
    Makes MCP adapter approval semantics exact in sub-agents; distinguishes current-session status from configuration. *(CLOSED, merged)*

---

## Feature Request Trends

The most requested feature directions from the issue tracker include:

- **Provider Diversity**: Strong demand for OpenCode Go/Zen (#1481), Kimi K3 (#4387), and OpenAI Codex OAuth (#2984). Users want choice beyond DeepSeek.
- **Platform Expansion**: Native Android/Termux support (#4236, #4242) and Windows ARM64 (#4506) are active work items. HarmonyOS/OpenHarmony builds (#4470) are also progressing.
- **Ecosystem Integration**: Requests to be listed in agentclientprotocol/registry for Zed compatibility (#3192) and concerns about unauthorized VSCode extensions (#2327).
- **Localization**: Korean, Spanish, Brazilian Portuguese (#3093), and Russian (#3092) README/website translation requests remain open.
- **Observability**: Users want visible routing decisions in Auto mode (#4405, #4500), per-turn tool budgets (#4415), and better provider health distinction (#4406).
- **Onboarding UX**: Multiple requests for keyless evaluation paths and guided multi-provider setup (#3927, #4504).

---

## Developer Pain Points

- **Agent Autonomy vs. User Intent**: Issues #4032 and #3275 highlight a recurring frustration — Codewhale creating its own scripts, self-proposing tasks, and over-extending scope without confirmation. This is the single biggest trust issue.
- **Windows Reliability**: Windows-specific pain continues: ConPTY crashes with exit code `2147483647` (#4100), hook process leaks (#4489), and TUI rendering glitches (#4479). These block production use on the dominant platform.
- **macOS Sandbox/File Provider**: Dropbox CloudStorage paths are inaccessible on macOS (#4085) due to File Provider restrictions — a blocker for users with cloud-synced workspaces.
- **Onboarding Friction**: The API-key gate (#3927) forces DeepSeek-specific signup before any exploration — a significant barrier for new or evaluation-oriented users.
- **Stale Issue Backlog**: The project acknowledges a cleanup problem (#3089) with duplicate requests and zombie issues, though a policy is being implemented to close waiting/inactive items.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*