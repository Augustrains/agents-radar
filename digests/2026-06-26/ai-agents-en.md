# OpenClaw Ecosystem Digest 2026-06-26

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-26 02:02 UTC

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

# OpenClaw Project Digest — 2026-06-26

## Today's Overview
OpenClaw demonstrates exceptionally high community activity, with 500 issues and 500 PRs updated in the last 24 hours. The project maintains a healthy open-to-closed ratio (475 open issues vs 25 closed; 406 open PRs vs 94 merged/closed), indicating strong ongoing development effort. However, a significant backlog of high-severity issues persists, particularly around session stability, memory management, and security concerns. No new releases were published today, suggesting the team is focused on resolving existing defects before cutting a new version. The maintainer responsiveness bottleneck remains visible, with numerous issues labeled `needs-maintainer-review` and `needs-product-decision` waiting for weeks.

## Releases
No new releases were published on 2026-06-26.

## Project Progress
94 Pull Requests were merged or closed today, indicating sustained development velocity:

**Notable merged/closed PRs:**
- [#96876 — feat(local-realtime-voice)](https://github.com/openclaw/openclaw/pull/96876) — Routes voice turns through the main OpenClaw agent loop, enabling voice sessions to use tools, sub-agents, and file writes like typed chat (closed).
- [#96173 — Add local-realtime-voice extension](https://github.com/openclaw/openclaw/pull/96173) — Self-hosted realtime voice/dictation provider using Whisper STT, Ollama chat, and Kokoro TTS (closed).
- [#68936 — Autofix pipeline + Windows daemon](https://github.com/openclaw/openclaw/pull/68936) — PR review autofix pipeline using Claude Agent SDK subscription plus Windows background daemon (closed).
- [#91168 — CLI-routing label in /model picker](https://github.com/openclaw/openclaw/pull/91168) — Shows CLI backend routing info in model picker UI (closed).
- [#95579 — Allow model fallback on harness-owned prompt timeout](https://github.com/openclaw/openclaw/pull/95579) — Fixes model fallback chain not triggering on timeout for Ollama/OpenRouter (closed).

**Key open PRs advancing:**
- [#81364 — ClawHub trust checks](https://github.com/openclaw/openclaw/pull/81364) — Blocks malicious community plugin/skill installs with explicit user acknowledgement (waiting on author).
- [#94857 — Neutral progress labels](https://github.com/openclaw/openclaw/pull/94857) — Replaces crustacean-themed default labels with neutral technical terms (needs proof).
- [#96391 — Preserve webchat session after restart](https://github.com/openclaw/openclaw/pull/96391) — Fixes session context loss on gateway restart (waiting on author).

## Community Hot Topics

**Most Active Issues:**

1. [#48788 — Centralized filename encoding utility](https://github.com/openclaw/openclaw/issues/48788) (18 comments, ★1) — Multi-encoding Content-Disposition handling across channel adapters. Community seeks a proper architectural solution beyond the current UTF-8/Latin-1 fix.

2. [#63918 — Cron sends thinking=none to OpenAI](https://github.com/openclaw/openclaw/issues/63918) (17 comments, ★1) — Cron jobs fail on models that don't accept `thinking=none`. Users need per-model thinking configuration in cron contexts.

3. [#58450 — Agent promises follow-up without action](https://github.com/openclaw/openclaw/issues/58450) (15 comments, ★3) — Agents hallucinate commitment to background work without starting any. High frustration from users who wait for non-existent follow-ups.

4. [#50090 — Community Skill Development & ClawHub](https://github.com/openclaw/openclaw/issues/50090) (15 comments, ★2) — Gap between promised ecosystem and reality. Users want better documentation, validation, and distribution for community skills.

5. [#45740 — gh-issues skill prompt injection](https://github.com/openclaw/openclaw/issues/45740) (14 comments, ★1) — Raw GitHub issue bodies injected directly into sub-agent prompts without sanitization — a security vulnerability.

**Analysis:** The community is most vocal about three themes: (1) agent reliability — promises that don't materialize, hallucinations, and silent failures; (2) security — particularly prompt injection vectors and credential exposure; and (3) the skill/publishing ecosystem needing maturation to fulfill its promise of community-driven extensibility.

## Bugs & Stability

**Critical (P0/P1, high impact):**

| Issue | Severity | Impact | Fix PR? |
|-------|----------|--------|---------|
| [#53599 — Chrome extension relay removed](https://github.com/openclaw/openclaw/issues/53599) | P1, ★5 | Breaks cross-machine browser automation for managed hosting | No fix PR |
| [#59964 — Keyboard trap in Chrome DevTools](https://github.com/openclaw/openclaw/issues/59964) | P1 | Cmd+W quits whole Electron app, compliance risk | No fix PR |
| [#57326 — CLI backend path bypass](https://github.com/openclaw/openclaw/issues/57326) | P1 | Embedded/API paths still used for CLI models | No fix PR |
| [#54531 — Reply fails to originate channel](https://github.com/openclaw/openclaw/issues/54531) | P1 | Telegram/Discord/WhatsApp responses lost | No fix PR |
| [#63216 — Repeated hard resets on session](https://github.com/openclaw/openclaw/issues/63216) | P1, ★3 | Context overflow despite high reserveTokensFloor | No fix PR |
| [#55334 — sessions.json unbounded growth](https://github.com/openclaw/openclaw/issues/55334) | P1 | Gateway OOM over time | No fix PR |
| [#54155 — Memory leak 389MB → 14.7GB](https://github.com/openclaw/openclaw/issues/54155) | P1 | Gateway crashes after ~4 days | No fix PR |
| [#52249 — ACP parent session stuck](https://github.com/openclaw/openclaw/issues/52249) | P1 | Parent sessions freeze until manual UI refresh | No fix PR |
| [#51429 — Hardcoded working path](https://github.com/openclaw/openclaw/issues/51429) | P2, Chinese community | User's working directory forced to `/Users/wangtao` | No fix PR |

**New/Updated Critical Bugs (today):**
- [#91009 — Codex PreToolUse spawns CPU-bound processes](https://github.com/openclaw/openclaw/issues/91009) (P1) — hooks relay processes consume 100% CPU each, stalling RPC. Linked PR open.

**Regression bugs:** [#51396](https://github.com/openclaw/openclaw/issues/51396) (operator scopes stripped), [#53599](https://github.com/openclaw/openclaw/issues/53599) (extension relay removal), [#52186](https://github.com/openclaw/openclaw/issues/52186) (ElevenLabs TTS ignored), [#48920](https://github.com/openclaw/openclaw/issues/48920) (docs ahead of release).

**Security bugs:** [#45740](https://github.com/openclaw/openclaw/issues/45740) (prompt injection), [#65624](https://github.com/openclaw/openclaw/issues/65624) (cleartext Mattermost tokens, CVSS 7.6/8.6), [#64046](https://github.com/openclaw/openclaw/issues/64046) (sensitive data in plaintext), [#56349](https://github.com/openclaw/openclaw/issues/56349) (missing outbound policy enforcement).

## Feature Requests & Roadmap Signals

**Top community-requested features:**

1. [#50090 — Community Skill Development & ClawHub](https://github.com/openclaw/openclaw/issues/50090) ★2 — Formalized skill publishing, validation, and discoverability. Likely in next major release given ongoing PR #81364 (ClawHub trust checks).

2. [#64046 — Sensitive data masking/redaction](https://github.com/openclaw/openclaw/issues/64046) — API keys, tokens, secrets in plaintext in configs, logs, and UI. High priority given security focus.

3. [#60572 — Multi-Slot Memory Architecture](https://github.com/openclaw/openclaw/issues/60572) ★3 — Replace single memory slot with multiple purpose-specific providers. Advanced feature targeting production deployments.

4. [#63990 — Multi-index embedding memory](https://github.com/openclaw/openclaw/issues/63990) ★1 — Model-aware failover for vector search without corrupting vector spaces.

5. [#50199 — Skill Priority Configuration](https://github.com/openclaw/openclaw/issues/50199) — Intelligent selection when multiple skills overlap.

6. [#52640 — Persistent task-status surface](https://github.com/openclaw/openclaw/issues/52640) ★2 — Long-running channel turns need visible progress indicators (Discord first).

7. [#64438 — Remote Reranker Endpoint Support](https://github.com/openclaw/openclaw/issues/64438) — Similar to remote embedding providers, for improved memory search quality.

**Prediction for next release:** The ClawHub trust model (PR #81364), multi-slot memory architecture, and sensitive data redaction are the most mature proposals with active PRs. The persistent task-status surface and skill priority configuration may arrive as follow-ups.

## User Feedback Summary

**Satisfaction signals:**
- Strong community engagement with 500 issues and 500 PRs updated daily
- Active contribution culture — PRs from 30+ unique authors today
- Appreciation for realtime voice, browser automation, and multi-channel support features

**Pain points (in order of frequency):**

1. **Session reliability** — Agents hallucinate follow-ups, parent sessions freeze, context resets loop despite high token reserves, session persistence lost on restart. Multiple reports of "agent promised X but didn't deliver."

2. **Memory management chaos** — [#43747](https://github.com/openclaw/openclaw/issues/43747) captures user frustration: "I never see any of our memory is managed in same way" — different users get different memory storage behavior.

3. **Memory leaks** — Gateway OOM after days of uptime ([#54155](https://github.com/openclaw/openclaw/issues/54155), [#55334](https://github.com/openclaw/openclaw/issues/55334)). Impact: forced restarts, lost in-flight approvals.

4. **Message loss** — replies not delivered to originating channel ([#54531](https://github.com/openclaw/openclaw/issues/54531)), missed messages on WhatsApp reconnect ([#50093](https://github.com/openclaw/openclaw/issues/50093)), delivered duplicates ([#51628](https://github.com/openclaw/openclaw/issues/51628)).

5. **Docs out of sync with releases** — [#48920](https://github.com/openclaw/openclaw/issues/48920) shows features documented but not yet shipped (★3 agreements).

6. **Hardcoded user paths** — [#51429](https://github.com/openclaw/openclaw/issues/51429) Chinese user reports their workspace forced to `/Users/wangtao` — a clear QA/CICD miss.

7. **Cron reliability** — Jobs fail with empty responses ([#95725](https://github.com/openclaw/openclaw/pull/95725)), timer chain dies on rejection ([#96637](https://github.com/openclaw/openclaw/pull/96637)), scheduler fails silently.

8. **Accessibility** — [#65538](https://github.com/openclaw/openclaw/issues/65538): Screen readers announce every streaming token due to `aria-live="polite"` — blocks accessibility compliance.

## Backlog Watch

**Most concerning long-unanswered items requiring maintainer attention:**

1. [#58450 — Agent promises follow-up without action](https://github.com/openclaw/openclaw/issues/58450) (★3, 15 comments, ~3 months old) — Labeled `needs-product-decision` and `needs-maintainer-review`. Core trust issue with agent behavior. Unanswered since March 31.

2. [#50090 — Community Skill Development & ClawHub](https://github.com/openclaw/openclaw/issues/50090) (★2, 15 comments) — Ecosystem health blocker. Multiple labels including `needs-security-review` and `needs-product-decision`. No product decision in 3 months.

3. [#63216 — Repeated hard resets despite high token floor](https://github.com/openclaw/openclaw/issues/63216) (★3, 11 comments) — `needs-live-repro` but users have provided detailed reproduction. Likely blocks production deployments.

4. [#55334 — sessions.json unbounded growth](https://github.com/openclaw/openclaw/issues/55334) (10 comments) — `needs-live-repro` despite clear root cause analysis. Gateway OOM is a critical blocker.

5. [#53599 — Chrome extension relay regression](https://github.com/openclaw/openclaw/issues/53599) (★5, 6 comments) — Highest reaction count, labeled `needs-product-decision` and `needs-security-review`. Managed hosting providers affected.

6. [#48920 — Docs ahead of release](https://github.com/openclaw/openclaw/issues/48920) (★3, 7 comments) — `IsolatedSessions` documented but not released. Confuses users trying to configure it.

7. [#52130 — Telegram restart storm](https://github.com/openclaw/openclaw/issues/52130) (★1, 6 comments) — `restart storm` and `SecretRef` confusion. Could cause service unavailability.

8. [#51429 — Hardcoded working path](https://github.com/openclaw/openclaw/issues/51429) (0 reactions, but operational severity) — Chinese community user blocked from using the tool. No maintainer response.

---

*Generated from OpenClaw GitHub data: 500 issues, 500 PRs updated in last 24 hours. 94 PRs merged/closed today. 0 new releases.*

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report — 2026-06-26

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem is experiencing a **high-velocity maturation phase** characterized by three simultaneous pressures: security hardening, reliability engineering, and architectural decentralization. Across 11 tracked projects, the dominant theme is **trust restoration**—projects are rushing to patch prompt injection vectors, supply-chain vulnerabilities, and credential exposure bugs that erode production confidence. A second major axis is **memory system sophistication**, with at least four projects (OpenClaw, IronClaw, ZeroClaw, CoPaw) investing in multi-slot, write-behind, or WASM-backed memory architectures. The ecosystem is bifurcating between **general-purpose orchestrators** (OpenClaw, IronClaw, ZeroClaw) and **niche/specialist frameworks** (NanoBot, CoPaw, PicoClaw), with the former group bearing the weight of enterprise feature demands while the latter focuses on platform-specific reliability.

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | PRs Merged (24h) | New Release | Activity Tier | Health Signal |
|---------|-------------|-----------|-------------------|-------------|---------------|---------------|
| **OpenClaw** | 500 | 500 | 94 | No | ⚡ Exceptional | Healthy but bottlenecked (475 open issues) |
| **IronClaw** | 50 | 50 | 24 | No | 🔥 High | Strong velocity, CI fragile (main "persistently red") |
| **ZeroClaw** | 47 | 50 | 1 | No | 🔥 High | Review bottleneck (49 open PRs, 1 merged) |
| **Hermes Agent** | 50 | 50 | 10 | No | 🔥 High | Stable, desktop build regressions |
| **NanoBot** | 25 | 40 | 16 | No | 🔥 High | Security incident response mode |
| **CoPaw** | 27 | 50 | 22 | No | 🔥 High | Post-migration stabilization |
| **PicoClaw** | 3 | 19 | 6 | No | 📊 Moderate | Healthy, dependency maintenance |
| **NanoClaw** | 1 | 16 | 11 | No | 📊 Moderate | Healthy, focused feature work |
| **LobsterAI** | 0 | 9 | 9 | No | 📊 Moderate | Spike day, stability sprint |
| **NullClaw** | 0 | 0 | 0 | N/A | 💤 Inactive | No activity |
| **TinyClaw** | 0 | 0 | 0 | N/A | 💤 Inactive | No activity |
| **Moltis** | 0 | 0 | 0 | N/A | 💤 Inactive | No activity |
| **ZeptoClaw** | 0 | 0 | 0 | N/A | 💤 Inactive | No activity |

**Note:** Health scores reflect current trajectory, not absolute quality. OpenClaw's raw volume is 10x peers but community-to-maintainer ratio is strained.

## 3. OpenClaw's Position

**Advantages:**
- **Community scale dominates:** 500 issues + 500 PRs updated in 24 hours is 10x the nearest competitor (IronClaw/ZeroClaw at ~50 each). This gives OpenClaw the largest contributor pool, bug discovery surface, and feature ideation engine.
- **Completeness of feature surface:** Voice, multi-channel (Telegram, Discord, WhatsApp, Web), cron jobs, sub-agents, ClawHub plugin ecosystem, and multi-model routing are all present in production. No other project matches the breadth of the integration matrix.
- **Proven extensibility:** 94 PRs merged in one day from 30+ unique authors demonstrates a healthy contribution culture and well-documented extension points.

**Technical approach differences:**
- OpenClaw uses a **single-agent-loop** architecture where voice, chat, and sub-agents all route through the same tool-use pipeline (PR #96876). Contrast with IronClaw's **Reborn stack** (capability policy + multi-user auth) and ZeroClaw's **WASM-first plugin runtime** (#8135 RFC).
- Memory model is **single-slot** with a community push for multi-slot (#60572). IronClaw already merged memory extension architecture (#5205) and ZeroClaw has accepted the goal-mode RFC (#8303). OpenClaw is behind on memory architectural evolution.

**Community size comparison:**
- OpenClaw's daily active contributors (30+) likely exceed the total monthly contributors of NanoBot, PicoClaw, and CoPaw combined. However, the maintainer bandwidth is a bottleneck: 475 open issues and 406 open PRs signal a **sustainability problem** if the team doesn't scale.

**Vulnerability:**
- The "docs ahead of release" problem (#48920) and the hardcoded user path (#51429) suggest OpenClaw's QA process doesn't match its development velocity. Critical bugs like Chrome extension relay removal (#53599, ★5) have no fix PR despite being the highest-reaction issue.

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|------------|----------|----------------|
| **Memory System Evolution** | OpenClaw (#60572), IronClaw (#5260, #5205), ZeroClaw (#8303), CoPaw (#5321) | Multi-slot memory, write-behind persistence, turn-based tracking replacing fragile reply IDs, semantic search |
| **Security Hardening** | OpenClaw (#45740, #65624), NanoBot (#4514-4521, #2439), ZeroClaw (#8177), IronClaw (credential proxies) | Prompt injection sanitation, supply-chain signing, exec sandbox bypasses, credential masking |
| **Multi-User/Enterprise Auth** | OpenClaw (ClawHub trust #81364), IronClaw (#5261 epic), ZeroClaw (#8238), NanoClaw (#2857) | Capability policies, per-user tool allowlists, admin→user delegation, multi-admin approval flows |
| **Platform Reliability** | OpenClaw (#54155 memory leak), Hermes Agent (#52735 desktop), CoPaw (#5379 Windows), NanoBot (#1710 "no response") | OOM prevention, desktop build CI, cross-platform parity, model fallback when API fails |
| **Context & Session Management** | OpenClaw (#63216 resets), IronClaw (#5276 automation), ZeroClaw (#5903 MCP leaks), CoPaw (#5162 infinite loop) | Persistent sessions, bounded context windows, cron reliability, sub-agent lifecycle |
| **Plugin Ecosystem Maturation** | OpenClaw (ClawHub), ZeroClaw (WASM runtime #8135), LobsterAI (OpenClaw extension system), CoPaw (pip plugins #5484) | Signed distribution, sandboxed execution, validation pipelines, version management |

## 5. Differentiation Analysis

| Dimension | OpenClaw | IronClaw | ZeroClaw | Hermes Agent | NanoBot | CoPaw |
|-----------|----------|----------|----------|--------------|---------|-------|
| **Target User** | Power users, self-hosters | Enterprise teams, compliance | Rust-native developers, edge deployers | Desktop-first individual users | Security-conscious teams | Chinese-market enterprises |
| **Architecture** | Python monolith, single agent loop | Reborn stack: capability policy + multi-user | Rust core, WASM plugin runtime | Node.js/Electron desktop app | Python, MCP-focused | Python, AgentScope 2.0 upstream |
| **Strength** | Breadth of integrations | Enterprise features (auth, approvals) | Performance, sandboxing | Desktop UX, Electron polish | Rapid security responses | Chinese ecosystem (DingTalk, QQ) |
| **Weakness** | Review bottleneck, memory leaks | CI instability, Reborn migration churn | Plugin ecosystem immature | Windows fragility, stale skills index | Small community, supply-chain history | Post-migration regression burden |
| **Release Cadence** | Continuous (main branch) | Feature-gated (Reborn milestones) | v0.8.x → v0.9.0 (breaking) | v0.17.x (stable) | Ad-hoc (security-driven) | v1.1.12.post2 (post-migration) |

**Key insight:** The ecosystem is not competing on the same axis. OpenClaw and IronClaw are **converging** toward enterprise multi-user support but from different starting points—OpenClaw from community breadth, IronClaw from enterprise compliance. ZeroClaw is taking a **radically different** path (Rust + WASM) that may leapfrog both in performance and security but risks ecosystem fragmentation. Hermes Agent and CoPaw serve **complementary niches** (desktop UX, Chinese enterprise) rather than competing head-on.

## 6. Community Momentum & Maturity

**Tier 1: Rapidly Iterating (pre-release churn, high feature velocity)**
- **OpenClaw**: Exceptionally high activity but sustainability concerns. The 94 PRs merged today is impressive, but 475 open issues means bugs are accumulating faster than fixes land. The lack of a new release despite massive PR volume suggests **feature debt**—the team is shipping code but not stabilizing it into releases.
- **IronClaw**: Strong architectural investment (Reborn) with 24 PRs merged. CI fragility is the main risk. Dogfooding culture (tracking issue #5119) shows maturity in quality process.
- **ZeroClaw**: Most ambitious roadmap (WASM, supply-chain signing, Rust→Wasm web UI). However, 49 open PRs with only 1 merged today indicates a **bottleneck** that, if resolved, could make ZeroClaw the fastest-evolving project. The long-term technical bet (Rust) is high-risk but high-reward.

**Tier 2: Stabilizing (post-migration, security hardening)**
- **NanoBot**: In active security incident response mode. The YLChen-007 audit discovered 8+ exec sandbox bypasses being patched in real-time. Community is small but responsive. Post-crisis, NanoBot could emerge with the strongest security posture.
- **CoPaw**: Heavy regression burden from AgentScope 2.0 migration. 22 PRs merged shows strong stabilization velocity, but critical Windows startup errors (#5379) and infinite-loop bugs (#5162) remain open. The plugin ecosystem (PR #4622, 34 days under review) needs maintainer attention.
- **Hermes Agent**: Most stable project by release cadence (v0.17.x), but desktop build fragility (#52735) and stale skills index (#38240, 23 days unfixed) show operational fatigue. Good community engagement (10 PRs merged) but no architectural moat—Hermes could be disrupted by OpenClaw's breadth or ZeroClaw's performance.

**Tier 3: Moderate/Inactive**
- **PicoClaw, NanoClaw, LobsterAI**: Healthy but lower volume. PicoClaw's token-waste fix (#3169) and NanoClaw's 11 PRs merged show focused, sustainable development. LobsterAI's stability sprint (9 PRs in one day) is a positive spike.
- **NullClaw, TinyClaw, Moltis, ZeptoClaw**: No activity—effectively dormant. These projects should be considered dead or in hibernation. Any ecosystem dependency on them carries risk.

## 7. Trend Signals

**Signal 1: "Trust is the new feature."** The ecosystem is shifting from "can it do X?" to "can I trust it to do X safely?" This is visible across:
- Prompt injection vulnerability fixes (OpenClaw #45740, NanoBot #4514-4521)
- Supply-chain signing proposals (ZeroClaw #8177, OpenClaw ClawHub trust)
- Credential masking demands (OpenClaw #64046, Hermes Agent #4656, NanoClaw #2860)
- Exec sandbox bypasses being systematically audited (NanoBot's YLChen-007 series)

**Value for developers:** When evaluating projects, security maturity (how quickly they patch, whether they have audit processes) is now as important as feature count. A project with fewer features but a proactive security response (NanoBot) may be safer than a feature-rich project with open security issues (OpenClaw).

**Signal 2: "Memory is the new compute."** Memory system architecture is becoming the primary differentiator:
- **IronClaw** merged extension manifest v2 (#5205) with source-aware trust and host-defined capability profiles
- **ZeroClaw** accepted goal-mode RFC (#8303) for bounded autonomous sessions
- **OpenClaw** community demands multi-slot memory (#60572)
- **CoPaw** PR #5321 proposes SQLite-backed durable history

**Value for developers:** The winning agent framework will likely be the one that figures out persistent, safe, and efficient memory first. This is the infrastructure bet for 2026-2027.

**Signal 3: "Multi-user is the enterprise unlock."** At least four projects are building enterprise-grade multi-user support:
- IronClaw's capability policy epic (#5261) with REST admin surface
- OpenClaw's ClawHub trust model (PR #81364) for admin-controlled plugin installs
- ZeroClaw's independent delegate mode (#8238) for specialist agent handoffs
- NanoClaw's multi-admin approval (#2857) for team deployments

**Value for developers:** The projects that first deliver a mature multi-user experience (with proper auth, auditing, and policy enforcement) will capture the enterprise market. IronClaw appears closest, but ZeroClaw's Rust+WASM foundation may make it more secure for compliance-heavy environments.

**Signal 4: "Windows parity is the last mile."** Multiple projects have Windows-specific failures:
- Hermes Agent: desktop builds broken (#52735), installer fails (#46260)
- CoPaw: internal server error on startup (#5379)
- OpenClaw: hardcoded paths (#51429), Electron keyboard trap (#59964)
- IronClaw: Nix gateway bypass (#48071)

**Value for developers:** If your target deployment includes Windows users (enterprise, education, casual), factor this into project choice. Currently, Hermes Agent has the best desktop experience but is breaking. OpenClaw's web-first approach bypasses some issues but misses native desktop UX.

**Signal 5: "Plugin ecosystems are being re-architected."** 
- **ZeroClaw**: WASM-first plugin runtime (#8135) with capability enforcement, signed distribution, and OCI registries (#7497)
- **OpenClaw**: ClawHub trust checks (PR #81364) for skill/marketplace safety
- **CoPaw**: pip-based plugin distribution (#5484) citing Hermes Agent as precedent
- **LobsterAI**: Precompiled TypeScript extension pipeline (PR #2203)

**Value for developers:** The plugin architecture choice will determine development velocity for third-party extensions. WASM (ZeroClaw) offers the best sandboxing but highest friction. Python pip (CoPaw) is easiest but least secure. OpenClaw's JSON-manifest approach is mid-ground. Choose based on how much you value security vs. developer onboarding speed.

---

**Bottom line for decision-makers:** OpenClaw is the safest choice for breadth and community support, but its sustainability issues are real. IronClaw is the enterprise bet with the most complete multi-user architecture. ZeroClaw is the moonshot—highest risk, highest potential payoff. Hermes Agent remains the best desktop experience but is losing architectural momentum. NanoBot is a security-first alternative for risk-averse deployments. For Chinese market deployments, CoPaw is the default. For resource-constrained environments (Raspberry Pi, FreeBSD), PicoClaw is the clear leader.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Based on the GitHub data for NanoBot (github.com/HKUDS/nanobot) on 2026-06-26, here is the project digest.

---

### NanoBot Project Digest — 2026-06-26

### 1. Today's Overview
Today marks a significant security-focused day for the NanoBot project, with a high volume of activity concentrated on patching vulnerabilities. Activity is very high: 25 issues were updated, and 40 pull requests (PRs) were updated, including 16 merged/closed. The community, particularly security researcher **YLChen-007**, has reported a coordinated set of bypass vulnerabilities affecting the `exec` tool and MCP server configurations. The project's maintainers have responded in kind, opening several fix PRs, indicating a rapid and active response to a reported security audit. Overall, project health is robust but under heavy scrutiny for its attack surface.

### 2. Releases
**No new releases were published today.** The project is currently between releases, with the last reported version being `v0.2.1`, which is the subject of several critical vulnerability advisories.

### 3. Project Progress
Sixteen PRs were merged or closed today. Key advancements and fixes include:
- **Security Patching:** A cluster of security fixes was merged/closed. Notably, PR [#4524](https://github.com/HKUDS/nanobot/pull/4524) (closed) directly addresses the MCP `enabledTools` scope bypass (Issue #4519) by applying allowlist filtering to resources and prompts.
- **Filesystem Safety:** PR [#4099](https://github.com/HKUDS/nanobot/pull/4099) (merged) fixes a critical security bug (Issue #4073) by keeping `extra_allowed_dirs` in the filesystem tools read-only for write operations, preventing write access to directories intended only for reading.
- **Platform Fixes:** Two community fixes were merged: one for DingTalk integration ([#4497](https://github.com/HKUDS/nanobot/pull/4497)) adding rich text support and timeout handling, and another for the WebUI ([#4493](https://github.com/HKUDS/nanobot/pull/4493)) converting WebM audio to WAV for Xiaomi MiMo ASR transcription.

### 4. Community Hot Topics
The most active discussions are almost entirely security-related, driven by a single researcher, YLChen-007.
- **[Issue #4519](https://github.com/HKUDS/nanobot/issues/4519) (Closed) - MCP `enabledTools` Scope Bypass:** This was the focal point of the day, with 2 comments. It described how the MCP allowlist only filtered tools but not resources/prompts. This was quickly fixed by PR #4524.
- **[Issue #2439](https://github.com/HKUDS/nanobot/issues/2439) (Closed) - Malicious Code in PyPI Package:** This 3-month-old critical security issue received renewed attention with 6 comments and 4 👍. It involves a `.pth` file in a past PyPI release executing data-exfiltration code. The age and severity of this closed issue highlight a historical supply-chain compromise.
- **The YLChen-007 Audit Series:** The researcher filed a chain of 8 distinct high-severity issues ([#4514](https://github.com/HKUDS/nanobot/issues/4514) through [#4521](https://github.com/HKUDS/nanobot/issues/4521)) all targeting the `exec.allowPatterns` allowlist. These bugs describe various bypasses using shell chaining (`;`, `&&`), comment stripping, and invoking login-shell startup files. This represents a deep, methodical audit of the shell execution sandbox.

### 5. Bugs & Stability
The day's activity is dominated by **critical security vulnerabilities** rather than general stability bugs. They are ranked as follows:
- **Critical (Supply Chain):** Issue [#2439](https://github.com/HKUDS/nanobot/issues/2439) (Closed) - Malicious code in a historical release (v0.1.4.post5). This is a significant trust and security event.
- **Critical (Config Bypasses):** Multiple issues (e.g., [#4514](https://github.com/HKUDS/nanobot/issues/4514) to [#4521](https://github.com/HKUDS/nanobot/issues/4521), currently **Open**) - Systematic bypasses of the `exec.allowPatterns` allowlist. These are actively being addressed with fix PRs like [#4526](https://github.com/HKUDS/nanobot/pull/4526).
- **High (Access Control):** Issues [#4519](https://github.com/HKUDS/nanobot/issues/4519) (Closed) and [#4073](https://github.com/HKUDS/nanobot/issues/4073) (Closed) - MCP resources/prompts bypassing deny-all policies and filesystem tools ignoring read-only intent. Both appear fixed today.
- **Medium (Core Output):** Issue [#1710](https://github.com/HKUDS/nanobot/issues/1710) (Closed) - Agent frequently returns "no response" with the `qwen 3.5` model, suggesting a provider-specific or prompt-formatting issue.

### 6. Feature Requests & Roadmap Signals
Several new features were proposed today, indicating a focus on agent reliability and user experience:
- **[Issue #4508](https://github.com/HKUDS/nanobot/issues/4508) (Open) - `ask_clarification` Tool:** A user requests a tool that allows the agent to pause and ask a question when a request is ambiguous or requires confirmation, improving autonomous decision-making safety.
- **[PR #4534](https://github.com/HKUDS/nanobot/pull/4534) (Open) - Verification Gates & Provider Recovery:** A new PR adds a reliability layer for the agent loop, including "verification gates" to check if tasks are complete and "provider recovery" to handle transient API errors. This could be a core improvement in the next release.
- **[PR #4506](https://github.com/HKUDS/nanobot/pull/4506) (Open) - MCP Idle Timeout:** A feature to auto-kill idle MCP server processes to prevent resource leaks.
- **[PR #4494](https://github.com/HKUDS/nanobot/pull/4494) (Open) - PWA & Mobile Gestures:** A user-experience enhancement bringing Progressive Web App support and sidebar swipe gestures to the WebUI.

### 7. User Feedback Summary
User feedback today is divided into two themes: **pain from security anxiety** and **praise for mobile UX**.
- **Dissatisfaction (Security & Reliability):** The flurry of security reports, especially the historical supply-chain issue ([#2439](https://github.com/HKUDS/nanobot/issues/2439)), creates significant trust concerns. Users are also frustrated by the agent's tendency to say "no response" ([#1710](https://github.com/HKUDS/nanobot/issues/1710)).
- **Satisfaction (Functionality):** The DingTalk integration fix ([#4497](https://github.com/HKUDS/nanobot/pull/4497)) and the PWA support proposal ([#4494](https://github.com/HKUDS/nanobot/pull/4494)) show users actively working to improve the platform's integration and mobile experience, indicating a high level of engaged satisfaction.

### 8. Backlog Watch
The most critical items on the backlog are the newly opened security issues from the YLChen-007 audit.
- **[Issues #4514](https://github.com/HKUDS/nanobot/issues/4514), [#4515](https://github.com/HKUDS/nanobot/issues/4515), [#4516](https://github.com/HKUDS/nanobot/issues/4516), [#4518](https://github.com/HKUDS/nanobot/issues/4518), [#4519](https://github.com/HKUDS/nanobot/issues/4519), [#4520](https://github.com/HKUDS/nanobot/issues/4520), [#4521](https://github.com/HKUDS/nanobot/issues/4521) (All Open, 0 comments):** These `exec.allowPatterns` bypasses are the most urgent items. While maintainers have opened fix PRs, these issues are currently unresolved and represent a live vulnerability. Failure to merge the fixes quickly would severely impact deployment safety.
- **[Issue #2439](https://github.com/HKUDS/nanobot/issues/2439) (Closed - Malicious Code):** This is a historical, closed issue, but it should be a major item for the maintainers to provide a post-mortem or advisory. It has high community attention (4 👍) and concerns a past supply-chain compromise that has likely already affected users.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-06-26

---

## 1. Today's Overview

Hermes Agent is experiencing a high-activity day with 50 issues and 50 PRs updated in the last 24 hours, signaling robust development and community engagement. The project remains stable with no new releases today, but the volume of bug reports and fixes suggests a wave of regressions following recent updates. Critical infrastructure concerns dominate the board, including desktop build failures after git pulls, gateway stalling issues, and FTS write corruption in session databases. The community is actively submitting PRs, with 10 merged/closed today and 40 open, indicating a healthy pull request pipeline.

---

## 2. Releases

**No new releases today.** The latest release remains version 0.17.0 (referenced in multiple bug reports). Users should be aware that recent `main` branch changes introduced regressions in desktop builds and gateway stability.

---

## 3. Project Progress

**Merged/Closed PRs (10 total) — key fixes advanced today:**

- **PR #52795** (closed): Reasoning-model thinking-timeouts no longer trigger phantom context-compression that deletes conversation history. Root cause identified as transport disconnect mid-thinking on NVIDIA NIM, OpenAI o1/o3, and other reasoning models.
- **PR #52761** (closed): Gateway event loop no longer stalls after cross-process agent-cache invalidation — fixes Discord heartbeat blocking issue (#52197).
- **PR #52671** (closed): Cron restore safety net now catches partial job loss (not just total loss), preventing tool-created cron jobs from being lost during desktop scheduler overwrites after updates.
- **PR #52744** (closed): Telegram polling gateway now detects CLOSE-WAIT TCP sockets with a persistent heartbeat loop, preventing silent failure (#48495).
- **PR #52755** (closed): README marketing-friendly overhaul — transformed from feature-list dump to a "Why Hermes?" card grid.
- **PR #52272** (closed): Two-part fix for reasoning-model thinking-timeout UX — classifier override routes transport disconnects to `FailoverReason.timeout` instead of `context_overflow`.

---

## 4. Community Hot Topics

**Most Discussed Issues:**

| Issue | Comments | Reactions | Topic |
|-------|----------|-----------|-------|
| [#38240](https://github.com/NousResearch/hermes-agent/issues/38240) 🔴 | 12 | 0 | Skills index stale/degraded — automated freshness probe failing for 23 days |
| [#4656](https://github.com/NousResearch/hermes-agent/issues/4656) | 11 | 1 👍 | Credential proxy daemon — zero-knowledge HTTP/HTTPS broker for agent credentials |
| [#52735](https://github.com/NousResearch/hermes-agent/issues/52735) ✅ | 9 | 1 👍 | Desktop app crashes on launch — `Cannot find module 'simple-git'` |
| [#39691](https://github.com/NousResearch/hermes-agent/issues/39691) | 8 | 10 👍 | Headroom-ai tool output compression integration (highly upvoted) |
| [#36658](https://github.com/NousResearch/hermes-agent/issues/36658) | 8 | 2 👍 | Dashboard chat broken after Hermes update (React minified error) |
| [#8552](https://github.com/NousResearch/hermes-agent/issues/8552) | 8 | 9 👍 | Slack Block Kit markdown support (table rendering) |

**Analysis:** The most active issue (#38240) reveals a systemic problem with the skills index freshness probe failing for 23 days without resolution. The most **upvoted** request (#39691, 10👍) for tool-level compression suggests users are hitting context limits frequently, while #8552 (9👍) shows strong demand for platform-native markdown rendering.

**Most Active PRs:**

| PR | Status | Topic |
|----|--------|-------|
| [#52799](https://github.com/NousResearch/hermes-agent/pull/52799) | Open | Gate credential pools by provider |
| [#52798](https://github.com/NousResearch/hermes-agent/pull/52798) | Open | Detect/repair FTS write corruption in gateway history |
| [#52789](https://github.com/NousResearch/hermes-agent/pull/52789) | Open | Skip symlinked stage2 chown targets in Docker |
| [#30179](https://github.com/NousResearch/hermes-agent/pull/30179) | Open | Iron-proxy credential-injection firewall for sandboxes |

---

## 5. Bugs & Stability

**P1 (Critical) Bugs:**

| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#52197](https://github.com/NousResearch/hermes-agent/issues/52197) ✅ | Gateway cross-process cache invalidation stalls event loop, blocking Discord heartbeats | ✅ #52761 (closed) |
| [#48137](https://github.com/NousResearch/hermes-agent/issues/48137) ✅ | Windows Docker terminal backend: raw Windows paths leak into Linux containers, exposes home dir | ✅ Closed |
| [#52023](https://github.com/NousResearch/hermes-agent/issues/52023) ✅ | GPT-4o-mini and GPT-4.1 fail with "Encrypted content not supported" after clean install | ✅ Closed |
| [#43719](https://github.com/NousResearch/hermes-agent/issues/43719) ✅ | Malicious third-party plugins targeting Hermes dashboards (security incident) | ✅ Closed |
| [#48071](https://github.com/NousResearch/hermes-agent/issues/48071) ✅ | Nix gateway install bypasses Hermes wrapper | ✅ Closed |
| [#52764](https://github.com/NousResearch/hermes-agent/issues/52764) 🔴 | `hermes update` produces broken Desktop asar when git pull adds npm deps to Electron main | No PR yet |
| [#52735](https://github.com/NousResearch/hermes-agent/issues/52735) ✅ | Desktop app crashes on launch — `simple-git` missing | ✅ Closed (duplicate of #52764) |
| [#29912](https://github.com/NousResearch/hermes-agent/issues/29912) 🔴 | Curator archives active skills during umbrella pass without verified consolidation | No PR yet |

**P2 Bugs:**

| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#46260](https://github.com/NousResearch/hermes-agent/issues/46260) | Hermes installer fails at "desktop" stage on Windows 10 (npm install exit code 1) | 🔴 No |
| [#28004](https://github.com/NousResearch/hermes-agent/issues/28004) | Telegram typing indicator stuck indefinitely after response | 🔴 No |
| [#40801](https://github.com/NousResearch/hermes-agent/issues/40801) | Cron script-path guard rejects profile-scoped jobs with default-profile scripts | 🔴 No |
| [#52786](https://github.com/NousResearch/hermes-agent/issues/52786) | Feishu adapter downgrades markdown tables to plain text | ✅ #52790 (open) / #27922 (open) |

**New Regressions Today:** The `simple-git` dependency added in commit `e2b801872` broke desktop builds (#52764, #52735, #52753). Multiple duplicate issues suggest this is affecting many Windows users. The fix is being addressed but no PR exists yet.

---

## 6. Feature Requests & Roadmap Signals

**Most Requested Features (by upvotes):**

1. **[#39691](https://github.com/NousResearch/hermes-agent/issues/39691) — Tool Output Compression (10👍):** Integrate headroom-ai for per-tool output compression instead of session-level summarization. Likely for next release given high upvotes and existing compression infrastructure.

2. **[#8552](https://github.com/NousResearch/hermes-agent/issues/8552) — Slack Block Kit Markdown (9👍):** Use Block Kit markdown block type instead of legacy mrkdwn for table support. Already has an open PR.

3. **[#44428](https://github.com/NousResearch/hermes-agent/issues/44428) — Telegram Bot API 10.1 Rich Messages (5👍):** Support rich draft streaming and new message types. Timely as Telegram just released this API.

**Other Notable Requests:**
- [#52137](https://github.com/NousResearch/hermes-agent/issues/52137) — Russian localization (part of growing i18n demand: French #47811, Chinese #39571, Portuguese #40239)
- [#52787](https://github.com/NousResearch/hermes-agent/issues/52787) — Minimize to system tray instead of closing on Windows/Linux
- [#48843](https://github.com/NousResearch/hermes-agent/issues/48843) — Bulk archive sessions in Desktop GUI
- [#52769](https://github.com/NousResearch/hermes-agent/issues/52769) — Auto-create Linux .desktop entry on first launch

**Prediction for Next Version:** Tool-level compression (#39691), Slack Block Kit (#8552), and Telegram 10.1 support (#44428) are strong candidates given their alignment with user needs and existing PRs.

---

## 7. User Feedback Summary

**Pain Points (Real User Reports):**
- **Desktop build fragility:** "After an in-app desktop update to current `main`, the Hermes desktop app fails to launch" (#52735) — indicates CI/CD gaps for Electron builds
- **Windows instability:** Multiple reports of failed installers (#46260), broken updates (#52753), and Docker path issues (#48137) — Windows remains a problem platform
- **Session isolation failures:** "Conversation history leaks across different active sessions" (#49106) — fundamental data integrity concern
- **Gateway reliability:** "Telegram typing indicator stuck indefinitely" (#28004), "gateway silently stops receiving messages" (#48495) — chronic gateway stability issues
- **Platform compatibility:** "Feishu adapter incorrectly downgrades markdown tables to plain text" (#52786), Slack table rendering (#8552)

**Satisfaction Signals:**
- High engagement with feature requests (9-10👍 on compression and Slack features)
- Active community submitting PRs for bug fixes (10 merged today)
- Detailed, well-scoped bug reports from users (many with root cause analysis)

**Dissatisfaction Indicators:**
- Skills index probe failing for 23 days without resolution (#38240) — systemic monitoring gap
- Duplicate desktop regression issues (#52735, #52753, #52764) — suggests testing coverage gaps before merging to main

---

## 8. Backlog Watch

**Critical Items Lacking Attention:**

| Issue | Age | Topic | Reason for Concern |
|-------|-----|-------|---------------------|
| [#38240](https://github.com/NousResearch/hermes-agent/issues/38240) 🔴 | 23 days | Skills index stale/degraded | Automated freshness probe failing; no comments from maintainers |
| [#29912](https://github.com/NousResearch/hermes-agent/issues/29912) 🔴 | 36 days | Curator archives active skills without verification | P1 severity — can cause operational skill loss |
| [#4656](https://github.com/NousResearch/hermes-agent/issues/4656) | 85 days | Credential proxy daemon | Important security feature; 11 comments, 1 👍, no maintainer response |
| [#29299](https://github.com/NousResearch/hermes-agent/issues/29299) | 37 days | HTTPS OAuth callback URL | Blocks enterprise OAuth setups (Salesforce MCP) |
| [#34390](https://github.com/NousResearch/hermes-agent/issues/34390) | 28 days | Dashboard `--allowed-hosts` flag for reverse proxy | Blocks Tailscale Serve and reverse-proxy deployments |

**Long-running Open PRs Requiring Review:**

| PR | Age | Topic |
|----|-----|-------|
| [#8427](https://github.com/NousResearch/hermes-agent/pull/8427) | 75 days | Vertex AI provider for Gemini models |
| [#27922](https://github.com/NousResearch/hermes-agent/pull/27922) | 39 days | Feishu markdown table rendering fix |
| [#30179](https://github.com/NousResearch/hermes-agent/pull/30179) | 35 days | Iron-proxy credential firewall |
| [#27829](https://github.com/NousResearch/hermes-agent/pull/27829) | 39 days | Bedrock API routing fix |

**Verdict:** Maintainers should prioritize the stale skills index (#38240) and curator bug (#29912) as they affect core operational reliability. The long-running Vertex AI PR (#8427) and OAuth HTTPS feature (#29299) are blocking enterprise adoption paths.

---

*Digest generated from GitHub issues, PRs, and releases data. Metrics based on items updated in the last 24 hours as of 2026-06-26.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-26

## Today's Overview
Project activity remains moderate with 19 PRs updated in the last 24 hours and 3 issues receiving attention. A cluster of stability-focused pull requests from both core contributors and a new external contributor (Alix-007) has been merged, addressing resource leaks, cold-path token waste, and type assertion safety. Dependency updates account for roughly a third of open PRs, signaling ongoing maintenance overhead. One high-priority open issue (#3088) calling for replacement of an insecure cryptographic library continues to lack a merged fix.

## Releases
No new releases were published. The latest stable version remains **v0.2.9** (referenced in issue #3012).

## Project Progress
Six pull requests were merged or closed in the last 24 hours:

- **#3169** (merged, by Alix-007) — `fix(evolution): skip cold path for heartbeat turns`. Prevents draft-mode evolution from spending tokens on periodic heartbeat checks. Includes regression test.
- **#3168** (merged, by Alix-007) — `fix(model): handle error response read failures`. Returns the body read error when fetching OpenAI-compatible model lists receives a non-200 response, avoiding misleading empty HTTP errors.
- **#3166** (merged, by Alix-007) — `fix(openai_compat): use structured logger for native_search warning`. Replaces a stray `log.Printf` with the proper structured logger, fixing a build failure.
- **#3092** (closed, by chengzhichao-xydt) — `fix(skills_install): add ok checks for version and force type assertions`. Prevents silent zero-value fallback when type assertions fail.
- **#3145** (closed, by dependabot) — `build(deps): bump github.com/github/copilot-sdk/go from 0.2.0 to 1.0.2`. Dependency upgrade.
- **#3045** (closed, by chengzhichao-xydt) — `fix(identity): allow_from fallthrough for Matrix user IDs with colon`. Fixes a bug where `allow_from` silently rejected Matrix user IDs like `@alice:example.com`.

## Community Hot Topics

**Most Active Issue:**
- **#3088** (open, 3 comments, 2 👍) — *[Feature] use vodozemac instead of libolm*  
  Author: pbsds | [GitHub](https://github.com/sipeed/picoclaw/issues/3088)  
  The community is calling for the removal of the unmaintained `libolm` library and adoption of `vodozemac`, the official replacement. With 2 reactions and a `priority: high` label, this reflects growing security awareness among Matrix-integration users.

**Most Active Pull Requests (by recency & volume):**
- **#3142** (open, stale) — *fix(spawn): clear ForUser in sub-turn ToolResult to prevent duplicate messages* by jincheng-xydt. Addresses a root cause of duplicate push notifications when sub-agent tasks complete.
- **#3118** (open, by jp39) — *Add remote Pico WebSocket mode to picoclaw agent*. Introduces optional remote connectivity, which generated sustained interest through the week.
- **#3063** (open, by trufae) — *feat: add deltachat gateway*. A long-open new channel feature that continues to see developer activity.

**Underlying Needs:** Users are prioritizing (a) security upgrades for cryptographic backends, (b) elimination of token waste in agent evolution, and (c) remote agent operation modes for headless/hub deployments.

## Bugs & Stability

**High Severity:**
- **#3012** (closed) — *Continuous consumption of tokens every minute when evolution is enabled* on FreeBSD with MiniMax provider. Root cause: heartbeat turns triggered evolution cold-path scheduling, wasting tokens. **Fix merged in #3169** by Alix-007. Resolved.

**Medium Severity:**
- **#1757** (closed) — *Channel error when asking agent to perform tasks every hour*. Affected v0.2.3 on Rpi Zero W with Telegram. Closed with 10 comments — likely related to cron scheduling edge cases, now addressed.

**New Fixes Submitted (open but with active PRs):**
- **#3172** (open) — *fix: explicitly ignore Close() errors in error paths and retry loops* (8 call sites, 4 files). Prevents misleading secondary errors from leaking to callers.
- **#3171** (open) — *fix(line): add ok checks for sync.Map type assertions in Send*. Prevents potential panics in the LINE channel.
- **#3170** (open) — *fix(agent): close base64 encoder on io.Copy error path*. Eliminates resource leaks when file processing fails.
- **#3115** (open) — *Fix inline data URL media extraction for generic tool output*. Prevents session-history corruption when `data:image/...;base64,...` strings appear in `read_file`/`exec` output.

**Overall Stability Trend:** The project is actively hardening error handling paths and resource cleanup. The three PRs from Alix-007 merged today specifically addressed token waste and error reporting correctness. No new crashes or regressions were reported in the last 24 hours.

## Feature Requests & Roadmap Signals

**Under Active Development (PRs open):**
- **Remote Pico WebSocket mode** (#3118) — Enables `picoclaw agent --remote ws://...` for headless/hub deployments. This directly addresses the need for centralized agent management.
- **DeltaChat gateway** (#3063) — Adds support for the DeltaChat messaging protocol, broadening the channel ecosystem beyond Telegram, Web, and LINE.

**High-Demand Feature (issue open, pending implementation):**
- **Vodozemac replacement for libolm** (#3088) — The `priority: high` label and 2 upvotes indicate this is likely slated for the next minor release (v0.3.0 or equivalent). The PR for this is still missing, but the roadmap alignment is clear.

**Prediction for Next Version:** Based on the current PR activity and issue priorities, the next version will likely include:
- Vodozemac migration (if implementation accelerates)
- Remote agent operation mode
- DeltaChat gateway
- All error-handling fixes currently in open PRs (Close() errors, type assertions, base64 encoder)

## User Feedback Summary

**Pain Points:**
- Token consumption problems in evolution mode remain the most prominent user-facing issue, now fixed in #3169.
- Channel errors in cron/scheduled tasks (issue #1757) frustrated Rpi Zero users, but was closed after 10 comments.
- Matrix integration users face security uncertainty due to unmaintained `libolm`, with explicit calls to migrate.
- The `allow_from` identity filter was silently breaking Matrix user ID matching — surprising for operators relying on access control.

**Use Cases Reflected:**
- **Scheduled automation on low-power hardware** (Raspberry Pi Zero W, FreeBSD) — users are running PicoClaw on minimal devices for periodic tasks.
- **Multi-platform agent deployment** — Telegram, Web, Matrix, and (soon) DeltaChat users all want consistent agent behavior.
- **Enterprise/team access control** — the Matrix fix (#3045) and LINE channel fixes suggest growing organizational use.

**Satisfaction Indicators:** No negative sentiment expressed in recent comments. The rapid closure of token-waste and Matrix identity bugs suggests maintainers are responsive to reported breaks.

## Backlog Watch

**High Priority, Unresolved:**
- **#3088** — *Use vodozemac instead of libolm* — Open for 17 days. Marked `priority: high` and `help wanted`. 2 user upvotes. No assignee. The libolm library is unmaintained; this is a growing security risk for all Matrix users.

**Stale PRs Requiring Attention:**
- **#3142** — *fix(spawn): clear ForUser in sub-turn ToolResult* — Open 9 days, marked `stale`. This fixes a duplicate-message delivery bug that affects Telegram/Web users with sub-agent tasks. Likely needs rebase or review.
- **#3092** (already closed today) — One less stale item after today's merges.

**Long-Open Feature PR:**
- **#3063** — *Add deltachat gateway* — Open 18 days. The contributor (trufae) has continued activity on the PR today, so it is alive but awaiting final maintainer review.

**Recommendation:** The maintainer team should prioritize #3088 (vodozemac) as a security blocker, and review #3142 to avoid continued duplicate-message issues in production deployments.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-26

## Today's Overview
The project saw high development activity with 16 pull requests updated in the last 24 hours, including 11 merged or closed, indicating a strong push toward stability and feature completion. Only one new issue was opened, focused on approval routing, while no new releases were cut. The velocity is above the project's typical 24-hour cadence, driven mainly by merges from multiple contributors addressing CLI, security, container, and authentication topics. Overall project health remains robust with a healthy mix of bug fixes, feature work, and skill additions.

## Releases
**No new releases** in the last 24 hours. The project has not published a new version in the past several weeks; users are running on the unreleased `main` branch for the latest features.

## Project Progress
**11 pull requests merged or closed today**, spanning several track:

**Approvals & Authorization:**
- [#2832](https://github.com/nanocoai/nanoclaw/pull/2832) — **Reject with reason** added to approval cards, allowing approvers to attach a one-line explanation relayed back to the agent instead of a plain "declined".
- [#2855](https://github.com/nanocoai/nanoclaw/pull/2855) — **Subscription-primary auth with API-key failover**: automatic fallback from OAuth to `ANTHROPIC_API_KEY` on subscription failure, with operator alerts.

**Container & Environment:**
- [#2856](https://github.com/nanocoai/nanoclaw/pull/2856) — **Per-container CPU/memory limits** introduced via `CONTAINER_CPU_LIMIT` and `CONTAINER_MEMORY_LIMIT` env vars, preventing resource monopolization on shared hosts.
- [#2854](https://github.com/nanocoai/nanoclaw/pull/2854) — **macOS TMPDIR fix** for OneCLI gateway CA bundle mounts, resolving self-signed certificate errors on Rancher Desktop.

**Stability & Security:**
- [#2817](https://github.com/nanocoai/nanoclaw/pull/2817) — **Stricter file-read confinement** in `send_file`, with realpath validation and symlink blocks outside `/workspace`.
- [#2815](https://github.com/nanocoai/nanoclaw/pull/2815) — **Guard against primitive JSON** in `safeParseContent`, treating arrays/primitives as raw text while maintaining engage-rule routing.
- [#2813](https://github.com/nanocoai/nanoclaw/pull/2813) — **Socket response cap by bytes** instead of character count, fixing multi-byte UTF-8 truncation edge cases.
- [#2830](https://github.com/nanocoai/nanoclaw/pull/2830) — **Dead peer registration cleanup**: launchd/systemd plists pointing at deleted binaries are now reaped automatically.

**Features & Skills:**
- [#2472](https://github.com/nanocoai/nanoclaw/pull/2472), [#2471](https://github.com/nanocoai/nanoclaw/pull/2471) — **Per-thread Slack sessions**: each top-level DM becomes its own session with in-thread bot replies; includes an adapter hook for per-thread threadId rewrites.
- [#2843](https://github.com/nanocoai/nanoclaw/pull/2843) — **`/learn` skill** — distills a reusable skill from any source (directory, URL, paste, conversation), added as a community contribution.

## Community Hot Topics
**No issues or PRs this period have accumulated significant comments or reactions.** The most substantive discussion-adjacent item is:

- [#2824 [OPEN]](https://github.com/nanocoai/nanoclaw/pull/2824) — **fix: drop stale "Global Memory" instruction from main seed prompt** — though no comments yet, this is a two-week-old open PR from a first-time contributor (`CutSnake01`) that touches core seeding behavior. The lack of maintainer response may indicate a bottleneck.

**Analysis:** The absence of back-and-forth on today's items suggests either the community is satisfied with the pace of fixes, or issues are being resolved before deep discussion forms. The approval-multi-admin issue (#2857) is the only discussion-ripe topic and may draw attention once more users encounter the single-admin bottleneck.

## Bugs & Stability
**No new bug reports** in the last 24 hours. Today's merges actively addressed several stability issues:

| Severity | Issue | Fix PR | Status | Notes |
|----------|-------|--------|--------|-------|
| **High** | macOS container CA failure | [#2854](https://github.com/nanocoai/nanoclaw/pull/2854) | Merged | Self-signed cert error on Rancher Desktop |
| **High** | File-read path traversal | [#2817](https://github.com/nanocoai/nanoclaw/pull/2817) | Merged | Stricter realpath validation |
| **Medium** | Socket response truncation with UTF-8 | [#2813](https://github.com/nanocoai/nanoclaw/pull/2813) | Merged | Byte-based cap replaces char-based |
| **Low** | JSON primitives causing routing failures | [#2815](https://github.com/nanocoai/nanoclaw/pull/2815) | Merged | Safe parsing for arrays/primitives |
| **Medium** | Dead peer registrations accumulating | [#2830](https://github.com/nanocoai/nanoclaw/pull/2830) | Merged | Auto-cleanup of orphaned plists |
| **High** | libsignal debug logging exposing key material | [#2860](https://github.com/nanocoai/nanoclaw/pull/2860) | Open | Pending merge |

All filed bugs have been addressed by today's merges, with the exception of the libsignal logging fix (#2860) which remains open.

## Feature Requests & Roadmap Signals
One feature request emerged today:

- [#2857](https://github.com/nanocoai/nanoclaw/issues/2857) — **Multi-admin approval with CLI fallback**: Requesting agents should be able to re-ask for approval from a different admin if the primary is unavailable, and operators with local machine access should be able to approve via terminal CLI.

**Predicted inclusion:** 50% chance in next release. The existing approval reject-with-reason PR (#2832) laid groundwork; extending to multi-admin is a natural next step that several contributors have touched.

Other roadmap-significant merges from today:
- Per-container CPU/memory limits (#2856) suggests growing multi-tenant deployment use.
- Subscription-primary auth (#2855) indicates enterprise reliability concerns.
- The `/learn` skill (#2843) reflects demand for self-documenting systems.

## User Feedback Summary
No direct user feedback was captured in issues or PR comments today. However, user pain points can be inferred from recent code changes:

- **Pain point: Single admin dependency** — repeatedly highlighted by the new multi-admin approval request (#2857), indicating operational friction in team deployments.
- **Pain point: Resource contention** — the container limits feature (#2856) suggests users are running multiple agents on single hosts and experiencing performance interference.
- **Pain point: Environment setup on macOS** — the TMPDIR fix (#2854) shows ongoing container workflow friction for Apple Silicon users.
- **Pain point: Noisy logs** — the libsignal debug log suppression (#2860) indicates annoyance with excessive logging exposing cryptographically sensitive data.

## Backlog Watch
Several items require maintainer attention:

1. **[#2824 — fix: drop stale "Global Memory" instruction](https://github.com/nanocoai/nanoclaw/pull/2824)** — Open since 2026-06-20 (6 days), no maintainer response. From first-time contributor `CutSnake01`. Risk of contributor churn if left unattended. **Status: needs review.**

2. **[#2795 — feat: add /add-clidash dashboard skill](https://github.com/nanocoai/nanoclaw/pull/2795)** — Open since 2026-06-17 (9 days), no maintainer response. A replacement PR (#2858) was opened today by a different contributor (`mksocial19-code`) incorporating requested fixes. The original author (`leetwito`) may feel superseded without communication.

3. **[#2860 — chore(logging): silence libsignal debug spam](https://github.com/nanocoai/nanoclaw/pull/2860)** — Opened today, fresh but exposes sensitive key material. Should be fast-tracked for security hygiene.

**Overall health assessment**: Green. High throughput, zero regressions introduced, security fixes landing promptly. Main risk is maintainer response latency to community contributions (items 1-2 in backlog watch). The 11 merges in 24 hours suggest a focused team clearing accumulated PR debt.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-26

## Today's Overview

IronClaw shows **very high activity** today with 50 issues and 50 PRs updated in the last 24 hours. The project is deep in a major **Reborn stack transformation** — 12+ related issues and PRs tackle capability policy, multi-user auth, and memory extension architecture simultaneously. The CI pipeline remains fragile (main is "persistently red"), but core contributors are shipping large features at pace (XL-sized PRs for trace commons, memory extension, and event-log batching). Three distinct workstreams dominate: the **capability policy epic** (#5261, 6+ sub-issues), **memory/self-learning system** (#5260, #5264), and **infrastructure reliability** (CAS migration, heartbeat batching, event-log write-behind). No new releases.

## Releases

*None — no new releases published in the tracking period.*

## Project Progress

**24 PRs were merged or closed** in the last 24 hours. Key advances:

- **Memory extension architecture (implements #3537)** — PR #5205 (XL, merged) ships Extension Manifest v2, source-aware trust, host-defined capability profiles, memory binding policy, and always-on native document-store provider. This is the foundation for Reborn's personal memory system.

- **PR #4997 (merged)** — Adds binary document extraction seam for PDF/PPTX/DOCX/XLSX files via `download_file`, enabling agents to read non-UTF-8 files from Google Drive.

- **PR #5222 (merged)** — Fixes triggered-run Slack delivery failures where runs parked in `BlockedApproval`/`BlockedAuth` were incorrectly marked as `Failed`.

- **PR #5255 (merged)** — 3→1 DB round-trip reduction for CAS `put` operations by folding directory pre-check into single statement.

- **PR #5278 (closed)** — Fixes WebUI v2 Logs page scrollability.

- **PR #5281 (open, unblocking main)** — Comprehensive CI fix addressing libsql feature flag, apt retry, fail-fast strategy, and `.codegraph` configuration.

## Community Hot Topics

1. **#5261 — [EPIC] Reborn capability policy: admin-shared tools & skills with per-user auth** (0 comments, but 6+ child issues created today)
   - *What it is:* Epic tracking the entire admin→user capability grant pipeline on the Reborn stack. Sub-issues cover REST surface (#5268), availability resolver (#5267), delta store + policy enforcement (#5273), multi-user auth (#5272), and DB-backed user roles (#5266).
   - *Underlying need:* Enterprise deployment viability — a company needs one host where admins control which capabilities (tools, skills) are available to which users.

2. **#5119 — IronClaw Reborn Local Dogfooding Findings 06/22-06/28** (1 comment, tracking issue)
   - *What it is:* Master tracker for UX/onboarding issues found by core contributors dogfooding the Reborn WebUI locally. Generated multiple closed issues today (#5210, #5211, #5208, #5212).
   - *Underlying need:* The team is aggressively polishing the Reborn WebUI before wider release.

3. **#5173 / #5220 — Daily failure taxonomies** (deepseek-v4-flash benchmarks)
   - *What they are:* Systematic analysis of benchmark suite failures showing infrastructure defects dominate over model quality issues.
   - *Underlying need:* Confidence in benchmark signal — distinguishing true model regressions from test harness flakiness.

## Bugs & Stability

**High severity:**
- **#5276 — Scheduled automation fails with "No thread attached"** (OPEN, 0% success rate). The Daily PR Digest automation creates run records but never links them to conversation threads, producing no output. This is a core automation infrastructure bug.

**Medium severity:**
- **#5192 — Denying a tool approval can still lead to additional approval requests** (OPEN). The approval deny path has a race/state issue where subsequent tool calls still prompt approval.
- **#5196 — "Ask each time" tool permission fails with authorization error, triggers duplicate approval flow** (OPEN). Approval succeeds but tool execution fails, then assistant re-requests authorization.
- **#5210 — Sending new message while approval gate is open causes repeated warnings and lost message state** (CLOSED, fixed). This was a confirmed UX-breaking race condition.
- **#5229 — Durable capability display previews use runtime owner scope in WebUI runs** (CLOSED, fixed). Railway production logs showed `unknown thread` errors for capability previews.

**Fix PRs in progress:**
- **#5250** — Classifying run-wait states to prevent forever-hangs and gate-parked-run kills (OPEN)
- **#5234** — Removing per-record lock convoys via shared CAS helper (OPEN)
- **#5253** — Moving runner-lease renewal off synchronous Postgres path (OPEN)

## Feature Requests & Roadmap Signals

Strong signals point to **Reborn becoming enterprise-ready** in the next 2-3 releases:

1. **Multi-user admin capability policy** (#5261 epic) — Predict next release will include the four-dimension policy system (configuration, identity, approval, availability) with REST admin surface. Likely version: `0.12.0` or similar feature bump.

2. **Personal memory & self-learning** (#5260 tracking, #5264 follow-ups) — The memory extension PR (#5205) just merged, so follow-ups for SQL storage-port, host-managed flow, semantic search, and default flip will land in subsequent releases.

3. **Write-behind/batching for infrastructure** — PR #5257 (event-log batching), #5253 (heartbeat lease write-behind), #5274 (runner-lease CAS loops) all target reducing synchronous Postgres pressure. This suggests an upcoming "Reborn performance optimization" release.

4. **Global auto-approve discoverability** — PR #5247 adds a navigation link from the approval card to global settings, responding to user confusion about where to manage persistent permissions.

## User Feedback Summary

**Pain points (from dogfooding issues):**
- Approval flow confusion: users don't know where global auto-approve settings are (#5246, #5243)
- Frozen message input while waiting for agent responses (#5208) — *fixed today*
- No auto-scroll for new responses (#5211) — *fixed today*
- Internal skill/debug messages leak into chat UI (#5191) — *open*
- Message timestamps missing after response completes (#5212) — *fixed today*
- "Always approve" not persisting for `outbound_delivery_target_set` (#5129) — *closed, but root cause unclear*
- Operators-only tools error when regular user opens Settings > Tools (#5242) — *closed*

**Satisfaction signals:**
- Core team is actively dogfooding and fixing UX issues within 24-48 hours (multiple "closed" items from 2026-06-25 fixed today)
- The memory extension architecture (#3537) merged after long development — suggests user demand for persistent agent memory

## Backlog Watch

**Open issues needing attention:**
- **#5274 — Migrate runner-lease sidecar CAS loops onto shared `cas_update`** (OPEN, 0 comments, created yesterday). This is a direct follow-up to the CAS migration PR (#5234) — likely blocked on that PR merging.
- **#5264 — Memory #3537 follow-ups** (OPEN, 0 comments). Since the main PR just merged, these follow-ups need prioritization.
- **#5219 — Harden activity identity invariants after gate lifecycle refactor** (OPEN, 1 comment). Follow-up to PR #5145 — future batching or direct block paths could silently lose activity identity.
- **#4980 — Automations empty state does not explain how to create automations** (CLOSED but worth watching). This was fixed but the underlying onboarding gap remains — automations are created via chat with no UI affordance.

**PRs needing review:**
- **#5279 — Fix Reborn queued message steering** (OPEN, XL, core contributor) — addresses queued message UI behavior
- **#5280 — Trace Commons: instance-wide enrollment** (OPEN, risk: high, DB migration) — significant scoping change requiring careful review
- **#5244 — Remove generated WebUI v2 dist from source control** (OPEN, XL) — build system change affecting all contributors

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the **LobsterAI Project Digest** for **June 26, 2026**.

---

## LobsterAI Project Digest – 2026-06-26

### 1. Today's Overview
Project activity spiked significantly today, driven by a major **bug-fixing and stabilization sprint**. Nine Pull Requests were merged/closed in the last 24 hours, all originating from the same day, indicating a high-velocity engineering push. While no new releases were cut, the codebase saw deep fixes across the OpenClaw extension system, the Cowork plan-mode feature, and the Settings UI. The lone open issue remains a stale (2-month old) UI bug regarding task toggles, suggesting that while core architecture is receiving intense attention, some frontend QoL issues linger.

### 2. Releases
**No new releases today.**

There are no release notes or version bumps to report for this date.

### 3. Project Progress (Merged/Closed PRs Today)
Today’s work focused heavily on the **OpenClaw plugin framework** and the **Cowork multi-agent** experience. Key advancements include:

- **OpenClaw Extension & Plugin Stability:**
    - **PR #2203** ([link](https://github.com/netease-youdao/LobsterAI/pull/2203)): Fixed the packaging pipeline to correctly precompile local extension entries (TypeScript) to `index.js`, ensuring local "ask-user" and media extensions load properly.
    - **PR #2202** ([link](https://github.com/netease-youdao/LobsterAI/pull/2202)): Hardened the plugin allowlist to ensure the critical "browser" plugin remains enabled even under restrictive security configurations.
    - **PR #2201** ([link](https://github.com/netease-youdao/LobsterAI/pull/2201)): Eliminated duplicate replies in multi-agent sessions during final history sync (`sessions_yield`).
    - **PR #2198** ([link](https://github.com/netease-youdao/LobsterAI/pull/2198)): Pre-installed QQ and Discord plugins for OpenClaw, fixing environment variable indexing for channel accounts.

- **Cowork (Plan Mode) Refinements:**
    - **PR #2204** ([link](https://github.com/netease-youdao/LobsterAI/pull/2204)): Fixed a rendering bug where plan tags were leaking into chat messages; the system now prefers block-level tags.
    - **PR #2200** ([link](https://github.com/netease-youdao/LobsterAI/pull/2200)): Fixed duplicate plan messages caused by stream jitter (snapshot length regression).
    - **PR #2199** ([link](https://github.com/netease-youdao/LobsterAI/pull/2199)): Ensured the UI continues polling for sub-agent results even after the parent session terminates.

- **Settings & UI:**
    - **PR #2206** ([link](https://github.com/netease-youdao/LobsterAI/pull/2206)): Fixed a discrepancy where the "Launch at Login" toggle state was not synced with the actual OS configuration (includes Windows cleanup).
    - **PR #2205** ([link](https://github.com/netease-youdao/LobsterAI/pull/2205)): Updated the plan mode icon to a theme-aware SVG component.

### 4. Community Hot Topics
The community issue tracker is quiet today. The only recently updated issue is a persistent, low-engagement bug:

- **[#1392] Scheduled Task Toggle Unresponsive** ([link](https://github.com/netease-youdao/LobsterAI/issues/1392))
    - **Activity:** 1 comment, stale (updated after 2 months).
    - **Analysis:** While large-scale architectural fixes are the team's focus, this user-reported UI bug persists. The user reports that a scheduled task switch cannot be turned off after running, though most other toggles work. The silent treatment of this issue may suggest the team is waiting for a broader UI/state refactor or lacks reproduction data.

### 5. Bugs & Stability
Today’s digest is dominated by **proactive stability fixes**. No new bugs were opened by the community directly, but the engineering team closed 6 bug-fix related PRs. Ranked by severity:

1.  **High: Data Integrity (Duplicate Messages)**
    - **Fix:** PR #2201 & #2200 addressed duplicate messages in agent sessions and plan mode. These were likely causing user confusion and wasted token usage.
2.  **Medium: Feature Breakage (Plugin/Toggle mismatch)**
    - **Fix:** PR #2202 (browser plugin missing) and PR #2206 (auto-launch state mismatch) fixed bugs where expected OS/plugin behavior was not reflected in the app state.
3.  **Low: Presentation Bugs**
    - **Fix:** PR #2204 (leaking tags) and PR #2205 (icon swap).

### 6. Feature Requests & Roadmap Signals
There are no explicit feature requests active in the issue tracker today. However, the aggressive expansion of the **OpenClaw plugin system** (PR #2198, #2202, #2203) signals a clear roadmap direction:

- **Prediction for next version:** Deeper integration with third-party communication channels (beyond just QQ/Discord). The fixes for precompiling extensions (PR #2203) suggest the team is preparing for a stable "Extensions API" release to power a plugin marketplace or local development tools.

### 7. User Feedback Summary
- **Pain Points:**
    - **UI Responsiveness:** The stale issue #1392 (toggle switch unresponsiveness) represents a persistent pain point for power users managing automation schedules.
    - **Plugin Reliability:** The volume of OpenClaw fixes today suggests users on the bleeding edge are likely hitting broken plugin allowlists and extension loading errors.
- **Use Cases:**
    - Multi-agent (Cowork) plan-mode users are the primary beneficiaries of today’s fixes, specifically regarding message duplication and rendering clarity.
    - Windows users benefit from the launch-at-login sync fix.
- **Satisfaction:** Likely improved by the end of the day as the 9 merged PRs clean up high-visibility bugs.

### 8. Backlog Watch
This section flags issues/PRs that risk becoming stale or blocking users.

- **Issue #1392** ([link](https://github.com/netease-youdao/LobsterAI/issues/1392))
    - **Status:** OPEN, 83 days old. Last updated due to a stale bot bump.
    - **Risk:** This is a **high-risk backlog item**. It demonstrates a non-functional UI toggle for a core feature (scheduling). If this behavior is reproducible on multiple OSes, it indicates a fundamental state-management bug in the renderer that has been ignored for nearly 3 months. **This requires maintainer attention to either reproduce, fix, or request logs from the user.**

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is your CoPaw project digest for **June 26, 2026**.

---

# CoPaw Project Digest — 2026-06-26

## Today's Overview
The CoPaw project is experiencing **high activity**, with 50 Pull Requests and 27 Issues updated in the last 24 hours. The community is heavily focused on stabilizing the project following the **AgentScope 2.0 migration**, with several critical regressions related to browser automation, context management, and model provider compatibility being actively addressed. While no new releases were published today, the merge rate (22 PRs closed/merged) indicates strong momentum toward a more stable baseline. Developer velocity is high, particularly around first-time contributors submitting targeted bug fixes for recent regressions.

## Releases
No new releases were published in the last 24 hours. The latest available version remains **v1.1.12.post2**.

## Project Progress
The following significant Pull Requests were merged or advanced today, primarily focusing on infrastructure stability and feature parity post-migration:

- **[PR #5542]** (Open) **test(e2e): adapt for agentscope 2.0** — Drops "Plan Mode" and fixes selectors and fixtures to restore CI stability after the upstream migration. Status: P0 regression suite now passing on fresh state.
- **[PR #5443]** (Merged) **fix(tui): restore ACP commands and inline approvals** — Re-enabled TUI slash commands (`/clear`, `/compact`, `/skills`, `/model`) that broke during the AgentScope 2.0 migration.
- **[PR #5471]** (Merged) **feat: generalize match pattern** — A backend refactor to improve pattern-matching logic across message routing.
- **[PR #5534]** (Merged) **refactor(readme): add trending badge** — Documentation enhancement for the main repository page.
- **[PR #5540]** (Open) **feat(memory): refactor auto memory system** — Introduces turn-based tracking (replacing fragile reply IDs) to improve the reliability of memory persistence in long conversations.

## Community Hot Topics
The most active discussions reflect two core community needs: **provider compatibility** and **platform-specific stability**.

- **[Issue #5345]** *"Custom OpenAI-compatible providers (e.g. OMLX) don't support function calling"* (8 comments) — A user reports that manually adding OMLX (a valid OpenAI-compatible endpoint) results in tool calls being ignored, while Ollama works. This is a **high-impact usability gap** for users with non-standard backends. [Issue Link](https://github.com/agentscope-ai/QwenPaw/issues/5345)
- **[Issue #5379]** *"Internal Server Error on startup after pip install"* (6 comments, still open) — A critical installation failure on Windows. The error points to `get_remote_addr(transport)` in the logs. Community is actively debugging. [Issue Link](https://github.com/agentscope-ai/QwenPaw/issues/5379)
- **[PR #5321]** *"Scroll context manager — durable history + recall REPL"* (Under Review) — An ambitious new feature for retrieval-driven context management using SQLite. It addresses a long-standing complaint about context loss during compression. [PR Link](https://github.com/agentscope-ai/QwenPaw/pull/5321)
- **[Issue #5403]** *"Browser autofill hijacks search input in Model Configuration page"* (4 comments) — A UI/UX bug where saved passwords pop up in the model search field, indicating poor HTML semantics (e.g., missing `autocomplete="off"`). [Issue Link](https://github.com/agentscope-ai/QwenPaw/issues/5403)

## Bugs & Stability
Stability is the dominant theme today. Several regressions from the v1.1.12 release cycle are being addressed directly by community patches.

- **CRITICAL — [#5379]** *Internal Server Error on Windows startup.* No fix PR yet. **Impact:** Users cannot start the application. [Issue Link](https://github.com/agentscope-ai/QwenPaw/issues/5379)
- **HIGH — [#5520]** *browser_use stop() leaves Chrome renderer processes running (memory leak)*. **Fix PR exists:** [#5536](https://github.com/agentscope-ai/QwenPaw/pull/5536) submitted by a first-time contributor (`C1-BA-B1-F3`). This is a regression from earlier fix [#2733](https://github.com/agentscope-ai/QwenPaw/issues/2733).
- **HIGH — [#5505]** *MiniMax-M3 image moderation errors cached as `rejects_media=True`*. **Fix PR exists:** [#5535](https://github.com/agentscope-ai/QwenPaw/pull/5535). Cached false negatives strip images from subsequent requests.
- **HIGH — [#5480]** *Console long message formatting collapse (CSS layout bug)*. **Fix PR exists:** [#5538](https://github.com/agentscope-ai/QwenPaw/pull/5538). Markdown rendering fails on long streams until a tab switch.
- **MEDIUM — [#5479]** *Session files >500KB cause frontend crash.* Reported as a "render error" with no graceful handling. No fix PR yet. [Issue Link](https://github.com/agentscope-ai/QwenPaw/issues/5479)
- **MEDIUM — [#5162]** *Dialogue thinking enters infinite loop.* A severe logic failure in the reasoning loop, still under investigation with no fix PR. [Issue Link](https://github.com/agentscope-ai/QwenPaw/issues/5162)
- **MEDIUM — [#5541]** *Ollama cannot access cloud models.* Configuration of URL and API key yields no model list. [Issue Link](https://github.com/agentscope-ai/QwenPaw/issues/5541)
- **LOW — [#5528]** *Linux browser tool fails with IME-wrapped default browser*. **Fix PR exists:** [#5526](https://github.com/agentscope-ai/QwenPaw/pull/5526). Parser fails on `Exec=env ... chrome`.

## Feature Requests & Roadmap Signals
The community is vocal about improving **model flexibility** and **plugin ecosystem**:

- **[Issue #5527]** *"When will models support dynamic switching in AgentScope 2.0?"* — User wants automatic failover to a backup model when the primary is rate-limited or down. **Prediction:** Likely a high-priority roadmap item given the enterprise use-case overlap.
- **[Issue #5484]** *"Support installing plugins via pip from PyPI"* — Suggests standardizing plugin distribution to match the Python ecosystem (citing Hermes Agent as precedent). This could unify the currently fragmented ZIP-based installation process.
- **[Issue #5162]** *"Add delete button for a single turn in a conversation"* — Users want to remove a bad assistant response and retry without losing the full history. A quality-of-life feature that would reduce friction in iterative workflows.
- **[PR #5321]** *"Scroll context manager"* — If merged, this will be the most significant new feature in the next release, providing a durable history alternative to lossy compression.

## User Feedback Summary
- **Pain Point — Windows Stability:** The ongoing `Internal Server Error` (Issue #5379) and the `send_file_to_user` 404 on Windows (Issue #5508) are causing significant frustration for Windows-native users, who feel the platform is a second-class citizen.
- **Pain Point — Provider Parity:** The gap between "OpenAI-compatible" and "full OpenAI compatibility" (e.g., missing function calling, missing Responses API) is a recurring theme. Users feel forced into provider lock-in.
- **Satisfaction (Implied):** The rapid response from maintainers and community (multiple first-time-contributor PRs merged/accepted within 24 hours) suggests a healthy, responsive ecosystem.
- **Feature Request (Urgent):** The toggle for single-turn deletion (Issue #5503) and dynamic model switching (Issue #5527) are the most-requested upcoming features.

## Backlog Watch
Several critical items are showing long gaps in maintainer response while remaining high-impact:

- **[Issue #2733]** *"Chrome processes not properly closed after browser automation"* — This was previously marked closed (by PR #2843), but the regression (Issue #5520) proves the fix was incomplete. Maintainers should consider re-opening #2733 and revisiting the root cause at the Playwright lifecycle level.
- **[Issue #5342]** *"Hard cap on tool result size at execution layer"* — Open for 6 days, no maintainer response. This is a defense-in-depth proposal to prevent context explosion when LLM calls fail, which is a **systemic risk** for production deployments. A maintainer acknowledgment is needed.
- **[Issue #5162]** *"Dialogue thinking enters infinite loop"* — Open for 14 days with no confirmed fix. Given the severity (application hangs), this should be prioritized for triage.
- **[PR #4622]** *"DataPaw data-analysis plugin"* — Under review since May 22, 2026 (34 days). This is a large, high-value plugin. Maintainers should provide a timeline for review or merge to avoid community demotivation. [PR Link](https://github.com/agentscope-ai/QwenPaw/pull/4622)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-26

## Today's Overview

ZeroClaw is in an **intense development cycle** with 47 issues updated and 50 pull requests touched in the last 24 hours, reflecting a highly active project pushing toward multiple concurrent milestones. The project maintains **34 open/active issues** alongside **49 open PRs**, with only 13 issues closed and 1 PR merged — indicating a sustained build-up of work-in-progress rather than a release crunch. Two major tracker issues frame the current focus: **v0.8.2 release-support** ([#8181](https://github.com/zeroclaw-labs/zeroclaw/issues/8181)) and the longer-term **v0.9.0 auth/security/breaking-change queue** ([#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432)), with the WASM-first plugin runtime RFC ([#8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135)) and supply-chain signing proposal ([#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177)) signaling major architectural shifts ahead. No new releases were published today.

## Releases

None in the last 24 hours. The most recent release is **v0.8.1**, with the v0.8.2 release preparation underway via PR [#8234](https://github.com/zeroclaw-labs/zeroclaw/pull/8234) (bump to v0.8.2 + changelog).

## Project Progress

Only **1 PR was merged/closed** today, but it was a critical stability fix:
- **[#8218](https://github.com/zeroclaw-labs/zeroclaw/pull/8218)** (merged) — **fix(agent/history): saturate tool-result trim accounting to avoid underflow panic** — a high-severity runtime crash fix where `fast_trim_tool_results` could overflow when tool message re-serialization produced longer strings than originals.

## Community Hot Topics

The most active discussions reflect the community's deep technical engagement with security, delegation patterns, and platform architecture:

1. **[#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) — RFC: Work Lanes, Board Automation, and Label Cleanup** (11 comments) — A governance RFC accepted and rolling out in v0.8.x to automate issue triage routing without manual overhead. This is a meta-process issue, indicating the project is maturing its contribution workflow.

2. **[#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177) — RFC: Supply chain signing** (8 comments) — Hardware-backed PGP, hermetic builds, and SLSA provenance for container images and release binaries. Community consensus is forming around the StageX model. Blocked, waiting for maintainer review.

3. **[#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165) — RFC: Prefer a lighter ZeroClaw core through external integrations** (5 comments) — Persistent interest in removing built-in tool code (gws-cli, Jira, GitHub) in favor of skill-based integration. Blocked but accepted.

4. **[#8238](https://github.com/zeroclaw-labs/zeroclaw/issues/8238) — Add independent delegate mode for specialist handoffs** (4 comments) — Follows from prior delegation RFCs; the community wants specialist agents running under their own policy and toolset, not just the caller's.

5. **[#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903) — MCP stdio child process leak** (4 comments) — A persistent daemon-level bug where MCP child processes accumulate (~48 orphans/day). No-stale status indicating long-standing user pain.

**Underlying needs:** The community is pushing for three things simultaneously: (a) **stronger security posture** (supply chain signing, capability-gated delegation, Wasm sandboxing), (b) **modular architecture** (light core, skill-based integrations, OCI plugin registries), and (c) **operational excellence** (process leak fixes, proper observability, release automation).

## Bugs & Stability

**Critical/Severity S0 (data loss / security):**
- **[#8279](https://github.com/zeroclaw-labs/zeroclaw/issues/8279) — delegate bypasses parent's tool allowlist** (closed/merged) — Sub-agents can invoke tools the parent policy excludes. **Fix: PR [#7590](https://github.com/zeroclaw-labs/zeroclaw/pull/7590) implementation is incomplete; RFC [#7743](https://github.com/zeroclaw-labs/zeroclaw/issues/7743) is the open response.**

**High Risk:**
- **[#8327](https://github.com/zeroclaw-labs/zeroclaw/issues/8327) — Native tool calling sends `[IMAGE:data:...]` as plain text** — Inflates token count with base64 data for OpenAI-compatible providers (e.g., llama.cpp). **Fix: PR [#8339](https://github.com/zeroclaw-labs/zeroclaw/pull/8339) opened today** to promote markers to `image_url` parts.
- **[#8312](https://github.com/zeroclaw-labs/zeroclaw/issues/8312) — fill-translations leak-repair leaves stale entries** — Silent data-loss path for translation text that survives prior fix. No fix PR yet.
- **[#8181](https://github.com/zeroclaw-labs/zeroclaw/issues/8181) tracker** captures 37 open items for v0.8.2 support, including runtime, security, and config fixes.

**Medium Risk:**
- **[#8154](https://github.com/zeroclaw-labs/zeroclaw/issues/8154) — Kimi Code dead endpoint** (closed) — Provider endpoint regression fixed.
- **[#8236](https://github.com/zeroclaw-labs/zeroclaw/issues/8236) — voice_wake.rs missing `subject` field** — Breaks `--all-features` build. Fix: awaiting PR.

**New Today (2026-06-26):**
- **[#8327](https://github.com/zeroclaw-labs/zeroclaw/issues/8327) — IMAGE markers as plain text** (opened today) — with fix PR [#8339](https://github.com/zeroclaw-labs/zeroclaw/pull/8339) submitted same day.
- **[#8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334) — `skills install/list/remove` targets wrong data_dir** — Skills CLI broken for multi-agent setups. **Fix: PR [#8335](https://github.com/zeroclaw-labs/zeroclaw/pull/8335) opened today.**

## Feature Requests & Roadmap Signals

**Likely for v0.8.2 (imminent):**
- [In-app upgrade with supervised restart from web dashboard](https://github.com/zeroclaw-labs/zeroclaw/issues/8170) — PR [#8173](https://github.com/zeroclaw-labs/zeroclaw/pull/8173) is open, implementing the full detect→release notes→apply→restart flow.
- [OpenRouter model fallbacks array](https://github.com/zeroclaw-labs/zeroclaw/issues/8138) — Small config addition to support auto-failover.
- [LAN peer discovery via mDNS](https://github.com/zeroclaw-labs/zeroclaw/pull/8325) — Default-off `[nodes.mdns]` config block.

**Likely for v0.8.3 / v0.9.0 (next quarter):**
- **WASM-first plugin runtime** ([#8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135)) — Making Wasm the default plugin runtime with capability enforcement and signed distribution. This is a major architectural change.
- **Goal mode for bounded autonomous sessions** ([#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)) — First-class mode for pursuing user objectives until completion/budget exhaustion. Accepted RFC.
- **SkillForge wiring** ([#8309](https://github.com/zeroclaw-labs/zeroclaw/issues/8309)) — Orphaned auto-discovery engine from Feb 2026; maintainers must decide to wire or remove.
- **Replace React/Vite web UI with Rust→Wasm framework** ([#8132](https://github.com/zeroclaw-labs/zeroclaw/issues/8132)) — Dioxus/Leptos/Yew replacement, eliminating Node.js from build/runtime.

**Long-signal items:**
- [OCI-Compliant registries for WASM plugins](https://github.com/zeroclaw-labs/zeroclaw/issues/7497) — Replace JSON index with OCI container registries for storage/discovery.
- [Capability-gated WASI hardware host functions](https://github.com/zeroclaw-labs/zeroclaw/issues/8187) — GPIO, SPI, I2C access for plugins.

## User Feedback Summary

**Pain points expressed through issues and comments:**
- **MCP child process leaks** ([#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903)) — Daemon accumulates ~48 orphan MCP processes per day. Long-standing (since April), no-stale status suggests users are living with this bug.
- **Telegram multi-image fragmentation** ([#5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514)) — Each image sent in a media group triggers a separate agent request, causing duplicate outputs. Users want consolidated handling.
- **Skills CLI broken for multi-agent** ([#8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334)) — Users cannot install/list/remove skills in multi-agent deployments. Fix PR submitted same day.
- **Skill audit false-positive for markdown links** ([#6714](https://github.com/zeroclaw-labs/zeroclaw/issues/6714), closed) — Real marketplace skills failed audit for citing legitimate docs URLs ending in `.md`. Users appreciate the removal of this check.
- **Kimi Code endpoint dead** ([#8154](https://github.com/zeroclaw-labs/zeroclaw/issues/8154), closed) — Provider regression blocked Kimi K2.6 model users until community identified correct URL.

**Positive signals:**
- The [before_llm_call hook RFC](https://github.com/zeroclaw-labs/zeroclaw/pull/7846) is being wired into the agent loop, addressing developer requests for LLM call interception.
- The [rotating log-persistence mode](https://github.com/zeroclaw-labs/zeroclaw/pull/8307) adds operators' requested archive control between rolling and full persistence.
- Thanks/upvote reactions on [#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) (goal mode) and [#8132](https://github.com/zeroclaw-labs/zeroclaw/issues/8132) (Rust→Wasm web UI) indicate strong community alignment with the architectural direction.

## Backlog Watch

**Items needing maintainer attention (blocked or awaiting review):**

1. **[#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177) — Supply chain signing RFC** (needs-maintainer-review, blocked) — Major security proposal without maintainer response since June 22.

2. **[#8135](https://github.com/zeroclaw-labs/zeroclaw/issues/8135) — Wasm-first plugin runtime RFC** (needs-maintainer-review, blocked) — Foundational architectural RFC; all plugin work depends on direction here.

3. **[#8309](https://github.com/zeroclaw-labs/zeroclaw/issues/8309) — SkillForge orphaned** (needs-maintainer-review, blocked) — Tool from February 2026 neither wired nor removed; maintainers need to make a decision.

4. **[#8138](https://github.com/zeroclaw-labs/zeroclaw/issues/8138) — OpenRouter fallbacks** (needs-maintainer-review) — Small config addition, 2 comments, no maintainer engagement since June 22.

5. **[#7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497) — OCI registries for plugins** (needs-maintainer-review) — Plugin discovery mechanism design, no maintainer response since June 11.

6. **[#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165) — Lighter core via external integrations** (blocked, accepted) — Accepted design direction but blocked on implementation; last activity from April.

**Project health signals:** The 50 open PRs vs 1 merged today suggests a **bottleneck in review velocity**. Several high-impact PRs (Wasm runtime, in-app upgrade, observability improvements) are stalled despite having code. The `needs-maintainer-review` tag on 5+ items with no response in 4+ days indicates maintainer bandwidth is the current rate-limiter for the project's progress.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*