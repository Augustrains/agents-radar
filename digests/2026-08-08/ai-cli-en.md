# AI CLI Tools Community Digest 2026-08-08

> Generated: 2026-08-08 00:41 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Developer Tools Comparison Report

**Date:** 2026-08-08

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem is maturing rapidly, with seven major players shipping releases, hardening security, and expanding platform coverage simultaneously. The landscape is bifurcating between **enterprise-focused platforms** (Claude Code's self-hosted runners, GitHub Copilot's enterprise policy controls) and **community-driven, open-source tools** (Kimi, OpenCode, DeepSeek TUI) racing to close feature parity gaps. Cross-cutting concerns dominate: **Windows stability, session lifecycle reliability, MCP/hybrid tooling robustness, and subagent orchestration trust** are the top community pain points across all tools. While feature velocity remains high (multiple releases per day at the top end), the volume of open, unaddressed high-signal issues suggests maintainers are prioritizing new capabilities over backlog triage. The market is consolidating around a core competency: reliable, predictable agentic execution without data loss, permission bypasses, or silent failures.

---

## 2. Activity Comparison

| Tool | Issues (Hot/Active) | PRs (Key/Merged) | Release Status | Release Cadence |
|---|---|---|---|---|
| **Claude Code** | 10 hot issues; #13354 (191👍, 73 comments) | 3 notable PRs (security hardening) | v2.1.224 stable | Steady, feature-rich |
| **OpenAI Codex** | 10 hot issues; #14599 (57👍), #26234 (41👍) | 10+ PRs (infrastructure focus) | v0.147.0 + pre-release alphas | Very high, iterative |
| **Gemini CLI** | 10 hot issues; multiple P1s on subagent reliability | 10 PRs (security: SSRF fix, Docker upgrades) | v0.54.4, v0.55.0-preview.2, nightly | Moderate, patch-heavy |
| **GitHub Copilot CLI** | 10 hot issues; #4118 (35👍), #1632 (23👍) | 0 PRs in last 24h | v1.0.79-7 → v1.0.79-9 (3 in 24h) | Very high, hotfix-driven |
| **Kimi Code** | 2 critical reliability issues | 2 competing PRs on data corruption fix | No release in last 24h | Quiet; pending fixes |
| **OpenCode** | 10 hot issues; billing complaints dominant | 10+ PRs (TUI/desktop, environment drivers) | v1.18.15 stable | Moderate, feature-focused |
| **Pi** | 10 hot issues; lifecycle bugs dominant | 10 PRs (session/recovery refactor) | v0.84.1 stable | Moderate, refactor-heavy |
| **Qwen Code** | 10 hot issues; Windows/UI bugs | 10 PRs (Web Shell, security guards) | v0.21.7-nightly | Moderate, nightly-only |
| **DeepSeek TUI** | 10 hot issues; subagent timeouts | 10 PRs (release blockers, bug fixes) | v0.9.4 pending (CI blockers cleared) | Slow, release-blocked |

**Notable:** GitHub Copilot CLI shipped 3 releases in 24h and Claude Code shipped self-hosted infrastructure in a single version — the speed differential between enterprise-backed and community-driven tools is widening.

---

## 3. Shared Feature Directions

**High-priority, cross-tool demands (appearing in 3+ communities):**

| Feature Need | Tools | Community Signal |
|---|---|---|
| **Session continuity & lifecycle** | Claude Code (#13354, 191👍), OpenCode (#41146), Pi (#6879), DeepSeek TUI (#2934) | Users feel cut off mid-workflow; want durable, resumable, restorable state |
| **Subagent/agent reliability & observability** | Gemini CLI (#22323, #21409), DeepSeek TUI (#1425), Pi (#5886), Claude Code (#84625) | False success reporting, indefinite hangs, permission bypasses — trust barrier #1 |
| **Granular permission/trust control** | Claude Code (#14920, 83👍), OpenAI Codex (#14599, 57👍), Kimi (#2596), OpenCode (#40183) | All-or-nothing trust models are failing; users want per-skill, per-directory, per-operation control |
| **MCP robustness & secret management** | OpenAI Codex (#26234, 41👍), Copilot CLI (#4392), Qwen (#8550), Pi (#7702) | Zombie processes, namespace flattening for third-party providers, env/secret config surfaces |
| **Windows platform parity** | Codex (#10090, #37043), Copilot CLI (#3622), Qwen (#8615, #8625), OpenCode (#6560) | Sandboxing, clipboard, IME, terminal rendering — consistent failure cluster |
| **Sandbox/security hardening** | Gemini CLI (SSRF fix, CVSS 8.6), Kimi (#2596 rm-rf), Qwen (#8687 git guard), Copilot (enterprise proxy policy) | Web-fetch SSRF, destructive op prevention, cross-worktree git mutations, deny-rule evasions |
| **Token/cost transparency** | OpenCode (#41146), Copilot CLI (#2947), Pi (#6879), DeepSeek TUI (#5257) | Quota exhaustion surprises, per-session token reports, model tier auto-selection |
| **Provider/model flexibility** | Codex (#26234), Pi (#7702, #7762), OpenCode (#40409, #24334), DeepSeek TUI (#5034) | Third-party parity, per-provider protocol bugs (reasoning_content, thinking blocks), model self-identification mismatches |
| **Byte-level file safety/atomicity** | Kimi (#2591, #2594, #2595), Qwen (#8695), Pi (#7780) | Silent corruption, lossy UTF-8 decoding, read-modify-write hazards |
| **TUI/terminal rendering stability** | Copilot CLI (#4311), Qwen (#8562, #8672), OpenCode (#6560), Pi (#7740) | Blank transcripts, flickering, broken mouse selection, custom renderer losses |

---

## 4. Differentiation Analysis

| Tool | Core Focus | Target User | Technical Approach | Key Differentiator |
|---|---|---|---|---|
| **Claude Code** | Full-stack agentic development, mobile/web/desktop | Enterprise teams, TUI power users | Self-hosted runners, plugin architecture, `archive` plugin source | Enterprise infrastructure depth; session continuity gap is top friction |
| **OpenAI Codex** | Unified agent + IDE + chat surface | OpenAI-platform users, VS Code developers | Rust core, code-mode host protocols, Agent Plugins, MCP-first | Rapid iteration; but third-party provider parity (MCP flattening) is a glaring gap |
| **Gemini CLI** | Google-model agentic coding | Google Cloud/Gemini users | Caretaker bot for issue triage, OS-level sandboxing proposals, auto-memory (client-side) | Auto-memory and Caretaker are ahead; but subagent reliability erodes trust |
| **GitHub Copilot CLI** | Enterprise developer workflow integration | GitHub/VS Code enterprise users | Everything-as-extension, enterprise policy (`allow-auto-only`, managed sandbox proxy), Agent Plugins under `com.github.copilot` | Compliance/enterprise feature velocity (3 releases/24h); Windows stability is the drag |
| **Kimi Code** | Lightweight agentic coding (Moonshot models) | Cost-sensitive, YOLO-mode enthusiasts | Read-only/write tool contracts, minimal TUI, model auto-tier selection | Community-driven safety fixes; but 2 critical reliability bugs expose immaturity |
| **OpenCode** | TUI + desktop + web for open models | Multi-provider, BYO-model users | Go backend, Go billing infra, native Mermaid rendering, Modal driver, background subagents | Cross-provider flexibility; but billing transparency and provider drift issues are alienating paid users |
| **Pi** | Elixir-based, IDE/CLI agent runtime | Open-source extensibility-focused users | Harness v2 recovery model, incremental markdown parsing, provider breadth (Cursor bridge, LM Studio) | Strongest session-recovery refactor; but long-session performance and lifecycle bugs remain |
| **Qwen Code** | Chinese-language-first agentic CLI | Alibaba/Qwen ecosystem, CJK users | Web Shell as unified surface, tmux-backed subagents, Wayland clipboard support, OTel-aligned telemetry | Web Shell consolidation is a bold bet; but Windows IME/installer issues are persistent |
| **DeepSeek TUI** | DeepSeek-model fleet orchestration | DeepSeek power users, multi-model fleets | Mixed-fleet architecture (any model any role), exec-policy deny rules, `model=auto` tier selection | Fleet/roster vision is unique; but subagent timeout fragility and release-blocking CI are chronic |

---

## 5. Community Momentum & Maturity

**Most Active (High velocity, high community engagement):**
- **Claude Code** — Highest engagement (#13354 with 191👍), largest community, but slow to respond to top requests → **mature but at risk of goodwill erosion.**
- **OpenAI Codex** — Busiest PR pipeline (10+ per day), strong community momentum, but third-party parity gap (#26234, 41👍) is a structural weakness → **rapidly iterating, early-trust stage.**
- **GitHub Copilot CLI** — Fastest release cadence (3 releases/24h), but zero PRs in the digest → **focused on stability over new features; community perceives non-determinism.**

**Moderately Active (Healthy, but with clear friction points):**
- **OpenCode** — High issue engagement, especially on billing (45 comments on #38257); features shipping but trust in Go billing is the top drag.
- **Qwen Code** — Fast feature pace (Web Shell, OTel, tmux subagents), but nightly-only releases and Windows UX gaps hold back mainstream adoption.
- **Gemini CLI** — Community is engaged, but P1 subagent reliability issues (#22323, #21409) and slow backlog triage are eroding user patience.

**Slower / Reliability-Limited (High signal, but velocity constrained):**
- **Pi** — Deep architectural work (recovery-state refactor), but session lifecycle bugs (#6879, #7020) and Node version incompatibilities (#7771) are blocking users.
- **DeepSeek TUI** — Release train was blocked by CI for multiple runs; community discussion is rich (50 threads) but shipping is slow.
- **Kimi Code** — Quiet on releases, but community surfaced 2 critical bugs (data corruption, rm-rf deletion) — maturity risk is highest here.

**Community Sentiment Summary:** The "big three" (Claude, Codex, Copilot) are racing on enterprise + infrastructure features, but all three are accumulating high-signal unaddressed issues (191👍, 57👍, 54👍 without responses). The open-source tools (Pi, DeepSeek, Kimi) are doing deeper reliability work but shipping slower. The most consistent frustration across ALL tools is **silent failures** — agents that hang, misreport success, corrupt data, or leak resources without any user-visible signal.

---

## 6. Trend Signals

**For Developers (adoption & workflow planning):**
1. **Windows is the weakest link everywhere** — sandboxing, clipboard, IME, installer, terminal rendering: pick your tool based on your OS at your own risk.
2. **Subagent orchestration is not yet trustworthy** — hover stops (Gemini), false success (Gemini), timeouts (DeepSeek), zombie processes (Codex), session resets (Pi): run long-running delegated tasks with extreme caution.
3. **Session continuity is the #1 UX gap** — whether it's session limits (Claude), post-compaction stalls (Pi), resume model resets (Copilot), or re-auth loops (OpenCode), the ability to pick up where you left off is the most requested feature across the board.
4. **Permission granularity is a hard requirement** — the era of YOLO mode is over; users across Kimi, Claude, Codex, and Qwen are demanding per-skill, per-directory, per-operation control and audit trails.
5. **Provider protocol quirks are a tax** — DeepSeek `reasoning_content`, Bedrock thinking blocks, Gemini `thought_signature`, and model self-identification mismatches create constant workarounds; prefer tools that abstract or paper over these differences.

**For Tool Maintainers (ecosystem direction):**
6. **Byte-level safety is table stakes** — silent corruption (Kimi #2591), grep OOM (Claude #82179), and crash-triggering prefetches (Codex #35799) are unacceptable; transactional file edits and strict refusal are the community's expected baseline.
7. **Security hardening is the next differentiator** — SSRF in web-fetch (Gemini, CVSS 8.6), symlink credential overwrites (Claude), deny-rule evasions (DeepSeek), cross-worktree git mutations (Qwen) — look for tools that proactively demonstrate secure-by-default engineering.
8. **Billing/usage transparency is a trust issue** — OpenCode's 401/quota exhaustion stories and Codex's silent 6% weekly rate-limit consumption show that metering must be visible, accurate, and auditable.
9. **Cross-tool standards are converging** — ACP (context usage updates in Qwen), OpenTelemetry (session lifecycle in Qwen), and Agent Plugins (Copilot, Codex, Claude) are the emerging shared vocabularies; tools that adopt these will win integration points.
10. **The "mixed fleet" pattern is emerging** — DeepSeek TUI's fleet/roster vision, Pi's Cursor bridge, and Qwen's Web Shell unification all point to a future where a single CLI orchestrates multiple models, providers, and environments — the tools that nail this orchestration layer will define the next generation.

**Bottom Line:** The market is converging on a core contract — reliable, sandboxed, observable, resumable agentic execution across any model, any provider, and any platform. The tools that ship this first, with Windows parity and byte-level safety, will win the trust war that currently has no clear victor.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

*Analysis period: 2025-10 through 2026-08 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Skills have generated the most discussion and community attention. Note that current PR comment counts are not yet reflected in the source data, so ranking is based on issue traction, reproduction reports, and the number of related PRs.

### 1.1 `skill-creator` — Eval Infrastructure (Multiple PRs)
**Functionality:** The meta-skill that helps users create new Claude Code Skills, including a description-optimization loop (`run_eval.py`, `run_loop.py`, `improve_description.py`).
**Discussion highlights:** This is the community's #1 pain point. Issue #556 ("0% trigger rate across all queries") has 12 comments and 7 👍, with 10+ independent reproductions. At least 6 PRs (#1298, #1099, #1050, #1261, #1323, #539) attempt to fix the same root causes: Windows subprocess broken pipes (`WinError 10038`), skill trigger detection missing real skill names, and eval artifacts polluting the live project registry.
**Status:** All fix PRs remain **open** as of 2026-06-25. No merged fix yet — the eval loop is effectively "optimizing against noise."

### 1.2 `document-skills` plugin — The DOCX/OOXML Family
**Functionality:** Document creation/editing skills (docx, pdf, pptx) maintained under the anthropic namespace.
**Discussion highlights:** This is the most heavily used cluster and the source of recurring technical debt. Issue #12 (whitespace reformatting corrupting documents) remains open with 4 comments, and PRs #538 and #541 fix case-sensitivity mismatches and `w:id` collisions in tracked changes respectively — both still open. The theme: document skills work, but subtle spec-compliance bugs cause real user frustration.
**Status:** Issues open; PRs open.

### 1.3 New Skill Proposals — Documents & Office (ODT, #486)
**Functionality:** OpenDocument text creation, template filling, and ODT-to-HTML conversion.
**Discussion highlights:** Proposed 2026-03-01, this PR demonstrates demand for LibreOffice/ODF support alongside the existing Microsoft formats. The skill would round out the document suite by covering non-Microsoft office formats.
**Status:** Open PR.

### 1.4 `color-expert` (#1302) and `pyxel` (#525) — Domain Experts
**Functionality:** `color-expert` provides color naming systems (ISCC-NBS, Munsell, RAL), color space selection heuristics (OKLCH vs OKLAB vs CAM16), and palette guidance. `pyxel` wraps the pyxel-mcp server for retro/pixel-art game development.
**Discussion highlights:** Both are examples of narrow-domain skills that the community values for their depth. The `pyxel` PR name-drops its own MCP server, showing the ecosystem pattern where Skills wrap MCP servers.
**Status:** Both open PRs.

### 1.5 Meta/Governance Skills — `skill-quality-analyzer` + `skill-security-analyzer` (#83)
**Functionality:** Two meta-skills for evaluating other skills across five dimensions (structure, documentation, security posture).
**Discussion highlights:** This proposal directly responds to the security incident in Issue #492 (43 comments — the most-commented issue in the repo). It addresses the trust gap by giving users tooling to audit skills before adoption.
**Status:** Open PR.

### 1.6 `self-audit` (#1367) and `plan-file-hygiene` (#1479) — Agent Self-Management
**Functionality:** `self-audit` performs mechanical file verification followed by a four-dimension reasoning audit before delivery. `plan-file-hygiene` addresses the lifecycle of planning artifacts.
**Discussion highlights:** Both target the same pain point: long-running agents accumulate state and produce unverified output. `plan-file-hygiene` explicitly credits three community members in its description, showing collaborative skill design.
**Status:** Both open PRs.

---

## 2. Community Demand Trends

The following directions show the strongest demand signals from Issues:

### 2.1 Trust & Security Boundary (Hot)
Issue #492 (43 comments, 2 👍) — community skills distributed under the `anthropic/` namespace impersonate official skills, enabling trust boundary abuse. This is the single most-discussed item in the repo and has prompted the meta-skill proposals in section 1.5. Expect immediate mitigation tools (security analyzers) and possible namespace policy changes.

### 2.2 Org-Wide Skill Sharing (Warm)
Issue #228 (16 comments, 8 👍 — highest 👍 count in the repo) — users want org-level skill distribution, not manual `.skill` file downloads over Slack. This is a platform feature, not a single skill, but indicates a cluster need for deployment and management tooling.

### 2.3 Skill Reliability & Eval Infrastructure (Warm)
Issue #556 and #1169 together document that the official `skill-creator` eval loop is fundamentally broken (0% recall on every query, including literal slash-command queries). The community wants working tooling to measure and improve skill descriptions — this is a blocker for the whole ecosystem's quality.

### 2.4 Context-Window Efficiency (Emerging)
Issue #1487 (claude-api skill eagerly injects ~156k tokens — exhausting context in a single call) and Issue #189 (duplicate skills from overlapping plugins wasting context) both point to the same problem: skills that are not token-frugal. Expect demand for "lean" skills and lazy-loading patterns.

### 2.5 Governance & Quality Gates (Emerging)
Issue #412 (agent-governance proposal) and #1385 (reasoning quality gate pipeline) both propose safety/quality patterns. Low comment counts but steady drumbeat of proposals suggests a niche-but-committed segment.

---

## 3. High-Potential Pending Skills

These PRs have active discussion, are not yet merged, and appear likely to land:

| Skill | PR | What it does | Signal |
|---|---|---|---|
| `skill-security-analyzer` / `skill-quality-analyzer` | [#83](https://github.com/anthropics/skills/pull/83) | Five-dimension audit of any skill | Directly addresses Issue #492 security concern; high relevance |
| `color-expert` | [#1302](https://github.com/anthropics/skills/pull/1302) | Deep color-theory knowledge, naming systems, color space selection | Self-contained, well-scoped; maintained by color expert (meodai) |
| `pyxel` | [#525](https://github.com/anthropics/skills/pull/525) | Retro game development via pyxel-mcp | Strong creator track record (kitao is Pyxel author) |
| `plan-file-hygiene` | [#1479](https://github.com/anthropics/skills/pull/1479) | Lifecycle management for planning artifacts | Collaborative design; addresses real long-session pain |
| `self-audit` | [#1367](https://github.com/anthropics/skills/pull/1367) | Mechanical + reasoning audit before delivery | Complements plan-file-hygiene; v1.3.0 shows iteration |
| `ODT` skill | [#486](https://github.com/anthropics/skills/pull/486) | LibreOffice/ODF document handling | Rounds out document suite; lacks IBM/Anthropic backing but community demand is clear |

**Notable:** The `skill-creator` eval fixes (#1298, #1099, #1050, #1323) are highly likely to be merged — they fix a bug every active skill author has hit, and the maintainers have the reproduction trail in Issues #556 and #1169.

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand at the Skills level is **trustworthy skill infrastructure**: they need reliable evaluation tooling to measure skill quality (the broken `run_eval.py` being the top blocker), and they need security verification to safely adopt community-contributed skills — infrastructure concerns that currently outrank any single domain-specific skill proposal.

---

# Claude Code Community Digest — 2026-08-08

## Today's Highlights

v2.1.224 introduces self-hosted runners, bringing Claude Code mobile, web, and desktop sessions to your own infrastructure for Team/Enterprise plans. The community remains highly engaged around session limit continuation (#13354, 73 comments, 191 👍) and granular plugin skill controls (#14920). A notable cluster of issues surfaced around Remote Control environment lifecycle management, with users reporting stale environments that cannot be deleted and ghost sessions causing 404 errors.

---

## Releases

**v2.1.224** — Added self-hosted environments via `claude self-hosted-runner`, enabling Claude Code web, mobile, and desktop sessions to run on your own machines or containers (Team/Enterprise only). Also introduced an `archive` plugin source for installing plugins from a zip over HTTPS without requiring git.

---

## Hot Issues

1. **[#13354 — Continue when session limit reached](https://github.com/anthropics/claude-code/issues/13354)** — [enhancement, area:tui] — 73 comments, 191 👍
   The most-voted open request: users want a way to continue past the session limit rather than being cut off. High engagement suggests this is a top workflow blocker.

2. **[#14920 — Disable individual plugin skills](https://github.com/anthropics/claude-code/issues/14920)** — [enhancement, platform:macos, area:core] — 14 comments, 83 👍
   Users want granular control over plugin-provided skills (e.g., keep `:commit` but disable `:commit-push-pr`). The 83 upvotes without Anthropic response indicates a gap between plugin flexibility and user control.

3. **[#50884 — Remove stale Remote Control environments](https://github.com/anthropics/claude-code/issues/50884)** — [enhancement, area:claude-code-web, area:cli] — 7 comments, 26 👍
   Users can't clean up dead environments from the claude.ai/code list. Pairs with the bug below to form a lifecycle-management story.

4. **[#77372 — Remote Control ghost sessions cause permanent 404s](https://github.com/anthropics/claude-code/issues/77372)** — [bug, has repro, platform:macos] — 3 comments
   Even freshly registered environments get 404s with different session IDs. Environment registration appears broken at worker-attach time, suggesting a backend race condition.

5. **[#72495 — Prompt suggestions suppressed by rate-limit gate](https://github.com/anthropics/claude-code/issues/72495)** — [bug, has repro, platform:linux, area:tui] — 4 comments
   A strict-equality gate in the binary silences prompt suggestions when client-derived rate-limit status is `allowed_warning`. The author located the gate in shipped code and confirmed with a pre-registered prediction — a well-documented, reproducible finding.

6. **[#81853 — Fable 5: text+tool-call responses hide text](https://github.com/anthropics/claude-code/issues/81853)** — [bug] — 5 comments
   With `claude-fable-5`, mixed text/tool-call responses only render the tool call in the TUI; the text is hidden from the main view (visible only via Ctrl+O transcript). Works with Opus 4.8, so it's model-specific.

7. **[#77208 — 100% CPU livelock on KVM guests (kvm64)](https://github.com/anthropics/claude-code/issues/77208)** — [bug, has repro, platform:linux, regression] — 3 comments
   Claude Code ≥ 2.1.205 hangs at 100% CPU even on `--version` when the CPU model is `kvm64`. This breaks the Linux desktop beta Code tab for VM users — a serious regression for that environment.

8. **[#82179 — grep shim catastrophic backtracking → OOM](https://github.com/anthropics/claude-code/issues/82179)** — [bug] — 1 comment
   The Bash tool's ugrep emulation hits catastrophic backtracking with `-o` + bounded quantifiers on alternation, using 6.6 GB RSS / OOM-killing on a 20 KB file. Safety shims should not be a memory hazard.

9. **[#84945 — Cross-session messaging socket bind failure](https://github.com/anthropics/claude-code/issues/84945)** — [bug] — 3 comments
   One of two identical sessions fails to bind the `/tmp/cc-socks` peer socket, causing one-way cross-session messaging. New in 2.1.224, affects macOS Apple Silicon.

10. **[#84689 — CVP-approved org still blocked by cyber safeguards](https://github.com/anthropics/claude-code/issues/84689)** — [bug] — 4 comments
    Even after CVP approval, org is blocked; the appeal form shows no fields. A policy-gating issue with no clear user path forward.

---

## Key PR Progress

1. **[#84711 — Fix yaml injection & symlink credential overwrites in plugin scripts](https://github.com/anthropics/claude-code/pull/84711)** — Security hardening for plugin scripts: prevents YAML injection and symlink-based credential overwrites (fixes #76580). Important for multi-user and CI environments.

2. **[#84747 — Fix hookify rule evaluation scope & secure file read](https://github.com/anthropics/claude-code/pull/84747)** — Ensures tools without mapped events (e.g., `Read`, `Browser`) only trigger `all`-scoped rules; also hardens file reads. Reduces surprise rule evaluations from plugins.

3. **[#84854 — Fix stale hooks doc link in bash_command_validator_example.py](https://github.com/anthropics/claude-code/pull/84854)** — Documentation hygiene: updates the example hook script to use the current `code.claude.com/docs` URL (46 other references already updated).

---

## Feature Request Trends

- **Session continuity**: The #1 request (#13354, 191 👍) is continuing past session limits — users are being cut off mid-workflow.
- **Plugin granularity**: Users want per-skill/per-command enable/disable for plugins (#14920, 83 👍). Plugin install is all-or-nothing today.
- **Environment lifecycle management**: Multiple requests to list, remove, or clean stale Remote Control environments (#50884, #77372) — dead entries linger in claude.ai/code.
- **Input ergonomics**: Pasting images from clipboard (#84961) and raising the `/goal` 4000-character limit (#84953) show friction at input boundaries.
- **Device/session visibility**: Users want to see which device/session a token belongs to (#84949) — an auth-management transparency request.

---

## Developer Pain Points

- **Remote Control reliability**: 404s on fresh environments, stale entries that can't be deleted, and ghost sessions dominate. The feature shipped but the lifecycle story is incomplete.
- **Silent failures**: Background tasks killed mid-run without errors (#84625); spawned agents blocking indefinitely on permission prompts with no timeout (#78487); text suppressed in mixed responses (#81853). "No signal when something goes wrong" is a recurring theme.
- **Performance landmines**: The grep shim OOM (#82179) and 100% CPU livelock on kvm64 (#77208) are extreme cases — but both are silent, hang-style failures that are hard to diagnose.
- **Stale issues not addressed**: #13354 (73 comments, 191 👍) and #14920 (83 👍) have no Anthropic response; #70480 and #70481 were closed as `stale`. Community sentiment is that high-signal requests are being ignored.
- **Windows & Linux desktop pain**: MSIX GPU crashes (#83028), relaunch file-locks (#76192), and the KVM livelock (#77208) suggest the desktop story is fragile outside macOS.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-08

## Today's Highlights

Codex v0.147.0 is out with portable Agent Plugins, enabling search across local, personal, workspace, and remote plugin catalogs. The community is heavily focused on Windows-specific issues — Computer Use failures, sandbox ACL problems, and a severe MCP zombie-process memory leak (37GB) remain top concerns. The team merged a steady stream of infrastructure PRs around code-mode protocols, skill refactoring, and connection resilience.

## Releases

**rust-v0.147.0** — Two headline features:
- Install **portable Agent Plugins** and search across local, personal, workspace, and remote plugin catalogs (#36544, #36409, #36919, #36796)
- Organize conversations into **persistent, manually ordered sections** and browse long transcripts incrementally (#35722, #36007, #36380, #36948)

**rust-v0.148.0-alpha.1 / alpha.2** — Pre-release builds published with no visible changelog beyond version bumps.

---

## Hot Issues

1. **[#12491 — MCP zombie processes leak 37GB memory in Codex.app GUI](https://github.com/openai/codex/issues/12491)** *(CLOSED; 38 comments, 👍5)*
   Codex.app failed to reap MCP child processes, accumulating 1,300+ zombies and 37GB RAM. The high comment count signals this hit many users hard. Closed status suggests a fix shipped — but the scar tissue remains.

2. **[#26234 — MCP tools flattened for non-OpenAI providers](https://github.com/openai/codex/issues/26234)** *(OPEN; 32 comments, 👍41)*
   MCP namespace tools are invisible to models when running against Ollama, LM Studio, OpenRouter, or Bedrock. **41 upvotes** — the strongest community demand right now for third-party provider parity.

3. **[#35481 — Codex Diff fails in VS Code on Windows](https://github.com/openai/codex/issues/35481)** *(CLOSED; 26 comments, 👍54)*
   "Oops, an error has occurred" in the Codex Diff view. **54 upvotes** — biggest emotional spike. Closed within two weeks; worth verifying regression coverage.

4. **[#10090 — `elevated_windows_sandbox` breaks all commands](https://github.com/openai/codex/issues/10090)** *(OPEN; 24 comments, 👍7)*
   `CreateProcessAsUserW failed: 5` — every agent command silently outputs `(no output)`. Windows sandboxing remains fragile; 7 months open.

5. **[#37043 — Windows Computer Use fails at EnumWindows](https://github.com/openai/codex/issues/37043)** *(OPEN; 17 comments, 👍3)*
   `EnumWindows failed: 0x80070003` in the bundled Computer Use helper. Fresh issue (3 days), fast-growing thread — Windows Computer Use is in rough shape.

6. **[#14599 — Trust-level `trusted` for any project](https://github.com/openai/codex/issues/14599)** *(OPEN; 16 comments, 👍57)*
   **Most-upvoted open issue.** Users want to permanently trust any project and skip the recurring approval prompt. Simple ask, huge quality-of-life win.

7. **[#34499 — Can't create Work chat inside ChatGPT Project on Windows](https://github.com/openai/codex/issues/34499)** *(OPEN; 15 comments, 👍6)*
   Session creation broken in Windows Desktop App within ChatGPT Projects. Another Windows-specific workflow blocker.

8. **[#21839 — Existing sessions with full access now require approvals](https://github.com/openai/codex/issues/21839)** *(OPEN; 15 comments, 👍1)*
   Regression: sessions that already had full-access approval are re-prompting. Trust model is eroding user patience.

9. **[#29908 — Bubblewrap sandbox fails on Ubuntu 24.04](https://github.com/openai/codex/issues/29908)** *(OPEN; 14 comments)*
   `apply_patch` and managed sandbox break with loopback/user-namespace errors on kernel 6.17. Linux sandbox reliability is a persistent theme.

10. **[#37425 — v0.147.0 regression: LiteLLM streaming broken](https://github.com/openai/codex/issues/37425)** *(OPEN; 4 comments, 👍3)*
    Fresh regression in the latest release — streaming consistently fails with custom LiteLLM providers. Users are cautioning against upgrading.

---

## Key PR Progress

1. **[#37513 — Reuse parent compactions in Guardian review sessions](https://github.com/openai/codex/pull/37513)**
   Guardian keeps encrypted compaction history across session rewrites — cheaper, faster reviews.

2. **[#37510 — Define the code-mode host gRPC protocol](https://github.com/openai/codex/pull/37510)**
   New `codex.code_mode.v1` protobuf API: sessions, executions, tool callbacks, and content results with Rust bindings via tonic.

3. **[#37504 — Disable Nagle's algorithm for code-mode WebSockets](https://github.com/openai/codex/pull/37504)**
   `TCP_NODELAY` on outbound remote-session sockets — direct latency win for interactive code-mode.

4. **[#37494 — Add MCP event discovery and subscriptions](https://github.com/openai/codex/pull/37494)**
   New `events/stream` subscriptions with proper cancellation. Foundation for reactive plugin UIs.

5. **[#37497 — Limit payload traces in diagnostic logs](https://github.com/openai/codex/pull/37497)**
   Stops high-volume HTTP/SSE/WebSocket payloads from flooding the SQLite log DB. Developers debugging on big sessions will feel this.

6. **[#37498 — Preserve child waiters during process termination](https://github.com/openai/codex/pull/37498)**
   Fixes unreaped PTY children losing exit status — a direct answer to the zombie-process class of bugs.

7. **[#37485 — Keep response streams alive through connection failures](https://github.com/openai/codex/pull/37485)**
   Retries with 5–60s exponential backoff and a "Reconnecting…" surface instead of dropping the stream.

8. **[#37486 — Expose runtime activity in server diagnostics](https://github.com/openai/codex/pull/37486)**
   Lifecycle gauges for in-flight requests, queued work, active turns, and live MCP connections — much-needed operational visibility.

9. **[#37480 — Delegate remote process sandboxing to the executor](https://github.com/openai/codex/pull/37480)**
   Remote `exec_command` now respects executor-native working dirs and permission profiles instead of host-platform resolution.

10. **[#37479 — Report temporary directories in exec-server environment info](https://github.com/openai/codex/pull/37479)**
    Exposes `:tmpdir` via `TMPDIR` (Unix) and `TEMP`/`TMP` (Windows) file URIs so clients can resolve executor-local defaults correctly.

---

## Feature Request Trends

1. **Third-party provider parity (highest demand).** Flatten MCP namespace tools for Ollama/LM Studio/OpenRouter/Bedrock (#26234, 👍41). Custom-provider users feel second-class.

2. **Trust model relief.** Allow `trust_level = "trusted"` for any project (#14599, 👍57 — the most-upvoted issue). Recurring approval prompts are a top UX complaint.

3. **MCP secret/env management.** Plugins need a supported path for user-provided secrets and env vars (#24401, 👍8). Plugin authors are blocked on config surface.

4. **Performance on resume.** Resume should bootstrap the latest turn instead of re-rendering full thread history (#34663). Long-session users hit real lag.

5. **Computer Use packaging parity.** Intel macOS x64 still missing the computer-use helper (#24437, #26842). Apple-silicon users get features Intel users can't.

## Developer Pain Points

1. **Windows sandbox is the #1 frustration.** `CreateProcessAsUserW failed: 5` across #10090, #13965, #14211 — elevated sandboxes and WindowsApps ACLs have been broken since January (6+ months).

2. **Background processes leak and consume limits.** MCP zombie-process memory leaks (#12491) and desktop app silently consuming 6% weekly rate limit on background suggestion runs (#37445) — runaway resource usage with zero user action.

3. **Windows Computer Use is unreliable.** EnumWindows failures (#37043), spawn EPERM (#37415), and wrong-owner window attachment (#37484) — three separate fresh bugs in days.

4. **Resuming old sessions is risky.** Missed tools/subagent runtime drift (#25990), duplicate MCP process stacks on resume (#37453), and 646MB crash-triggering prefetches (#35799).

5. **`gpt-5.6-sol` model surfaced but unsupported** in the desktop app with no usage limit (#36082) — product surfaces racing ahead of backend support.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-08

## Today's Highlights

Three patch releases landed today (v0.54.4, v0.55.0-preview.2, and a nightly build), primarily cherry-picking fixes onto stable and preview branches. On the security front, two notable PRs address a critical SSRF vulnerability (CVSS 8.6) in the `web-fetch` tool and upgrade the sandbox Dockerfile from Node 20 to Node 22 ahead of EOL. Agent reliability issues remain the top community concern, with longstanding bugs around subagent turn limits, hangs, and permission enforcement still open.

## Releases

- **[v0.54.4](https://github.com/google-gemini/gemini-cli/releases)** — Patch release cherry-picking fix `56f9688` onto the v0.54.0 branch; includes version bump to 0.54.2.
- **[v0.55.0-preview.2](https://github.com/google-gemini/gemini-cli/releases/tag/v0.55.0-preview.2)** — Preview patch cherry-picking `2139b12` from PR #28716 onto the preview branch.
- **[v0.56.0-nightly.20260807.gd5c9a97dc](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260807.gd5c9a97dc)** — Nightly build with changelog preparation for v0.55.0-preview.1 and v0.54.

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, 12 comments, reopened) — `codebase_investigator` subagents report success when they actually hit turn limits, masking real failures. This is a serious correctness issue that undermines trust in subagent results.

2. **[#21409 — Generalist agent hangs indefinitely](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, 8 comments, 8 👍) — Simple tasks like folder creation hang for up to an hour. Workaround exists (disable subagent delegation), but this remains a top-priority reliability blocker.

3. **[#19873 — Leverage model's bash affinity via OS sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)** (P2, 8 comments) — Proposal to let Gemini 3 models use native POSIX toolchains (grep, sed, awk) in a zero-dependency sandbox, with post-execution intent routing for safety.

4. **[#24353 — Robust component-level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (P1, 7 comments) — EPIC tracking expansion of the behavioral eval suite beyond the current 76 tests, covering 6 supported Gemini models. Critical for quality assurance across the agent ecosystem.

5. **[#22745 — Impact of AST-aware file reads and codebase mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (P2, 7 comments) — Investigation EPIC into whether AST-aware tools can reduce token noise and improve navigation precision. Could significantly improve large-codebase performance.

6. **[#25166 — Shell command stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, 4 comments, 3 👍) — Simple CLI commands hang after completion while UI shows "Awaiting user input." Highly reproducible for basic commands, affecting daily workflow.

7. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, 5 comments) — Background extraction agent re-surfaces the same low-signal sessions repeatedly, wasting tokens and time on memory processing.

8. **[#26525 — Deterministic redaction for Auto Memory](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, 4 comments) — Security concern: transcript content is sent to extraction models before prompt-based redaction happens. Requests deterministic pre-redaction.

9. **[#20079 — Symlinked agent files not recognized](https://github.com/google-gemini/gemini-cli/issues/20079)** (P2, 4 comments) — `~/.gemini/agents/filename.md` symlinks are silently ignored. Breaks common dotfile management patterns.

10. **[#22093 — Subagents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** (P2, 3 comments) — Users report subagents (like generalist) executing despite agents being disabled in all configurations. Permission model regression.

## Key PR Progress

1. **[#28725 — Fix SSRF via DNS resolution bypass in web-fetch](https://github.com/google-gemini/gemini-cli/pull/28725)** (P2, Open) — Critical fix for CVSS 8.6 SSRF where custom domains pointing to private IPs (e.g., `169.254.169.254`) bypassed DNS protections. Should be prioritized for merge.

2. **[#28726 — Upgrade sandbox Dockerfile to node:22-slim](https://github.com/google-gemini/gemini-cli/pull/28726)** (P1, Open) — Mitigates unpatched Node 20 CVEs by upgrading all Dockerfiles (sandbox + caretaker Cloud Run) to Node 22. Security-relevant for production deployments.

3. **[#28730 — Resolve false model capacity exhaustion](https://github.com/google-gemini/gemini-cli/pull/28730)** (Open) — Fixes misleading capacity errors and corrects client-side quota lookup mapping. Preserves the "Keep trying" option during transient capacity surges.

4. **[#28673 — Add Gemini 3.6 Flash and 3.5 Flash-Lite configurations](https://github.com/google-gemini/gemini-cli/pull/28673)** (P2, Open) — Brings support for newer model variants with capabilities (`thinking`, `multimodalToolUse`), aliases, and code execution configs.

5. **[#28729 — Fix swallowed directory mismatch in IDE connections](https://github.com/google-gemini/gemini-cli/pull/28729)** (Open) — Resolves Cider/VS Code fork connection failures caused by virtual or different FUSE directory paths.

6. **[#28597 — Load environment variables before settings placeholders](https://github.com/google-gemini/gemini-cli/pull/28597)** (P2, Open) — Fixes a load-order race condition where settings expansion ran before `.env` was loaded, causing placeholder resolution failures.

7. **[#28730 — Core quota lookup model mapping fix](https://github.com/google-gemini/gemini-cli/pull/28730)** (Open) — Corrects client-side mapping between models and quota lookups in core, preventing false exhaustion errors.

8. **[#28581 — Skip diff hunk markers during @ processing](https://github.com/google-gemini/gemini-cli/pull/28581)** (P2, Open) — Prevents diff hunk markers being interpreted as `@file` references, eliminating recursive glob searches that caused heap growth on large diffs.

9. **[#28597 — Settings lifecycle race condition fix](https://github.com/google-gemini/gemini-cli/pull/28597)** (P2, Open) — Moves env loading before settings file parsing/expansion to fix placeholder resolution order.

10. **[#28690 — Issue comment handling and re-triage workflow](https://github.com/google-gemini/gemini-cli/pull/28690)** (Closed) — Adds `issue_comment.created` webhook processing to the Caretaker Agent, enabling `@caretaker-agent` mentions for re-triage on `NEEDS_INFO` issues.

## Feature Request Trends

- **AST-aware tooling** — Multiple issues (#22745, #22746) propose AST-aware file reads, searches, and codebase mapping to reduce token waste and improve navigation on large repositories.
- **OS-level sandboxing** (#19873) — Enable model's native bash affinity with zero-dependency OS sandboxing and intent routing post-execution.
- **Subagent self-awareness** (#21432) — Improve CLI's ability to explain its own mechanics (flags, hotkeys, capabilities) to users.
- **Better subagent observability** (#22598) — Make subagent trajectories visible/shareable via `/chat share` for easier debugging and evaluation.
- **Resilience for browser_agent** (#22232) — Automatic session takeover and lock recovery for persistent browser profiles.
- **Deterministic security redaction** (#26525) — Pre-redact sensitive content before sending to extraction models, not via prompt instruction.

## Developer Pain Points

1. **Subagent reliability** — Recurring complaints: subagents hanging (#21409), reporting false success (#22323), running without permission (#22093), and not using custom skills/agents proactively (#21968).
2. **Shell command hangs** — Multiple reports of completed commands showing "Waiting input" (#25166) and interactive prompts deadlocking (#22465).
3. **Memory system inefficiency** — Auto Memory retries low-signal sessions (#26522), silently skips invalid patches (#26523), and logs too much (#26525).
4. **Tool/agent limits** — 400 error with >128 tools (#24246) signals scaling issues for power users with many MCP tools.
5. **Configuration friction** — Symlinked agent files ignored (#20079), settings.json overrides not respected by browser agent (#22267), and environment variable load-order bugs (#28597).
6. **Destructive behavior prevention** (#22672) — Users want agents to avoid `git reset --force` and other risky commands when safer alternatives exist.
7. **Workspace pollution** (#23571) — Models creating tmp scripts in random directories adds cleanup overhead.

**Community sentiment**: The volume of P1 issues on agent reliability, especially around subagent execution and false success reporting, indicates that agent orchestration robustness is the single biggest trust barrier for users. The active security hardening (SSRF fix, Node upgrades) is a positive signal for production adoption, but the breadth of open, long-running issues (many from March 2026) suggests maintainers are prioritizing new features over triaging the backlog.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest - 2026-08-08

## Today's Highlights
Three rapid-fire releases (v1.0.79-7 through v1.0.79-9) shipped today, adding enterprise policy controls for sandbox networking, support for the Kimi K3 model, and a new `--plan` + `--mode autopilot` combo for plan-then-implement workflows. The community is buzzing about a Windows clipboard regression that silently fails and a fresh report that the npm shim loads versions non-deterministically (1.0.77 → 1.0.78 within 101s on the same path).

---

## Releases
**v1.0.79-7** · **v1.0.79-8** · **v1.0.79-9** (all within 24h)

**Added:**
- Agent Plugins can now ship extensions under `com.github.copilot/extensions/`
- Kimi K3 model support
- `--plan` + `--mode autopilot` — plan first, then execute without approval
- Enterprise `allow-auto-only` policy: `/allow-all auto` works while full allow-all remains blocked
- Enterprise-managed sandbox policy can enforce an proxy URL while credentials stay user-controlled

**Improved:**
- `/sandbox` config dialog now shows where settings are stored in `settings.json`
- Sandbox dialog groups git/gh settings more logically
- Multi-select prompts improved UX

---

## Hot Issues

**[#2494 — Login auto-enters keychain prompt (regression)**](https://github.com/github/copilot-cli/issues/2494) 
`copilot login` no longer waits for y/N input when the keychain is unavailable — it auto-submits, breaking auth flows. 11 comments, open for months, still unfixed.

**[#1632 — Support subfolders for skills](https://github.com/github/copilot-cli/issues/1632)** 
Flat skills-only layout with 20+ skills becomes unmanageable. 23 👍, strong demand for hierarchy support.

**[#3622 — Copy to clipboard silently fails on Windows](https://github.com/github/copilot-cli/issues/3622)** 
Copy appears to succeed but paste yields stale content. Regression from 1.0.48; affects Windows users broadly.

**[#4118 — /app doesn't select CWD by default](https://github.com/github/copilot-cli/issues/4118)** 
35 👍 — strongest signal of the week. `/app` should default to the current working directory, not force a manual path pick.

**[#4311 — Transcript blanks until width change (terminal rendering)](https://github.com/github/copilot-cli/issues/4311)** 
Measured-line cache invalidation bug causes blank transcript regions in interactive mode; `/resume` doesn't help. Core UX degradation.

**[#4402 — npm shim loads non-deterministic versions](https://github.com/github/copilot-cli/issues/4402)** 
Same `npm -g/bin/copilot` path served 1.0.77 then 1.0.78 within 101s. Loader-not-pin design surprises users; `--prefer-version` exists but is undocumented.

**[#4401 — Skill tool can't find ~/.agents/skills](https://github.com/github/copilot-cli/issues/4401)** 
Regression in 1.0.78 with incomplete fix reference to #2230. Valid skills with SKILL.md present aren't found.

**[#4392 — MCP rebuild orphans stdio server processes](https://github.com/github/copilot-cli/issues/4392)** 
Post-auth MCP client rebuild spawns a second generation of stdio processes without killing the first — process leak at every startup.

**[#4397 — Resume session resets model](https://github.com/github/copilot-cli/issues/4397)** 
`copilot --resume` switches back to the default model instead of persisting the session's configured model (e.g., gpt-5.6).

**[#4394 — Can't disable/remap Ctrl+C twice to exit](https://github.com/github/copilot-cli/issues/4394)** 
Power users hit Ctrl+C for cancel/copy out of habit; double-press exits unintentionally. No config to disable or remap.

---

## Key PR Progress
No pull requests were updated in the last 24 hours. This is unusually quiet — the team appears focused on stabilizing the v1.0.79 line with hotfix releases.

---

## Feature Request Trends

1. **Skill organization** (#1632) — subfolders, namespacing, and hierarchy for skills; 23 👍.
2. **Session workflow defaults** (#4396, #4395, #4118) — persistent default workspace type (branch vs worktree), default CWD for `/app`, and quick-delete in session list.
3. **Token tracking & cost metrics** (#2947) — per-session token usage reporting; 7 👍.
4. **Interruptibility & notifications** (#4394, #2941) — desktop notifications when the CLI needs input; remappable exit shortcuts.
5. **Model persistence** (#4397) — sessions should retain their chosen model across resume.

---

## Developer Pain Points

- **Authentication regressions** — #2494 remains open for months; auto-entering keychain prompts on login is a critical blocker for users with locked keychains.
- **Terminal rendering fragility** — #4311, #4391, #4384, #4043: blank transcripts, screen clears on copy (codepage 936), terminal title squatting, obscured model picker. Windows users are disproportionately affected.
- **MCP process hygiene** — #4392 and #1129: orphaned stdio processes and false-positive "working" MCP indicators erode trust in the MCP integration.
- **Perception of non-determinism** — #4402 (loader vs pinned version) plus #4397 (model reset on resume) make behavior feel unpredictable.
- **Permission & config inconsistencies** — #4398 (`allowed_directories` ignored), #1409 (dash-to-underscore conversion breaks OneDrive paths), #1409's permission loops.

**Bottom line:** The release train is moving fast on enterprise/compliance features, but the community is churning on Windows terminal+clipboard stability, skill management UX, and session-state predictability.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**2026-08-08**

---

## 1. Today's Highlights

The community is focused on two critical reliability issues: a file-corruption bug in `StrReplaceFile` that destroys non-UTF-8 bytes during edits, and a safety incident where the agent executed `rm -rf` on a pre-existing directory outside the workspace in YOLO mode. Two competing PRs address the UTF-8 corruption issue with different strategies (byte-level preservation vs. refusing non-UTF-8 files), signaling a broader debate about how the tool should handle binary files. No new releases were published in the last 24 hours.

---

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Hot Issues

### #2591 — StrReplaceFile corrupts undecodable bytes outside the edited region
**Author:** shoemoney | **Comments:** 3 | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2591)

**Summary:** `StrReplaceFile` decodes the entire file with `errors="replace"`, meaning any invalid UTF-8 byte anywhere in the file (even far from the edit) is replaced with U+FFFD and written back to disk as `EF BF BD`, permanently corrupting the file's content.

**Why it matters:** This is a silent data-corruption bug — the file length changes and content is destroyed without the agent or user being notified. It affects any binary file, mixed-encoding file, or file with embedded non-UTF-8 sequences. The fix is non-trivial because it requires rethinking how the tool handles raw bytes vs. strings.

### #2596 — Agent ran rm -rf on a pre-existing directory outside the workspace, deleting user session data
**Author:** iMaxTomas | **Comments:** 0 | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2596)

**Summary:** The agent (in YOLO mode) was asked to clean up a symlink it had created at `~/.pi/agent/sessions`. The original symlink creation had silently failed (because a real directory already existed), and the agent didn't notice. It then followed up by recursively deleting what it believed was its own symlink.

**Why it matters:** This is a critical safety failure in the "autonomous" permission mode. The agent's inability to verify pre-conditions (did the symlink actually get created?) led to catastrophic data loss. It highlights a need for pre-destructive-action verification, filesystem state checks, and guardrails even in YOLO mode.

---

## 4. Key PR Progress

### #2594 — fix(tools): preserve non-UTF-8 bytes in StrReplaceFile edits
**Author:** 686f6c61 | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2594)

**Summary:** Applies `old`/`new` as UTF-8 byte substrings on the raw buffer instead of decoding the whole file with `errors="replace"` and re-encoding. This preserves invalid UTF-8 sequences outside the edited region. Requires UTF-8 boundaries to be respected.

**Assessment:** This is the more advanced fix — it directly addresses the corruption by working at the byte level. It allows edits on files that contain some non-UTF-8 bytes (as long as the edit region itself is valid, and boundaries are respected). Requires careful validation of byte-boundary alignment.

### #2595 — fix(StrReplaceFile): refuse to edit files that are not valid UTF-8
**Author:** shoemoney | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2595)

**Summary:** Resolves #2591 by detecting files that are not valid UTF-8 and refusing to edit them outright, rather than corrupting them.

**Assessment:** A simpler, more conservative approach: "don't touch what you can't handle." This avoids the technical complexity of byte-level editing but means the tool simply refuses to operate on a class of files. Trade-off between safety and capability.

**Community note:** The fact that two PRs were filed within the same day suggests the issue is high-priority and the community is split on the "right" answer — preserve bytes vs. refuse entirely.

---

## 5. Feature Request Trends

Distilled from all open issues, the community is pushing for:

1. **Byte-level file operations / binary safety:** The #2591 cluster demonstrates demand for tools that can safely handle non-text files — either byte-exact editing or early refusal with clear error messages. Expect requests for `errors="strict"` behavior and explicit encoding declarations in tool schema.

2. **Workspace boundary enforcement:** The #2596 incident reinforces a recurring theme across issues: users want hard guarantees that the agent cannot operate on files outside the workspace without explicit, per-operation approval — even in YOLO mode. Requests for filesystem capability scoping (similar to OS-level sandboxing) are likely.

3. **Pre-flight checks before destructive operations:** Users want the agent to verify state (e.g., "is the symlink actually a symlink?") before running `rm -rf`, `mv`, or other destructive commands.

4. **Transactional file edits:** A desire for atomic, undoable file modifications (write to temp + rename, or diff-and-apply) rather than whole-file read-modify-write.

---

## 6. Developer Pain Points

Recurring frustrations from the issue tracker:

- **Silent failures are worse than loud ones:** In #2596, the symlink creation failed silently and the agent pressed on. Developers expect the agent to notice when its own operations didn't achieve the intended effect.
- **Permission modes are one-dimensional:** YOLO mode is seemingly all-or-nothing, with no granular "allowed to touch workspace files, but never anything outside" option. Users want multi-dimensional permission profiles.
- **File corruption without warning:** #2591 demonstrates that read-modify-write with lossy decoding is never acceptable, and it's surprising users had to file a bug rather than the tool being byte-safe by default.
- **Lack of undo/rollback:** Multiple issues reference a need to recover from agent mistakes (e.g., deleted session data in #2596), but there's no mechanism to restore or audit what the agent changed.

---

*Digest generated from MoonshotAI/kimi-cli GitHub activity (2026-08-08). All links reference the official repository.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-08

## Today's Highlights

OpenCode Go billing discrepancies dominate community discussion this week, with multiple users reporting unexpected quota exhaustion and 401 errors despite healthy account status. Meanwhile, a significant new PR introduces native Mermaid diagram rendering in the TUI, signaling continued investment in the 2.0 desktop experience. Several web app fixes landed to address the "Nothing here yet" empty state on fresh sessions, a top complaint from `opencode web` users.

## Releases

**v1.18.15** — Bugfix release focused on message ordering integrity:
- Chronological message ordering now correct even with imported/legacy message IDs out of order
- Revert and fork actions use real message chronology instead of ID ordering
- Truncation cleanup now removes stale files by file timestamp more reliably

No new features in this patch; stability fixes only.

---

## Hot Issues

1. **[#38257 — OpenCode Go: 401 Request blocked by upstream provider](https://github.com/anomalyco/opencode/issues/38257)** (45 comments, 👍11)  
   Server-side issue where `chat/completions` returns 401 while `/v1/models` works fine. Affects all models on Go subscriptions since July 22. No resolution yet after 2+ weeks — high anxiety among paid users.

2. **[#5359 — Unable to read images for some models](https://github.com/anomalyco/opencode/issues/5359)** (18 comments)  
   Image attachments fail on versions 1.0.137+, works on 1.0.134. Backend: LiteLLM + Vertex AI. Long-lived bug (since December 2025) with active community engagement.

3. **[#23153 — Feature: Pay Go with crypto](https://github.com/anomalyco/opencode/issues/23153)** (17 comments, 👍37)  
   High upvote count (37) indicates strong community desire for cryptocurrency payment options on the Go plan. No official response yet.

4. **[#14332 — Amazon Bedrock Opus 4.6 compaction failure](https://github.com/anomalyco/opencode/issues/14332)** (16 comments, 👍8)  
   Compaction sends `thinking` blocks back to the API, violating Bedrock constraints. Closed — but 8 upvotes suggest others experienced this.

5. **[#40409 — OpenCode Go `deepseek-v4-flash` serving wrong model](https://github.com/anomalyco/opencode/issues/40409)** (14 comments)  
   Model self-identifies as V3.2 with knowledge cutoff 2025-05, despite being billed as V4 Flash. Billing/quality mismatch — closed, but leaves trust questions.

6. **[#6560 — Paste not working in PowerShell TUI](https://github.com/anomalyco/opencode/issues/6560)** (13 comments)  
   Windows 11 PowerShell: clipboard paste fails inside OpenCode TUI (right-click and Ctrl+V). Closed, but a persistent Windows UX annoyance.

7. **[#24334 — DeepSeek `reasoning_content` must be passed back](https://github.com/anomalyco/opencode/issues/24334)** (10 comments)  
   Thinking-mode tokens from DeepSeek need to be echoed back; OpenCode drops them, causing 400 errors. Closed — core ACP issue affecting agentic workflows.

8. **[#41146 — Overcharged on Go plan: weekly limit at $7.50 despite $30 limit](https://github.com/anomalyco/opencode/issues/41146)** (2 comments)  
   Usage dashboard shows $7.50 spent but quota shows 100% used and blocked. Fresh report today — billing accuracy is a recurring theme.

9. **[#40183 — Copilot re-auth prompted every session](https://github.com/anomalyco/opencode/issues/40183)** (3 comments)  
   Credential stored (`expires:0`, refresh==access) but OpenCode still prompts for device-code login each new session. Student Copilot plan users affected.

10. **[#41165 — Relay sends assistant message with missing `content` key](https://github.com/anomalyco/opencode/issues/41165)** (1 comment, opened today)  
    After `next-16998`+, DeepSeek agentic sessions fail with HTTP 400. Serializer emits assistant message missing required content field — a regression.

---

## Key PR Progress

1. **[#41113 — feat(tui): render Mermaid diagrams](https://github.com/anomalyco/opencode/pull/41113)**  
   Vendored `@opencode-ai/merman` package renders flowcharts, sequence, and state diagrams inline in the session transcript via OpenTUI. Significant TUI enhancement.

2. **[#41118 — feat(server): add Modal environment driver](https://github.com/anomalyco/opencode/pull/41118)**  
   First hosted binding of the Environment contract — Modal sandbox driver with measured performance. Live-gated conformance suite included.

3. **[#40923 — feat: native background subagents + auto-continue](https://github.com/anomalyco/opencode/pull/40923)**  
   Introduces `Task(background: true)` orchestration and self-recovering transient provider errors. Potentially transformative for multi-agent workflows.

4. **[#41158 — fix(app): default project picker to home](https://github.com/anomalyco/opencode/pull/41158)**  
   Returns server home directory from location endpoint; hydrates V2 app path state; defaults both Open Project dialogs appropriately.

5. **[#41160 — feat(tool): add Synthetic web search backend](https://github.com/anomalyco/opencode/pull/41160)**  
   Third search provider alongside exa/parallel, with zero-data-retention guarantee. Closes #41164.

6. **[#41161 — fix(session): extract tool-result media for models without attachment capability](https://github.com/anomalyco/opencode/pull/41161)**  
   Fixes `supportsMediaInToolResult` returning `true` unconditionally for Anthropic/OpenAI SDKs — extraction for models lacking attachment support.

7. **[#41159 — fix(provider): propagate config-level npm override to inherited models](https://github.com/anomalyco/opencode/pull/41159)**  
   Config `npm` override for existing providers (e.g., `provider.synthetic.npm`) was silently dropped; now propagates to inherited models.

8. **[#41154 — fix(app): show server projects until the first bookmark](https://github.com/anomalyco/opencode/pull/41154)**  
   Falls back to server `/project` when client bookmarks are empty. Fixes the "Nothing here yet" fresh-session issue.

9. **[#41153 — fix(app): list the base directory on an empty project search](https://github.com/anomalyco/opencode/pull/41153)**  
   Empty queries now list base directory subfolders instead of showing "No folders found" — fixes the stale empty-search state.

10. **[#40845 — [beta] feat(app): redesign non-modal settings](https://github.com/anomalyco/opencode/pull/40845)**  
    Reorganizes settings navigation, adds Figma-aligned Projects/Extensions views, improves multi-server selection and default-server menu.

---

## Feature Request Trends

- **Billing transparency & flexibility**: Multiple issues (#41146, #41072, #23153) about quota miscalculations, unexpected blocks, and desire for crypto payments. Billing accuracy is the #1 trust issue this week.
- **Model routing & provider correctness**: Community frustrated by models serving wrong underlying versions (#40409, #40607) and provider-specific protocol failures (#14332, #24334).
- **Multi-agent orchestration**: PR #40923 and issue #17595 (runtime model override for subagents) indicate direction toward more sophisticated agent control.
- **Web/app UX parity**: Fixes for empty states, project discovery, and git branch visibility (#41105) — the V2 app is still maturing.
- **Plugin ecosystem expansion**: Web search backends, Copilot quota viewers, and settings redesigns show ecosystem growth.

---

## Developer Pain Points

- **Billing surprises**: Quota exhaustion reports at 30–60% of advertised limits are frequent and unresolved. The $10/month Go plan getting blocked at $7.50 is a major trust issue.
- **Provider API incompatibilities**: DeepSeek `reasoning_content` requirements, Bedrock `thinking` block restrictions, and model self-identification mismatches force constant workarounds.
- **Session persistence & state loss**: Models not reading images, paste failures, and re-auth loops break otherwise solid workflows.
- **Fresh-session emptiness**: `opencode web` showing "Nothing here yet" frustrates new users — fixed this week but highlights broader onboarding polish gaps.
- **Background orchestration gaps**: No way to switch subagent models at runtime; background agents require manual workaround — community wants this as a first-class feature.

---

*Digest generated 2026-08-08 from anomalyco/opencode repository activity.*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-08

## Today's Highlights

v0.84.1 ships with Qwen token plan support and auth readiness checks, but the community's attention is on a cluster of session-lifecycle bugs: auto-compaction failing to trigger until provider overflow (#6879), post-compaction stalls (#7020), and an `Agent.reset()` race that leaves assistant-only transcripts (#7703). A significant refactor PR (#7784) reworks recovery state derivation, and TUI performance work (#7780) is merging incremental markdown parsing for large sessions.

**Release:** [v0.84.1](https://github.com/earendil-works/pi/releases/tag/v0.84.1)

## Releases

### v0.84.1
- **Qwen Token Plan Individual** — Use the built-in provider for models documented for Individual subscriptions. See [API Keys](https://github.com/earendil-works/pi/blob/v0.84.1/packages/coding-agent/docs/providers.md#api-keys).
- **Authentication readiness checks** — `pi auth` now includes checks to verify authentication state before starting sessions.

## Hot Issues

1. **[#6879 — Auto-compaction never triggers after context grows past 100% until provider overflow](https://github.com/earendil-works/pi/issues/6879)** (13 comments, 👍15)
   A 2-hour agentic turn on gpt-5.6-sol pushed context past 100% with no compaction; the API rejected at 373k tokens. Community wants compaction checks after every agent step, not just on API rejection.
2. **[#7128 — New default PI_* guideline over-encourages unnecessary bash calls](https://github.com/earendil-works/pi/issues/7128)** (11 comments, 👍7)
   Recent system prompt addition biases agents toward env-inspection bash commands even when unneeded, wasting tokens and time.
3. **[#7020 — Sometimes Pi doesn't continue after compaction](https://github.com/earendil-works/pi/issues/7020)** (10 comments)
   Long-running "coordinator" sessions hit post-compaction warts where the agent fails to continue. Companions #5886 (meta-issue) and #7703 (reset race) suggest this is a systemic lifecycle problem.
4. **[#5886 — AgentSession settlement/continuation and assistant-tail lifecycle bugs](https://github.com/earendil-works/pi/issues/5886)** (6 comments, 👍4)
   Meta-issue for recurring post-run continuation bugs — the root cause behind several reported symptoms.
5. **[#7730 — High CPU usage on Mac OS with long session](https://github.com/earendil-works/pi/issues/7730)** (4 comments, 👍5)
   50–110% CPU swing, 600–800MB memory, apparently correlated with session/context size. No fix yet.
6. **[#7053 — Parallel tool batches lose completed results when one sibling stalls](https://github.com/earendil-works/pi/issues/7053)**
   `Promise.all` in `executeToolCallsParallel` means a stalled sibling discards already-completed tool results → "No result provided" errors.
7. **[#7702 — DeepSeek reasoning_content must be passed back via opencode zen gateway](https://github.com/earendil-works/pi/issues/7702)** (6 comments)
   Multi-turn DeepSeek conversations hit 400 errors; `detectCompat()` fails to round-trip `reasoning_content`.
8. **[#7771 — Unable to start 0.84.1: zlib.createZstdDecompress is not a function](https://github.com/earendil-works/pi/issues/7771)**
   Node 23 incompatibility — likely missing `zstd` support in the bundled zlib. Blocks all usage for affected users.
9. **[#7791 — Global Undici dispatcher inherits 16 KiB maxHeaderSize → UND_ERR_HEADERS_OVERFLOW](https://github.com/earendil-works/pi/issues/7791)**
   Valid responses with large headers are rejected; no override configured for the global `EnvHttpProxyAgent`.
10. **[#7740 — TUI after /reload doesn't honor custom tool renderers registered on session_start](https://github.com/earendil-works/pi/issues/7740)**
    Load-order bug: after `/reload`, tools registered during `session_start` lose their custom renderers.

## Key PR Progress

1. **[#7784 — refactor(agent): derive recovery state from record queries](https://github.com/earendil-works/pi/pull/7784)**
   Removes recovery-specific query APIs (e.g., `findOpenOperations()`) in favor of bounded `findRecords()` queries; retains write-side enforcement and rejects invalid replay transitions.
2. **[#7801 — feat(coding-agent): lazily load uncommon syntax grammars](https://github.com/earendil-works/pi/pull/7801)**
   Experimental highlighting refactor — reduces startup cost by loading rare grammars on demand. Public API impact noted.
3. **[#7780 — TUI performance improvement](https://github.com/earendil-works/pi/pull/7780)**
   Incremental markdown parsing + lazy render invalidation; partial old-content parsing on startup. Directly addresses long-session CPU issues (#7730).
4. **[#7710 — feat(agent): restore suspended harness operations](https://github.com/earendil-works/pi/pull/7710)**
   Implements R3 of the harness v2 plan: create/load a new harness from a session with existing lifecycle state.
5. **[#7749 — fix(coding-agent): preserve custom tool renderers after reload](https://github.com/earendil-works/pi/pull/7749)**
   Fixes #7740 by emitting `session_start` before rebuilding historical chat messages, so registered renderers survive `/reload`.
6. **[#7792 — feat(coding-agent): bridge Cursor CLI auth via local agent session](https://github.com/earendil-works/pi/pull/7792)**
   Hidden `cursor-agent` extension — `pi cursor status`, Cursor models in `--list-models`, and `pi -p --provider cursor` via `agent -p`, no API key required.
7. **[#7762 — feat(provider): Introduce LM Studio provider](https://github.com/earendil-works/pi/pull/7762)**
   New provider for local LM Studio; tests guarded by `LM_STUDIO_BASE_URL`. Solves #7668.
8. **[#7757 — feat(coding-agent): allow opting out of fullscreen copy-on-select](https://github.com/earendil-works/pi/pull/7757)**
   Adds a setting to disable copy-on-select in fullscreen; `app.message.copy` keybind then copies selection if present, else last message.
9. **[#7758 — feat(coding-agent): add exit foreground task and ctx.version](https://github.com/earendil-works/pi/pull/7758)**
   Enables extensions to take over the foreground process post-shutdown (e.g., handoff to a `/web` server) and exposes `ctx.version`.
10. **[#7722 — feat(coding-agent): add theme override](https://github.com/earendil-works/pi/pull/7722)**
    Adds `--use-theme` CLI flag overriding stored theme for the current run; supports `dark` and `dayowl/nightowl` appearance-based notation.

## Feature Request Trends

- **Session/Transcript Controls** — Sticky header for last prompt (#7802), half-page scroll keybindings (#7735), collapsed-paste preview before sending (#7754).
- **Provider Breadth** — LM Studio (#7668/#7762), Cursor CLI bridge (#7792/#7793), Amazon Bedrock Mantle (#6216).
- **Extension API Expansion** — Safe session replacement API (#5952), tool decoration without full re-registration (#7800), Agent Plugins spec support (#7776), foreground task handoff (#7758).
- **Theme & Rendering** — Theme override flag (#7722), fix auto-theme repaint gaps (#7595), correct Dark/Light detection on macOS (#7770).

## Developer Pain Points

- **Session lifecycle fragility** — compactions (#6879, #7020), resets (#7703), and continuation failures (#5886) dominate issue volume; users running long-lived "coordinator" sessions are most affected.
- **Provider round-trip compatibility** — DeepSeek `reasoning_content` (#7702), Gemini `thought_signature` (#6733), OpenAI Responses `namespace` drops (#7709), and `strict:false` omissions (#7250) — a steady drip of similar per-provider protocol bugs.
- **Post-`/reload` state loss** — custom renderers (#7740) and tool registration order; PR #7749 addresses one path but the class of bugs persists.
- **Performance degradation on long sessions** — high CPU (#7730) and TUI lag; incremental parsing PR (#7780) is the first serious mitigation.
- **Environment portability** — Node version incompatibilities (#7771), `which` dependency (#7795/#7796), and undici header limits (#7791) — small but recurring annoyances across setups.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-08

## Today's Highlights
The Qwen Code team shipped one nightly release (v0.21.7-nightly.20260807) focused on CI pipeline fixes, while the community surfaced a notable batch of Windows and terminal-UI bugs, including Chinese IME pinyin display issues and a bundled runtime crash on workspace open. On the feature front, several significant proposals moved forward, including a Qwen WebBridge for direct browser control, a "Local Control" QR-code pairing mode, and an orchestration policy layer for the Workflow tool.

## Releases
**v0.21.7-nightly.20260807.fca8f3c1f** — Nightly release containing a single CI fix: `fix(ci): surface blocked autofix takeover admission` by @qqqys (PR #8410). This nightly addresses CI pipeline visibility when autofix takeover is blocked, helping maintainers identify stalled automation workflows.  
📦 [View release](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.7-nightly.20260807.fca8f3c1f)

## Hot Issues
1. **[#8625 — Windows terminal: Chinese IME pinyin display unreadable](https://github.com/QwenLM/qwen-code/issues/8625)** (P2, UI/Windows)  
   Users on Windows terminals report that Chinese input via IME shows garbled pinyin, making composition impossible to read. With 6 comments, this is the most-discussed open issue today, highlighting a persistent gap in CJK font/rendering support on Windows.

2. **[#8660 — Add runtime and client attribution to usage telemetry](https://github.com/QwenLM/qwen-code/issues/8660)** (P3, Feature Request)  
   Request to append stable runtime and client attribution to telemetry payloads; current `properties.channel` distinguishes entry points (VS Code extension vs. `--acp`), but the community wants more granularity for cross-client analytics.

3. **[#8092 — Build a lower-maintenance desktop app around Web Shell](https://github.com/QwenLM/qwen-code/issues/8092)** (Feature Request, `/web-shell`)  
   Proposal to replace the bespoke desktop UI with a wrapper around the existing Web Shell — reducing maintenance burden and unifying UX. Actively discussed across 5 comments, suggesting strong community appetite for a unified surface.

4. **[#8615 — Desktop 0.1.0 Windows: EISDIR lstat 'C:' crash on workspace open](https://github.com/QwenLM/qwen-code/issues/8615)** (P1, Windows)  
   The bundled Node runtime crashes with `EISDIR lstat 'C:'` when opening a workspace on Windows. This P1 regression blocks Desktop users from opening folders on the primary drive, making it a critical hotfix candidate.

5. **[#8562 — tmux screen flickering via SSH/iTerm2 on Ubuntu](https://github.com/QwenLM/qwen-code/issues/8562)** (P2, UI/Linux)  
   Users report flashed screens in tmux splits after recent updates, with diagnosis pointing to Qwen Code rendering issues rather than terminal emulator problems. Related to #8659 below, indicating a broader rendering regression trend.

6. **[#8593 — Desktop: markdown links styled but unclickable](https://github.com/QwenLM/qwen-code/issues/8593)** (P2, UI)  
   Markdown links in assistant messages are styled (accent color, hover underline) but silently do nothing on click. A UX gap that erodes trust in the Desktop's interactive capabilities.

7. **[#8550 — `qwen mcp list` hangs indefinitely on SSE servers](https://github.com/QwenLM/qwen-code/issues/8550)** (P2, CLI/MCP)  
   `qwen mcp list` blocks forever if an SSE MCP server accepts the HTTP connection but never emits the legacy `endpoint` event. A robustness issue for production MCP workloads.

8. **[#8672 — Middle-mouse selection broken in PuTTY over SSH (regression)](https://github.com/QwenLM/qwen-code/issues/8672)** (P2, CLI)  
   After upgrading to v0.21.1, middle/right mouse button selection is broken in PuTTY sessions, breaking a common xterm-style workflow for remote developers.

9. **[#8695 — Context usage percentage displayed twice](https://github.com/QwenLM/qwen-code/issues/8695)** (P3, UI)  
   With the default status line visible, context usage appears both in the status line and the footer — a minor but noted duplication that clutters the interface.

10. **[#7118 — Windows installer fails when PowerShell can't resolve Get-FileHash](https://github.com/QwenLM/qwen-code/issues/7118)** (P2, Windows)  
    The standalone installer fails SHA-256 verification when `Get-FileHash` cannot be resolved, forcing users to fall back to npm installation. Persistent since July; 3 👍 indicate community impact.

## Key PR Progress
1. **[#8526 — `feat(cli): expose reasoning effort through ACP`](https://github.com/QwenLM/qwen-code/pull/8526)** (Open)  
   Adds a standard ACP session selector for reasoning effort (`thought_level` from Default to Max) with `session/set_config_option` support — giving ACP clients programmatic control over reasoning tiers.

2. **[#8528 — `fix(acp): emit standard context usage updates`](https://github.com/QwenLM/qwen-code/pull/8528)** (Open)  
   Emits standard ACP `usage_update` notifications after each model round, reporting prompt context occupancy with fallback to provider total tokens — improving client-side context visibility.

3. **[#8613 — `feat(web-shell): tmux-backed interactive terminal sub-agent`](https://github.com/QwenLM/qwen-code/pull/8613)** (Open)  
   Enables agents to run interactive CLIs (REPLs, other agent CLIs, TUI apps) inside a tmux session, surfaced as a live terminal view in Web Shell. A significant step for interactive sub-agent workflows.

4. **[#8687 — `feat(daemon): guard cross-worktree Git mutations`](https://github.com/QwenLM/qwen-code/pull/8687)** (Open)  
   Adds a host-side guard that blocks model-issued `run_shell_command` calls when Git commands (`-C`, `--work-tree`, `--git-dir`) escape the session's workspace — a security hardening for `qwen serve`.

5. **[#8694 — `feat(workflows): add orchestration policy layer to Workflow tool description`](https://github.com/QwenLM/qwen-code/pull/8694)** (Open)  
   Rewrites the `Workflow` tool description with a policy layer (when to use workflows, sizing, orchestration shape, verification guidance) alongside existing runtime facts, improving model decision quality.

6. **[#8509 — `fix(cli): keep stream-json sessions alive after interrupt`](https://github.com/QwenLM/qwen-code/pull/8509)** (CLOSED)  
   Separates session lifetime from active-turn cancellation — protocol `interrupt` now aborts only the current turn's controller, while stdin close and SIGINT/SIGTERM still terminate the session. Closes the regression in #8495.

7. **[#8614 — `feat(web-shell): add fullscreen view for the right artifact panel`](https://github.com/QwenLM/qwen-code/pull/8614)** (Open)  
   Adds a fullscreen toggle for the Web Shell right panel (artifacts, subagents, review changes, monitors, scheduled tasks) — improving workspace ergonomics for complex sessions.

8. **[#8481 — `fix(cli): prefer wl-copy on Wayland`](https://github.com/QwenLM/qwen-code/pull/8481)** (Open)  
   Native Wayland sessions now prefer `wl-copy` for application-managed copying, with fallback to `xclip`, `xsel`, and OSC 52 — fixing clipboard behavior on Wayland-only environments.

9. **[#8616 — `feat(telemetry): align session lifecycle with OpenTelemetry`](https://github.com/QwenLM/qwen-code/pull/8616)** (Open)  
   Emits standard `session.start` and `session.end` LogRecords with `event.name` and `session.id`, plus `session.previous_id` for resumed conversations — standardizing telemetry with the broader OTel ecosystem.

10. **[#8683 — `fix(review): stop the agent transcript from executing workflow commands`](https://github.com/QwenLM/qwen-code/pull/8683)** (Open)  
    Wraps the review agent's invocation in `::stop-commands::` so its transcript can't accidentally execute workflow commands — a critical safety fix for review pipelines.

## Feature Request Trends
- **Browser/WebBridge control (#8699)**: Direct browser-command bridge via `qwen serve` (inspired by Kimi WebBridge), avoiding MCP as a mandatory path for automation.
- **Local Control / phone access (#8595)**: QR-code pairing to access and control local sessions from a phone, zero manual setup — CLI + desktop app.
- **Monorepo of Web Shell consolidation (#8092, #6699, #6701)**: Continued push to make Web Shell the single UI surface (desktop wrapper, composer toolbar redesign, "Start In" context selector).
- **Agentic workflow policy (#8690, #8701)**: Users and maintainers both pushing for explicit orchestration policies and evidence-based verification — "先验证再下结论" (verify before concluding) is now a formal proposal.
- **Telemetry standardization (#8660, #8697)**: Alignment with OpenTelemetry conventions, including OTLP exporter compatibility fixes.
- **Internationalization (#8551, #8625)**: Korean docs support request alongside Chinese input rendering fixes on Windows.

## Developer Pain Points
- **Windows UX gaps**: Persistent issues across IME input display (#8625), standalone installer PowerShell dependency (#7118), and bundle runtime path crashes (#8615) — Windows continues to be the most problematic platform.
- **Terminal rendering regressions**: Flickering in tmux (#8562) and web-based terminals (#8659), plus broken mouse selection in PuTTY (#8672), suggest recent TUI changes introduced cross-terminal compatibility issues. The `useTerminalBuffer: true` default is a suspected culprit.
- **Telemetry env-var fragility (#8697)**: Setting `OTEL_METRICS_EXPORTER=otlp` (common in multi-tool environments) can silently kill all native metrics export — a silent failure that confuses teams diagnosing missing data.
- **MCP robustness (#8550)**: `qwen mcp list` hanging indefinitely on non-conforming SSE servers is a reliability gap for teams experimenting with MCP-based tooling.
- **Integration test hygiene (#8692)**: `integration-tests/tsconfig.json` has never type-checked due to a malformed `compilerOptions.paths` key — a "new project" quality issue that signals a need for stricter CI gates on new test infrastructure.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-08

## 1. Today's Highlights

The DeepSeek TUI (CodeWhale) project is actively converging on the v0.9.4 release, with maintainer-driven PR #5282 clearing four CI blockers to unblock shipping. Meanwhile, a significant README overhaul (PR #5283) reframes the project's identity around "mixed fleets" — any model in any role — reflecting a major architectural shift toward multi-agent orchestration, while community PRs contribute fixes for sub-agent workspace bugs, session title caching, and MCP registry performance. The project remains highly discussion-driven, with 50 open threads, many centered on subagent reliability, resource exhaustion, and release readiness.

## 2. Releases

No new releases in the last 24 hours. The project is currently at v0.9.4 with a pending release train; PR #5282 addresses the final CI blockers holding the release.

## 3. Hot Issues

**#2934 — feat: sidebar sessions panel** [CLOSED]
A long-running enhancement (13 comments) proposing a persistent sidebar for session browsing and auto-resume, addressing friction where users must remember `Ctrl+R` to find old conversations. High community engagement signals strong demand for better session management UX.
[Link](https://github.com/Hmbown/CodeWhale/issues/2934)

**#1425 — Large text processing hangs on agent_wait timeout** [OPEN]
A user analyzing a 3-million-character novel hit a critical bug: 10 sub-agents launched in parallel got stuck in `agent_wait` timeouts, freezing the session. The root cause appears to be a stale agent state being misinterpreted as "running." This is a canonical example of subagent orchestration reliability issues.
[Link](https://github.com/Hmbown/CodeWhale/issues/1425)

**#4785 — Dead-code sweep: 464 #[allow(dead_code)] attributes** [OPEN]
Maintainer-flagged technical debt: the codebase has 464 dead-code allowances across 143 files, suppressing compiler diagnostics and hiding structural drift. A "wall" that makes refactoring and reliability work harder than it should be.
[Link](https://github.com/Hmbown/CodeWhale/issues/4785)

**#2492 — No cross-session memory** [OPEN]
Users report that the TUI forgets prior session context on restart, and even when memory is written, it isn't read back automatically. Community notes the response speed is excellent but persistent memory is a major missing feature.
[Link](https://github.com/Hmbown/CodeWhale/issues/2492)

**#425 — Subagents: add resume_from continuation chains** [CLOSED]
Closed enhancement requesting a `task_id` parameter for `agent_spawn` to resume prior subagents rather than starting fresh. Addresses the common failure mode where long-running delegated work must be restarted from scratch.
[Link](https://github.com/Hmbown/CodeWhale/issues/425)

**#5123 — Release-blocker: agent spawn surface has too many knobs** [OPEN]
Dogfooded on 0.9.4: labeled builder agents run read-only and self-BLOCK when they lack write capability. The tool contract (read-only vs. write) is not aligned with the agent's labeled role — a critical UX and reliability gap for the fleet/roster system.
[Link](https://github.com/Hmbown/CodeWhale/issues/5123)

**#3306 — Refactor: converge runtime ownership, delete duplication** [OPEN]
A v0.9.3 umbrella issue noting 18 Rust packages (~771k lines) with 87% living inside `codewhale-tui`. Parallel runtime/tool/config/session/hook paths are a maintenance burden and reliability risk.
[Link](https://github.com/Hmbown/CodeWhale/issues/3306)

**#5161 — execpolicy deny rules evadable** [CLOSED]
Security bug: `command_segments` splits on `&&`, `||`, `|`, `;` but not single `&` or subshell wrappers, allowing deny rules to be bypassed (`ls & rm -rf /` stays one segment). Closed, presumably fixed, but highlights ongoing security hardening.
[Link](https://github.com/Hmbown/CodeWhale/issues/5161)

**#5034 — Provider switch retains unrelated default model** [OPEN]
Switching providers can leave a stale default model (e.g., `gpt-5.5` after switching to a different provider). Provider and model resolution need to be updated as one coherent unit — an important correctness bug for users running mixed fleets.
[Link](https://github.com/Hmbown/CodeWhale/issues/5034)

**#5187 — turn_meta churns bytes on every user message** [CLOSED]
Closed "pleasantness audit" finding: the engine appends a large `<turn_meta>` block to every user message (date, workspace path, permission posture, context pressure, etc.), creating byte churn and possibly guiding the model toward unwanted caution. Fix: emit only on change.
[Link](https://github.com/Hmbown/CodeWhale/issues/5187)

## 4. Key PR Progress

**#5282 — fix(release): clear four CI blockers holding v0.9.4** [CLOSED]
Maintainer PR resolving the last red lanes preventing the v0.9.4 release. Directly unblocks the release train. Merged.
[Link](https://github.com/Hmbown/CodeWhale/pull/5282)

**#5283 — docs(readme): lead with mixed fleets** [CLOSED]
Reframes the README to highlight that roles within a single fleet can span different models and vendors, not just mid-task switching. Aligns documentation with the fleet architecture.
[Link](https://github.com/Hmbown/CodeWhale/pull/5283)

**#5284 — fix(subagent): stop counting finished children as shared-checkout contenders** [OPEN]
Fixes a real bug where a builder sub-agent couldn't run `echo x > file` because finished children were still counted as contenders for the shared workspace. Improves shared-workspace write claims.
[Link](https://github.com/Hmbown/CodeWhale/pull/5284)

**#5255 — Layer 5.3: Palette, completion, and discovery filtering** [OPEN]
Contributes to the command-boundary refactor: verifies and consolidates user-command integration in command palette and slash-completion surfaces (Layer 5.3 following 5.2 in #4992).
[Link](https://github.com/Hmbown/CodeWhale/pull/5255)

**#5258 — fix(tui): stop stale cached session title from pinning New Session** [OPEN]
Fixes a session-title bug where titles stuck at "New Session" because a stale copy in the in-memory metadata cache overwrote the computed title. Session snapshots done right.
[Link](https://github.com/Hmbown/CodeWhale/pull/5258)

**#5256 — feat(mcp): background incremental registry sync** [OPEN]
Performance win: `registry_sync` now serves a fresh local snapshot with zero network requests and runs downloads in the background via tokio, guarded by a process-wide mutex. Fast and safe.
[Link](https://github.com/Hmbown/CodeWhale/pull/5256)

**#5254 — Build fix for FreeBSD** [CLOSED]
Adds a build fix for FreeBSD where `rquickjs` doesn't ship bindings. Community-contributed portability improvement. Merged.
[Link](https://github.com/Hmbown/CodeWhale/pull/5254)

**#5257 — feat(config): add model = auto for prompt-based tier selection** [OPEN]
New config option that auto-selects between `deepseek-v4-pro` (complex) and `deepseek-v4-flash` (simple) based on prompt analysis. Directly addresses cost/performance tradeoff UX.
[Link](https://github.com/Hmbown/CodeWhale/pull/5257)

**#5252 — feat(subagents): allow embedders to isolate runtime state roots** [CLOSED]
Adds `EngineConfig::subagent_state_root` for embedding hosts needing session-owned delegated-agent state, while keeping legacy defaults unchanged. Merged.
[Link](https://github.com/Hmbown/CodeWhale/pull/5252)

**#5229 — docs: Windows beginner guide in zh-CN** [CLOSED]
Community documentation contribution: a Chinese-language Windows beginner guide with validated commands and screenshots (tested on Windows 10). Merged.
[Link](https://github.com/Hmbown/CodeWhale/pull/5229)

## 5. Feature Request Trends

1. **Session & memory persistence** — Requests for persistent sidebar panels, auto-resume, and cross-session memory dominate. Users want a durable "workspace" that survives restarts (issues #2934, #2492, #3303).

2. **Subagent lifecycle management** — Resume chains, advisor watchers, and multi-named fleet configurations repeatedly surface. The community wants fine-grained control over delegated agents, including role-specific models and policies (issues #425, #3982, #5039, #5038).

3. **MCP ergonomics & hot-reload** — Users want model-visible MCP tool pools to hot-reload without full restarts, plus faster registry sync (issues #4068, PR #5256).

4. **Fleet/roster model capability visibility** — Multiple requests to surface model capabilities during fleet configuration and roster management, so users can make informed choices (issue #5038).

5. **Plan artifacts & auditability** — Persist reviewable plan documents with line comments, plus structured compaction survival contracts, indicating a push toward stronger governance and replayability (issues #4390, #4394).

## 6. Developer Pain Points

1. **Subagent timeouts and hangs** — Recurring reports (~#1425, #4416) of sessions freezing when sub-agents exceed `agent_wait` timeouts or when stale failed-agent state leaks into new sessions. Reliability of parallel delegation is the #1 frustration.

2. **Resource exhaustion in long contexts** — Large text processing and long coding turns hit memory bloat or context pressure; users report "卡死" (freeze/hang) as a primary symptom.

3. **Read-only tool contract confusion** — Labelled builder agents run read-only and self-BLOCK; the mismatch between role labels and actual tool permissions confuses users and breaks delegation (issue #5123).

4. **Config/gate persistence gaps** — Documented config knobs cannot be discovered, edited, or persisted from the TUI; exec-policy deny rules are evadable; provider/model resolution is inconsistent (issues #3303, #5161, #5034).

5. **Credential and approval UX friction** — Save confirmations name the wrong destination, credential precedence is unintuitive, and user-typed `!` shell commands incorrectly trigger approval modals (issues #5195, #5197, #5191).

6. **Test/CI flakiness** — Fleet roster tests read real user configs and fail on developer machines; release-blocking CI has been red for multiple runs — a clear signal of fragility in the test environment isolation (issue #5151, PR #5282).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*