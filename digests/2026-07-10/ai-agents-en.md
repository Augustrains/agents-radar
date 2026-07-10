# OpenClaw Ecosystem Digest 2026-07-10

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-10 01:27 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-10

---

## 1. Today's Overview

OpenClaw is experiencing a period of **high engineering velocity** alongside **significant stability friction**. The project saw 500 issues and 500 PRs updated in the last 24 hours, with 210 PRs merged or closed and 317 open/active issues remaining. No new releases were published today, but a large body of critical P1 bugs — particularly around **silent message loss, session state corruption, and authentication reliability** — continue to dominate the tracker. The maintainer team (led by `steipete`) contributed heavily today with several PRs targeting CI reliability, UI lifecycle tests, release validation, and the charming but peripheral "Lobsterdex" feature. Meanwhile, the community is grappling with regressions in the Codex OAuth path, Discord/Telegram/WhatsApp session wedging, and a worrying trend where tool outputs render as unreadable images.

---

## 2. Releases

**No new releases in the last 24 hours.** There are no migration notes, changelogs, or version bumps to report.

---

## 3. Project Progress

Today's merged/closed activity (210 items) includes several important fixes:

- **Slack session deduplication fix** ([#103141](https://openclaw/openclaw/pull/103141)) — resolves mpDM bot messages creating two parallel sessions per agent by persisting resolved channel types.
- **Telegram TTS text churn elimination** ([#83988](https://openclaw/openclaw/pull/83988)) — deferred text settlement for final-mode TTS to prevent brief visible text before voice note replacement.
- **Release notes validation** ([#103222](https://openclaw/openclaw/pull/103222)) — ensures GitHub release bodies don't exceed limits before publishing.
- **Slack channel ID case preservation** ([#103214](https://openclaw/openclaw/pull/103214)) — fixes `channel_not_found` errors from lowercased delivery targets.
- **CI reliability** ([#103223](https://openclaw/openclaw/pull/103223), [#103217](https://openclaw/openclaw/pull/103217)) — MCP timeout retry failures and performance gate exclusions for setup RSS.

**Notable feature progress:**
- **Interactive parity with Codex runtime** ([#102261](https://openclaw/openclaw/pull/102261), still open) — a major PR adding `ask-user-question`, `plan mode`, and `goal mode` to every OpenClaw session, styled as "The agent that asks, plans, and pursues."
- **Durable workflow worker loop** ([#102983](https://openclaw/openclaw/pull/102983), still open) — an opt-in durable runtime stack, PR 5/5 in the series.
- **Windows MXC sandbox backend** ([#97086](https://openclaw/openclaw/pull/97086), still open) — adds Microsoft eXecution Containers support for Windows hosts.

---

## 4. Community Hot Topics

The following issues and PRs have drawn the most community engagement and signal real user pain:

### Most Active Issues (by comment count)

1. **[#44925](https://openclaw/openclaw/issues/44925)** — [OPEN] *"Subagent completion silently lost — no retry, no notification, no auto-restart on timeout"* (21 comments, P1, Diamond Lobster)
   - **Underlying need:** Users running subagent orchestrations (Telegram forum mode, complex workflows) have no visibility when a subagent fails silently. The model moves on without completing the subtask. This is a **trust-breaking reliability gap** that erodes confidence in multi-agent systems.

2. **[#63918](https://openclaw/openclaw/issues/63918)** — [CLOSED] *"Cron agentTurn sends thinking=none to OpenAI (gpt-5-nano 400)"* (18 comments)
   - **Underlying need:** Cron job configurations using `payload.kind=agentTurn` fail because the thinking value `none` is rejected by certain models. This is a **configuration inconsistency** where the runtime should validate or default to a supported value.

3. **[#99241](https://openclaw/openclaw/issues/99241)** — [OPEN] *"Tool outputs sometimes render as image attachments and become unreadable to the agent"* (15 comments, P1, Platinum Hermit)
   - **Underlying need:** A **critical text accessibility issue** — long-running or ANSI-heavy tool outputs collapse into image placeholders, making stdout/stderr invisible to the LLM. This breaks debugging and evidence-driven workflows. The community is watching this closely.

4. **[#73148](https://openclaw/openclaw/issues/73148)** — [CLOSED] *"Image tool: opaque 'Failed to optimize image' when sharp is not installed"* (15 comments)
   - **Underlying need:** Missing native dependency feedback — users get a cryptic error instead of a helpful "install sharp" message. This is a **UX polish issue** that frustrates self-hosters.

5. **[#48003](https://openclaw/openclaw/issues/48003)** — [OPEN] *"Steer mode does not inject messages mid-turn for main sessions"* (15 comments, P1, Diamond Lobster)
   - **Underlying need:** The `steer` messaging mode is supposed to inject user messages mid-turn, but a regression from March 2026 broke this. Users relying on real-time steering find it **non-functional**.

### Most Upvoted

- **👍 4:** Issue [#45608](https://openclaw/openclaw/issues/45608) — *Pre-reset agentic memory flush*: Strong support for silent memory flush before destructive commands.
- **👍 3:** Issue [#73148](https://openclaw/openclaw/issues/73148) — *Image tool failure with missing sharp* (closed, but high engagement).
- **👍 3:** Issue [#84569](https://openclaw/openclaw/issues/84569) — *WhatsApp session stalls on long model_call*: Concern from WhatsApp power users.
- **👍 3:** Issue [#48003](https://openclaw/openclaw/issues/48003) — *Steer mode injection broken*.

### Most Active PRs

- **PR #102261** (55 lines of summary, "Interactive parity with Codex") — the **largest feature PR** in the pipeline, touching 20+ files (docs, Slack, web-ui, gateway, scripts, agents, Codex extension). Community eager for ask-user-question interactivity.
- **PR #102983** ("Durable workflow worker loop") — the **most architecturally significant** PR currently open, implementing the durable core runtime. Notably uses blank template and dirty-candidate triage labels.

---

## 5. Bugs & Stability

Today's tracker shows a **concerning density of P1 bugs** affecting core reliability. Ranked by severity:

### Critical (P1, possible message loss or crash)

| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#99241](https://openclaw/openclaw/issues/99241) | Tool outputs → image attachments, unreadable to agent | Needs product decision |
| [#84569](https://openclaw/openclaw/issues/84569) | WhatsApp session stalls on long model_call, reply never delivered | Linked PR open |
| [#89278](https://openclaw/openclaw/issues/89278) | Codex OAuth refresh succeeds but cron/heartbeat fail with 10s timeout | Needs maintainer review |
| [#96834](https://openclaw/openclaw/issues/96834) | WhatsApp 1:1 image wedges lane ~3min before processing | Needs live repro |
| [#99912](https://openclaw/openclaw/issues/99912) | Agent heartbeat routes to wrong agent's session | CLOSED |
| [#94251](https://openclaw/openclaw/issues/94251) | Ollama remote provider streaming not consumed | Needs live repro |
| [#102175](https://openclaw/openclaw/issues/102175) | `room_event` forces `message_tool_only`, destabilizing prompt cache | Needs product decision |
| [#49876](https://openclaw/openclaw/issues/49876) | Cron sessions hallucinate output on tool failure instead of failing cleanly | Needs security review |
| [#54155](https://openclaw/openclaw/issues/54155) | Gateway memory leak: 389MB → 14.7GB over 4 days | Needs live repro |
| [#52249](https://openclaw/openclaw/issues/52249) | ACP parent session stuck until refresh when child completes | Needs product decision |

### High (P1/P2, data loss or security)

| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#45740](https://openclaw/openclaw/issues/45740) | `gh-issues` skill: untrusted issue body injected directly into sub-agent prompt | Needs security review |
| [#45049](https://openclaw/openclaw/issues/45049) | Agent loop allows simulated tool calls instead of real invocation | Needs security review |
| [#46786](https://openclaw/openclaw/issues/46786) | `tools.elevated.enabled: true` breaks exec routing logic (all exec goes to host) | Needs security review |
| [#92516](https://openclaw/openclaw/issues/92516) | Self-hosted container deploys can't use externalized channel plugins | Needs security review |
| [#53408](https://openclaw/openclaw/issues/53408) | Write/exec tool parameters silently dropped after long conversations | Needs live repro |

### Regression (worked before, now fails)

- **Codex OAuth refresh timeout** ([#89278](https://openclaw/openclaw/issues/89278), P1)
- **All tool results rendered as images in Discord** ([#100782](https://openclaw/openclaw/issues/100782), CLOSED)
- **Room event destabilizes prompt cache** ([#102175](https://openclaw/openclaw/issues/102175), P1)
- **Sandbox container exits immediately with `no-new-privileges`** ([#43996](https://openclaw/openclaw/issues/43996), P1)

### Newly Reported (today)

- **PR #103220** ([#103220](https://openclaw/openclaw/pull/103220)) — Fix for zero-argument XML tool calls being rejected (critical for models emitting `<function=get_system_info></function>` style).
- **PR #103216** ([#103216](https://openclaw/openclaw/pull/103216)) — Fix for Azure deployment maps with mixed-case model IDs.

---

## 6. Feature Requests & Roadmap Signals

### Strong Community Demand

1. **Skill Priority Configuration** ([#50199](https://openclaw/openclaw/issues/50199), P2, 8 comments) — Users want intelligent skill selection when multiple skills overlap. High demand in multi-skill environments.

2. **Persistent task-status surface** ([#52640](https://openclaw/openclaw/issues/52640), P2, 7 comments, 2 👍) — Long-running channel turns need an authoritative status surface beyond typing indicators.

3. **YAML config support** ([#45758](https://openclaw/openclaw/issues/45758), P3, 7 comments, 2 👍) — DevOps users want YAML as an alternative to JSON5 for configuration.

4. **Configurable session startup message** ([#45501](https://openclaw/openclaw/issues/45501), P2, 6 comments) — Users want to customize the `/new` and `/reset` startup prompt rather than the hardcoded version.

### Most Likely for Next Release

Based on PR velocity and maintainer attention:
- **Ask-user-question / plan mode / goal mode** ([#102261](https://openclaw/openclaw/pull/102261)) — This PR is massive (XL size, 5 merge-risk labels) and represents the next **major interactive parity milestone**. Likely to land in the next minor release.
- **Durable workflow worker loop** ([#102983](https://openclaw/openclaw/pull/102983)) — The final PR in a 5-PR stack. If merged, this unlocks durable execution for workflows.
- **Stranded message-tool final recovery** ([#99536](https://openclaw/openclaw/pull/99536)) — A P1 fix for the common failure where substantive final answers are never delivered. Very likely to ship soon.

### Long-term Signals

- **Pre-reset agentic memory flush** ([#45608](https://openclaw/openclaw/issues/45608)) has 4 👍 and 11 comments — growing consensus for memory preservation before destructive commands.
- **System event priority mode** ([#50739](https://openclaw/openclaw/issues/50739), 2 👍) — users want bypass-queue injection for critical alerts.

---

## 7. User Feedback Summary

### Pain Points (most reported)

1. **Silent failures** — Subagent completions lost (`#44925`), cron tasks hallucinate output (`#49876`), tool parameters dropped (`#53408`). Users are frustrated by **non-obvious failures** that require digging through logs.

2. **Channel wedging** — WhatsApp stalls for 3 minutes on image input (`#96834`), Telegram replay duplicates (`#51628`), Telegram session corruption (`#43549`). **Native/niche channels are second-class citizens** of reliability.

3. **Authentication friction** — Codex OAuth 10s timeout (`#89278`), GitHub Copilot auth order ignored (`#46031`), Telegram restart storm (`#52130`). **Multiple auth paths have untested edge cases.**

4. **Missing dependency feedback** — `sharp` not installed (`#73148`), `python3` missing from sandbox (`#57713`). Users want **actionable error messages**, not opaque failures.

### Satisfaction Signals

- High engagement on the **Lobsterdex** feature (PR #103172) and **dreams scene** (PR #103167) — users appreciate whimsical community-oriented features.
- **WhatsApp list reply support** (PR #83600, waiting on author) — shows demand for richer channel interactivity.
- Many closed issues (183) in 24h indicates **responsive maintainer triage**, even if resolution isn't always immediate.

### Use Cases Highlighted

- **Telegram forum bot** — multi-agent orchestration in forum threads (#44925, #52130)
- **Cron agent jobs** — automated standalone tasks with reliability concerns (#49876, #45494, #89278)
- **WhatsApp business flows** — interactive list replies, image processing (#83600, #96834)
- **Self-hosted container deploys** — plugin unbundling headaches (#92516, #73148)
- **Azure OpenAI users** — deployment map casing inconsistencies (#103216)
- **Codex users** — interactive parity with ask-user-question (#102261)

---

## 8. Backlog Watch

The following important items have been **open for extended periods** without maintainer resolution:

### Long-unanswered Issues (open 3+ months)

| Issue | Created | Last Updated | Comments | Status |
|-------|---------|--------------|----------|--------|
| [#44925](https://openclaw/openclaw/issues/44925) | 2026-03-13 | 2026-07-09 | 21 | Needs maintainer review, needs product decision |
| [#48003](https://openclaw/openclaw/issues/48003) | 2026-03-16 | 2026-07-09 | 15 | Needs maintainer review, needs product decision |
| [#45740](https://openclaw/openclaw/issues/45740) | 2026-03-14 | 2026-07-09 | 14 | Needs maintainer review, needs product decision |
| [#45608](https://openclaw/openclaw/issues/45608) | 2026-03-14 | 2026-07-09 | 11 | Needs maintainer review, needs product decision |
| [#49876](https://openclaw/openclaw/issues/49876) | 2026-03-18 | 2026-07-09 | 9 | Needs maintainer review, needs product decision, needs security review |
| [#50126](https://openclaw/openclaw/issues/50126) | 2026-03-19 | 2026-07-09 | 6 | Needs maintainer review, needs product decision, needs security review |
| [#50739](https://openclaw/openclaw/issues/50739) | 2026-03-20 | 2026-07-09 | 7 | Needs maintainer review, needs product decision, needs security review |
| [#45718](https://openclaw/openclaw/issues/45718) | 2026-03-14 | 2026-07-09 | 6 | Needs maintainer review, needs product decision |
| [#45565](https://openclaw/openclaw/issues/45565) | 2026-03-14 | 2026-07-09 | 7 | Needs maintainer review, needs product decision |
| [#45224](https://openclaw/openclaw/issues/45224) | 2026-03-13 | 2026-07-09 | 6 | Needs maintainer review, needs product decision |

### Critical backlog items needing security review

- **`gh-issues` skill prompt injection vector** ([#45740](https://openclaw/openclaw/issues/45740)) — raw issue bodies injected into sub-agent prompts. **This is a security vulnerability** that has been open since March 14, 2026 (nearly 4 months).
- **Sandbox `no-new-privileges` breakage** ([#43996](https://openclaw/openclaw/issues/43996)) — containers exit with `operation not permitted` — open since March 12.
- **Agent loop allows simulated tool calls** ([#45049](https://openclaw/openclaw/issues/45049)) — models can generate fake "tool usage" text instead of real calls — open since March 13.

### PRs pending maintainer attention (long-open)

- **WhatsApp list reply actions** ([#83600](https://openclaw/openclaw/pull/83600)) — open since May 18, 2026 (7+ weeks), proof supplied, waiting on author.
- **Node allowlist writeback restoration** ([#78226](https://openclaw/openclaw/pull/78226)) — open since May 6, 2026 (9+ weeks), needs real-behavior proof.
- **Plugin API compatibility diagnostics** ([#94019](https://openclaw/openclaw/pull/94019)) — open since June 17, 2026 (3+ weeks), needs proof.
- **Deferred text settlement for TTS** ([#83988](https://openclaw/openclaw/pull/83988)) — open since May 19, 2026, proof sufficient, waiting on author.

### Risk Assessment

The **longest-standing unaddressed vulnerabilities** involve prompt injection (#45740) and sandbox enforcement (#43996). Combined with the **silent tool simulation** (#45049), these represent a **trust and safety gap** that grows with each passing week. The maintenance team appears to be prioritizing new feature work (#102261, #102983) and CI improvements (#103222, #103223) over these older security issues.

---

**Summary:** OpenClaw is **thriving in complexity** but **straining under its own reliability debt**. The community continues to grow while the burden of maintaining stable multi-channel, multi-model orchestration across Telegram, Discord, WhatsApp, Slack, Signal, and QQBot manifests as a steady stream of P1 regressions and session lifecycle bugs. The next release will likely focus on **interactive parity** (ask-user-question, plan mode) and **durable workflows** — but the silent message loss issues and unresolved security vulnerabilities should give the team pause before shipping major new surfaces.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — 2026-07-10

## 1. Ecosystem Overview

The open-source personal AI assistant and agent ecosystem is experiencing a period of **intense maturation**, characterized by high engineering velocity across core projects, simultaneous stabilization efforts, and a clear divergence in architectural philosophy. The ecosystem is now grappling with the consequences of rapid feature expansion: **reliability debt**, **security vulnerabilities**, and **fragmented user experiences** across messaging channels. Multiple projects are converging on shared challenges—multi-agent orchestration, durable workflows, interactive parity, and channel-specific reliability—while differentiating on target users (developer-centric vs. generalist, self-hosted vs. cloud) and core architecture (monolithic vs. modular, local-first vs. gateway-mediated). The ecosystem shows strong community engagement, with thousands of issues and PRs updated daily, but also reveals growing pains as projects scale beyond their initial design envelopes.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | PRs Merged/Closed (24h) | Release Status | Health Score |
|---------|---------------------|-------------------|------------------------|----------------|--------------|
| **OpenClaw** | 500 | 500 | 210 | No new release; P1 bug density high | ⚠️ High velocity, high reliability debt |
| **NanoBot** | 23 | 22 | 5 | Pre-0.2.2 state; point release likely | ✅ Healthy, active regressions under fix |
| **Hermes Agent** | 50 | 50 | 18 | No new release; stabilization phase | ⚠️ High bug density, rapid fix response |
| **PicoClaw** | 3 | 16 | 4 | v0.2.9 latest; RC approaching | ✅ Stable, focused maintenance |
| **NanoClaw** | 9 | 17 | 3 | No new release; security patch imminent | ⚠️ Security disclosures active |
| **NullClaw** | 0 | 0 | 0 | N/A (inactive) | 🔴 No activity |
| **IronClaw** | 32 | 50 | 28 | RC pending (0.29.1); no release today | ⚠️ Heavy bug bash, Slack auth issues |
| **LobsterAI** | 0 | 14 | 11 | No new release; backlog clearing | ✅ Stable, low community activity |
| **Moltis** | 0 | 1 | 0 | Latest release unchanged | ✅ Clean state, zero open issues |
| **CoPaw** | 35 | 50 | 32 | v2.0.0-beta.5 released yesterday | ⚠️ Major version growing pains, high engagement |
| **ZeptoClaw** | 0 | 0 | 0 | N/A (inactive) | 🔴 No activity |
| **ZeroClaw** | 36 | 50 | 11 | v0.8.2 latest; v0.8.3/v0.9.0 in progress | ✅ High velocity, stable pre-release |
| **TinyClaw** | 0 | 0 | 0 | N/A (inactive) | 🔴 No activity |

**Health Score Key:** ✅ Active/Stable | ⚠️ Active with concerns | 🔴 Inactive

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale:** OpenClaw processes 500+ issues and PRs daily—10x more than any other project in the ecosystem. This reflects the largest community and contributor base.
- **Channel breadth:** Supports Telegram, Discord, WhatsApp, Slack, Signal, QQBot, and Matrix—more native channel integrations than any peer. IronClaw and CoPaw have deeper Slack/Feishu integrations but narrower overall coverage.
- **Interactive parity ambitions:** The massive PR #102261 (ask-user-question, plan mode, goal mode) is a differentiator—no other project has a comparable feature pipeline for bidirectional agent-user interaction.
- **Durable workflow investment:** PR #102983 (durable core runtime) is architecturally unique. Most peers (NanoBot, Hermes, CoPaw) focus on session lifecycle within a single runtime; OpenClaw is building multi-session durability.

**Technical Approach Differences:**
- **Monolithic core, modular channels:** OpenClaw uses a single core runtime with channel-specific adapters. This contrasts with ZeroClaw's gateway-focused architecture and CoPaw's CoW (Cooperative Work) pattern. The monolithic approach enables feature parity across channels but creates a single point of failure for reliability.
- **Heavy MCP/Codex integration:** OpenClaw's deep integration with Codex runtime (ask-user-question, plan mode) distinguishes it from peers. Most other projects support Codex as a provider; OpenClaw extends Codex's interaction model.

**Community Size Comparison:**
- OpenClaw has the largest community by a wide margin (500 issues/PRs updated vs. 50 for Hermes/IronClaw/ZeroClaw). However, this scale creates **triaging bottlenecks**—critical P1 bugs (silent message loss, session state corruption, OAuth timeouts) persist for months without resolution.
- LobsterAI (240+ stars) and Moltis (clean repo, GPT-5.6 support) target smaller, community-driven ecosystems.

**Vulnerability:**
- OpenClaw's reliability debt—particularly around silent failures (subagent completion loss #44925, tool output image collapse #99241)—is the most severe in the ecosystem. Users trust is eroding despite high feature velocity. The maintenance team prioritizes new feature work (#102261, #102983) over longstanding security vulnerabilities (#45740 prompt injection, open since March).

---

## 4. Shared Technical Focus Areas

**1. Multi-Agent Orchestration (OpenClaw, NanoBot, CoPaw, ZeroClaw)**
- OpenClaw: Subagent lifecycle management (#44925—silent loss, #49876—cron hallucination)
- NanoBot: Subagent control planes (#1006), subagent lifecycle improvements
- CoPaw: Cowork/Cooperative Work pattern (v2.0.0-beta.5)
- ZeroClaw: Channel-based multi-agent routing (#7836)
- **Common need:** Deterministic subagent execution with failure visibility, no silent message loss.

**2. Interactive Parity & Bidirectional Communication (OpenClaw, NanoBot, IronClaw)**
- OpenClaw: PR #102261 (ask-user-question, plan mode, goal mode)
- NanoBot: Task-specific model configuration (#912), scheduled task orchestration
- IronClaw: Approval workflow notifications (#5553—disappearing notifications)
- **Common need:** Real-time agent-to-user interaction (approval flows, questions, progress updates) across all channels.

**3. Durable / Scheduled Execution (OpenClaw, NanoBot, IronClaw, Nanoclaw, CoPaw)**
- OpenClaw: Durable workflow worker loop (#102983)
- NanoBot: Cron job model presets (#4622), task scheduling
- IronClaw: Routine lifecycle management (#5836—"No thread attached")
- NanoClaw: Scheduled tasks train (#2981, #2988, #2992)
- CoPaw: Scheduled task notifications (#5797—toggle demand)
- **Common need:** Reliable, observable scheduled execution that survives restarts and network disruptions.

**4. Channel-Specific Reliability (All active projects)**
- **Telegram:** OpenClaw (#44925, #52130), NanoClaw (#2989, #2990, #2991), CoPaw (stable)
- **WhatsApp:** OpenClaw (#84569, #96834), NanoBot (#4823—group regression), ZeroClaw (#7535)
- **Slack:** OpenClaw (#103141), IronClaw (#5877, #5882, #5898—five bugs)
- **Discord:** OpenClaw (#100782), ZeroClaw (#7831)
- **Matrix:** PicoClaw (#3203—sync loop death), NanoBot (#4859—mxc fix)
- **Common need:** Each channel has unique failure modes; universal reliability remains unsolved.

**5. Configuration & Onboarding Friction (Hermes, NanoBot, PicoClaw, ZeroClaw)**
- Hermes: Malformed YAML crashes (#58361, #61733)
- NanoBot: CLI commands missing from installed binary (#4860)
- PicoClaw: v2→v3 config migration failure (#3206)
- ZeroClaw: Amazon Bedrock configuration confusing (#8925)
- **Common need:** Resilient configuration parsing, clear error messages, working first-run experience.

**6. Security Hardening (OpenClaw, NanoBot, Nanoclaw, ZeroClaw)**
- OpenClaw: Prompt injection via `gh-issues` skill (#45740—4 months open), sandbox `no-new-privileges` (#43996)
- NanoBot: Symlink workspace escape fix (#4629—merged today), sandbox isolation (#940)
- NanoClaw: `add_mcp_server` approval bypass (#2827, #2762—fix PR #2998 open)
- ZeroClaw: SSRF gate fix (#8713—merged today), unauthorized model changes (#8044)
- **Common need:** Deterministic, auditable security approval flows; prompt injection defenses; sandbox enforcement.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes Agent | CoPaw | ZeroClaw | IronClaw |
|-----------|----------|---------|--------------|-------|----------|----------|
| **Target User** | Generalist power user | DevOps / self-hoster | CLI/terminal power user | Generalist (Chinese market) | Developer / TUI enthusiast | Enterprise automation |
| **Architecture** | Monolithic core + channel adapters | Modular (CLI, webui, gateway) | CLI/TUI + Desktop (Electron) | CoW (Cooperative Work) pattern | Gateway-centric, multi-user | Reborn stack (Rust + WASM tools) |
| **Language** | TypeScript/Node.js | Python | Python | TypeScript | Go | Rust |
| **Channel Depth** | Broad (Telegram, Discord, WhatsApp, Slack, Signal, QQBot, Matrix) | Multi-platform (Telegram, WhatsApp, Matrix, Slack) | Desktop TUI + web dashboard | DingTalk, Feishu, WeChat (Chinese focus) | Discord, WeChat, Signal, Email, Telegram | Slack-centric, expanding |
| **Key Differentiator** | Largest community, interactive parity roadmap | Task-specific model config, cron presets | Remote agent + local exec (#18715) | v2.0 sandbox + security focus | Local-first small model support | WASM tool ecosystem, enterprise workflow |
| **Maturity** | High velocity, low reliability | Growing, stable base | Stabilizing with config fixes | Beta (v2.0.0) | Pre-release (v0.8.x) | Reborn migration in progress |

---

## 6. Community Momentum & Maturity

### Tier 1: High Velocity, High Engagement (OpenClaw, Hermes Agent, IronClaw, CoPaw, ZeroClaw)
- **OpenClaw:** 500+ items daily—by far the largest. However, velocity is masking reliability debt (P1 bugs open 3+ months, silent failures). The community is large but frustrated.
- **Hermes Agent:** 50+ items daily, rapid fix response (18 PRs merged). Stabilization phase after feature expansion.
- **IronClaw:** 50+ PRs, 28 merged. Heavy bug bash (Slack auth), but rapid fix velocity. Reborn migration causing regression churn.
- **CoPaw:** 50+ PRs, 32 merged—highest merge rate. v2.0.0-beta.5 just released; community fully engaged in testing and shaping.
- **ZeroClaw:** 50+ PRs, 11 merged. Steady progress toward v0.8.3/v0.9.0; organized milestone tracking.

### Tier 2: Stable Growth (NanoBot, NanoClaw, PicoClaw)
- **NanoBot:** 22 PRs, 5 merged. Healthy closure rate (52%). Point release likely imminent.
- **NanoClaw:** 17 PRs, 3 merged. Security disclosures active, but core team responding (fix PR #2998 opened same batch).
- **PicoClaw:** 16 PRs, 4 merged. RC approaching; focused on ARM support and streaming features.

### Tier 3: Low Activity (LobsterAI, Moltis)
- **LobsterAI:** 14 PRs, 11 merged. Clearing backlog; community requests from same author (MaoQianTu) remain unmerged since April.
- **Moltis:** 1 PR (GPT-5.6 support). Clean, low-velocity project; zero open issues.

### Tier 4: Inactive (NullClaw, ZeptoClaw, TinyClaw)
- **NullClaw:** No activity. Likely dormant or abandoned.
- **ZeptoClaw:** No activity.
- **TinyClaw:** No activity.

---

## 7. Trend Signals

**1. Reliability Over Features** — Across all high-velocity projects, users are consistently reporting **silent failures**, **disappearing notifications**, and **channel wedging** as top frustrations. The ecosystem is hitting a wall where new feature introduction (interactive parity, durable workflows, multi-agent orchestration) is outpacing the reliability of core message delivery. **Takeaway for developers:** Prioritize observability, error surfacing, and deterministic failure modes before adding major new surfaces.

**2. Security Is an Afterthought** — Three projects (OpenClaw, NanoClaw, ZeroClaw) have active security vulnerabilities that have been open for months. OpenClaw's `gh-issues` prompt injection (#45740) has been unaddressed since March. Nanoclaw's MCP approval bypass (#2827) existed for weeks before a fix PR. **Takeaway:** Security approval flows and sandbox enforcement are being retrofitted rather than designed-in. For developers: invest in deterministic, auditable privilege enforcement from the start.

**3. Interactive Parity Is the Next Frontier** — OpenClaw's PR #102261 (ask-user-question, plan mode) and IronClaw's approval workflow improvements signal that bidirectional agent-user interaction is the ecosystem's next major capability. This is driven by operational use cases (approval gates, progress updates, user-in-the-loop decision-making). **Takeaway:** Projects without interactive parity risk being perceived as chatbots rather than agents.

**4. Channel Fragmentation Is a Liability** — Every active project has Telegram, WhatsApp, or Slack-specific bugs. The failure modes are distinct per channel (Telegram session corruption, WhatsApp group broadcasting, Slack delivery routing), indicating that channel adapters are independently fragile. **Takeaway:** A unified channel reliability framework is needed across the ecosystem. Currently, each project solves channel problems in isolation.

**5. Self-Hosting UX Is a Barrier** — Configuration parsing issues (Hermes, PicoClaw, ZeroClaw), missing CLI commands (NanoBot), and documentation mismatches are blocking first-run experiences. The ecosystem assumes technical proficiency but doesn't deliver reliable onboarding. **Takeaway:** For projects targeting self-hosters, comprehensive error messages, resilient config defaults, and working first-run documentation are table stakes.

**6. Multi-Agent Orchestration Is Fragile** — Subagent silent failures (OpenClaw #44925), control plane gaps (NanoBot #1006), and cross-session task invisibility (NanoClaw #2992) indicate that the ecosystem has not yet solved multi-agent lifecycle management. **Takeaway:** The "agent of agents" pattern is attracting interest but lacks production reliability. Deterministic subagent execution with failure propagation is a prerequisite for production use.

**7. Chinese-Language Projects Are a Parallel Ecosystem** — CoPaw (DingTalk, Feishu, WeChat), NanoClaw (WeChat, QQ), and ZeroClaw (WeChat, Signal) serve a distinct user base. CoPaw's v2.0.0-beta.5 release and high engagement (35 issues, 50 PRs) suggest this ecosystem is growing independently of Western-focused projects. **Takeaway:** Developers targeting global markets should consider Chinese messaging channels (WeChat, DingTalk) as non-negotiable for reach.

**8. Desktop/CLI vs. Cloud Gateway Architecture Divergence** — A clear split is emerging between local-first TUI projects (Hermes, ZeroClaw) and gateway/cloud-oriented projects (OpenClaw, IronClaw, CoPaw). Hermes's most requested feature (#18715—remote agent with local tools) bridges both worlds. **Takeaway:** The winner likely combines local execution for latency-sensitive tools with gateway-mediated multi-channel routing.

---

*Report generated 2026-07-10 from project digest data.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-10

## Today's Overview
NanoBot is experiencing a high-activity period with 23 issues and 22 PRs updated in the last 24 hours, driven by a mix of regression fixes, feature development, and community engagement. The project maintains a healthy 52% closure rate on recent issues (11 closed of 23), though several critical bugs in WhatsApp groups, MCP reconnection, and tool execution remain open with active fix PRs. No new releases were published today; the most recent work focuses on stabilizing the core agent loop, improving subagent lifecycle management, and expanding channel support. The development velocity suggests a near-term point release is likely as priority P1 fixes converge.

## Releases
No new releases were published on 2026-07-10. The last available version remains the pre-0.2.2 state referenced in community issues.

## Project Progress
Five PRs were merged or closed today:
- **#4859** [fix(matrix): preserve mxc markdown image sources](https://github.com/HKUDS/nanobot/pull/4859) — fixes a regression where Matrix `mxc://` image sources were being rewritten to `#harmful-link` by Mistune 3.3.3, restoring proper image rendering in Matrix channels
- **#4857** [Add Dockerfile arg to override optional Python dependencies](https://github.com/HKUDS/nanobot/pull/4857) — introduces a `NANOBOT_EXTRAS` build arg allowing users to customize which optional deps (defaulting to WhatsApp) are installed at build time
- **#4629** [fix(exec): block relative symlink workspace escapes](https://github.com/HKUDS/nanobot/pull/4629) — closes a security hole where restricted exec commands could follow symlinks outside the workspace via relative paths
- **#4851** [Feature: non-interactive config refresh with 'nanobot onboard --refresh'](https://github.com/HKUDS/nanobot/pull/4851) — adds a CLI flag to refresh configuration without interactive prompts, enabling automated/CI config updates
- **#935** [Remote MCP URL times out with asyncio.CancelledError](https://github.com/HKUDS/nanobot/issues/935) — closed after troubleshooting; underlying fix for stale stack cleanup is in open PR #4843

## Community Hot Topics
- **#4823** [bug: whatsapp groups](https://github.com/HKUDS/nanobot/issues/4823) (4 comments, 0 👍) — Users report that WhatsApp group responses now broadcast to every group the bot is in, breaking the `group_allow` configuration. This is a high-impact regression for multi-group deployments.
- **#912** [Feat: Support Task-Specific Model Configuration](https://github.com/HKUDS/nanobot/issues/912) (5 comments, 3 👍) — Long-running feature request for assigning different models to conversational, tool-use, and browser-use tasks. Remains open with 3 upvotes and no maintainer response visible.
- **#4860** [bug: no such command "onboard" or "webui"](https://github.com/HKUDS/nanobot/issues/4860) (2 comments) — Fresh install via `uv tool install` yields a binary whose `-h` output lacks commands documented on the website, suggesting a packaging/documentation mismatch.
- **#240** [Feat request: add support for SimpleX Chat](https://github.com/HKUDS/nanobot/issues/240) (2 comments, 3 👍) — Request for decentralized encrypted messaging channel support, open since February with sustained community interest.

## Bugs & Stability
**Critical (P1 fix in progress):**
- **WhatsApp group regression** (#4823) — Broadcasting to all groups despite `allow` config. Regression post-0.2.2; no PR filed yet, but community identifying root cause.
- **MCP reconnect gateway crash** (#4843) — Stale `AsyncExitStack` cleanup during reconnect causes crash on streamable HTTP MCP session expiry. Fix PR #4843 defers cleanup to shutdown.
- **WebUI Docker build failure** (#4863) — `npm ci` fails from fresh clone due to out-of-sync `package-lock.json`. PR #4863 provides the sync fix.
- **Endless loop with complete_goal tool** (#4864) — Tool call loops because gateway parses `recap` parameter as bare string instead of JSON object; likely a recent serialization change.
- **Zombie process accumulation** (#4840) — Shell subprocesses not reaped on all exit paths. PR #4840 adds `os.waitpid(WNOHANG)` safety net.

**High (open, no fix PR):**
- **Missing CLI commands** (#4860) — `onboard` and `webui` subcommands absent from installed binary despite documentation. Affects new user onboarding.

**Medium (tracked but lower priority):**
- **No such command "onboard" or "webui"** is a documentation/packaging issue that blocks first-run experience.
- **Endless loop for complete_goal** suggests a breaking change in tool parameter serialization that may affect many tool-based interactions.

## Feature Requests & Roadmap Signals
**Likely in next release:**
- **Non-interactive config refresh** (`--refresh` flag) was merged today (#4851) and is stable infrastructure.
- **Cron job model presets** (#4622) enables per-cron-run provider/model/context overrides, likely for the next minor version.
- **Eden AI provider** (#4861) adds an EU-hosted aggregator with 100+ models via OpenAI-compatible API; likely merges as a low-risk addition.

**Roadmap predictions:**
- **Task-Specific Model Configuration** (#912) is the most-upvoted open feature and would align with the cron model presets work already in PR.
- **Multi-Tenant Gateway** (#936) and **Control Plane for Subagents** (#1006) indicate a shift toward production-grade orchestration capabilities.
- **Pre-handler hooks for zero-token routing** (#990) reflects power users' cost-consciousness for high-volume deployments.
- **SimpleX Chat support** (#240) remains the longest-standing channel request with moderate demand.

## User Feedback Summary
**Satisfaction signals:**
- Users successfully deploying in multi-platform setups (Telegram, WhatsApp, Matrix, Slack)
- Community contributors actively filing improvement PRs (7 open PRs from 7 different authors today)
- Positive reaction to tool isolation work (#4862) and symlink escape fixes (#4629), showing security-conscious user base

**Pain points:**
- **WhatsApp group functionality is broken** post-0.2.2 (#4823) — a regression causing real operational issues for field deployments
- **MCP reliability degrades** on streamable HTTP session expiry (#4843, #935) — affects users relying on remote MCP tools
- **Fresh install experience is confusing** (#4860) — web-documented commands don't match installed binary
- **LLM hallucination in exec tool** (#937) — a user stopped evaluation entirely due to tool reliability
- **Sandbox isolation limits skills development** (#940) — files written by agent go to sandbox, not user-accessible workspace
- **Cron jobs auto-restore after deletion** (#1100) — with AI ethics alerts, suggesting persistence issues
- **Unbounded disk growth** from media downloads (#896) — Telegram/Discord media files never cleaned up

## Backlog Watch
**Critical unaddressed items needing maintainer attention:**
- **#912** (Task-Specific Model Configuration, 3 👍, open since Feb 20) — Highly requested, no official roadmap response. With cron model presets merging (#4622), this natural next step has strong community support.
- **#240** (SimpleX Chat support, 3 👍, open since Feb 7) — No maintainer engagement on this decentralized channel request despite clear community interest.
- **#931** (Native Sandbox Interface, open since Feb 21) — Security-critical proposal for untrusted plugin execution isolation; no maintainer feedback.
- **#940** (Filesystem access blocked for skills, open since Feb 21) — Blocking feature for agent skill development; no resolution path visible.
- **#896** (Media file cleanup, open since Feb 20) — Operational stability issue causing unbounded disk growth; root cause identified but unmerged.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for July 10, 2026.

---

## Hermes Agent Project Digest for 2026-07-10

### 1. Today's Overview
Activity is very high, with 50 issues and 50 PRs updated in the last 24 hours, signaling a significant maintenance and feature-fix push. The 36 open/active issues suggest a persistent backlog of bug reports and feature requests despite a high rate of closed items (14 issues, 18 PRs). No new releases were made today, but the team is actively merging high-priority fixes for config stability, session state, and provider-specific issues. Overall, the project is in a phase of intensive stabilization, addressing community-reported regressions and a wide range of infrastructure bugs.

### 2. Releases
No new releases were created today. The latest available version remains the previous release, pending the merge of several critical fixes currently in the pipeline.

### 3. Project Progress
Today saw 18 PRs merged or closed, focusing on stability and bug fixes.

- **Config & Startup Robustness:** Multiple PRs were merged to prevent crashes from malformed or empty YAML keys, addressing issues like empty `terminal:` keys (#58361, #58306, #61733) and scalar gateway config blocks (#40837, #40835, #61740).
- **Agent Session State & Recovery:** A critical fix prevents data loss from gateway session-hygiene compression (#61209, #61145). A fix for `restore_primary_runtime()` failing with MoA presets (#61712) was also merged. The `switch_model()` function received fixes to prevent routing requests to the wrong provider's endpoint (#61732, #61347, #61099).
- **Memory & Database Stability:** The holographic memory provider received multiple fixes to resolve permanent write-locks on `memory_store.db`. Key merges include refactoring to a shared SQLite connection per store (#61726, #43819) and adding retry logic for locked states (#55521, #40167).
- **Provider Support:** The OpenRouter header reapplication fix (#61732) ensures requests are properly identified. A fix was also merged for the Z.AI provider pool's key exhaustion cascade (#61487).

### 4. Community Hot Topics
- **Remote Agent & Local Execution (Issue #18715):** With 8 comments and 20 👍, this remains the most popular feature request. The community strongly desires the ability to run a lightweight client that connects to a remote agent instance while keeping tool execution local.
- **Agent Violating Rules (Issue #60429):** This bug report has 4 comments and is a source of frustration. Users report that the agent either fails to save or ignores custom rules, directly impacting reliability and trust. This is tagged `needs-repro`.
- **Cron Ticker Thread Death (Issue #37179):** A long-running issue with 3 comments describing a silent crash of the cron ticker thread after certain jobs. The community is concerned about silent failure in a critical system component.
- **Configuration Ignored by Desktop TUI (Issue #48269):** A persistent complaint that changes to `config.yaml` are ignored by the Electron version of Hermes, specifically for vision settings and module toggles (Issue #50944).

### 5. Bugs & Stability
Today's reports are dominated by configuration and session state stability issues.

- **Critical (P1):**
    - **Gateway Hypgiene Data Loss (#61145, #61099):** Auto-compression was permanently deleting conversation history instead of archiving it. **Fix PRs #61209 and #40835 are merged**, resolving this.
- **High (P2):**
    - **Credential Pool Cascade Exhaustion (#61487):** A single quota hit on one key could incorrectly mark all keys in a pool as exhausted. **Fix merged.**
    - **Model Switch Provider Cross-Wiring (#61427, #61296):** Switching models live could pin the request to the *old* provider's endpoint, causing 400 errors. **Fix merged** (#61732).
    - **Nous Inference API Unreachable (#60715):** Complete connection failure to the portal API for one user. Needs reproduction.
    - **Cron Tests Writing to Live Store (#61673):** A significant testing infrastructure bug where running the test suite could create real, recurring jobs on the user's machine.
- **Medium (P3):**
    - **OpenRouter App Identification (#61099):** Requests frequently show as `Unknown` instead of `Hermes Agent`. **Fix merged**.
    - **Honcho Tool Empty API Key (#61661):** The memory write tool sends an empty key, causing authentication errors.
    - **Desktop Install Failure (#61657):** The Windows installer fails at the build step for new users.

### 6. Feature Requests & Roadmap Signals
- **Strong Signal—Next Release Likely:** The **auto-reasoning mode** (Issue #40306) and **thin-client desktop installer** (Issue #61329) are features directly impacting user experience. Given the community interest and the push for config fixes, a thin-client mode feels imminent.
- **Medium Signal—Backlog:** **Per-cron reasoning effort overrides** (Issue #23524) and **dashboard IdP logout** (Issue #35410) are clearly defined, non-breaking improvements. They are likely to be scheduled as they align with enterprise and advanced user use cases.
- **Weak Signal—Research Phase:** The **remote agent with local tools** (Issue #18715) is a complex architectural change. While highly requested, it represents a major shift in the agent's topology and is likely still in the design discussion phase.

### 7. User Feedback Summary
- **Pain Points:** Configuration reliability is the top frustration. Users find the system fragile with malformed YAML and inconsistent behavior between the CLI, TUI, and Desktop versions (Issues #50944, #48269, #40834).
- **Reliability:** There is growing unease about the agent's "promise-keeping," highlighted by the violation of rules bug (#60429) and the silent death of background cron jobs (#37179).
- **Desired Features:** The most desired feature is the ability to run a remote agent with a local thin client (#18715, #61329), indicating a strong use case for home servers and remote workstations. The auto-reasoning mode (#40306) also signals a desire for reducing manual configuration overhead.
- **Satisfaction:** While bugs are numerous, the rapid merging of high-severity fixes (especially for data loss and session state) indicates a responsive development team, likely maintaining community trust despite the churn.

### 8. Backlog Watch
- **Issue #18715 - Remote Agent with Local Tools:** High community demand (20 👍) but open since May 2nd. This architectural request requires a detailed proposal and significant development time.
- **Issue #35410 - Dashboard IdP Logout:** Open since May 30th. A security and user lifecycle improvement that is important for enterprise deployments using SSO. No public PR is linked.
- **Issue #17977 - Configurable Startup Panels / TUI Skins:** Open since April 30th. A non-critical but quality-of-life improvement for the TUI interface. It has gone without a response from maintainers for over two months.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-10

## 1. Today's Overview

PicoClaw shows high development activity today, with **16 PRs** updated in the last 24 hours (12 open, 4 merged/closed) and **3 open issues** attracting discussion. The project is in a strong maintenance and feature-addition phase, characterized by focused bugfix PRs, automated dependency bumps, and infrastructure improvements. No new releases were published today, but the volume of merged PRs and active issue tracking suggests a release candidate may be approaching. Project health appears robust, with steady contributor engagement and clear attention to stability concerns.

## 2. Releases

No new releases were published today. The latest stable release remains **v0.2.9** (git 2992…).

## 3. Project Progress

**Merged/Closed PRs (4 total):**

- **#3226** — `fix(tools): stop write_file from coaching destructive overwrite` (by ACMYuechen) – Prevents the `write_file` tool from suggesting overwrite behavior to the model, improving memory-update safety. *Merged.*
- **#3171** — `fix(line): add ok checks for sync.Map type assertions in Send` (by chengzhichao-xydt) – Adds type-assertion safety checks to the LINE channel to prevent panics from unexpected map values. *Merged.*
- **#3213** — `build(deps): bump github.com/aws/aws-sdk-go-v2/config 1.32.25→1.32.27` (by dependabot) – Routine AWS SDK dependency update. *Merged.*
- **#3207** — `build(deps): bump github.com/github/copilot-sdk/go 0.2.0→1.0.5` (by dependabot) – Major version bump for GitHub Copilot SDK integration. *Merged.*

**Notable open PRs advancing:**
- **#3180** (fix invalid CLI tool-call arguments), **#3118** (remote Pico WebSocket mode), **#3163** (Bedrock prompt caching), and **#3222** (DeltaChat refactor, -320 LOC) all continue to receive updates, signaling active review cycles.

## 4. Community Hot Topics

The most engaged issues and PRs, based on comment volume and recency:

1. **#3201** [OPEN] — *[Feature] Support streaming output for QQ channel* (2 comments, created Jul 1)
   - *Link:* [sipeed/picoclaw Issue #3201](https://github.com/sipeed/picoclaw/issues/3201)
   - *Analysis:* Users want token-by-token streaming for QQ, mirroring Telegram and WebSocket channels. This reflects a growing expectation for real-time LLM interaction across all chat platforms. The feature is relatively self-contained (implement `StreamingCapable`), making it a strong candidate for the next release.

2. **#3206** [OPEN] — *v2→v3 config migration fails with false 'unknown field(s): build_info, session.dm_scope'* (1 comment, created Jul 2)
   - *Link:* [sipeed/picoclaw Issue #3206](https://github.com/sipeed/picoclaw/issues/3206)
   - *Analysis:* A regression affecting fresh installs during config migration. The stale tag suggests low priority, but the impact on new users is significant. Likely needs maintainer triage.

3. **#3203** [OPEN] — *Matrix sync loop has no reconnection logic — silent death* (1 comment, created Jul 2)
   - *Link:* [sipeed/picoclaw Issue #3203](https://github.com/sipeed/picoclaw/issues/3203)
   - *Analysis:* A reliability bug where Matrix channel silently dies after network disruption. The author notes systemd's restart policy doesn't help, indicating a design gap in the sync-loop architecture.

## 5. Bugs & Stability

**High Severity:**
- **#3203** — *Matrix sync loop silent death* – Critical for production Matrix users. The process stays alive but stops syncing. No fix PR exists yet; the stale tag may delay resolution.

**Medium Severity:**
- **#3206** — *v2→v3 config migration fails on fresh install* – Blocks new users from running `picoclaw status` or any config-loading command. Workaround may exist (manual config cleanup), but no fix PR identified.

**Low Severity / Niche:**
- **#3180** (open PR) — *Skip CLI tool calls with invalid JSON arguments* – Addresses a malformed-input edge case in CLI tool calling. Fix is under review.
- **#3171** (merged today) — *LINE channel sync.Map panic fix* – Resolved with merged PR.

**Bug Fixes Merged Today:**
- **#3226** – Destructive overwrite coaching removed.
- **#3171** – LINE channel panic fixed.
- **#3205** (open) – Fixes 9router gateway response parsing and adds Linux ARMv7 build support (Raspberry Pi).

## 6. Feature Requests & Roadmap Signals

**Active feature requests:**
- **#3201** — *QQ channel streaming output* – High demand, narrow scope, likely next release.
- **#3118** (PR) — *Remote Pico WebSocket mode* – Enables remote agent connections. Nearing completion with continued updates.
- **#3163** (PR) — *Bedrock prompt caching via cache points* – Cost optimization for AWS users. Advanced but actively reviewed.
- **#3222** (PR) — *DeltaChat refactor* – Cleanup and modernization of DeltaChat integration. Already -320 LOC.

**Roadmap signals:**
- The **Copilot SDK dependency jump** (0.2.0 → 1.0.6) suggests a GitHub Copilot integration feature is being actively developed or stabilized.
- **Raspberry Pi / ARM support** (#3205) indicates growing interest in edge deployments.
- The **`write_file` coaching fix** (#3226) hints at memory-management UX improvements.

**Prediction for next release:** QQ streaming (#3201), ARM build targets (#3205), and the Copilot SDK upgrade are the strongest candidates.

## 7. User Feedback Summary

**Pain Points:**
- *"Matrix sync loop dies silently after network disruption"* (#3203) — A reliability issue impacting self-hosted Matrix users.
- *"Config migration fails on fresh install"* (#3206) — A frustrating onboarding blocker for new users of the latest release.
- *"No ARM build target for launcher"* (#3205) — Raspberry Pi users forced to cross-compile.

**Use Cases:**
- Real-time streaming (QQ channel) for low-latency interaction.
- Remote agent operation via WebSocket (#3118) for distributed deployments.
- Cost-optimized LLM inference via Bedrock prompt caching (#3163).

**Satisfaction Signals:**
- Multiple contributors actively submitting fixes and features (16 PRs updated in 24h).
- Stale-tagged issues still receiving comments, indicating engaged user base.

## 8. Backlog Watch

**Issues requiring maintainer attention:**
- **#3203** — *Matrix sync loop silent death* (stale since Jul 2, no fix PR) – Two users impacted. Needs a reconnection strategy or process health check.
- **#3206** — *v2→v3 config migration failure* (stale since Jul 2, no fix PR) – Blocks new installs. Needs a quick patch or workaround documentation.
- **#3180** — *CLI tool-call JSON validation* (open since Jun 26) – Under review but no merge yet; minor but affects CLI reliability.

**Stale PRs needing review:**
- **#3163** — *Bedrock prompt caching* (open since Jun 23) – Complex but valuable; waiting for maintainer feedback.
- **#3115** — *Fix inline data URL media extraction* (open since Jun 12) – Solves a session-history corruption bug; has been open for nearly a month.

---

*Digest generated 2026-07-10 from PicoClaw GitHub data (github.com/sipeed/picoclaw).*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-10

## 1. Today's Overview

NanoClaw is in a period of intense development velocity, with 9 issues updated and 17 pull requests active in the last 24 hours. The project is currently processing a major feature train (scheduled tasks + guarded actions) while simultaneously addressing a wave of Telegram-specific bugs and two serious security disclosures related to the `add_mcp_server` approval flow. Project health is strong: three PRs were merged/closed today, and core-team members are actively responding to the most critical vulnerabilities with fix PRs. However, the volume of open issues and long-standing PRs (some since April) suggests the team is stretched across multiple high-priority tracks.

## 2. Releases

No new releases today. The latest published version remains the last tagged release. Given the volume of pending fixes and security patches, a minor or patch release is likely imminent.

## 3. Project Progress

Three PRs were merged or closed today:

- **#2621** (closed) — `chore: add .gitattributes to enforce LF line endings for shell scripts` by GarethWright. A minor but important cross-platform compatibility fix ensuring shell scripts work correctly on Windows.
  
- **#2993** (closed) — `Make NanoClaw resilient to a down container runtime` by shiranLupo. A critical resilience fix: `main()` no longer crashes with `process.exit(1)` when Docker Desktop isn't running. Instead, channels connect and the scheduler starts normally, degrading gracefully. This explains previously reported "Discord looked disconnected" symptoms.

- **#2981** (merged) — `Scheduled tasks: ncl tasks control plane, isolated sessions, script gate` by omri-maya. Part 2/5 of the scheduled-tasks feature train. Ships the full `ncl tasks` resource: create/update/run/append-log operations, per-series isolated sessions, run history, and the pre-task script gate. This is a major feature milestone.

**Feature advances still in flight:** The guarded-actions phase 2 (#2986) and tasks one-door delivery (#2988) were opened today by core-team members, indicating continued momentum on security architecture and task isolation.

## 4. Community Hot Topics

**Most commented issues:**
- **#2989** (1 comment) — `Telegram: channels are silently blackholed when the bot token previously polled with a narrower allowed_updates`. The discussion highlights a server-side Telegram API persistence issue that leads to silent message loss. This is a high-impact bug for any deployment using a token that was previously used elsewhere.

- **#2985** (1 comment) — `opencode provider: silent no-reply when the final text snapshot misses session.idle`. Zero-error silent failures on long agentic turns. The comment analysis suggests this is a timing race between the agent completing its turn and the provider session state.

**Most active PRs (by recency + core-team involvement):**
- **#2986** — `Guard seam: one decision function for every privileged action`. This is the second phase of a fundamental security architecture change, standardizing all privilege checks through a single `guard()` function. This directly addresses the `add_mcp_server` security issues.

- **#2988** — `Tasks: one-door delivery — send_message is the only path out of a task session`. Part of the tasks train, enforcing that task fires can only send messages through an explicit destination—a design decision to prevent silent message leakage.

**Underlying needs:** The community and core team are clearly prioritizing:
1. **Deterministic privilege enforcement** — The guard seam architecture and security fixes show a deep need for predictable, auditable approval flows.
2. **Message delivery reliability** — Multiple issues (#2989, #2985, #2995, #2996) all trace back to silent delivery failures, indicating this is the top user-facing pain point.
3. **Task/agent lifecycle management** — The scheduled-tasks train (#2981, #2988, #2992, #2997) shows demand for robust, cross-session task management.

## 5. Bugs & Stability

### Critical severity:
- **#2827, #2762** — `add_mcp_server` approval flow hides runtime `args` and `env`, enabling approval smuggling. **Two duplicate security advisories** (same root cause). An attacker-controlled agent can submit a request where the approval card shows only the MCP server name, while `args` and `env` are silently persisted. **Fix PR exists: #2998** (renders full MCP server payload on the approval card). This should be treated as a P0 security patch.

### High severity:
- **#2997** — `hasIdenticalSend matches sends from previous fires, so recurring reminders with fixed text stop arriving`. Recurring tasks with unchanging reminder text deliver once and then silently stop. **No fix PR yet.** This is a regression in the new task scheduling system.

- **#2995** — `Outbound messages to an offline channel adapter are marked delivered without any send`. Messages to unregistered/offline adapters are silently marked delivered with `status=delivered`. **Fix PR exists: #2996** (routes missing-adapter messages into the retry path). Also related: PR #2226 (throw on missing channel adapter, still open since May).

- **#2989** — Telegram channels silently blackholed due to server-side `allowed_updates` persistence. **No fix PR yet.** The Telegram adapter needs to explicitly pass `allowed_updates` on every polling request.

### Medium severity:
- **#2992** — `Scheduled tasks are invisible and unmanageable across sessions of the same agent group`. Tasks live in per-session databases, so `list_tasks`/`cancel_task` etc. only see the calling session's tasks. **No fix PR yet.** This is a design limitation of the current task storage model.

- **#2991** — `Telegram: channel wirings with sender_scope='known' never engage (channel posts are anonymous)`. Telegram broadcast channel posts lack individual sender info, so `known` scope never matches. **No fix PR yet.**

- **#2990** — `Telegram: bot does not react to being added to a chat (my_chat_member updates are discarded)`. Membership updates are silently dropped by the adapter. **No fix PR yet.**

## 6. Feature Requests & Roadmap Signals

**Likely in next release:**
1. **Guarded actions framework (phase 2)** — PR #2986 will standardize all privilege checks through a single `guard()` function, making approval flows auditable and secure. This is clearly the team's answer to the security disclosures.

2. **Per-group harness capability toggles** — PR #2983 adds lean defaults for new groups and grandfathers existing ones, allowing operators to disable Claude Code's built-in scheduling in favor of NanoClaw's own task system.

3. **Local audit log skill** — PR #2987 introduces `/add-audit`, an opt-in SIEM-shaped audit log for the `ncl` command surface. This signals growing enterprise/ops focus.

4. **Scheduled tasks completion (parts 4-5)** — With #2981 and #2988 merged/opened, the remaining scheduled-tasks train PRs will likely follow quickly. This is a major roadmap item converging.

**Emerging signals:**
- **Telegram rich rendering** — PR #2877 (native `sendRichMessage` via Bot API 10.1) indicates investment in Telegram as a first-class channel, despite the current bug cluster. This suggests Telegram deployments are growing.
- **Multimodal v1 restoration** — PR #2618 (image/voice/PDF + reactions) has been open since May 25 with no merge, suggesting v2 feature parity is a lower priority than stability and security.

**Predictions for next version:**
- Security patch release including #2827/#2762 fix (PR #2998)
- Guarded actions phase 2 (PR #2986)
- Scheduled tasks complete train (parts 4-5)
- Per-group capability toggles (PR #2983)
- Audit log skill (PR #2987)

## 7. User Feedback Summary

**Pain points (explicit from issues):**
- **Silent failures are the #1 user frustration.** Four separate issues (#2985, #2989, #2995, #2997) all describe scenarios where the bot silently fails to deliver or process messages with zero error logs. Users are left debugging "the bot ignored the message" or "nothing was delivered" without any trace.
- **Telegram-specific pain is acute.** Three Telegram issues opened today alone (#2989, #2990, #2991) covering channel blackholing, admin detection failure, and scope filtering. The platform-specific bug density suggests Telegram support is either new or recently refactored.
- **Task management is confusing.** Issue #2992 explicitly describes a scenario where "an agent group wired to more than one messaging group therefore cann[ot] manage its own tasks"—a real operational headache for multi-channel deployments.

**Positive signals:**
- The rapid response to security issues (PR #2998 opened same batch as advisories were updated) indicates strong maintainer engagement.
- The resilience fix (#2993 merged) directly addresses a real-world operational pain point (Docker Desktop downtime causing full process crash).

## 8. Backlog Watch

**High priority — security:**
- **#2827, #2762** — `add_mcp_server` approval flow bypass (duplicate). Both have had zero comments from maintainers since June 14/21. The fix PR #2998 was opened today, but the issues themselves need triage labeling and confirmation of the fix scope.

**High priority — long-stale PRs:**
- **#2226** (opened May 3) — `fix(host): throw on missing channel adapter instead of silently dropping the message`. This PR directly addresses the same class of bug as #2995 (which has a newer fix PR #2996). The older PR should be evaluated for supersedure or conflict.
- **#1598** (opened April 2) — `feat: add-remote-storage skill (WebDAV/S3 via rclone + systemd)`. A core-team PR by glifocat that has been open for over 3 months with no update. This represents significant committed work that may need conflict resolution or redesign given the project's direction changes since April.

**Medium priority:**
- **#2802** (opened June 17) — `fix(security): ncl socket hardening (client timeout/cap + server fail-closed/frame-cap)`. A security hardening PR for the `ncl` socket transport. No comments from maintainers for 23 days despite the security focus.
- **#2544** (opened May 18) — `feat(telegram): enable message_reaction + callback_query in allowedUpdates`. Directly related to the `allowed_updates` persistence bug (#2989). This PR may need revision to explicitly pass the full allowed updates list on every poll.
- **#2618** (opened May 25) — `feat(multimodal,reactions): restore v1 image/voice/PDF + chat.onReaction`. No recent activity. This may be deprioritized in favor of security/stability work.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-10

## Today's Overview

IronClaw shows signs of intense stabilization activity, with 32 issues updated in the last 24 hours and 50 pull requests in flight. The project is processing a significant bug bash wave (P1-P3 severity), particularly around Slack integration, approval workflows, and run lifecycle management. The merged/closed count of 28 PRs confirms sustained engineering output, though the 22 open PRs suggest ongoing review bottlenecks. No new releases were cut today, indicating the team is still consolidating fixes before the next version ship. Overall, the project is healthy but under active triage pressure from regression and integration bugs.

## Releases

No new releases were published today. The last release candidate PR (#5598, still open) would bump `ironclaw` from 0.24.0 to 0.29.1 with breaking API changes in `ironclaw_common` (0.5.0) and `ironclaw_skills` (0.4.0). No migration notes are available yet.

## Project Progress

**28 PRs were merged or closed in the last 24 hours**, spanning three major themes:

**Architecture & Tech Debt:**
- [#5791](https://github.com/nearai/ironclaw/pull/5791) — Consolidated default-backed builder setters across Reborn crates, improving ergonomics and test readability.
- [#5792-5800, #5811-5812, #5793-5794, #5798-5799] — A 10-PR stack converting sparse configuration fixtures to `::default().set_*()` chains across trigger poller config, memory backends, event stores, CLI config, and composition fixtures.
- [#5652](https://github.com/nearai/ironclaw/pull/5652) — Promoted `unused_must_use` to workspace-wide deny, ensuring dropped `Result` values now fail the build.
- [#5826](https://github.com/nearai/ironclaw/pull/5826) & [#5827](https://github.com/nearai/ironclaw/pull/5827) — Removed legacy v1 coverage-focused test binaries and their orphaned trace fixtures.

**Bug Fixes & Stabilization:**
- [#5876](https://github.com/nearai/ironclaw/pull/5876) (open) — Fixes Postgres CAS delete race condition in the filesystem layer.
- [#5902](https://github.com/nearai/ironclaw/pull/5902) (open) — Keeps LocalDev tool results out of model context to prevent context compaction failures (fixes #5838).
- [#5898](https://github.com/nearai/ironclaw/pull/5898) (open) — Fixes three Slack automation failure classes: wrong-channel delivery, ID-to-name enrichment, and single-delivery contract.

**CI & Testing:**
- [#5899](https://github.com/nearai/ironclaw/pull/5899) (open) — Adds 9 live-canary automation delivery probes for Slack failure classes.
- [#5900](https://github.com/nearai/ironclaw/pull/5900) (open) — Introduces a scheduled hosted Postgres API capacity nightly job.
- [#5901](https://github.com/nearai/ironclaw/pull/5901) (open) — Co-locates the Reborn runner control plane into a single named crate, completing Wave 4.

## Community Hot Topics

**Most Active Issues:**

1. **[#5553](https://github.com/nearai/ironclaw/issues/5553) — Approval notifications disappear (4 comments):** Users report that approval notifications for automation runs (e.g., "web-access.search") flash once and vanish, or never appear at all. This blocks critical user-in-the-loop workflows and has been open for 8 days without a fix PR, suggesting it's a systemic notification persistence bug.

2. **[#5747](https://github.com/nearai/ironclaw/issues/5747) — No way to unpair Slack on host-beta mount (3 comments):** Ironclaw users who pair Slack via the built-in `slack-v2-host-beta` channel have no UI or command to disconnect. The `/pair` command refuses with "already connected," and the WebUI has no disconnect action. This is a usability blocker for multi-account users.

3. **[#5701](https://github.com/nearai/ironclaw/issues/5701) — Activity panel hides tool details (3 comments):** The activity panel collapses tool call details into a summary line and does not update during active runs. Users must wait for completion to see what tools were called. This degrades debugging and observability.

4. **[#5504](https://github.com/nearai/ironclaw/issues/5504) — Routine creation hangs (closed, 2 comments):** Asking IronClaw to create a routine shows initial planning but never returns confirmation or error. This was marked P1 and recently closed, possibly indicating a fix landed.

**Most Active Pull Requests:**
- [#5499](https://github.com/nearai/ironclaw/pull/5499) — WASM tool install from zip (open, XL, 10 days old): Lays foundation for configurable tools in the Reborn stack. This is a major architectural feature.
- [#5662](https://github.com/nearai/ironclaw/pull/5662) — Surface best-effort failures instead of silent `let _` drops (open, L, 5 days old): Converts 90 ignored cleanup failures into debug diagnostics, improving observability.

**Underlying Needs:**
- Users are frustrated by missing or unreliable notifications, especially around approval flows.
- Slack integration is fragile: pairing, unpairing, and delivery routing all have bugs.
- Observability during active runs is poor — the activity panel needs real-time updates.

## Bugs & Stability

**24 open bugs were reported or updated today**, primarily from the bug bash session. Severity breakdown:

**P1 (Critical) — 1 bug:**
- [#5877](https://github.com/nearai/ironclaw/issues/5877) — Slack notification delivered to the wrong user. This is a security/privacy issue where sensitive workflow results go to unintended recipients. No fix PR yet.

**P2 (High) — 12 bugs:**
- [#5886](https://github.com/nearai/ironclaw/issues/5886) — Pending approval blocks subsequent scheduled runs. Workflow scheduler does not proceed until an unrelated approval is resolved.
- [#5887](https://github.com/nearai/ironclaw/issues/5887) — Runs hitting max action limit discard all progress. No option to continue from where it stopped.
- [#5878](https://github.com/nearai/ironclaw/issues/5878) — Revoked GitHub token produces misleading "tool input could not be encoded" instead of re-auth flow.
- [#5885](https://github.com/nearai/ironclaw/issues/5885) — Approval notification opens action page but approval card is missing. User cannot approve/deny.
- [#5884](https://github.com/nearai/ironclaw/issues/5884) — Routine loses credentials after external token revocation.
- [#5883](https://github.com/nearai/ironclaw/issues/5883) — Generic "model output could not be used" error after successful tool execution. No actionable error.
- [#5882](https://github.com/nearai/ironclaw/issues/5882) — Repeated Slack reconnects leave auth flow in broken state.
- [#5881](https://github.com/nearai/ironclaw/issues/5881) — Auth notification sent to wrong Slack app/channel.
- [#5880](https://github.com/nearai/ironclaw/issues/5880) — Slack auth completed externally not reflected in Web UI.
- [#5879](https://github.com/nearai/ironclaw/issues/5879) — Stale error banner persists after successful follow-up.
- [#5838](https://github.com/nearai/ironclaw/issues/5838) — Context compaction error after successful tool execution (fix PR #5902 open).
- [#5836](https://github.com/nearai/ironclaw/issues/5836) — Routine fails on every scheduled run with "No thread attached" (0% success rate).

**P3 (Medium) — 6 bugs:**
- [#5891](https://github.com/nearai/ironclaw/issues/5891) — "Last completed" shows active run timestamp instead of last finished.
- [#5890](https://github.com/nearai/ironclaw/issues/5890) — Slack notifications use inconsistent sender identity.
- [#5889](https://github.com/nearai/ironclaw/issues/5889) — "Load older messages" button does nothing.
- [#5888](https://github.com/nearai/ironclaw/issues/5888) — Cannot delete old threads from thread list.
- [#5897](https://github.com/nearai/ironclaw/issues/5897) — Tech debt: decompose first-party skill activation module.

**Notable: P2 bugs dominate the bug landscape, particularly around Slack auth, notifications, and run lifecycle.** A fix PR (#5898) exists for the Slack automation routing bugs. The context compaction bug (#5838) has a fix in review (#5902).

## Feature Requests & Roadmap Signals

- [#2601](https://github.com/nearai/ironclaw/issues/2601) — CLI/TUI for managing secrets (open since April, 1 comment, updated today). User reports poor documentation and confusing authentication patterns. This is now 3 months old and may be deprioritized as Reborn reworks the secrets system.
- [#5861](https://github.com/nearai/ironclaw/issues/5861) — Require IronLoop fix agents to validate issue fixability before editing (closed, 0 comments). This process improvement suggests the team is refining the auto-fix pipeline.
- [#5499](https://github.com/nearai/ironclaw/pull/5499) — WASM tool install from zip (open, XL PR) signals the ability to import custom tools, which is a major extensibility feature likely for the next release.
- [#5903](https://github.com/nearai/ironclaw/pull/5903) — New contributor adds JMT x402 Agent Tools (25 paid x402 endpoints on Base mainnet). This third-party tool integration PR suggests the tool ecosystem is expanding.

**Prediction:** The next release (0.29.1) will likely include: Slack automation routing fixes (#5898), context compaction fix (#5902), WASM tool install (#5499), and the default-backed builder refactors. The Slack notification P1 bug (#5877) may delay the release if not resolved.

## User Feedback Summary

**Real pain points (from issue descriptions):**
1. **Slack integration is unreliable:** Notifications go to wrong users/channels, unpairing is impossible, auth flows break after multiple reconnects, and completed Slack auth isn't reflected in the Web UI.
2. **Approval workflows are broken:** Notifications disappear, approval cards are missing when clicking notifications, and pending approvals block subsequent scheduled runs.
3. **Error messages are misleading:** Generic errors like "model output could not be used" or "tool input could not be encoded" replace actionable re-auth prompts.
4. **Observability is poor:** Activity panel hides tool details, "Load older messages" is non-functional, and the sidebar shows raw thread IDs under load.
5. **Routine management is frustrating:** "Last completed" shows wrong timestamps, routines fail with "No thread attached," and old threads cannot be deleted.
6. **Credential loss is silent:** External token revocation causes silent failures in scheduled routines with no re-auth prompt.

**Overall sentiment:** Users are experiencing significant friction with Slack automation and approval flows. The bug bash is surfacing many regression-level issues. While the project is actively fixing these (evidence: 28 merged PRs, open fix PRs for several P2 bugs), the volume of high-severity bugs suggests the Reborn migration may have introduced instability. Satisfaction is likely low among users relying on Slack automation.

## Backlog Watch

- [#2601](https://github.com/nearai/ironclaw/issues/2601) — CLI/TUI for Managing Secrets (3 months old, 1 comment, updated today). This user-facing feature request has no assigned owner or milestone. Given the ongoing secrets/auth issues surfaced in the bug bash, this may need prioritization.
- [#5553](https://github.com/nearai/ironclaw/issues/5553) — Approval notifications disappear (8 days old, 4 comments, P2). No fix PR. This bug blocks critical approval workflows and has been open for over a week.
- [#5747](https://github.com/nearai/ironclaw/issues/5747) — No way to unpair Slack (3 days old, 3 comments). No fix PR. Basic UX missing for a key integration.
- [#5836](https://github.com/nearai/ironclaw/issues/5836) — Routine fails with "No thread attached" (2 days old, 0 comments, P2). Scheduled routines are completely broken for this user. No fix PR.

**Maintainer attention needed:** The Slack auth and notification bugs are the most urgent, as they affect security (#5877 — wrong user), usability (#5747 — no unpair), and reliability (#5553 — disappearing notifications). The "No thread attached" routine bug (#5836) may indicate a deeper infrastructure issue.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-07-10**, generated from the provided GitHub data.

---

### LobsterAI Project Digest – 2026-07-10

#### 1. Today's Overview
The project shows **very high velocity**, with 14 Pull Requests (PRs) updated in the last 24 hours and an **85% merge/close rate** (11 out of 14). Activity is heavily concentrated on the `cowork` (agent collaboration) and `openclaw` (backend orchestration) areas, indicating a major push to stabilize agent interactions and fix critical data routing bugs. While no new releases were cut today, the team closed several long-standing feature PRs from April, suggesting a focus on clearing the backlog. The community issue queue is stable, with 4 open issues remaining stale for over three months.

#### 2. Releases
No new releases were tagged today.

#### 3. Project Progress
The following major fixes and features were merged today, primarily focusing on the **Cowork** and **OpenClaw** core architecture:

- **Agent Display Consistency:** PR #2305 was merged, syncing agent display names across OpenClaw entries, chips, and artifact panels, improving UI clarity.
- **Task Management & UX:** PR #2304 merged incremental task loading and drag-and-drop agent sorting in the sidebar.
- **Self-Hosted Agent Tools:** PR #2303 merged support for agent-scoped local tools, allowing non-main desktop agents to use `AskUserQuestion` and media generation tools.
- **Memory System Hygiene:** PR #2301 explicitly disables memory dreaming when the feature is off, preventing stale cron jobs and config drift.
- **Cowork Input Enhancements:** PR #2300 merged support for file attachments in the steer queue, and PR #2302 introduced a new Windows-native title bar with simplified sidebar controls.
- **Subagent Tool History:** PR #2299 fixed a critical bug where tool call results were missing from subagent child session pages.
- **Prompt Sanitization:** PR #2308 fixed a hard-rejection issue by stripping null bytes (U+0000) from prompts before sending to the OpenClaw gateway.
- **Localization:** PR #1397 (closed) adds localized compact time suffixes (e.g., "刚刚" instead of "now") for the session list.
- **[Stale] Uninstaller UX:** PR #1396 (closed) enhances the Windows NSIS uninstaller to fully clean user data and handle running processes gracefully.

#### 4. Community Hot Topics
Community engagement remains low, with most open issues being old (stale). The most notable activity revolves around feature gaps identified by users:

- **Issue #1339 & PR #1340: Missing Message Timestamps** - This remains the most discussed open topic. A user `MaoQianTu` has submitted both the request and a fix PR, but it has gone unmerged since April. The underlying need is clear: users lack basic temporal context in conversations.
    - Issue: [netease-youdao/LobsterAI Issue #1339](https://github.com/netease-youdao/LobsterAI/issues/1339)
    - PR: [netease-youdao/LobsterAI PR #1340](https://github.com/netease-youdao/LobsterAI/pull/1340)
- **Issue #1341 & PR #1342: Direction Key History** - Another feature gap by the same user. Power users expect terminal-like keyboard shortcuts (Up/Down arrows) to recall past commands in the input box, a critical workflow efficiency tool.
    - Issue: [netease-youdao/LobsterAI Issue #1341](https://github.com/netease-youdao/LobsterAI/issues/1341)
    - PR: [netease-youdao/LobsterAI PR #1342](https://github.com/netease-youdao/LobsterAI/pull/1342)

#### 5. Bugs & Stability
No new critical bugs or crashes were reported today. The main focus was on **data integrity and reliability fixes**:

- **High Severity (Fixed):** "Null bytes in prompts" (PR #2308) was a major hard-rejection bug that prevented any communication containing empty characters. This has been fixed at both ingestion and outbound boundaries.
- **Medium Severity (Fixed):** "Missing subagent tool history" (PR #2299) was a data display regression where tool calls were not visible on child agent pages, impacting debugging.
- **Low Severity (Fixed):** "OpenClaw cron job pollution" (PR #2301) prevented stale background jobs from being left behind when the memory dreaming feature was disabled.

#### 6. Feature Requests & Roadmap Signals
A cluster of user-requested features, all from the same author (`MaoQianTu`), remain open and provide strong signals for the next version:

- **Full-Text Search (Issue #1343):** Users cannot search inside conversation messages. This is a high-impact request, as functionality is currently limited to session titles.
- **Conversation Export (Issue #1345):** Users want Markdown export to allow text extraction and editing, rather than being limited to screenshots. This suggests growing use of the tool for note-taking and documentation.
- **Direction Key History (Issue #1341):** As noted above, this is a strong UX efficiency signal.
- **Prediction:** The `full-text search` and `export` features are likely candidates for the next minor version, given they are well-specified and address clear user workflows.

#### 7. User Feedback Summary
User feedback is sparse but highly specific and actionable. The primary sentiment is the desire for **"read-only" polish and utility features**:

- **Pain Points:**
    - **Lack of temporal context:** Users cannot see when messages were sent (Issue #1339).
    - **Poor text reusability:** Inability to export conversations to Markdown or recall past input with keyboard shortcuts.
    - **Inadequate search:** The global search is seen as broken for its primary use case (finding conversations by keywords within the chat).
- **Satisfaction:** The one closed bug (Issue #1394 – scheduled tasks being auto-deleted) was a significant bug fix that likely improved user trust in the platform.

#### 8. Backlog Watch
The following important, user-authored PRs remain unmerged and are at risk of becoming stale project blockers. These are the top items needing maintainer attention:

- **PR #1340 (closes #1339):** A fully functional, small-scope PR to add timestamps to user messages. Unmerged since April 2, 2026.
    - [netease-youdao/LobsterAI PR #1340](https://github.com/netease-youdao/LobsterAI/pull/1340)
- **PR #1342 (closes #1341):** A well-implemented PR to add direction key history. Unmerged since April 2, 2026.
    - [netease-youdao/LobsterAI PR #1342](https://github.com/netease-youdao/LobsterAI/pull/1342)
- **Issue #1343:** Full-text search request. Unaddressed since April 2, 2026.
    - [netease-youdao/LobsterAI Issue #1343](https://github.com/netease-youdao/LobsterAI/issues/1343)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-10

## 1. Today's Overview
Moltis shows low activity today with zero issues updated in the last 24 hours and only one open pull request (PR #1146) proposed yesterday. No new releases are available, and no issues were opened or closed. The project appears to be in a stable, low-velocity phase, with community contributions focused on extending model support rather than addressing regressions or bugs. The single active PR indicates maintainers are reviewing a substantial model-catalog addition.

## 2. Releases
*No new releases were published in the last 24 hours. The latest release remains unchanged.*

## 3. Project Progress
- **No PRs were merged or closed today.** The only activity is a single newly-opened PR (see Community Hot Topics), which has not yet been reviewed or integrated.

## 4. Community Hot Topics
- **#1146 [OPEN] Add GPT-5.6 model support**  
  *Author:* PeterDaveHello | *Created:* 2026-07-09 | *Updated:* 2026-07-09  
  *URL:* [PR #1146](https://github.com/moltis-org/moltis/pull/1146)  
  *Analysis:* This is the only active item. The PR adds GPT-5.6 Sol, Terra, and Luna to both OpenAI and OpenAI Codex fallback catalogs, aligns with the documented 1.05M context window, and updates configuration templates. The underlying need appears to be keeping pace with rapid OpenAI model releases (Sol, Terra, Luna naming suggests tiered capabilities/costs). No comments or reactions yet, suggesting the community is still reviewing. The lack of discussion may also indicate that this PR is straightforward and uncontroversial.

## 5. Bugs & Stability
*No bugs, crashes, or regressions were reported in the last 24 hours. The project has zero open issues, indicating a clean stability state at present.*

## 6. Feature Requests & Roadmap Signals
- **GPT-5.6 family support** (via PR #1146) is the most concrete feature signal. If merged, it will add three new model variants (Sol, Terra, Luna) with distinct context limits.  
- **Prediction:** Given the clean repository state and no competing PRs, this model-support addition is likely to be included in the next minor release (e.g., v0.x.y). There are no other roadmap signals from the community today.

## 7. User Feedback Summary
*No user feedback was captured in the last 24 hours (zero issue comments, zero reactions on the sole PR). The absence of feedback may indicate user satisfaction with current functionality, or simply low engagement during this period.*

## 8. Backlog Watch
*No long-unanswered issues or PRs currently exist. The project has zero open issues and only one recently-opened PR (#1146), which requires maintainer review. No items are currently languishing in the backlog.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the project digest for **CoPaw** (GitHub: [agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw)), generated from data observed on **2026-07-10**.

---

## CoPaw Project Digest — July 10, 2026

### 1. Today's Overview

CoPaw shows **very high activity**, with 35 issues and 50 PRs updated in the last 24 hours, indicating a project in an aggressive development and stabilization phase. The release of `v2.0.0-beta.5` yesterday has triggered a wave of user feedback, particularly around the new sandbox and context management features. The community is highly engaged, contributing both bug reports and design proposals, while the core team is rapidly merging fixes for regressions and improving test coverage. Overall, the project is healthy but is currently managing the typical growing pains of a major version upgrade (v2.0.0).

### 2. Releases

**Version:** [v2.0.0-beta.5](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.0.0-beta.5) (Released 2026-07-09)

**What's Changed:**
- **Fix (scroll):** Eviction index now correctly labels un-headlined spans and anchors the live turn with a seam banner to improve context management visualization.

**Analysis:** This is a minor patch release focused on fixing UI/UX bugs in the context compaction (scroll) feature. There are no breaking changes or migration notes for this version.

### 3. Project Progress

In the last 24 hours, **32 PRs were merged or closed**, demonstrating significant forward momentum. Key advancements include:

- **Core Stability:** Several fixes addressed deep-seated bugs, including a critical fix for the `rm -rf ${HOME}` bypass in the rule guardian (`PR #5866`), and recovery of malformed tool-call JSON arguments (`PR #5841`).
- **Channels & Communication:** A fix for DingTalk delivery failures was merged (`PR #5654`), and the default `preserve_thinking` model setting was changed to `false` to prevent recursive reasoning loops (`PR #5870`).
- **Testing Blitz:** A major push to improve code quality saw the merging of four dedicated test PRs covering integration tests for tool-calls (`PR #5895`), unit tests for channels (`PR #5812`), runtime/security regression tests (`PR #5813`), and console hook/store tests (`PR #5808`).
- **MCP & Approvals:** A fix was merged to ensure the frontend `OFF` approval level is correctly honored for Driver policies (`PR #5853`), and the MCP version dependency was pinned (`PR #5904`).
- **Documentation:** The docs were updated for the v2.0 release (`PR #5899`).

### 4. Community Hot Topics

The community is deeply involved in testing and shaping the v2.0 release. The most active discussions are:

- **#2291 - Help Wanted: Open Tasks:** The official community contribution board remains the most active issue, with 64 comments. It is the project's primary mechanism for onboarding new contributors. ([Link](https://github.com/agentscope-ai/QwenPaw/issues/2291))
- **#5879 - Feature Request: Close Sandbox:** With 6 comments, this request highlights a major pain point for power users who find v2.0's sandbox too restrictive for installing libraries. This is a hot topic reflecting the tension between security and flexibility. ([Link](https://github.com/agentscope-ai/QwenPaw/issues/5879))
- **#5797 - Toggle for Scheduled Task Notifications:** Another 6-comment thread where users are pushing back on a recent change that removed pop-up notifications for scheduled tasks, arguing for user-configurable options rather than binary choices. ([Link](https://github.com/agentscope-ai/QwenPaw/issues/5797))

### 5. Bugs & Stability

Several new bugs were reported today, with varying severity.

**High Severity:**
- **Context Compaction Data Loss:** `#5856` reports a critical bug where context compaction strips `tool_call` structure, causing 400 errors. This directly impacts model reliability. (Open, no fix PR yet)
- **Auto Memory Search Failure:** `#5910` shows that the "Auto Memory Search" beta feature generates malformed `function_call` history for the OpenAI Responses API, leading to 502 errors from the provider. (Open, no fix PR yet)
- **Docker `browser_use` Failure:** `#5872` describes a critical bug for Docker users where the browser tool fails due to missing `dbus` connectivity. (Open, no fix PR yet)

**Medium Severity:**
- **False Positive Repetition Detection:** `#5906` reports that the "prevent repetition" feature is incorrectly triggering a "doom loop" flag on normal conversations. (Open)
- **Iteration Limit Miscalculation:** `#5896` indicates the iteration counter is based on the last tool call, not the user's last message, causing premature termination. (Open)
- **OneBot Channel Default Crashes:** `#5898` finds that the OneBot channel starts on default, causing an infinite restart loop and resource consumption. (Fixed/Closed)
- **Windows Sandbox Shell Ignored:** `#5911` reports that the Windows sandbox ignores the configured shell (e.g., PowerShell) and forces `cmd.exe`. (Open, no fix PR yet)
- **MCP Session Auto-Reconnect:** `#5900` reports that terminated `streamable_http` MCP sessions are not automatically reconnected. (Open)

### 6. Feature Requests & Roadmap Signals

The top feature requests point to a need for greater **user configurability and control** over the v2.0 core features.

- **Configurable Sandbox (#5879):** Users want a toggle to disable or configure the sandbox for trusted environments. This is a strong signal for the next minor release.
- **Session Grouping & Import/Export (#5903):** A quality-of-life request to better manage multiple sessions under one agent.
- **Configurable Theme/Skin Module (#5909):** A design proposal for task #1 from the contribution board, indicating community interest in branding and UI customization.
- **Togglable Notifications (#5797):** Persistent demand for user-controlled pop-up notifications for scheduled tasks.

**Prediction:** The "Configurable Sandbox" feature has the highest chance of appearing in a `v2.0.0-beta.6` or `v2.0.0-rc.1`, as it is a blocker for many advanced users migrating from v1.x.

### 7. User Feedback Summary

User sentiment is **polarized**. While the community is actively contributing code and ideas (a sign of high engagement), there is clear **dissatisfaction with the rigidity of v2.0's new systems**.

- **Pain Points:** The **sandbox** is the number one pain point, severely limiting agent capabilities (e.g., installing Python libraries). Users feel it is a "one-size-fits-all" solution that doesn't suit local, trusted deployments.
- **Frustration with Stability:** Multiple reports of the new system falsely triggering repetition loops, miscalculating iteration limits, and failing to render session thumbnails (`#5863`).
- **Desire for Choice:** Users are consistently asking for **options** (e.g., for notifications, sandbox, thinking display) rather than having development decisions remove features entirely.
- **Positive Signal:** The high number of "first-time-contributor" and "Under Review" PRs shows that the community is willing to help fix these issues, indicating a healthy and invested user base.

### 8. Backlog Watch

The following issues/PRs require maintainer attention:

- **#5757 - Feishu Bot Not Replying (13 comments):** A long-standing, high-severity bug affecting a major Chinese channel (Feishu). The bot replies to the first message but goes silent afterward. Despite many comments, it remains open with no attached fix PR. This is a critical issue for users in that ecosystem. ([Link](https://github.com/agentscope-ai/QwenPaw/issues/5757))
- **#5856 - Context Compaction Data Loss (3 comments):** An architecturally significant bug. If this is not resolved, the core context management feature becomes unreliable for complex multi-turn interactions. Needs immediate triage. ([Link](https://github.com/agentscope-ai/QwenPaw/issues/5856))
- **#5187 - Windows GUI Automation (Open PR):** This large-scale `feat(computer-use)` PR has been open for nearly a month. It is a major feature that is likely resource-intensive to review, but it's beginning to stall. Maintainer feedback is needed to keep this contribution moving. ([Link](https://github.com/agentscope-ai/QwenPaw/pull/5187))

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-10

## Today's Overview

ZeroClaw shows **high sustained development velocity** with 36 issues and 50 PRs updated in the last 24 hours. The project has **25 active open issues** and **39 open PRs**, indicating a healthy pipeline of both bug fixes and new features. Activity is concentrated on v0.8.3 milestone work (observability, CI, configuration policy, tool access) and the early stages of v0.9.0 (authentication, security hardening, multi-user isolation). No new releases were published today. The project remains in a **stable, pre-release phase** with significant structural work underway.

## Releases

**No new releases today.** The latest published version is **v0.8.2**, with v0.8.3 and v0.9.0 visible as active milestones in the issue tracker.

## Project Progress

**11 PRs were merged/closed today**, including several high-impact fixes:

- **`[CLOSED] fix(channels/orchestrator): use resolved agent config for strict_tool_parsing and parallel_tools`** ([#7836](https://github.com/zeroclaw-labs/zeroclaw/pull/7836)) — Fixes channel turns ignoring runtime-profile tool flags, a high-severity bug where `strict_tool_parsing` and `parallel_tools` were always `false` for channel messages. Merged by ZOOWH.

- **`[CLOSED] test(log): cover llm request UTF-8 truncation`** ([#8884](https://github.com/zeroclaw-labs/zeroclaw/pull/8884)) — Improves test coverage for UTF-8-safe logging.

- **`[CLOSED] fix(cli): UTF-8-safe stdin cap in exit prompt + audit trail`** ([#8873](https://github.com/zeroclaw-labs/zeroclaw/pull/8873)) — Follow-up audit for byte-limited UTF-8 truncation issues.

- **`[CLOSED] fix(zerocode): use runtime profile max_context_tokens for context meter`** ([#8872](https://github.com/zeroclaw-labs/zeroclaw/pull/8872)) — Fixes context window meter in ZeroCode TUI.

- **`[CLOSED] fix(cron): expose wechat, signal, email in cron delivery schema`** ([#8881](https://github.com/zeroclaw-labs/zeroclaw/pull/8881)) — Expands cron delivery channel support.

- **`[CLOSED] bug(config): degraded-section warning`** ([#8875](https://github.com/zeroclaw-labs/zeroclaw/pull/8875)) — Fixes misleading error messages in config loading.

- **`[CLOSED] fix(tools): add allowed_private_hosts opt-in to file_download SSRF gate`** ([#8713](https://github.com/zeroclaw-labs/zeroclaw/pull/8713)) — Closes a security audit finding for SSRF protection.

- **`[CLOSED] Harden /model --agent scope with per-sender authorization`** ([#8044](https://github.com/zeroclaw-labs/zeroclaw/issues/8044)) — Security fix preventing unauthorized model changes.

## Community Hot Topics

### Most Active Discussions

1. **`[Bug]: zeroclaw does not know it can add cron`** ([#5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862)) — 13 comments. User reports that the agent fails to recognize its own `zeroclaw cron` capability when asked to schedule recurring tasks. **Underlying need**: The agent lacks self-awareness of available CLI tools/capabilities, pointing to a gap in tool discovery or system prompt construction.

2. **`RFC: Work Lanes, Board Automation, and Label Cleanup`** ([#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)) — 13 comments. A governance RFC proposing structured work routing and automation. **Underlying need**: The project is growing and maintainers need systematic triage processes to scale.

3. **`tool_filter_groups is a no-op for real MCP tools (prefix-check bug)`** ([#6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699)) — 9 comments, now closed. Two distinct bugs causing MCP tool filtering to be ineffective. **Underlying need**: Configuration features must actually work; users expect documented behavior to be enforced.

4. **`[Bug]: 单轮对话以及多轮对话会出现丢失 user message的现象`** ([#6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034)) — 8 comments, now closed. Chinese-language bug report about user messages being dropped in conversations. **Underlying need**: Reliable message delivery in multi-turn conversations is critical for production use.

## Bugs & Stability

### New Bugs Reported (Last 24h — Severity Ranked)

| Issue | Severity | Summary | Fix PR Exists? |
|-------|----------|---------|----------------|
| [#8925](https://github.com/zeroclaw-labs/zeroclaw/issues/8925) | S3 (support question) | Configuring Amazon Bedrock — user struggling with AWS profile configuration | No |
| [#8915](https://github.com/zeroclaw-labs/zeroclaw/issues/8915) | S2 (degraded) | `agent_start`/`agent_end` events never emitted for channel turns — observability gap | PR [#8921](https://github.com/zeroclaw-labs/zeroclaw/pull/8921) (open) |
| [#8578](https://github.com/zeroclaw-labs/zeroclaw/issues/8578) | S3 (minor) | On startup failure, process doesn't terminate — leaves zombie process | No |
| [#8762](https://github.com/zeroclaw-labs/zeroclaw/issues/8762) | S2 (degraded) | Anthropic provider uses fixed 120s timeout for long turns — fails legitimate requests | No |
| [#8871](https://github.com/zeroclaw-labs/zeroclaw/issues/8871) | S3 (task) | Third-party API 429 rate-limit responses not handled explicitly | No |

### Critical Issues in Active State

- **`[Bug]: reasoning_content not passed back in agentic tool-call loops`** ([#6672](https://github.com/zeroclaw-labs/zeroclaw/issues/6672)) — Severity S0, affects Xiaomi thinking mode models. No fix PR. Marked as stale-candidate.
- **`Local-First Mode for Small Models`** ([#5287](https://github.com/zeroclaw-labs/zeroclaw/issues/5287)) — Feature request with priority p2, 4 comments, 2 👍. No PR yet.

## Feature Requests & Roadmap Signals

### Top User-Requested Features

1. **OpenAI-compatible chat completions endpoint** ([#8550](https://github.com/zeroclaw-labs/zeroclaw/issues/8550)) — Would allow Open WebUI, LobeChat, and custom integrations to connect. Likely for **v0.9.0** given gateway architecture work underway.

2. **Local-First Mode for Small Models** ([#5287](https://github.com/zeroclaw-labs/zeroclaw/issues/5287)) — Compact no-tools prompting, strict parser, no prompt leakage. Highly active discussion. Likely for **v0.8.3** given existing runtime profile work.

3. **Right-click context menu in ZeroCode chat** ([#8919](https://github.com/zeroclaw-labs/zeroclaw/issues/8919)) — Small UX improvement. Likely for **v0.8.3** as a quick win.

4. **Plugin/capability catalog pane in ZeroCode TUI** ([#8907](https://github.com/zeroclaw-labs/zeroclaw/issues/8907)) — Part of Track A of plugin unification (#8850). PR [#8909](https://github.com/zeroclaw-labs/zeroclaw/pull/8909) is open. Likely for **v0.8.3**.

5. **Discord interaction-surface parity** ([#7831](https://github.com/zeroclaw-labs/zeroclaw/issues/7831)) — Embeds, typed slash options, components, voice. Tracker for multi-PR effort. Likely for **v0.9.0**.

### Roadmap Signals

- **v0.8.3** is being tracked by [#8073](https://github.com/zeroclaw-labs/zeroclaw/issues/8073) (observability, CI, docs) and [#8363](https://github.com/zeroclaw-labs/zeroclaw/issues/8363) (config-driven runtime policy, routing, tool access). These appear close to completion.
- **v0.9.0** is a major auth/security/gateway milestone tracked by [#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432) with 111 open items.
- **Multi-user milestone** ([#8290](https://github.com/zeroclaw-labs/zeroclaw/issues/8290)) is building toward per-principal isolation.

## User Feedback Summary

### Pain Points

1. **Configuration is confusing**: Users report difficulty configuring Amazon Bedrock ([#8925](https://github.com/zeroclaw-labs/zeroclaw/issues/8925)), finding documentation wrong for Telegram ([#8810](https://github.com/zeroclaw-labs/zeroclaw/issues/8810)), and having Anthropic provider not visible until reset ([#8094](https://github.com/zeroclaw-labs/zeroclaw/issues/8094)).

2. **Context overflow causes hallucination**: A Discord user reports that long conversations lead to topic drift and hallucination ([#6517](https://github.com/zeroclaw-labs/zeroclaw/issues/6517)), suggesting context window management is immature.

3. **Agent doesn't know its own capabilities**: [#5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862) highlights a fundamental UX issue where the agent can't self-describe available tools.

4. **Chinese-language users impacted**: [#6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) (message dropping) and [#6558](https://github.com/zeroclaw-labs/zeroclaw/issues/6558) (provider errors) both from Chinese-speaking users, suggesting regional/localization issues.

### Satisfaction Signals

- The project has strong contributor interest: 50 PRs updated in 24h from diverse authors (tidux, Alix-007, wangmiao0668000666, yanchenko, JordanTheJet)
- Quick feature requests like **right-click context menu** ([#8919](https://github.com/zeroclaw-labs/zeroclaw/issues/8919)) are quickly actionable
- The **SSRF security audit fix** ([#8713](https://github.com/zeroclaw-labs/zeroclaw/pull/8713)) shows proactive security posture

## Backlog Watch

### Stale-Candidate Issues Needing Maintainer Attention

| Issue | Age | Priority | Need |
|-------|-----|----------|------|
| [#5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862) — Cron self-awareness | 84 days | p2 | Needs reproduction steps |
| [#6672](https://github.com/zeroclaw-labs/zeroclaw/issues/6672) — reasoning_content not forwarded | 56 days | p2 (S0 severity) | Needs author response and fix |
| [#6558](https://github.com/zeroclaw-labs/zeroclaw/issues/6558) — Provider errors | 61 days | p3 (S0 severity) | Needs author response |
| [#6517](https://github.com/zeroclaw-labs/zeroclaw/issues/6517) — Context overflow hallucination | 64 days | p2 | Needs reproduction steps |

### Stale PRs Requiring Maintainer Review

| PR | Age | Risk | Status |
|----|-----|------|--------|
| [#7098](https://github.com/zeroclaw-labs/zeroclaw/pull/7098) — Mattermost WebSocket listener | 38 days | High | Needs-author-action, stale-candidate |
| [#7215](https://github.com/zeroclaw-labs/zeroclaw/pull/7215) — Quickstart webhook port field | 36 days | High | Needs-author-action, stale-candidate |
| [#7535](https://github.com/zeroclaw-labs/zeroclaw/pull/7535) — WhatsApp reactions | 28 days | Medium | Needs-author-action, stale-candidate |
| [#7637](https://github.com/zeroclaw-labs/zeroclaw/pull/7637) — ZeroCode alias normalization | 26 days | Low | Needs-author-action, stale-candidate |
| [#7914](https://github.com/zeroclaw-labs/zeroclaw/pull/7914) — Windows update test coverage | 22 days | Medium | Needs-author-action, stale-candidate |
| [#8443](https://github.com/zeroclaw-labs/zeroclaw/pull/8443) — Matrix single-message progress | 12 days | High | Needs-author-action |

**Notable**: Five PRs from `chengzhichao-xydt` and one from `xianshishan` are all marked `needs-author-action` and `stale-candidate`, suggesting contributors may have stepped away or are awaiting maintainer guidance. These represent significant feature work (Mattermost, WhatsApp, Quickstart improvements) that could be valuable if revived.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*