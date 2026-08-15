# OpenClaw Ecosystem Digest 2026-08-15

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-15 00:30 UTC

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

# OpenClaw Project Digest — 2026-08-15

## 1. Today's Overview

OpenClaw is experiencing high sustained activity with 500 issues and 500 PRs updated in the last 24 hours, indicating a healthy and active development ecosystem. Issue volume is dominated by open/active items (489), with only 11 closed, while PRs show a stronger closure rate (95 closed/merged vs 405 open). There are no new releases today, and the project continues to process a substantial backlog of P0/P1 priority bugs, particularly around memory leaks, message loss, and session-state integrity. The maintainer team appears engaged with a steady stream of ClawSweeper-labeled PRs and maintainer review cycles, though several critical issues remain open for extended periods. Notably, a significant cluster of issues relates to Codex integration instability, memory growth, and silent message-delivery failures across multiple channels.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

The project saw 95 PRs merged or closed today, with notable completed work including:

- **#123895** — `refactor(gateway): consolidate pairing completion tests` (steipete) — cleanup/consolidation of pairing completion test coverage.
- **#123863** — `fix(memory): report truthful index outcomes for empty workspaces` (steipete) — fixes misleading "Memory index updated" message when no files exist.
- **#120981** — `fix(sessions): preserve transcript ownership after key canonicalization` (`thostr1`) — addresses stale transport-specific session keys after canonicalization.
- **#116489** — `feat(security): require acknowledgement for install policy warnings` (jesse-merhi) — this **closed** PR adds a critical security flow where external `security.installPolicy` commands can return `warn`, requiring interactive CLI confirmation before plugin/skill installs.

Active PRs advancing key areas include:

- **#123899** (IWhatsskill) — `fix(session-catalog): preserve explicit agent ownership across UI and CLI`
- **#123276** (jesse-merhi) — `Start new sessions with folder group defaults`
- **#123703** (clawsweeper) — `fix(tui): deduplicate session identity` (AI-assisted)
- **#123901** (steipete) — `fix(workers): bound Gateway bundle cache growth` — directly addresses cache growth concerns.
- **#120900** (jesse-merhi) — `feat(ui): review install policy warnings` — UI counterpart to the closed runtime security feature.

The breadth of PRs suggests work is progressing on session-catalog integrity, UI polish, security policy enforcement, and infrastructure reliability (cache bounding).

## 4. Community Hot Topics

The most active discussions highlight deep user engagement with complex, production-impacting issues:

1. **#121058** — *Silent reply failures still recurring after #116277 closed* (94 comments, 0 reactions) — [Issue Link](https://github.com/openclaw/openclaw/issues/121058) — This is the hottest topic, with massive community engagement around a recurring silent reply failure. The original fix (#116277) didn't resolve the problem, and monitoring continues to log new occurrences. This clearly indicates an unresolved root cause that is causing significant production pain.

2. **#91588** — *Critical: Gateway Memory Leak* (24 comments, 1 reaction) — [Issue Link](https://github.com/openclaw/openclaw/issues/91588) — P0 memory leak growing from 350MB RSS to 15.5GB over 2-3 days, causing repeated OOM crashes and `launchd-handoff` restart cycles. Tagged with `clawsweeper:needs-maintainer-review` and `needs-live-repro`, indicating maintainer engagement is pending.

3. **#91009** — *Codex PreToolUse native hook relay spawns CPU-bound processes* (20 comments, 2 reactions) — [Issue Link](https://github.com/openclaw/openclaw/issues/91009) — P1: Codex integration spawns multiple CPU-hogging `openclaw-hooks` processes, stalling gateway RPC. Needs maintainer review and product decision.

4. **#48003** — *Steer mode does not inject messages mid-turn* (19 comments, 4 reactions) — [Issue Link](https://github.com/openclaw/openclaw/issues/48003) — P1: `messages.queue.mode: "steer"` fails to inject user messages mid-turn; root cause traced to `KeyedAsyncQueue` introduction in commit `9889c6da5`.

5. **#121953** — *Cron agent turns stall on DeepSeek* (19 comments) — [Issue Link](https://github.com/openclaw/openclaw/issues/121953) — P1: Cron turns stall because OpenClaw's `[cron:...]` user-message prefix is deprioritized by DeepSeek's API. A provider-specific incompatibility.

**Analysis**: The underlying need across these hot topics is **production reliability**. Users are running OpenClaw in production and suffering from message loss, OOM crashes, and provider-specific incompatibilities. The community is heavily engaged on the silent-reply failure issue (#121058) with almost 100 comments, suggesting it's the most impactful user-facing problem right now.

## 5. Bugs & Stability

The following bugs were reported or updated today, ranked by severity:

| Severity | Issue | Problem | Fix PR? |
|----------|-------|---------|---------|
| **P0** | [#91588](https://github.com/openclaw/openclaw/issues/91588) | Gateway RSS grows to 15.5GB causing OOM crashes and crash-loop | Needs maintainer review/live repro |
| **P0** | [#48920](https://github.com/openclaw/openclaw/issues/48920) | Live docs ahead of release — `IsolatedSessions` documented but not in 2026.3.13 | Needs product decision |
| **P0** | [#119270](https://github.com/openclaw/openclaw/issues/119270) | File tools strip leading `@` from destination paths, writing/deleting wrong files (data-loss) | Needs maintainer review |
| **P1** | [#121058](https://github.com/openclaw/openclaw/issues/121058) | Silent reply failures recurring — no queued reply payload (94 comments) | Original fix (#116277) ineffective |
| **P1** | [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex PreToolUse hook spawns CPU-bound processes stalling RPC | Needs maintainer review |
| **P1** | [#48003](https://github.com/openclaw/openclaw/issues/48003) | Steer mode message injection broken | Linked PR open (#123594 – not listed) |
| **P1** | [#123073](https://github.com/openclaw/openclaw/issues/123073) | `openclaw update` fails on dev channel — `EUNSUPPORTEDPROTOCOL` for `workspace:` deps (pnpm vs npm) | No fix PR yet |
| **P1** | [#122618](https://github.com/openclaw/openclaw/issues/122618) | Compaction safeguard oversized suffix evicts summary body, losing headings | Fix shape clear, queueable |
| **P1** | [#123799](https://github.com/openclaw/openclaw/issues/123799) | Production affected by Codex compact 404 on 2026.5.12 — needs upgrade guidance | Needs info |

**Critical trend**: A cluster of P0/P1 issues remain open with *no new fix PRs* (tagged `clawsweeper:no-new-fix-pr`), including the gateway memory leak, the file-tool `@` stripping data-loss bug, and the silent reply failures. There is strong evidence of **stability regression** across multiple channels (WhatsApp, LINE, Telegram, Feishu, Matrix) with silent message loss being a recurring theme.

## 6. Feature Requests & Roadmap Signals

Strong signals for upcoming versions based on active feature requests and PRs:

1. **Dynamic Model Discovery (#10687)** — [Issue Link](https://github.com/openclaw/openclaw/issues/10687) — Users need dynamic model catalogs for OpenRouter and fast-moving providers. Active discussion (10 comments), P2, tagged with maintainer review. This is a strong roadmap candidate for the next minor release.

2. **Agent-Triggered Context Compaction (#6757)** — [Issue Link](https://github.com/openclaw/openclaw/issues/6757) — Agents want self-compact capability. P2, 8 comments, enhanced by recent compaction-related PRs. The concurrent work on compaction safeguards (#123737) suggests this area is on the roadmap.

3. **Per-Model Usage Logging (#13219)** — [Issue Link](https://github.com/openclaw/openclaw/issues/13219) — Cost tracking and model-mix optimization. P2, 8 comments. A practical feature likely to be picked up soon given user demand for financial visibility.

4. **Configurable Upload Size Limit (#71142)** — [Issue Link](https://github.com/openclaw/openclaw/issues/71142) — Hardcoded 5MB upload limit in Control UI is too restrictive. P2, 8 comments. Small scope suggests easy implementation.

5. **Production-Readiness Labels (#73537)** — [Issue Link](https://github.com/openclaw/openclaw/issues/73537) — Users want release stability labels (e.g., "production-ready"). P2, 8 comments. Signals a community desire for more formal release management.

**Prediction**: The next release may include **install policy security warnings** (#116489, closed PR) and **UI polish for session management** (#123276), with a strong push to address the **memory leak and message reliability** issues as they are blocking production adoption.

## 7. User Feedback Summary

Real user pain points expressed today:

- **Message Reliability**: "The sender receives no response in the LINE app, and the OpenClaw agent has no visibility into the failure" (#86012). Multiple channel-specific silent message loss reports (WhatsApp #50093, #92186; LINE #86012; Feishu #54409) — this is the **#1 user concern**.
- **Memory / Crash-Loop**: "The gateway process suffers from a severe memory leak... eventually causing the process to be killed by the OS OOM killer" (#91588). Users are experiencing repeated crashes and restarts in production.
- **Codex Integration Instability**: "Codex app-server client closes mid-turn during image/tool requests" (#86214), "runaway response.create input growth" (#84662), "CPU-bound openclaw-hooks processes" (#91009). The Codex integration is a source of significant instability.
- **Session-State Corruption**: Multiple issues (#47975, #48003, #122618) report subagent session persistence, missing message injection, and compaction destroying structured summaries.
- **Documentation/Reality Gap**: "Heartbeat IsolatedSessions is in the live docs but not in the latest version" (#48920) and the `SecretRef provider: "default"` implicit alias (#121083) are causing user confusion and configuration errors.

**Satisfaction**: Users are clearly invested in OpenClaw (some mention running it for family/business and daily workflows), but production reliability issues are testing that goodwill.

## 8. Backlog Watch

Long-unanswered or neglected items requiring maintainer attention:

1. **#91588 (P0, 2026-06-09)** — [Issue Link](https://github.com/openclaw/openclaw/issues/91588) — *Critical Gateway Memory Leak*. Over 2 months old, P0, 24 comments, still needs maintainer review and live repro. This should be an immediate priority.

2. **#91009 (P1, 2026-06-06)** — [Issue Link](https://github.com/openclaw/openclaw/issues/91009) — *Codex PreToolUse CPU-bound processes*. 2+ months old, 20 comments, still awaiting maintainer decision.

3. **#10687 (P2, 2026-02-06)** — [Issue Link](https://github.com/openclaw/openclaw/issues/10687) — *Dynamic Model Discovery*. 6+ months old, 10 comments, maintainer review pending. Long-standing feature need.

4. **#119270 (P0, 2026-08-04)** — [Issue Link](https://github.com/openclaw/openclaw/issues/119270) — *File tools strip leading `@` from destination paths* — silent wrong-file writes/deletes. P0 data-loss, labeled `clawsweeper:bulk-filed`, needs maintainer review.

5. **#50093 (P2, 2026-03-19)** — [Issue Link](https://github.com/openclaw/openclaw/issues/50093) — *WhatsApp backfill missed messages after reconnection*. 5 months old, 12 comments, still needs live repro and product decision.

6. **#123073 (P1, 2026-08-13)** — [Issue Link](https://github.com/openclaw/openclaw/issues/123073) — *`openclaw update` fails on dev channel* — This is recent, fix-shape clear, and queueable, yet no PR has been opened. High visibility (blocks updates for dev-channel users).

**Overall**: While activity is vigorous, the project health is **mixed**. The maintainer team is active, but critical P0 issues (memory leaks, data-loss) have been lingering for 1-2 months without resolution. The high volume of `clawsweeper:needs-maintainer-review` tags indicates a bottleneck in maintainer bandwidth. The project signals **strong adoption with concurrent production pain**, and the next release will be closely watched for stability improvements.

---

## Cross-Ecosystem Comparison

# AI Agent & Personal AI Assistant Ecosystem Report
**Date:** 2026-08-15

---

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is experiencing robust, production-driven growth. Across the twelve tracked projects, development activity is high (500+ issues and PRs updated daily in the largest project), but the dominant themes are **stability** and **production hardening**—not raw feature expansion. Users are deploying agents for family, business, and daily workflows, and are hitting real-world reliability issues: silent message failures, memory leaks leading to OOM crashes, and provider-specific incompatibilities. Security is also emerging as a core concern, with multiple projects (ZeroClaw, Hermes Agent, OpenClaw) actively working on shell policy and authentication RFCs. The ecosystem is clearly segmented by user persona—from the power-user generalist (OpenClaw) to specialized verticals (NanoBot's knowledge-graph focus, Moltis's communication hub, IronClaw's enterprise automation).

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release | Health Score* |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | None | ⚠️ High activity, critical P0s linger |
| **CoPaw** | 50 | 41 | 2.1.0 (prior) | ✅ High throughput, agile triage |
| **ZeroClaw** | 33 | 50 | None (v0.8.5 line) | ✅ Stabilization with RFC bottleneck |
| **LobsterAI** | 2 | 27 | **2026.8.14** (today) | ✅ Strong delivery, quiet issues |
| **IronClaw** | 25 | 46 | None (1.2.0 merged) | ✅ Pre-release hardening, rapid fixes |
| **NanoBot** | 3 | 22 | None | ✅ Responsive, conflict friction |
| **NanoClaw** | 0 | 11 | None | ✅ Stabilization phase |
| **PicoClaw** | 3 | 9 | None | ✅ Active, stale cleanup risk |
| **Hermes** | Active (filed) | 4 | None | ⚠️ Windows instability |
| **Moltis** | 0 | 1 | None | 🔵 Quiet, single PR critical |
| **NullClaw** | 0 | 1 | None | 🔵 Clean, mature, static |
| **TinyClaw / ZeptoClaw** | 0 | 0 | None | ⚫ Inactive |

***Health Score** is qualitative: ✅ = healthy velocity + responsiveness; ⚠️ = high velocity with unresolved criticals; 🔵 = stable but low signal; ⚫ = inactive.*

**Cluster Analysis:**
- **High-velocity & large-scale:** OpenClaw (500/500), CoPaw (50/41), ZeroClaw (33/50), IronClaw (25/46), LobsterAI (2/27)
- **Moderate-velocity & focused:** NanoBot (3/22), NanoClaw (0/11), PicoClaw (3/9), Hermes (active issues)
- **Low-velocity & quiet:** Moltis (0/1), NullClaw (0/1), TinyClaw/ZeptoClaw (0/0)

---

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Scale & dominance:** With 500 issues/PRs in 24h, OpenClaw's community and contributor base dwarf the rest of the ecosystem combined (LobsterAI #2 has 27 PRs). This creates a flywheel of rapid bug triage, feature breadth, and visibility.
- **Multi-channel maturity:** No other project matches OpenClaw's channel support (WhatsApp, LINE, Telegram, Feishu, Matrix). Peers specialize: PicoClaw has DingTalk/WeChat, ZeroClaw has Slack/Lark but does not match the breadth.
- **Reference implementer:** As the likely "original" project (other names like *Claw/NanoClaw/ZeptoClaw suggest forks/inspiration), OpenClaw is setting architectural patterns (session catalog, memory indexing, security `installPolicy` warnings) that others replicate.

**Technical approach differences:**
- OpenClaw is a **monolithic gateway** (single binary, multi-channel, session memory, TUI/CLI/UI). Peers are diverging: IronClaw (WASM-compiled, pluggable memory over MCP, unbound-turns architecture), NanoBot (Python, strict typing, WebUI-focused), CoPaw (ZeroMQ-ish agent architecture, skill lifecycle).
- OpenClaw uses **ClawSweeper** (AI-assisted PR labeling) to manage scale—a sophistication peers lack.

**Community size comparison:**
| Metric | OpenClaw | Next largest (CoPaw) |
|---|---|---|
| Issues updated/24h | 500 | 50 |
| PRs updated/24h | 500 | 41 |
| Closed/merged PRs/24h | 95 | 15 |
| P0/P1 critical issues | 7+ | 2 |

**Weakness risk:** OpenClaw's sheer scale is also its vulnerability. Its P0s (gateway memory leak, silent message loss) are 2+ months old, and `clawsweeper:needs-maintainer-review` is a bottleneck. The ecosystem is cheering for OpenClaw to fix its stability issues—if it fails, users may migrate to more predictable peers.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging across **multiple** projects, indicating market-wide needs:

| Area | OpenClaw | NanoBot | Hermes | ZeroClaw | IronClaw | CoPaw | Others |
|---|---|---|---|---|---|---|---|
| **Silent message loss / reliability** | ✅ P0 (#121058) | — | ✅ Voice failed | — | — | — | PicoClaw (#3269 hang) |
| **Memory leaks / OOM crashes** | ✅ P0 (#91588) | ✅ (session race #5271) | — | — | — | — | Moltis (persistence, #1190) |
| **Provider-specific incompatibilities** | ✅ DeepSeek (#121953) | ✅ Anthropic (#5391) | ✅ xAI TTS | ✅ Output-limit (#9421) | ✅ Telegram login (#7667) | ✅ MiniMax (#2303) | NanoClaw (Node/CPU) |
| **File-tool correctness / data loss** | ✅ `@` stripping (#119270) | — | ✅ read_file off-by-one | — | — | — | — |
| **Security: shell policy & permissions** | ✅ installPolicy warnings | — | ✅ git-bash backdoor fix | ✅ RFC #7155 | ✅ Extension tenancy (#7659) | ✅ commandSafety tests (LobsterAI, PR #1154) | — |
| **Context compaction / session preservation** | ✅ #122618 | ✅ Stale race | — | — | — | ✅ Scroll compression (#6951) | — |
| **Cross-platform Windows support** | — | ✅ `os.replace()` fix | ❌ (#86223) | ❌ 74 test failures | — | ❌ cmd flash/#6197 | NanoClaw (setup fixes) |
| **Installation / setup reliability** | — | — | — | — | — | — | ✅ NanoClaw (#3245, #3248) |
| **API interoperability (OpenAI-compatible)** | — | — | — | ✅ RFC #8603 | — | — | — |
| **Dynamic skill / model discovery** | ✅ #10687 | ✅ skill_names (#5018) | — | — | — | ✅ skill loading (#7029) | — |

**Key takeaway:** The ecosystem is converging on **reliability over novelty**. Every project has at least one "production-blocking" bug that threatens trust.

---

## 5. Differentiation Analysis

| Project | Core Focus | Target Users | Architecture |
|---|---|---|---|
| **OpenClaw** | General-purpose multi-channel assistant | Power users, families, small business | Monolithic gateway, multi-channel, AI-assisted triage |
| **NanoBot** | WebUI-first AI agent + knowledge graph | Developers, data-chat users | Python (strict typing), WebUI + TUI, MCP-driven |
| **Hermes** | Research-grade agent (Nous Research) | Researchers, deep-deployment users | God-file refactoring, Discord-centric, Windows focus |
| **PicoClaw** | Chinese ecosystem integrated (DingTalk/WeChat) | Chinese-market SMBs, embedded developers | Go, SIP-based (Seahorse), TTS providers |
| **NanoClaw** | Lightweight dev-tool agent | Developers, CI/CD users | Bun, container-heavy (hardened images), Cron/scheduling |
| **NullClaw** | Minimum viable agent core | Toolchain users, lean deployments | Minimal, SQLite-backed, no open issues (mature/static) |
| **IronClaw** | Enterprise automation reliability | Ops teams, serious automators | WASM-compiled, structured automation contracts, unbound-turns |
| **CoPaw** | Ecosystem agent (AgentScope) + computer use | Enterprise multi-agent, Windows users | Dynamic skills, channels (Feishu/OneBot), desktop app |
| **LobsterAI** | Youdao backend assistant (desktop) | Chinese-market desktop users | Electron-style (renderer/main), Team Editions, sidebar UX |
| **Moltis** | Personal comms hub (calendar/email/chat) | Privacy-conscious PKM users | Durable connectors, atomic persistence |
| **TinyClaw / ZeptoClaw** | Minimal/clipped agents | Undefined (likely niche) | Inactive — watch for abandonment |

**Summary:** Two broad camps are emerging:
1. **Generalists** (OpenClaw, CoPaw, Hermes): Full-featured, multi-channel, high-complexity.
2. **Specialists** (Moltis, NullClaw, IronClaw): Narrow scope, high-domain-reliability.

---

## 6. Community Momentum & Maturity

| Tier | Projects | Characteristics |
|---|---|---|
| **Tier 1: Rapidly iterating / production-adopted** | OpenClaw, CoPaw, IronClaw, ZeroClaw | High issue+PR velocity, enterprise/power-user adoption, release trains with hardening cycles |
| **Tier 2: Steady growth / consolidating** | LobsterAI, NanoBot, NanoClaw, PicoClaw | Frequent PR merges, but smaller scale; often in stabilization/cleanup phases before next jump |
| **Tier 3: Low activity / mature or stagnant** | Hermes, Moltis, NullClaw | Low daily churn; either stable/mature (NullClaw) or at risk of lost contributor momentum (Moltis's single-PR backlog; Hermes's Windows battle) |
| **Tier 4: Inactive** | TinyClaw, ZeptoClaw | Zero activity — evaluate for abandonment |

**Notable momentum shifts:**
- **IronClaw** is rising fast with a disciplined v1.3.0 plan (automation hardening, pluggable memory, Slack bridge) and rapid QA bug-fix turnaround (same-day fixes).
- **CoPaw** is closing a massive backlog (38 issues in 24h) while delivering on requested features (dynamic skills, auto-title sync)—strong signal of maintainer responsiveness.
- **OpenClaw** retains dominance by raw volume but is at risk of a "reliability winter" if P0s persist.

---

## 7. Trend Signals

Distilled for AI agent developers:

1. **Reliability is the new battleground.** Users will tolerate missing features before they tolerate silent failures, OOM crashes, or provider-specific stalls. Invest in: message-delivery acknowledgment, memory-leak surveillance (RSS tracking), and graceful degradation when APIs deprecate.

2. **Provider-lock anxiety is real.** Multiple projects (OpenClaw, IronClaw, CoPaw) are adding **per-provider / per-contract model pinning** and **output-limit classification** to make agent behavior deterministic across model backends. Design agents for provider-neutral execution.

3. **Security is becoming a first-class feature, not a patch.** ZeroClaw (shell confirmation RFC), Hermes (git-bash backdoor), OpenClaw (installPolicy warnings), and CoPaw (commandSafety tests) all signal that users are asking for **fine-grained, auditable control** before production deployment. Expect a "security-hardened agent" milest

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-15

## 1. Today's Overview
NanoBot saw a **high-activity day** with 3 issue updates and 22 PR updates in the last 24 hours. Of the 22 PRs touched, **8 were merged or closed** while **14 remain open** — indicating a healthy but heavily loaded review pipeline. The repository is currently in a **"strict-mode" migration period** for Pyright type checking, which has triggered a wave of code-quality refactors. Notably, **no new releases** were cut, suggesting the maintainers are consolidating multiple in-flight features (WebUI improvements, session management hardening, and MCP SDK migration) before packaging the next version.

---

## 2. Releases
**No new releases** were published in the last 24 hours. The project appears to be between release cycles, with the most recent activity focused on expanding feature breadth and stabilizing existing functionality.

---

## 3. Project Progress

**8 PRs were merged or closed today:**

| PR | Description | Status |
|----|-------------|--------|
| [#5392](https://github.com/HKUDS/nanobot/pull/5392) | **fix(anthropic):** resolve stream idle timeout acting as total timeout (fixes #5391) — critical provider bug fix | ✅ Merged |
| [#5393](https://github.com/HKUDS/nanobot/pull/5393) | **feat(webui):** polish sidebar and session transitions (UI-only, split from #5358) | ✅ Merged |
| [#5395](https://github.com/HKUDS/nanobot/pull/5395) | **feat(webui):** refine conversation groups and shared shapes — localization and drag-to-group workflow | ✅ Merged |
| [#5390](https://github.com/HKUDS/nanobot/pull/5390) | **feat:** Agent/knowledge graph | ✅ Merged |
| [#5018](https://github.com/HKUDS/nanobot/pull/5018) | **feat(skills):** support explicit context loading via `skill_names` input | ✅ Merged |
| [#4689](https://github.com/HKUDS/nanobot/pull/4689) | **feat(providers):** surface OAuth status and expiry warnings across CLI/WebUI/runtime | ⚪ Closed (invalid) |
| #5389, #5358, #5309, etc. | Multiple WebUI/feature PRs remain open with conflicts | 🔄 Open |

**Key advancements:** The **Anthropic idle timeout fix** (#5392) closes a real-world bug where long but active generations were killed. The **explicit skill context loading** (#5018) gives direct API callers more control over skill injection. **Knowledge graph support** (#5390) also landed, marking a potentially significant feature addition.

---

## 4. Community Hot Topics

### #1: [PR #5396 — Pyright strict-mode refactor](https://github.com/HKUDS/nanobot/pull/5396)
**Open | 1 comment on parent issue | 22 files touched**
The most debated topic is the sweeping refactor to narrow file-level Pyright suppressions (Issue [#5161](https://github.com/HKUDS/nanobot/issues/5161)) after enabling `strict` mode across `nanobot/`. **Underlying need:** The codebase needs type-safe ownership — the question is how aggressively to remove file-level directives that protect future diagnostics.

### #2: [PR #5271 — Stale background task race condition (p0)](https://github.com/HKUDS/nanobot/pull/5271)
**Open | Priority: P0**
Prevents stale background work from overwriting a session after `/new` or lifecycle replacement. **Underlying need:** Session data integrity under concurrency; the lack of this fix can silently lose user context.

### #3: [PR #4329 — Native TypeScript terminal UI](https://github.com/HKUDS/nanobot/pull/4329)
**Open | Created 2026-06-13 | Still active**
The long-running effort to rebuild `nanobot agent` as a native TS/OpenTUI client. **Underlying need:** Cross-platform terminal experience without a Python runtime dependency — popular direction but slow to merge.

### #4: [PR #5358 — Session collaboration via mentions](https://github.com/HKUDS/nanobot/pull/5358)
**Open | Conflict**
Adds team collaboration by mention. **Underlying need:** Multi-user session sharing — a clear product roadmap signal.

---

## 5. Bugs & Stability

| Severity | Bug | Fix Status |
|----------|-----|------------|
| 🔴 **High** | [#5391](https://github.com/HKUDS/nanobot/issues/5391) — Anthropic idle timeout kills long but active generations (90s cap on no-callback path) | ✅ Fixed in [#5392](https://github.com/HKUDS/nanobot/pull/5392) |
| 🟠 **Medium** | [#5378](https://github.com/HKUDS/nanobot/issues/5378) — File-cap archive failure mutates session before persistence | 🟡 No fix PR yet |
| 🟠 **Medium** | [#5382](https://github.com/HKUDS/nanobot/pull/5382) — `os.replace()` crashes gateway on transient Windows `PermissionError` during heartbeat | 🟡 Open PR with retry logic |
| 🟡 **Low** | [#5271](https://github.com/HKUDS/nanobot/pull/5271) — Stale background saves overwrite sessions after `/new` | 🟡 Open PR (P0 priority) |

The **Anthropic timeout bug** was the most impactful — users on long generations (e.g., extensive agent loops) were silently losing work. The fix redefines the timeout as **inactivity-only**, preserving active streams.

---

## 6. Feature Requests & Roadmap Signals

Several features merged or advanced today point to the next release:

1. **Knowledge graph support** (#5390) — merged; likely part of next release with semantic session indexing.
2. **OAuth status + expiry warnings** (#4689) — closed as invalid but signals enterprise demand for provider lifecycle visibility.
3. **Explicit skill context loading** (#5018) — merged; enables programmatic skill injection.
4. **WebUI localization for agent activity** (#5367) — open and active; indicates strong internationalization push.
5. **Drag-and-drop session organization** (#5389) — open; user-driven UX polish.
6. **Session collaboration via mentions** (#5358) — open; strong signal for team-use cases.

**Prediction:** The next minor release will likely include: the Pyright refactor, WebUI localization, and session organization improvements — bundled with the Anthropic timeout fix.

---

## 7. User Feedback Summary

- **Pain point (urgent):** Anthropic stream timeout kills long active generations — a user-reported regression resolved within 24 hours, demonstrating **responsive maintainership**.
- **Pain point (recurring):** Windows session persistence crashes (`os.replace()` PermissionError) — reported in logs and actively being patched with retry logic.
- **Positive signal:** The community actively explores advanced use cases (knowledge graphs, terminal UI, collaboration) — indicating a mature user base pushing product boundaries.
- **Frustration signal:** Multiple PRs marked `[conflict]` (e.g., #5358, #5371, #5389, #5340) suggest **review-bottleneck friction** — feature branches are colliding, delaying merges.

---

## 8. Backlog Watch

| Item | Age | Status |
|------|-----|--------|
| [PR #4329 — TS Terminal UI](https://github.com/HKUDS/nanobot/pull/4329) | **63+ days** (Created 06-13) | Open; no maintainer response visible — high-value but risks bit-rotting |
| [#4145 — Weather Skill fix](https://github.com/HKUDS/nanobot/pull/4145) | 75+ days | Open; merged multi-file PR awaiting review |
| [#5309 — Marketplace skills shadow builtins](https://github.com/HKUDS/nanobot/pull/5309) | ~6 days | Open; critical skill-install UX bug |
| [#5152 — Subagent partial completion](https://github.com/HKUDS/nanobot/pull/5152) | ~18 days | Open; regression fix for agent orchestration |

**Maintainer attention needed:** [#4145](https://github.com/HKUDS/nanobot/pull/4145) (Weather Skill) and [#4329](https://github.com/HKUDS/nanobot/pull/4329) (TS Terminal UI) are long-standing feature contributions awaiting review. The **P0 stale-session race** (#5271) also deserves expedited merge given its data-loss potential.

---

**Overall health assessment:** NanoBot is in a **growth phase** — high feature velocity, active bug fixes, and a broad contributor base (10+ unique authors in 24h). The main risk is **accumulating PR conflicts and review lag**, which could accelerate as WebUI and core refactors overlap. The maintainer response time on critical bugs (24h for the Anthropic fix) is excellent and should be celebrated as a project strength.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Based on the GitHub data for Hermes Agent (2026-08-15), here is the project digest:

---

## Hermes Agent Project Digest — 2026-08-15

### 1. Today's Overview
The Hermes Agent project is in a period of **high velocity and substantial consolidation**. Activity is dominated by two major campaigns: the completion of the "All Gods Must Die" god-file refactoring epic (closed) and the ongoing "Discord Omniscience" feature parity push, which accounts for the majority of new issues filed today. While there are no new releases, the project is processing a significant number of bug reports and feature implementations, indicating a mature codebase undergoing active refinement. The maintenance workload is high, with a stable flow of closed issues and focused PRs addressing critical Windows-specific stability and security concerns.

### 2. Releases
No new releases were published on 2026-08-15.

### 3. Project Progress
Only four PRs were merged or closed within the last 24 hours. The most significant closure was the **long-running Epic #78647**, "All Gods Must Die: 20/20 killed," which marks the successful completion of a repo-wide campaign to shard "god-files" into clean modules. Additionally, a major bug affecting the desktop UI was resolved with the closure of Issue #60260 (approval bar not rendering). On the PR side, two critical fixes were closed: PR #77285, which rewrote the xAI streaming TTS protocol to fix broken voice output, and PR #86368, which addressed a duplicate issue regarding the same xAI TTS WebSocket protocol. Notably, the massive "single gateway, multiple agents" PR (#62944) remains open after being rebased onto current `main`.

### 4. Community Hot Topics
The community is actively engaged in improving the agent's internal architecture and extending its platform reach.

- **[Issue #78647 (Closed): Epic — God-file sharding complete](https://github.com/NousResearch/hermes-agent/issues/78647)** — With 76 comments, this was the most active topic. It signifies the successful completion of a major technical debt reduction initiative, signaling a strong commitment to code maintainability.

- **[Issue #66616: Skills index freshness degraded](https://github.com/NousResearch/hermes-agent/issues/66616)** — With 31 comments, this automated watchdog issue highlights an operational reliability concern. The community is likely discussing the impact of a stale skills index and the need for more robust CI/CD pipelines.

- **[Issue #85622: External memory provider suppresses built-in memory](https://github.com/NousResearch/hermes-agent/issues/85622)** — This bug report (10 comments) touches on a core expectation for users: the "additive, never replacing" contract for memory. The underlying need is for strict adherence to documented behavior, especially for power users relying on hybrid memory setups.

- **[Issue #79564: Discord Feature Parity Campaign](https://github.com/NousResearch/hermes-agent/issues/79564)** — This meta-issue (6 comments) is the parent for nearly a dozen new feature requests filed today (e.g., #86535, #86536, #86549). It demonstrates a strong community-driven effort to bring the Discord integration to full feature parity with the API.

### 5. Bugs & Stability
The project is juggling several critical stability issues, particularly on Windows.

- **P1 — Windows Desktop Client Failures (Issue #86223):** The desktop client is broken after recent updates, with backend exits and restart failures. This is the highest-severity issue. Two PRs are actively addressing this: **[PR #86555](https://github.com/NousResearch/hermes-agent/pull/86555)** fixes the restart race condition for the rebuilt executable, and **[PR #86269](https://github.com/NousResearch/hermes-agent/pull/86269)** rebuilds the Desktop after release artifact loss during updates.

- **P2 — Cron Scheduler Hang (Issue #86482):** A bug report indicates that a failure in `create_execution` can strand a job in the "running" set, causing an infinite 'already running — skipping' loop. This is a serious reliability issue for automated workflows.

- **P2 — File Tools Host-Filesystem Dependency (Issue #86513):** The `file_tools` module incorrectly stats the host filesystem for remote/container backends, breaking correctness for users relying on containerized execution.

- **P2 — Telegram Topic Migration Atomicity (Issue #86483):** A bug causes the migration to potentially run a non-atomic transaction, risking partial failure and loss of data bindings.

- **P2 — read_file Off-by-One (Issue #86510):** A bug in `read_file` miscounts lines for files without trailing newlines, leading to potential data truncation for users.

- **Security PRs:** **[PR #71354](https://github.com/NousResearch/hermes-agent/pull/71354)** closes a security hole where Git-Bash MCP backdoors on Windows could bypass exfiltration and persistence guards, and **[PR #77605](https://github.com/NousResearch/hermes-agent/pull/77605)** adds strict host file-tool scope for profiles, reinforcing security boundaries.

### 6. Feature Requests & Roadmap Signals
The roadmap is heavily focused on **platform-specific feature parity** and **developer experience**.

- **Discord Omniscience (I, M, R, T, V, W Phases):** The wave of issues (#86535-86539, #86521, #86498, #86500, #86502, #86504, #86484, #86486, #86549) indicates a clear roadmap for Discord enhancements, including slash-command autocomplete, component authorization, native voice-message validation, and thread permission correctness. These are likely to land in upcoming minor releases.

- **Cross-Surface Lifecycle Hooks (Issue #67798):** This long-standing feature request seeks to make the event-hook system a shared runtime contract across all execution surfaces (TUI, CLI, Desktop, etc.), not just the gateway. This is a strong signal for a more unified, modular architecture.

- **Desktop Enhancements:** PR #86548 adds the ability to configure tool scopes for any profile without switching the active profile, and Issue #86554 requests optional semantic colors for better readability, indicating a focus on polish and usability for the desktop client.

- **Claude Code Ports:** PRs #86553 and #86552 show a proactive strategy of porting useful features from Claude Code, specifically prompt-cache launch staggering for batch subagents and per-command memory ceilings for the terminal. This suggests continuous performance and stability improvements are on the horizon.

### 7. User Feedback Summary
Real user pain points are concentrated on **Windows platform stability** and **broken voice functionality**.

- **Severe dissatisfaction with Windows updates:** Users (e.g., aKa368 in #86223) are experiencing frequent breakages after updates, with the client failing to restart. This is a major friction point that could erode trust in the update pipeline.
- **Frustration over broken voice features:** The closure of PRs #77285 and #86368 indicates that the xAI streaming TTS was broken for some time, a significant regression for users relying on voice interaction.
- **Confusion over documentation vs. reality:** Users (TeaShaman-cyber in #85622) report that documented contracts (like memory being additive) are not being honored in practice, leading to unexpected behavior.
- **Feature requests for usability:** Users are asking for simple quality-of-life improvements, such as a URL address bar in the desktop preview pane (#80158) and semantic color coding for text emphasis (#86554).

### 8. Backlog Watch
Several important items remain open and require maintainer attention to reach a resolution.

- **[PR #62944: Single gateway, multiple agents](https://github.com/NousResearch/hermes-agent/pull/62944)** — This is a major architectural PR (P2) that has been rebased onto `main` but remains open since July 12. Given its breadth and impact, a maintainer decision or merge plan is critical to avoid it becoming stale again.

- **[Issue #67798: Make lifecycle hooks a shared runtime contract](https://github.com/NousResearch/hermes-agent/issues/67798)** — Marked as `needs-decision`, this feature request has been open since July 20 and remains unanswered. It touches multiple components and needs a maintainer to weigh in on its architectural direction.

- **[Issue #66616: Skills index is stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616)** — This automated watchdog has been open for nearly a month, indicating the underlying cause for the stale skills index has not been resolved. This is a continuous operational debt that will keep impacting users until fixed.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-15

## 1. Today's Overview

PicoClaw is in a moderate activity phase with 3 issues and 9 pull requests updated in the last 24 hours, though no new releases were published. The project appears to be in a **consolidation and cleanup cycle**, with 5 PRs merged/closed (predominantly marked `[stale]` after an extended open period) and 4 PRs still open for review. The standout activity is a **fresh fix PR for the MCP connection hang** (Issue #3269 → PR #3337), submitted just yesterday, indicating responsive maintenance on a critical reliability bug. Several stale PRs from July are receiving final attention, suggesting maintainers are clearing the backlog. The absence of new releases suggests changes are accumulating on nightly builds. Overall project health appears positive: the critical hang bug has a dedicated fix in flight, and channel integrations (DingTalk, WeChat, DeltaChat) continue to mature.

## 2. Releases

**No new releases were published** in the last 24 hours. The latest available version remains the nightly build referenced in issue #3269 (git commit `2cf030d2`). Users tracking stable releases should note that recent features (DashScope TTS, DingTalk image support, model fallback chains) are still only available in nightly builds until the next official tag.

## 3. Project Progress

Five PRs were **merged or closed** in the last 24 hours, all marked as `[stale]` after being open for 2–4 weeks:

- **PR #3271** — `chore(providers)`: Updated default model names across 9 providers to the latest 2026-07 models (OpenAI `gpt-5.6` series, Anthropic, etc.), verified against official documentation. This keeps default configurations current with provider API changes.
- **PR #3270** — `feat`: Added **DashScope TTS provider** (Alibaba Cloud Bailian) and **WeChat audio file sending**. New file `pkg/audio/tts/dashscope_tts.go` adds a substantial TTS capability with multi-modal API calls.
- **PR #3283** — `fix(dingtalk)`: Added **picture/image message inbound support** for the DingTalk channel, including OpenAPI token caching and graceful degradation on download failures.
- **PR #3279** — `fix(seahorse)`: Prevented **tool-call format leakage** into LLM summaries via `partsToReadableContent`, fixing a cross-cutting bug class where raw tool-call JSON could appear in user-facing messages.
- **PR #3303** — `build(deps)`: Bumped `actions/stale` GitHub Action from v10 to v11 (maintenance).

## 4. Community Hot Topics

The most active discussion is the **MCP server connection hang bug**:

- **Issue #3269** (`[BUG] If the MCP server connection fails, the agent loop will hang`) — **5 comments, 1 👍** — Opened July 20, updated Aug 14. This is the clear hotspot, describing a complete loss of chat responsiveness when an MCP server is unreachable. A corresponding fix PR (#3337) landed yesterday, showing active developer attention.
- **Issue #3308** (`[stale]` Code review: concurrency hazards, goroutine leaks in SeaHorse/Channel Manager/Hooks) — **2 comments** — A community member provided a detailed code review flagging concurrency issues. Closed as stale, but the content may warrant future attention.

## 5. Bugs & Stability

| Severity | Issue | Description | Status | Fix |
|----------|-------|-------------|--------|-----|
| 🔴 **Critical** | [#3269](https://github.com/sipeed/picoclaw/issues/3269) | MCP server connection failure **hangs the entire agent loop**, causing chat interface to stop replying until process restart | **Open** | [PR #3337](https://github.com/sipeed/picoclaw/pull/3337) submitted 2026-08-14 |
| 🟡 Moderate | [PR #3319](https://github.com/sipeed/picoclaw/pull/3319) | `exec` tool ignores per-run `timeout` argument (always uses global); `background`/`pty` schema declares strings instead of booleans | Open PR (fix) | PR #3319 under review |
| 🟢 Low | [PR #3279](https://github.com/sipeed/picoclaw/pull/3279) (merged) | Tool-call format leakage into LLM summaries via seahorse path — **now fixed** | Fixed | Merged |

## 6. Feature Requests & Roadmap Signals

- **Session management for non-Web channels** (`Issue #3307`, closed as stale): Users want **session list/switch/delete commands via Telegram** and other chat channels, mirroring the Web UI's `session-history-menu.tsx` functionality. Closed due to inactivity but represents an unmet UX gap for channel-based users.
- **Configurable model fallback chain** (`PR #3200`, still open): Adds a default fallback chain for models in the Web UI with reordering and backend persistence — useful for providers with intermittent availability. Open since July 1; worth monitoring.
- **DashScope TTS** (merged in #3270): Signals continued investment in the Chinese ecosystem (Alibaba Cloud), alongside existing DingTalk and WeChat integrations.

## 7. User Feedback Summary

- **Pain point — MCP reliability (Issue #3269)**: Users experience **silent chat interface failures** when MCP servers are unreachable — no error shown, no retry, nothing. The agent loop exits entirely. This is the most severe UX degradation: the assistant simply does not respond.
- **Pain point — Channel feature parity (Issue #3307)**: Feature parity gaps exist between the **Web UI (full session management)** and **chat channels (Telegram et al. lack even basic session listing)**. Users on channels cannot manage conversations without switching to the Web UI.
- **Positive signal — Community scrutiny**: One user (Rehanasharmin) performed a **detailed code review** of concurrency/goroutine handling, indicating an engaged and technically sophisticated user base that contributes beyond bug reports.
- **Positive signal — Fast fix turnaround**: The MCP hang (reported July 20) received a dedicated fix PR within ~3 weeks, suggesting the maintainers prioritize reliability issues.

## 8. Backlog Watch

| Item | Age | Status | Action Needed |
|------|-----|--------|---------------|
| [PR #3200](https://github.com/sipeed/picoclaw/pull/3200) — Configurable default fallback chain | **45 days** (since Jul 1) | Open, no recent maintainer comment | Needs review — adds meaningful UX value for model reliability |
| [PR #3222](https://github.com/sipeed/picoclaw/pull/3222) — DeltaChat cleanup (-200 LOC, docs) | **42 days** (since Jul 3) | Open, unchanged since Aug 14 | Refactor touches core channels; needs maintainer sign-off |
| [PR #3319](https://github.com/sipeed/picoclaw/pull/3319) — Exec tool timeout/boolean fix | 8 days | Open, awaiting review | Small but correctness-critical fix; low risk to merge |

## Project Health Summary

**Health: Good** — The project is actively maintained with a clear responsiveness to critical bugs (MCP hang fixed in ~3 weeks). The community is engaged and technically skilled. The main risk area is **stale issue/PR management**: several items closed as `[stale]` (including a substantive feature request and a concurrency code review) may represent missed opportunities for improvement. The open backlog items (model fallback chain, DeltaChat refactor) are 6+ weeks old and need maintainer attention to avoid losing contributor momentum.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-15

---

## 1. Today's Overview

NanoClaw is in a **moderate-to-high activity state** with 11 PRs updated in the last 24 hours, though only 3 were merged/closed (all core-team live-fire tests). Two new issues were filed today, both related to the **setup and installation experience** — one on Node version detection logic and one on CPU compatibility (AVX2) of the prebuilt Bun binary. The PR queue shows **strong momentum on hardening** (Windows container cleanup, malformed cron handling, signature verification) and **two long-running feature branches for a new "Dial" channel** (SMS + AI voice calls) that remain open and actively updated. No new releases were published in the last day, suggesting the team is consolidating fixes before the next tag.

---

## 2. Releases

**No new releases** were published on 2026-08-15 (or in the 24h window). The most recent activity is in the PR queue, not in tagged releases.

---

## 3. Project Progress

Three PRs were closed (all authored by **gavrielc**, core-team):

| PR | Title | Status | Significance |
|----|-------|--------|--------------|
| [#3243](https://github.com/nanocoai/nanoclaw/pull/3243) | verify-agent-image: arming auto-merge is not a verdict | **Merged** | Fixes a CI logic bug where `enable-auto-merge` failure on a draft PR would incorrectly fail the `verify` job. This is a **correctness fix for the image-signature verification pipeline**. |
| [#3244](https://github.com/nanocoai/nanoclaw/pull/3244) | DO NOT MERGE — live-fire the signature approver (take 2) | **Closed unmerged** | Test harness, not a feature. |
| [#3242](https://github.com/nanocoai/nanoclaw/pull/3242) | DO NOT MERGE — live-fire test of the signature approver | **Closed unmerged** | Test harness, not a feature. |

**Notable open progress (8 PRs, all still moving):**

- **[#3249](https://github.com/nanocoai/nanoclaw/pull/3249) — fix(setup): handle an existing Node that is too old** (author: glifocat): Fixes the exact bug reported in #3248. Touches the same `setup.sh` logic — good signs this will land quickly.
- **[#3247](https://github.com/nanocoai/nanoclaw/pull/3247) — fix(scheduling): retire a malformed cron string instead of re-erroring every sweep tick** (jsboige): Prevents infinite error loops on bad cron input.
- **[#3246](https://github.com/nanocoai/nanoclaw/pull/3246) — fix(container-runtime): stop orphan cleanup from silently no-oping on Windows** (jsboige): POSIX quoting issue in `execSync` breaks Windows orphan cleanup.
- **[#3230](https://github.com/nanocoai/nanoclaw/pull/3230) — fix(skills): stop removal docs pointing at the retired data/env mirror** (teran13): Docs cleanup.
- **[#3050](https://github.com/nanocoai/nanoclaw/pull/3050) & [#3041](https://github.com/nanocoai/nanoclaw/pull/3041) — feat: Dial channel adapter (SMS + AI voice calls)** (OmriBenShoham): Two-part feature (channel picker/wizard + adapter). Still open for a month. **This is the largest pending feature.**

---

## 4. Community Hot Topics

No issues or PRs today have substantive comment threads yet (all ≤1 comment, 0 reactions). The most **discussed or significant by content** are:

- **[#3248 — setup.sh's "Node missing or too old" branch cannot handle too old](https://github.com/nanocoai/nanoclaw/issues/3248)** (glifocat): Reports a logic bug where `install-node.sh` short-circuits if *any* Node exists, even one too old. The code explicitly routes "too old" into the helper, but the helper can't handle it. This is a **sharp code-level bug report with a fix PR already submitted (#3249)** — a model contributor cycle.

- **[#3245 — Bun binary requires AVX2, SIGILL on older CPUs](https://github.com/nanocoai/nanoclaw/issues/3245)** (sergeykad): Prebuilt agent image crashes with SIGILL on CPUs without AVX2 (e.g., Intel Elkhart Lake Atoms, Celeron J6413/N5105). The default wizard-recommended image (`NANOCLAW_HARDENED_IMAGE=true`) is affected. **No fix PR yet** — this is a real compatibility gap.

**Underlying needs:** Both hot topics point to a **hardening of the install experience** — the "it just works" path (wizard defaults) is failing on two real-world machines (old Node, old CPU). The community values setup reliability over new features right now.

---

## 5. Bugs & Stability

| Severity | Issue/PR | Description | Fix Available? |
|----------|----------|-------------|----------------|
| **High** | [#3245](https://github.com/nanocoai/nanoclaw/issues/3245) | Prebuilt Bun image requires AVX2 → SIGILL on non-AVX2 CPUs (modest Atom/Elkhart Lake hardware). Breaks the default wizard flow. | **No** — needs a baseline-x64 build or CPU detection. |
| **Medium** | [#3248](https://github.com/nanocoai/nanoclaw/issues/3248) | `setup.sh` cannot actually handle "Node too old" because the helper short-circuits; user is left with broken install. | **Yes — PR [#3249](https://github.com/nanocoai/nanoclaw/pull/3249) submitted (draft?)**, needs review/merge. |
| **Medium** | [#3247](https://github.com/nanocoai/nanoclaw/pull/3247) | Malformed cron strings cause repeated error logging every sweep tick (no crash, but log spam + repeatedly re-attempting failure). | Yes — PR open, needs review. |
| **Low** | [#3246](https://github.com/nanocoai/nanoclaw/pull/3246) | Windows orphan cleanup silently no-ops due to POSIX quoting in `execSync`. Functional but invisible failure on Windows. | Yes — PR open, needs review. |

**Overall stability assessment:** Two real bugs in the installation path (Node version, CPU arch) are the most urgent; both hit the "default" user journey. The CI/verify pipeline fix (merged #3243) is a good sign of internal rigor.

---

## 6. Feature Requests & Roadmap Signals

- **[Dial channel (SMS + voice calls)](https://github.com/nanocoai/nanoclaw/pull/3041) — OmnriBenShoham, open since 2026-07-14, still active:** Two PRs (#3041 adapter + #3050 wizard/skills integration) implement a full new channel. This is the strongest signal for a **next-version feature** — it's been in review a month and is still being updated. Predict: **lands in the next minor release (e.g., v0.x with Dial channel)**.

- **Silent/background signals:** The number of `fix` PRs (7 of 11 today) suggests the team is in a **stabilization phase** — the roadmap signal is "fewer new features, more reliability."

---

## 7. User Feedback Summary

- **Pain point — setup reliability:** Two issues today (#3245, #3248) both hit the install wizard flow. Users on modest hardware (Celeron, Elkhart Lake Atoms) or with pre-existing older Node installations are hitting walls. Sign of **dissatisfaction with the "default" path**.
- **Positive contributor experience:** Issue #3248 was filed and a matching PR (#3249) was submitted by the *same author* within hours — a healthy sign of contributor engagement and a responsive maintainer community.
- **Windows second-class experience:** PR #3246 confirms Windows users face silent failures (orphan cleanup), a recurring theme across many projects — but here it's a *documented fix*, meaning someone cares about Windows users.

---

## 8. Backlog Watch

| Item | Age | Why It Needs Attention |
|------|-----|------------------------|
| **PR [#2427](https://github.com/nanocoai/nanoclaw/pull/2427) — fix: attachment issues** (b1ek) | **~3 months** (created 2026-05-12) | Longest-open PR in the queue. Last updated 2026-08-14 (still active), but blocking? Closes #2426, which is likely an attachment-handling bug. Needs maintainer triage: merge, request changes, or close with rationale. |
| **PR [#2752](https://github.com/nanocoai/nanoclaw/pull/2752) — Discord inbound attachments** (chubbicorn245) | **~2 months** (created 2026-06-12) | Also attachment-related, also updated recently. Two open attachment PRs suggests a **known attachment subsystem problem** waiting for review time. |
| **PR [#3050](https://github.com/nanocoai/nanoclaw/pull/3050)** (Dial channel, part 2) | **~1 month** | Large feature; needs sustained maintainer attention to avoid rot. |

**Backlog health note:** No stale (silent >30 days) issues or PRs are visible — everything is an *active* backlog, not an abandoned one. The main risk is **review bandwidth**, not contributor abandonment.

---

### Net Assessment

NanoClaw is **healthy but in a stabilization phase**: the community is actively reporting install-path bugs, the core team is running live-fire CI tests for signature verification, and there's one big feature (Dial) waiting to land. The two setup bugs (#3245, #3248) are the **highest-priority items for project health** — both affect the "happy path" new-user experience. The attached fix PRs (especially #3249) should be prioritized for review in the next 48 hours.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest
**Date:** 2026-08-15

---

## 1. Today's Overview

NullClaw is in a low-activity but steady state, with no new issues reported or updated in the last 24 hours. The project saw one Pull Request merged/closed, signaling that maintainers are processing existing work rather than taking in new bug reports or feature requests. There were no new releases, and the open issue backlog remains at zero, indicating a clean triage state. The single merged PR focused on infrastructure-level configuration (SQLite memory database paths), which suggests a shift toward deployment flexibility and DevOps hardening rather than user-facing features. Overall, the project appears stable and healthy, with maintainers actively clearing technical debt.

---

## 2. Releases

**No new releases** were published on 2026-08-15. The most recent release remains the prior version, and there is no changelog or migration note to report for this digest period.

---

## 3. Project Progress

**One Pull Request was merged/closed today:**

- **[PR #986 – GEN-548: make SQLite memory database path configurable](https://github.com/nullclaw/nullclaw/pull/986)**
  - **Author:** gently-whitesnow
  - **Status:** Closed/merged (created 2026-08-14, updated 2026-08-14)
  - **What advanced:** This PR adds a new `memory.database_path` configuration setting for SQLite-backed primary memory engines. It preserves backward compatibility by keeping the default `<workspace>/memory.db` location when the setting is left empty. It also improves deployment flexibility by resolving relative paths from the workspace and supporting absolute paths for read-only workspace deployments. Documentation for the new setting was included.
  - **Significance:** This is an infrastructure-level improvement that enables more flexible deployments (e.g., containerized or read-only filesystem environments). It does not introduce user-facing features but removes a hardcoded path constraint.

---

## 4. Community Hot Topics

No issues or PRs received comments or reactions in the last 24 hours. The only activity was the merged PR #986, which had **0 comments and 0 👍 reactions**.

**Analysis:** The lack of community discussion is likely a reflection of the project's current phase—a mature tool with fewer open questions and a user base that is either satisfied or actively engaged via other channels (e.g., Discord/forums). The absence of unanswered issues reduces community friction, but also leaves little signal for new feature demand.

---

## 5. Bugs & Stability

**No new bugs, crashes, or regressions were reported** in the last 24 hours.

**Stability assessment:** With zero open issues and no new bug reports, NullClaw is in a strong stability posture. The merged PR #986 does not touch core runtime behavior but adjusts configuration loading, which has a low regression risk. There are no known stability concerns to rank or escalate.

---

## 6. Feature Requests & Roadmap Signals

**No user-submitted feature requests** were filed in the last 24 hours.

**Predictive signal from PR #986:** The nature of this PR (making memory database paths configurable) hints at a growing requirement for:
- **Containerization support** (allowing persistent storage volumes to be mounted at explicit paths).
- **Read-only deployment environments** (e.g., serverless functions, immutable infrastructure).
- **Multi-instance or multi-tenant setups** where default workspace paths could collide.

**Next version prediction:** The next minor release could include an umbrella "deployment flexibility" feature set, potentially including:
- Environment variable overrides for all path-based settings.
- Docker/Kubernetes example manifests referencing the new `memory.database_path`.
- A configuration validation utility for absolute paths in read-only contexts.

These are logical extensions of the pattern introduced in PR #986.

---

## 7. User Feedback Summary

**No explicit user feedback (comments, 👍, or issue reports) was captured in the last 24 hours.**

**Inferred sentiment from PR #986:** The contributor's  effort to make database paths configurable suggests they are using NullClaw in a production or semi-production deployment where the default workspace-relative database file is not sufficient. The pain point addressed is: *"I need to control where state is stored to fit my infrastructure constraints."* This is a positive signal—users are mature enough to deploy NullClaw seriously and are contributing back improvements rather than abandoning the tool. The lack of complaints in issue tracker indicates general satisfaction, or at least acceptance of the current feature set.

---

## 8. Backlog Watch

**No items in backlog.** Currently, the project has:
- **0 open issues**
- **0 open PRs**
- **1 merged PR today**

**Maintainer attention:** There are no long-unanswered issues or stale PRs requiring intervention. This is an exceptionally clean state, suggesting that either the maintainers are highly responsive or the project has a limited issue influx. The only item to monitor is whether PR #986's documentation update triggers any community questions about migration (e.g., users who previously relied on hardcoded paths might need guidance). No action is required from maintainers at this time.

---

*Digest generated from NullClaw GitHub activity data for 2026-08-15.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-15

## 1. Today's Overview

IronClaw is in a high-velocity stabilization and platform-hardening phase, with 71 items updated in the last 24 hours (25 issues, 46 PRs) and a 50/50 split between open and closed work. The project is actively executing on two parallel fronts: (a) a major **automation reliability epic (#6879)** targeting v1.3.0, with multiple structured-execution PRs open and in-flight, and (b) an aggressive **QA bug-bash cycle** (epic #7414) producing a steady stream of P2 bugs from the `qa-testing-libsql` Railway instance, most of which are receiving fix PRs within hours. A significant unbound-turns architecture switchover (PR #7634) is close to completion, and the 1.2.0 release line has been successfully merged back into `main` (PR #7657). The repository is clearly in a pre-release hardening window for v1.3.0, with strong throughput on bug fixes and feature completion.

---

## 2. Releases

**No new releases in the last 24 hours.**

Notable: The **IronClaw 1.2.0 release line was merged back into `main`** (PR #7657), indicating a recent successful release. A follow-up PR (#7663) is forward-porting 1.2 fixes onto current `main` *without* legacy migration paths, which suggests the team is intentionally cutting migration debt for future releases.

---

## 3. Project Progress

**23 PRs were closed/merged in the last 24 hours.** Key advances:

| Area | PR | What landed |
|---|---|---|
| **Unbound-turns architecture** | [#7562](https://github.com/nearai/ironclaw/pull/7562) (merged) | Base PR for the unbound-turns train: prepared-context accept door, unbound run lane, kernel binding-ref deletion — plus the phase-1 implementation and design docs |
| **1.2.0 release line** | [#7657](https://github.com/nearai/ironclaw/pull/7657) | Merged validated `release/2026-08-11` back into `main` with state-preserving migrations, Windows fixes, and upgrade canaries |
| **Extension truthfulness** | [#7666](https://github.com/nearai/ironclaw/pull/7666) | Extension cards/install results now tell the truth (QA #7660 + install guidance); device-link installs direct users to Web UI link step |
| **Telegram 2FA gate** | [#7658](https://github.com/nearai/ironclaw/pull/7658) | Recognizes the 2FA gate on migrated DCs and informs users where login codes arrive |
| **Provider auth diagnostics** | [#7668](https://github.com/nearai/ironclaw/pull/7668) | Surfaces bounded GitHub provider errors with stable codes through WASM, ABI, capability, and gate paths |
| **Origin-scoped MCP OAuth** | [#7665](https://github.com/nearai/ironclaw/pull/7665) | Supports the narrowly bounded hosted-MCP OAuth shape used by MKT1 (HTTPS `/mcp` endpoint) |
| **DB write measurement** | [#7652](https://github.com/nearai/ironclaw/pull/7652) | Production-graded measurement of per-turn DB write workloads (10 tool calls, 11 model attempts, journaling) |
| **Perf: heartbeat churn** | [#7628](https://github.com/nearai/ironclaw/pull/7628) (open) | Stops appending heartbeat journal rows; leases authoritative on materialized process row |
| **CI coverage re-pin** | [#7655](https://github.com/nearai/ironclaw/pull/7655) | Re-pins slack/telegram integration coverage floors to observed reality (a pragmatic CI fix) |
| **Frontend cleanup** | [#7520](https://github.com/nearai/ironclaw/issues/7520) (closed) | Epic retired superseded/unreachable WebUI surfaces |
| **Per-user LLM selection** | [#7183](https://github.com/nearai/ironclaw/issues/7183) (closed) | Feature request for per-user model selection — closed, likely landed |

---

## 4. Community Hot Topics

The most active **issues** are those in the **automation reliability epic (#6879)** — all authored by `serrrfirat` (likely the core/lead engineer), each spawning dedicated enhancement issues:

- **[#6879 — Automation runs are hit-or-miss](https://github.com/nearai/ironclaw/issues/6879)** (1 comment, open since 07-29) — the parent epic; describes structural failure in trigger→run execution, especially on small models (DeepSeek V4 Flash). This has spawned **five** sub-issues (#7644–#7647, #7532) and at least three PRs (#7650, #7651, and the merged #7532).

- **The v1.3.0 enhancement cluster** — [#7644](https://github.com/nearai/ironclaw/issues/7644) (verify automation before arming), [#7645](https://github.com/nearai/ironclaw/issues/7645) (pin LLM model profile per contract), [#7646](https://github.com/nearai/ironclaw/issues/7646) (preflight grants + standing approval leases), [#7647](https://github.com/nearai/ironclaw/issues/7647) (deterministic no-delivery outcome) — collectively represent a careful, defense-in-depth approach to making scheduled automations trustworthy.

- **Pluggable memory (#7664)** + the draft MCP-backed provider PR ([#7661](https://github.com/nearai/ironclaw/pull/7661)) is a significant architectural signal — memory systems will become config-bound rather than compile-time. Mnesis Core is the first consumer.

**Underlying needs analysis:** The automation epic reveals a deep need for **deterministic, verifiable unattended execution** — structured contracts, preflight grants, model pinning, and explicit suppression outcomes. This is production-grade reliability engineering for agent automation, not just feature work.

---

## 5. Bugs & Stability

**9 issues closed** and **several active QA bugs** reported today. Ranked by severity:

| Severity | Issue | Description | Fix status |
|---|---|---|---|
| **P2 — Functional** | [#7662](https://github.com/nearai/ironclaw/issues/7662) | **MP4 attachment fails** in Telegram with `invalid_value (attachments.mime_type)` despite correct `video/mp4` recognition | No fix PR yet |
| **P2 — UX/Data** | [#7659](https://github.com/nearai/ironclaw/issues/7659) | **Extension state leaking between users** — extensions installed by other users visible as installed | No fix PR yet (privacy/tenancy concern) |
| **P2 — UX** | [#7660](https://github.com/nearai/ironclaw/issues/7660) | Slack UI shows **"Reconnect"/"Finish Setup"** despite active working connection | Fixed via [#7666](https://github.com/nearai/ironclaw/pull/7666) (card truth batch) |
| **P2 — Login** | [#7667](https://github.com/nearai/ironclaw/issues/7667) | Telegram phone-mode login: **code-hint doesn't reflect `sentCode.type_`** on raw-TL send path (real user blocked from login) | Fixed via [#7658](https://github.com/nearai/ironclaw/pull/7658) (2FA gate recognition) |
| **P2 — UX** | [#7638](https://github.com/nearai/ironclaw/issues/7638) | Thread deletion failures use blocking `window.alert()` — inconsistent with toast system | Open (workaround active) |
| **—** | [#6869](https://github.com/nearai/ironclaw/issues/6869) (closed) | **Generated DOCX files unreadable by Word** (from 07-29) | **Closed today** — resolved |

**Notable closed bug:** The DOCX corruption issue (#6869) that was first reported on 07-29 was closed today, indicating a difficult, multi-week debugging effort finally landed.

---

## 6. Feature Requests & Roadmap Signals

**In active development (v1.3.0):**

- **Structured automation contracts** (parent #6879): model pinning per automation (#7645), preflight grant verification + standing approval leases (#7646), deterministic no-delivery suppression (#7647), and one-time verification before arming (#7644).
- **Slack-to-Console bridge** ([#7656](https://github.com/nearai/ironclaw/issues/7656), closed today — likely implemented): Slack replies tied back to Console threads with deep links + run metadata.
- **Structured "Ask User" cards in WebUI** ([#7653](https://github.com/nearai/ironclaw/issues/7653)): OMP-inspired `ask` tool — not a resumable gate, but a completion-with-answer pattern.
- **Pluggable memory over MCP** ([#7664](https://github.com/nearai/ironclaw/issues/7664)): Mnesis Core as first consumer; provider crate in draft (#7661).

**Deferred/laddered:**

- **ACP harness executor (v0)**: [#7624](https://github.com/nearai/ironclaw/issues/7624) — claude-code as the loop, dev-only. Explicitly the only pluggable-loops item to build now; #7621–#7623 are a "deferred ladder."

**Likely in next release (v1.3.0+):** The automation hardening suite, pluggable memory (Mnesis), and the Slack bridge all have strong momentum. Per-user LLM selection (#7183) was closed, suggesting it shipped.

---

## 7. User Feedback Summary

**Real user pain points surfacing today:**

- **Automation reliability** (from #6879): "the same stored prompt sometimes succeeds and sometimes produces nothing useful" — users cannot trust unattended runs, particularly on smaller models. This is the single biggest user-facing trust issue.
- **DOCX generation** (#6869, from Davin Basi): "ChatGPT and Claude can do this easily" — a direct competitive comparison where IronClaw failed twice. Closed today, but noteworthy that users compare directly against frontier chatbots for document generation.
- **Login friction** (#7667): A live QA user on `qa-testing-libsql` was blocked from phone-mode login because the code arrived in an unexpected channel and the error message didn't explain where to look. Fixed in #7658.
- **Extension/tenancy confusion** (#7659): Extension state leaking between users undermines trust in the registry as a personal workspace.

**Satisfaction signals:** The rapid fix rate on QA findings (same-day fixes for #7660, #7667) indicates a responsive maintainer team. The Slack deep-link bridge (#7656) responds to a perception that IronClaw needs better cross-platform observability.

---

## 8. Backlog Watch

| Item | Age | Why it matters |
|---|---|---|
| **[#6879 automations epic](https://github.com/nearai/ironclaw/issues/6879)** | 17 days | Longest-running critical issue; not stale (actively worked), but a v1.3.0 blocker with high user impact |
| **[#7624 ACP harness v0](https://github.com/nearai/ironclaw/issues/7624)** | 2 days | Designated as the only pluggable-loops work to build now; others deferred — worth watching for slip |
| **[#7255 APDD governance kit PR](https://github.com/nearai/ironclaw/pull/7255)** | 10 days | Open, no recent maintainer comment; scope/gov process question pending |
| **[#7379/#7378 docs-release PRs](https://github.com/nearai/ironclaw/pull/7379)** | 8 days | Doc-truth track (4/5 and 3/5) — open for over a week; important for docs↔release parity |
| **[#7456 durable storage profile-agnostic](https://github.com/nearai/ironclaw/pull/7456)** | 5 days | XL, medium-risk, long-open — foundational architecture work |

**No items appear abandoned.** The most concerning signals are the **MP4 attachment bug (#7662)** and **extension tenancy leak (#7659)** — both P2 QA bugs without fix PRs yet, both potentially pointing to systemic issues (MIME handling; multi-tenancy isolation).

---

**Overall health: Positive.** High throughput, rapid bug-fix turnarounds, and a clear release plan (v1.3.0) with structured work decomposition. Residual risks: P2 bugs accumulating without fixes, and the automation reliability epic needing to close out before v1.3.0 ships credibly.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-15

## 1. Today's Overview

LobsterAI saw a high-velocity development day. 27 pull requests were updated in the last 24 hours, with an impressive 22 merged or closed versus only 5 still open. The project shipped a new patch release (2026.8.14) and executed a major release merge (`2026.7.30`) that brings substantial new functionality to the main branch. Activity is concentrated on bug fixes, UI polish (sidebar, typography, account credits), and i18n improvements. The issue tracker remains relatively quiet with only 2 items touched, indicating the maintainers are prioritizing PR throughput and release stabilization over new issue triage today.

## 2. Releases

**LobsterAI 2026.8.14** (released 2026-08-14) — patch release.

**What's Changed:**
- **feat(sidebar):** Support check-in and banner carousel — PR [#2411](https://github.com/netease-youdao/LobsterAI/pull/2411)
- **feat(sidebar):** Add multi-agent task activity filter — PR [#2418](https://github.com/netease-youdao/LobsterAI/pull/2418)
- **feat(sidebar):** mov… (truncated in source data)

**Migration/Breaking Changes:** No breaking changes or migration notes were identified in the release notes.

---

**Additionally, a major release merge was completed today:**

- **PR [#2498](https://github.com/netease-youdao/LobsterAI/pull/2498) — Release: 2026.7.30** (merged today, closed) — This merges 67 commits (264 files changed, +24,736/−4,253) from the release branch into `main`. Key highlights include:
  - Introduction of **Team Edition** account and quota flows
  - Refresh of the **Skills and Connectors** experience
  - Cross-cutting changes across renderer, main, openclaw, cowork, docs, IM, artifacts, and Windows platform areas

**Migration implication:** While not explicitly documented in the PR, the Team Edition and quota flows may introduce new account-related configuration expectations. Users on older builds should review the updated account settings after upgrading.

## 3. Project Progress

The project completed 22 PRs today. Key merged/closed items include:

| Area | Change | PR |
|---|---|---|
| **Cowork** | Fix: keep turn process expanded until an answer exists (prevents premature collapse showing empty duration lines) | [#2499](https://github.com/netease-youdao/LobsterAI/pull/2499) |
| **Cowork/UI** | Fix: keep badge popovers within viewport and above later messages | [#2496](https://github.com/netease-youdao/LobsterAI/pull/2496) |
| **Cowork/Artifacts** | Feat: preview browser annotation attachments (full-page screenshots as numbered cards in a dedicated artifact panel) | [#2490](https://github.com/netease-youdao/LobsterAI/pull/2490) |
| **OpenClaw** | Fix: key `skills.entries` by frontmatter name — resolves UI skill toggle being silently ineffective when directory/frontmatter names mismatch (two PRs: [#2491](https://github.com/netease-youdao/LobsterAI/pull/2491), [#2483](https://github.com/netease-youdao/LobsterAI/pull/2483)) | |
| **Typography** | Feat: bump default UI/code font sizes with one-time migration | [#2495](https://github.com/netease-youdao/LobsterAI/pull/2495) |
| **Account** | Fix: update credits icon style (inline SVG, consistent theming) | [#2494](https://github.com/netease-youdao/LobsterAI/pull/2494), [#2492](https://github.com/netease-youdao/LobsterAI/pull/2492) |
| **Session Export** | Fix: session export image and card toggle UI | [#2493](https://github.com/netease-youdao/LobsterAI/pull/2493) |
| **i18n** | Fix: improve cowork goal and steer copy wording | [#2497](https://github.com/netease-youdao/LobsterAI/pull/2497) |
| **Release** | Merged release/2026.7.30 into main | [#2498](https://github.com/netease-youdao/LobsterAI/pull/2498) |

## 4. Community Hot Topics

The issue/PR community activity is moderate today. The most active threads:

- **Issue [#2489](https://github.com/netease-youdao/LobsterAI/issues/2489) — "快更新v4pro！" (Update v4pro quickly!)** — Created yesterday. A user requesting a specific model update. This is a signal of user impatience for a particular capability. 1 comment, no maintainer response visible yet.

- **Issue [#1154](https://github.com/netease-youdao/LobsterAI/issues/1154) — "为 commandSafety 和 coworkMemoryJudge 补充 Vitest 单元测试"** — A long-standing request (created March 31) to add unit tests to two security-critical modules (`commandSafety.ts` for dangerous command detection and `coworkMemoryJudge.ts` for memory quality scoring). The issue is marked stale but was recently touched. It underscores community concern about safety module accuracy, particularly the risk of a false negative causing destructive command execution.

- **PR [#2374](https://github.com/netease-youdao/LobsterAI/pull/2374) — [OPEN] Add permanent setting to hide sidebar ad banner** — Community-driven UX improvement responding to Issue [#2342](https://github.com/netease-youdao/LobsterAI/issues/2342). Addresses the pain point that banner dismissal could only be temporary.

**Underlying needs:** Users want (a) newer/faster model support, (b) control over UI ads, and (c) greater confidence in the safety and memory quality layers of the agent.

## 5. Bugs & Stability

Three notable bug fixes were merged today, ranked by severity:

1. **[HIGH] OpenClaw skill toggle silently ineffective** — PRs [#2491](https://github.com/netease-youdao/LobsterAI/pull/2491) and [#2483](https://github.com/netease-youdao/LobsterAI/pull/2483) fix a key-mismatch bug where skills configured with a directory name different from the frontmatter `name` would not respond to UI enable/disable toggles. *This was a silent configuration-breaking bug; now fixed.*

2. **[MEDIUM] Cowork turn collapse showing false failure** — PR [#2499](https://github.com/netease-youdao/LobsterAI/pull/2499) fixes a UI logic issue where a turn ending mid-wait (e.g., right after a `sessions_yield`) would collapse into an empty duration line, reading as a failure. *Now requires a trailing answer chunk before folding.*

3. **[LOW] Badge popover positioning** — PR [#2496](https://github.com/netease-youdao/LobsterAI/pull/2496) fixes badge popovers overflowing the viewport or appearing behind later messages.

**No crashes or new regressions were reported today.**

## 6. Feature Requests & Roadmap Signals

- **Team Edition & Quota Flows (shipped via [#2498](https://github.com/netease-youdao/LobsterAI/pull/2498))** — The merge of the 2026.7.30 release brings team-oriented features to `main`. This signals a strategic pivot toward multi-user/enterprise scenarios.

- **Sidebar banner carousel and check-in feature** — Released in 2026.8.14 (PRs [#2411](https://github.com/netease-youdao/LobsterAI/pull/2411)) — This is a monetization/engagement feature. The community pushback via the "hide ad banner" PR ([#2374](https://github.com/netease-youdao/LobsterAI/pull/2374)) suggests users want control over these surfaces.

- **Community-requested: v4pro model support** — Issue [#2489](https://github.com/netease-youdao/LobsterAI/issues/2489) asks for a newer model (likely a Next-Gen LLM). Expect this to land in an upcoming release.

- **Long-open feature: In-session Ctrl+F search** — PR [#1155](https://github.com/netease-youdao/LobsterAI/pull/1155) has been open and stale since March, despite a fully built implementation. It is a candidate for merging in a future UI polish cycle.

## 7. User Feedback Summary

- **Ads are annoying:** The new banner carousel feature is prompting users to request a permanent hide option ([#2374](https://github.com/netease-youdao/LobsterAI/pull/2374) responding to [#2342](https://github.com/netease-youdao/LobsterAI/issues/2342)). Comments indicate the dismissal button is not discoverable enough, and ads should be more discreet.

- **Model demand is high:** "快更新v4pro！" (Update quickly!) reflects a strong desire for faster adoption of state-of-the-art models.

- **The community is watchful of safety:** The long open issue about adding tests for `commandSafety` and `coworkMemoryJudge` (Issue [#1154](https://github.com/netease-youdao/LobsterAI/issues/1154)) shows users are aware of, and concerned about, the risk profile of AI executing destructive commands. This is a trust signal that the maintainers should prioritize.

- **Overall sentiment seems positive/neutral**, as no closed issues today indicate user dissatisfaction, and the flow of merged fixes is robust.

## 8. Backlog Watch

Items that have been open a long time without maintainer action:

- **Issue [#1154](https://github.com/netease-youdao/LobsterAI/issues/1154) (opens since 2026-03-31)** — Add Vitest unit tests for `commandSafety` and `coworkMemoryJudge`. Imminent safety-critical gap. *Recommendation: Assign to a maintainer; mark as priority.*

- **PR [#1153](https://github.com/netease-youdao/LobsterAI/pull/1153) (open since 2026-03-31, stale)** — Fix URL construction bug in `buildOpenAIChatCompletionsURL` for Google Gemini base URLs ending in `/v1`, where a character-slicing bug omits the path separator. *Actionable bug fix; needs rebase and merge.*

- **PR [#1155](https://github.com/netease-youdao/LobsterAI/pull/1155) (open since 2026-03-31, stale)** — Fully implemented Ctrl+F in-session search feature using CSS Custom Highlight API. *High-value UX improvement; needs rebase, conflict resolution, and review.*

- **PR [#2374](https://github.com/netease-youdao/LobsterAI/pull/2374) (open since 2026-07-21)** — Add permanent hide for sidebar ad banner. *Directly addresses user pain point; waiting on review/decision.*

---

*Digest generated from GitHub data as of 2026-08-15 for netease-youdao/LobsterAI.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the **Moltis project digest** for **2026-08-15**, based on the provided repository data.

---

### 1. Today’s Overview
Moltis is currently in a **low-activity development phase**. Over the last 24 hours, there were **zero issue updates** (open or closed) and **zero new releases**, indicating a stabilization period or maintainers focusing on deep implementation rather than triage. The sole point of activity is **Pull Request #1190**, which remains open and is awaiting review or further iteration. The project appears to be consolidating its architecture around provider-neutral connectors and persistence layers, with no active bug reports or community disruptions currently surfacing. Overall, project health is stable, with momentum concentrated on a single, substantial feature integration.

---

### 2. Releases
**None.** No new releases, tags, or version bumps were published in the last 24 hours. There are no changelogs, migration notes, or breaking changes to report for this digest period.

---

### 3. Project Progress
**No PRs were merged or closed today.** The only significant item is the **open** PR #1190, which has been updated (last update: 2026-08-14) but not yet accepted. This indicates that the core team is actively engaging with the codebase, likely addressing review feedback. The feature introduced in this PR is substantial, targeting the following advanced capabilities:
- **Provider-neutral connector persistence** with atomic snapshots and scheduling.
- **Bounded local full-text search** capabilities.
- New connectors for **CalDAV, Gmail, and Himalaya v2**.
- Emphasis on **provider-owned schemas** and security (no copied credentials).

This progress suggests the next major milestone will revolve around **robust data synchronization and external service integration**.

---

### 4. Community Hot Topics
The single most active (and only) topic is **PR #1190**:
- **Title:** [OPEN] Add durable calendar, channel, and email connectors
- **Author:** penso
- **Link:** [View PR #1190](https://github.com/moltis-org/moltis/pull/1190)

While the comment count is unspecified, this PR represents the entire current community focus. The underlying need here is clear: users are asking for **reliability and interoperability**. The request for "atomic snapshots," "durable" connectors, and "reusable channel-history datasets" suggests that users are moving beyond simple chat history and demanding that Moltis act as a **centralized, durable hub for all personal communication** (email, calendar, and chat). The emphasis on "no copied credentials" and provider-scoped trust indicates a strong community desire for **privacy and security** in the integration layer.

---

### 5. Bugs & Stability
**No bugs, crashes, or regressions were reported today.** There are zero open issues regarding stability or errors in the last 24 hours. The open PR #1190 does not list any critical bug fixes; its scope is strictly feature additions. The absence of bug reports suggests that the current stable version is performing well in the field, or that the user base is currently focused on testing the new connectors via the PR branch during the review process.

---

### 6. Feature Requests & Roadmap Signals
While no explicit "feature request" issues were filed today, the contents of **PR #1190** serve as the definitive roadmap signal for the next version.
- **Durable Cross-Platform Connectors:** If merged, this will be the headline feature of the next release. Expect support for reading calendar events (CalDAV), email (Gmail/IMAP via Himalaya), and unified channel histories.
- **Local Search:** The "bounded local full-text search" indicates a move toward **offline-first** or **hybrid search** capabilities, allowing users to query their data without relying solely on external APIs.
- **Data Portability & Security:** The design around "provider-owned schemas" and avoiding credential duplication points towards a future where Moltis acts as a **read-only, high-security aggregator**.

**Prediction:** Based on the 3-day update cadence on PR #1190, we predict this feature will be merged and released as **v0.x (minor bump)** within the next 1–2 weeks.

---

### 7. User Feedback Summary
**No direct user feedback (issues or comments) was captured in this window.** However, the existence and content of PR #1190 imply the following user sentiment:
- **Pain Point:** Users are frustrated with fragmented data silos (calendar, email, chat) and need a unified interface.
- **Use Case:** Power users are likely using Moltis for **personal knowledge management** or **AI-agent memory**, requiring the ability to ingest and index data from non-chat sources (like emails and calendar events) to provide context-aware responses.
- **Satisfaction:** The lack of bug reports suggests general satisfaction with the current baseline, while the active development of connectors indicates users are eager for expansion rather than fixes.

---

### 8. Backlog Watch
**Attention Required:** **PR #1190** is now **4 days old** (created 2026-08-11) and has been updated recently, but remains unmerged. For a project with this low volume of activity, this PR is the critical path forward. Maintainers should prioritize a **final review and merge** to unblock downstream testing and to validate the architectural decisions regarding provider-scoped trust. If left stale, this risks creating a bottleneck for future development on top of the connector layer.
- **Action:** Maintainers should explicitly comment on the PR with either requested changes or approval status to keep the community informed.

---

*Digest generated: 2026-08-15*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest
**Date:** 2026-08-15
**Repository:** [github.com/agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw)

---

## 1. Today's Overview

CoPaw shows strong momentum with 50 issues and 41 PRs updated in the last 24 hours. The issue closure rate is high (38 of 50 updated issues are now closed), indicating an efficient triage process, though 12 remain open and active. Development activity is concentrated on the skill system (dynamic loading/unloading), computer use capabilities, and multi-session session management fixes. Notably, there are no new releases today, with the latest version being **2.1.0**. A significant portion of recent issue churn involves the backlog being cleaned up—dozens of issues filed between March and July are being closed out, many with active discussion. Meanwhile, new issues (#7011, #7016, #7025, #7040) continue to stream in, focusing on regression bugs in 2.1.0 and UX friction points. The project remains highly responsive, though the influx of closed issues without visible merged PRs suggests a mix of bug-fix releases and issue cleanup.

---

## 2. Releases

No new releases were published in the last 24 hours. The latest available version remains **QwenPaw 2.1.0**.

---

## 3. Project Progress

Several meaningful merged/closed PRs were finalised today, marking notable progress in multiple areas:

- **[#6969 — fix: avoid duplicate tool result when MCP returns structuredContent](https://github.com/agentscope-ai/CoPaw/Pull/6969)** *(Closed)* — Fixes issue #6958. When a FastMCP-backed tool returns both `content` and `structuredContent`, the adapter now writes a single canonical copy, eliminating duplicate data in tool result files. This is a **bug fix** for a reliability issue surfaced by users.

- **[#7029 — feat(skill-system): 动态技能加载+自动卸载+frontmatter修复](https://github.com/agentscope-ai/CoPaw/Pull/7029)** *(Closed)* — The Chinese-language variant of the skill system PR (see #7031/#7033 below). Introduces dynamic skill lifecycle management: `load_skill`/`unload_skill`/`check_skill_status` tools, an `AutoUnloadHook` that unloads idle skills every 5 turns, and frontmatter path fixes.

- **[#7030 — feat(auto-title-sync): auto-memory linked chat title refresh + observability](https://github.com/agentscope-ai/CoPaw/Pull/7030)** *(Closed)* — Improves chat titles linked to auto-memory. Titles are no longer static placeholders but refresh to reflect evolved conversation topics. An earlier iteration of this PR, [#7032](https://github.com/agentscope-ai/CoPaw/Pull/7032), remains open.

- **[#6943 — feat(channels): support interactive configurators for plugin channels](https://github.com/agentscope-ai/CoPaw/Pull/6943)** *(Closed)* — Restores the ability for plugin channels to register `get_configurator()` methods, enabling interactive configuration via the CLI channel menu. Also uses a temporary FastAPI app to ensure router registration succeeds.

- **[#6715 — feat(onebot): localize inbound media before agent processing](https://github.com/agentscope-ai/CoPaw/Pull/6715)** *(Closed)* — Aligns OneBot inbound media (image, audio, video, file) with the AgentScope 2.0 `DataBlock` pipeline, resolving and downloading remote references into managed local storage before processing.

- **[#2105 — docs: add whisper installation instructions](https://github.com/agentscope-ai/CoPaw/Pull/2105)** *(Closed)* — A long-pending documentation PR (filed March 23) finally merged, adding Whisper (local speech-to-text) setup instructions to README files.

Additionally, **15 PRs were closed/merged** overall in the last day, showing steady feature delivery.

---

## 4. Community Hot Topics

The most active discussions (by comment count) reveal critical needs and recurring pain points:

1. **[#3045 — [Bug]: 自动获取模型为什么不可用 / Why is auto model discovery unavailable?](https://github.com/agentscope-ai/CoPaw/Issue/3045)** *(8 comments, closed)* — Users report that automatic model fetching fails. Dated April 7 but closed out today, this suggests the issue was resolved (likely in a later release) or triaged as a support ticket.

2. **[#2418 — [Question]: 能否在新增skills-hub管理页面 / Skill-hub management page request](https://github.com/agentscope-ai/CoPaw/Issue/2418)** *(7 comments, closed)* — A four-month-old feature request asking for a skill marketplace/manager to "faster and more conveniently download mainstream skills." **Relevance:** Directly tied to the new dynamic skill loading PRs (#7031/#7033), indicating the feature is now being delivered.

3. **[#2846 — [Feature]: Desktop auto-update + taskbar icon fix](https://github.com/agentscope-ai/CoPaw/Issue/2846)** *(6 comments, closed)* — Windows users repeatedly ask for an auto-update mechanism ("每次都要卸载后再更新很麻烦") and a proper CoPaw taskbar icon instead of the generic Python icon.

4. **[#7010 — [Question]: qwenpaw app 只能前台运行 / No true daemon mode](https://github.com/agentscope-ai/CoPaw/Issue/7010)** *(6 comments, closed today, filed 2026-08-14)* — **Active signal.** Users need `qwenpaw app` to support a background/daemon mode when launched via SSH or a script; the current foreground-only mode blocks the shell. This is a deployment/ops concern for server-side use.

5. **[#6405 — [Question]: 升级2.0以后，mcp工具总是提示Tool notfound](https://github.com/agentscope-ai/CoPaw/Issue/6405)** *(6 comments, closed)* — **Recurring regression concern.** After upgrading to 2.0, MCP tools are reported as "not found" despite correctly renamed tool identifiers (`[mcp-key]__[tool_name]`). The issue was closed, but the fix path is unclear — potentially related to the MCP dedup fix (#6969) or a broader 2.1.0 remediation.

6. **[#7011 — [OPEN] Console stop request cancels active Feishu session](https://github.com/agentscope-ai/CoPaw/Issue/7011)** *(5 comments, updated 2026-08-14)* — **Critical bug under investigation.** Session identity values "crossed between two UI sessions," causing a Console UI stop request to cancel an unrelated active Feishu conversation. This is one of the most severe issues currently open.

---

## 5. Bugs & Stability

Several bugs were reported or fixed in the last 24 hours, ranked by severity:

**High Severity (Potential data loss / service interference):**

- **[#7011 — Console stop request can cancel an active Feishu session under multiple UI sessions (2.1.0)](https://github.com/agentscope-ai/CoPaw/Issue/7011)** *(OPEN)* — The reporter explicitly corrected their initial framing: there is "direct evidence of an active Feishu conversation being cancelled by a Console UI stop request after session identity values crossed between two UI sessions." **No fix PR yet.** This is a session safety / isolation bug.

- **[#6951 — Scroll compression hides pre-compaction chat history](https://github.com/agentscope-ai/CoPaw/Issue/6951)** *(closed, 3 comments)* — After `/compact` with `strategy="scroll"`, users re-entering a session only see internal eviction indices and the recent tail, not their original transcript. The raw data remains in `history.db`, but the UI renders compressed `AgentState.context` instead of the full conversation. Context compression should not destroy visible history.

- **[#6405 — MCP tools "not found" after v2.0 upgrade](https://github.com/agentscope-ai/CoPaw/Issue/6405)** *(closed, 6 comments)* — Docker users on `2.0.0.post3` report the tool registry is broken post-upgrade. Closed without an explicit root-cause PR visible; potentially fixed by #6969 or a more recent patch.

**Medium Severity (UX meltdowns / crashes):**

- **[#7025 — QwenPaw Creator plugin disables all other plugins](https://github.com/agentscope-ai/CoPaw/Issue/7025)** *(OPEN, 4 comments)* — Installing the Creator plugin makes every plugin fail. The reporter shared before/after screenshots; logs point to a runtime conflict. This is likely a plugin isolation issue.

- **[#6197 — Frozen Desktop binary hangs on startup when `nvidia-smi` hangs](https://github.com/agentscope-ai/CoPaw/Issue/6197)** *(closed, 3 comments)* — Windows PyInstaller/Tauri build stalls indefinitely if `nvidia-smi` doesn't return. Should be fixed with a watchdog/timeout pattern.

- **[#6972 — Chrome extension WebSocket dies on `tab.create`](https://github.com/agentscope-ai/CoPaw/Issue/6972)** *(closed, 3 comments)* — Browser tool sends a JSON-RPC command but the connection drops immediately, indicating a protocol handling bug in the browser tool.

- **[#6819 — Channel tool does not prompt for approval when required](https://github.com/agentscope-ai/CoPaw/Issue/6819)** *(closed, 3 comments)* — User can't tell if a tool call is pending approval or stuck. A UX/observability bug in the approval workflow.

**Low Severity (Polish):**

- **[#7040 — typo: "Stopp Running"](https://github.com/agentscope-ai/CoPaw/Issue/7040)** *(closed today, 3 comments)* — User flagged broken English copy in the UI ("Stopp Running" instead of "Stop Running"), noting "文案错别字很多" (many typos). Marked invalid/closure, but highlights broader i18n inconsistency.

- **[#4832 — cmd.exe window flash on Windows](https://github.com/agentscope-ai/CoPaw/Issue/4832)** *(closed, 3 comments)* — Missing `CREATE_NO_WINDOW` flag in `execute_shell_command` caushes a distracting cmd flash on Windows. Classic subprocess hygiene bug; likely a quick fix.

---

## 6. Feature Requests & Roadmap Signals

The following user voices are strong signals for the next releases:

1. **Dynamic Skill Lifecycle** *(#2418, #7031, #7033, #7029)* — The skills-hub request is being directly addressed: PR #7033 (#7031 closed variant) adds dynamic loading/unloading of skills, frontmatter fixes, and an `AutoUnloadHook`. **This is near-certain to land in the next minor release.**

2. **Per-Session Model Overrides** *(PR #5992, OPEN — first-time contributor)* — Users want model switching without affecting global defaults. The PR is 30+ days old and marked "Under Review." If merged, it unlocks the workflow requested in #2763 (`/model <provider>-<model>` commands). **Watch this one.**

3. **Session Splitting / Partial Conversation Export** *(#4436, OPEN)* — Ongoing request to move selected messages or turns into a new session to save tokens and preserve context. Related to #4001 (delete single messages). Both remain open and represent the "advanced session management" bucket.

4. **Auto-Update + Native Desktop Polish** *(#2846, #3464)* — Windows users continue to beg for an auto-update mechanism and a proper taskbar icon. Two separate issues with overlapping asks, both closed today — likely tracked as an umbrella roadmap item.

5. **Zero-Setup Local Models** *(#6433, closed)* — Download + run GGUF models in-app using a bundled llama.cpp runtime. This would move CoPaw beyond a thin-client and make it truly self-contained for local-first users.

6. **Computer Use Expansion** *(#5551, closed; PR #7037 OPEN)* — Users are asking about computer use; PR #7037 expands observation to related window surfaces (menus, dialogs, dropdowns). **CoPaw is doubling down on computer-use.**

7. **DataPaw Native Runtime** *(PR #6940, OPEN — first-time contributor)* — A proposed "native DataPaw app runtime and durable analysis workspace." If this is a real datapaw product line, it deserves attention as a strategic direction.

---

## 7. User Feedback Summary

**Real Pain Points (with intensity):**

- **Windows desktop friction is the single loudest complaint:** auto-update, icon bugs, cmd window flashes, silent NVIDIA driver hangs, and the need to fully uninstall before upgrading. CoPaw's Windows desktop experience feels like a second-class citizen.
- **Model configuration is a recurring sore spot:** auto-discovery fails (#3045), MiniMax provider hits unsupported `/models` endpoints (#2303), Azure/OpenAI-compatible gateways require the Responses API (#3002, #944, #2737), and provider history formats block on-the-fly switching (#2314).
- **Context management sorely needs transparency:** scroll-compression hides history (#6951), users want manual message deletion (#4001), session splitting (#4436), and auto-titles that reflect memory updates (PR #7032).
- **Deployment/server-side workflows are underserved:** the absence of daemon mode (#7010) and the Channel tool's silent approval state (#6819) frustrate ops-minded users.
- **Plugin/MCP isolation is fragile:** #7025 (Creator plugin nukes all plugins) and #6958 (duplicate MCP output) both erode trust in the extension ecosystem.

**Satisfaction Signals:**

- The community explicitly praises the direction toward dynamic skills and memory-linked titles.
- First-time contributors are actively landing PRs (#5992, #6940, #2105), and maintainers appear responsive — many old issues are being closed out today, signalling cleanup and velocity.

---

## 8. Backlog Watch

Issues or PRs that are old, high-value, and need maintainer attention:

- **[#5992 — Add per-session model overrides (PR)](https://github.com/agentscope-ai/CoPaw/Pull/5992)** — First-time contributor, "Under Review," opened July 12. This solves a real recurring complaint (#2763, #2314). It needs a maintainer's decision to merge or provide feedback.

- **[#4436 — Support session splitting (Issue)](https://github.com/agentscope-ai/CoPaw/Issue/4436)** — Opened May 16, still open with only 2 comments. It directly addresses token waste and context continuity, but no maintainer has engaged. This is a strong candidate for a roadmap commit.

- **[#4001 — Manual deletion of single chat messages (Issue)](https://github.com/agentscope-ai/CoPaw/Issue/4001)** — Opened May 2, 4 comments, still open. Basic UX expectation; users compare it to WeChat. No maintainer response is visible.

- **[#6433 — Zero-setup local GGUF model download/run (Issue)](https://github.com/agentscope-ai/CoPaw/Issue/6433)** — Closed today after a July 24 filing, but the underlying value proposition (local, llama.cpp, model browser) remains. Watch for follow-up artifact.

- **[#2105 — Whisper docs (PR)](https://github.com/agentscope-ai/CoPaw/Pull/2105)** — Only merged today after being filed March 23. It's an example of a quick win (docs) taking 5 months — a signal that documentation PRs may need lighter triage.

---

*Data current as of 2026-08-15 00:00 UTC. Generated from GitHub API snapshot.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-15

## 1. Today's Overview

ZeroClaw is in a high-velocity stabilization and hardening phase, with 33 issues and 50 PRs updated in the last 24 hours. The project is currently executing against a finite **v0.8.5 stabilization line** (tracker #9459) with intake frozen since August 4, and weekly cuts shipping ready work. Activity is heavily concentrated around security architecture RFCs (authentication, shell policy, egress control) and bug-fixing PRs targeting critical reliability issues, including a new wave of fixes submitted today (#9999, #10002, #10001). Notably, no new releases were published this cycle, and maintainer attention is clearly focused on merging a large backlog of high-risk, large-size PRs, many of which are marked `needs-author-action`. While the volume is strong, the high number of RFCs awaiting maintainer review suggests a substantial decision-making bottleneck.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

The last 24 hours saw 3 merged/closed PRs, but they were not listed in the top 20 by comment count. The most notable closings in issues were one `wontfix` (#9982) and a merged Telegram feature (#6663). Key features and fixes that advanced toward merge across the open PR backlog include:

- **Security: Atomic Action Budget Accounting** (#9996): Audacity88's PR makes action-budget accounting atomic, preventing parallel tool calls from exceeding limits.
- **Provider Reliability: Output-Limit Classification** (#9999): vrurg's PR classifies `finish_reason: "length"` responses as typed output-token-limit failures, addressing the critical issue #9421.
- **Config Fixes**: PR #9707 migrates bare `vision_model_provider` settings to dotted alias refs, and #9281 improves transactional rollback for `config/set`.
- **Channel & Web**: PR #9002 keeps agent turns alive after dashboard viewer disconnect; PR #9574 authorizes approval responders across Slack, Telegram, Lark, and Matrix; PR #8443 adds single-message progress drafts for Matrix.
- **CI Optimization**: A series of stacked PRs (#9962, #9985) extend Blacksmith runner support and provider-aware caching to improve CI speed and reliability.
- **ZeroCode & Tools**: PR #9994 adds a transcript copy context menu to ZeroCode; #10002 fixes camelCase validation for Google Workspace tools; #10001 gates non-UTF-8 browser path tests to Linux only, addressing Windows test failures.

## 4. Community Hot Topics

The most active discussions revolve around Security Architecture and Escalated Privileges for the Agent. These are the top discussions, ranked by engagement:

| Issue/PR | Title & Link | Comments | Analysis |
| :--- | :--- | :--- | :--- |
| #8303 | **RFC: Goal mode v1 — bounded foreground Matrix work** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)) | 22 | The community is deeply engaged in defining how an agent should handle long-lived, multi-turn goals. High engagement signals a strong desire for a more structured, bounded execution model beyond simple prompt-response loops. |
| #7155 | **RFC: Per-execution confirmation tier for high-risk shell commands** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)) | 20 | This is a hot topic, centering on a Claude Code-style `allow/ask/deny` policy for shell commands. This indicates users need more granular, secure control over agent execution, making it a likely candidate for the next major security milestone. |
| #8603 | **RFC: ZeroClaw Chat Completions profile** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)) | 19 | High interest in offering an OpenAI-compatible API endpoint. This is a major integration signal, suggesting users are looking to plug ZeroClaw into established tools (Open WebUI, LobeChat, Aider, LangChain) but are currently blocked by the lack of this protocol. |
| #7141 | **RFC: Pluggable inbound authentication and canonical principals** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)) | 16 | Users and maintainers are focused on moving beyond basic API keys to standard, pluggable identity (OIDC, etc.) with a canonical principal model, indicating enterprise adoption pressure. |
| #7462 | **[Bug]: 74 test failures on Windows** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)) | 15 | The active engagement on Windows test failures is a clear sign of a growing Windows user base facing stability issues. This is a significant quality gate for the project's portability. |
| #9487 & #9488 | **RFC: Runtime-owned conversation sessions & Unified attachment architecture** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/9487), [#9488](https://github.com/zeroclaw-labs/zeroclaw/issues/9488)) | 14 each | The discussion around runtime-owned sessions and unified attachments comes from the same author (NiuBlibing), signaling a need to centralize core session/attachment logic in the runtime rather than in channel-specific code. This is a strong architectural direction for the "Web" and "Gateway" milestones. |

## 5. Bugs & Stability

While no new bugs were *filed* today, the PR activity reveals a major push to fix critical, long-standing stability issues. This is a strong sign of a release-hardening phase. The most severe are:

- **S1 - Workflow Blocked: Incomplete terminal responses reported as successful** ([#9421](https://github.com/zeroclaw-labs/zeroclaw/issues/9421)): A provider can end a turn without a trustworthy final answer, yet ZeroClaw reports success. This is a critical trust issue for automation. **Fix PR:** [#9999](https://github.com/zeroclaw-labs/zeroclaw/pull/9999) is actively working to address this.
- **S2 - Degraded Behavior: Windows test failures** ([#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)): 74 tests fail on Windows due to Unix-only commands and path semantics. **Fix PRs:** None directly addressed it, but [#10001](https://github.com/zeroclaw-labs/zeroclaw/pull/10001) is a related fix for a browser test. This remains a major portability blocker.
- **S2 - Degraded Behavior: High-entropy detector redacts Solana wallet addresses** ([#9486](https://github.com/zeroclaw-labs/zeroclaw/issues/9486)): The leak detector is over-aggressive, redacting legitimate crypto addresses on the Telegram channel, making the agent useless for finance use cases.
- **S1 - Workflow Blocked (CI): cron custom-shell test hits ETXTBSY under parallel runtime gate** ([#9965](https://github.com/zeroclaw-labs/zeroclaw/issues/9965)): This CI flakiness is causing unrelated PRs to fail, blocking progress.
- **S2 - Degraded Behavior: Qdrant silently falls back to MarkdownMemory in builder-only factory** ([#9919](https://github.com/zeroclaw-labs/zeroclaw/issues/9919)): Can silently select the wrong persistence layer, leading to data loss or misconfiguration.

## 6. Feature Requests & Roadmap Signals

The current cycle is strongly focused on the **"v0.8.5 stabilization line"** (#9459). Looking at the RFCs in the queue, the roadmap beyond this cycle is heavily oriented toward security and ecosystem integration, with the following features likely to be in upcoming versions:

- **Security & Compliance:** Pluggable auth (#7141), runtime-owned security decision pipeline (#7142), and per-execution shell confirmation (#7155) are all accepted/high-priority RFCs and clear next moves for a security milestone.
- **Interoperability:** The **Chat Completions API** (#8603) is the strongest signal for the next "integration" milestone, opening up the entire OpenAI client ecosystem.
- **Architecture & Extensibility:** The unified catalog (#9346), runtime-owned sessions (#9487), and shared plugin egress (#9137) point to a more robust, plugin-friendly core architecture.
- **Operational Experience:** New trackers for harness evaluation (#9967) and localization cleanup (#9972) indicate the project is beginning to invest in developer velocity and quality-of-life for larger teams.

## 7. User Feedback Summary

- **Pain Point: Fortress Security Needs.** Users are actively engaging in detailed RFC discussions around shell command policies, credential boundaries, and granular agent permissions, showing a need for fine-grained, auditable control before scaling up.
- **Pain Point: Ecosystem Blockage.** The strong desire for a Chat Completions API (#8603) indicates users are currently locked out of popular AI tools and are *demanding* an OpenAI-compatible surface.
- **Satisfaction:** The `merge` of the Telegram tool-call progress feature (#6663) so quickly is a positive signal, showing maintainers listen to UX requests.
- **Dissatisfaction: Platform Gap.** The proliferation of Windows and Linux test failures (#7462, #10001) is a source of friction for a growing non-Linux user base, directly impacting trust in the project's cross-platform claims.
- **Dissatisfaction: Notification/Redaction Abuse.** The Solana wallet redaction bug (#9486) is a classic case of a security feature causing severe functional harm, frustrating users in crypto/web3 domains.

## 8. Backlog Watch

This section highlights important items that appear stalled or need imminent maintainer attention to unblock progress.

- **Blocked: Active shell dialect in system prompt** ([#9788](https://github.com/zeroclaw-labs/zeroclaw/issues/9788)): Marked `status:blocked`. Waiting on a dependency or decision but is a critical improvement for agent accuracy.
- **Large PRs in Need of Author Action:** A huge fraction of the PR backlog (e.g., #9137, #8443, #9713, #9420) are marked `needs-author-action`. This indicates that revisions have been requested, and the ball is in the contributor's court. The project needs these authors to cycle back to keep momentum.
- **Maintainer-Review Queue:** A clear queue of high-risk RFCs await maintainer review (e.g., #8603, #6971, #6954, #9621). The `needs-maintainer-review` label on these items is a critical bottleneck for architectural decisions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*