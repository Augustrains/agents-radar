# OpenClaw Ecosystem Digest 2026-08-04

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-04 01:16 UTC

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

# OpenClaw Project Digest — 2026-08-04

## 1. Today's Overview

OpenClaw shows very high activity on 2026-08-04: 500 issues and 500 PRs were updated in the last 24 hours, with 31 issues closed and 168 PRs merged/closed. Two patch releases (v2026.7.1-1, v2026.7.1-2) shipped with targeted reliability fixes for npm plugin updates and Codex progress replies. The maintainer team (led by `vincentkoc`) is actively filling QA coverage gaps with a wave of new test PRs (`#118813`, `#118862`, `#119021`, `#119028`, `#119031`, `#119032`), signalling a push toward production-readiness hardening. However, the project is carrying a notable backlog of high-severity (P0/P1) bugs around session-state integrity and message loss, many of which await maintainer review or product decisions.

## 2. Releases

**v2026.7.1-2** — Patch release. Fixes npm plugin updates: accepts singleton-array metadata from newer npm clients so tracked official plugins install/update correctly. No breaking changes or migration notes.

**v2026.7.1-1** — Patch release. Two fixes:
- **Codex progress replies:** keeps app-server turns running after delivered progress messages so GPT/Codex reaches its authoritative terminal response (fixes #106961, #108487).
- **Memory Core startup repair:** recovers derived legacy-index and cache state on startup.

Neither release introduces breaking changes or requires migration.

## 3. Project Progress

Merged/closed today include QA and reliability PRs. Notable merged/closed items:

- **#118813 (closed)** — Gateway update/setup RPC QA coverage (maintainer, `vincentkoc`). Closes a gap in `wizard.*` setup lifecycle proof.
- **#118275 (open, in active triage)** — MCP tool filters now accept projected names (e.g., `docs__read-page`), aligning `toolFilter` with probe output — low-risk compatibility fix.
- **#118013 (open)** — CLI health summaries now surface failed plugins; visibility-only fix that leaves the underlying metadata ownership bug open.
- **#118261 (open)** — Fixes 500ms grace-window race in Control UI Talk-mode fallback (P1, UI).
- **#119017 (open)** — CI budget fix: macOS Swift runner timeout now bounds forks so fork PRs finish.

A significant cluster of new QA/coverage PRs from `vincentkoc` today: `#118862` (vision channel offload), `#119021` (workspace mutation tools), `#119028` (agent session streaming), `#119031` (live search continuity), `#119032` (session scope continuity). These are test-only additions, not product changes.

## 4. Community Hot Topics

The most active issue by far is **#116277** (100 comments, closed) — *DeepSeek v4 Flash silent reply failure*. A "diamond lobster"-rated P1 bug where the model silently generated no reply and OpenClaw posted a generic fallback. Users are clearly frustrated; the issue is closed but a linked PR appears open, suggesting a fix may be in flight.

**#116201** (50 comments, open) — *Realtime voice work retains unbounded provider/consult state*. Diamond-lobster P1; maintainer-tagged and awaiting product decision on resource limits. This is a design-level problem, not a quick patch.

**#7707** (24 comments) — *Memory Trust Tagging by Source* — long-open feature request (since Feb) with security implications (memory-poisoning prevention). Still awaiting maintainer review, and represents a growing concern about prompt-injection via ingested content.

Other active items: **#44925** (23 comments) and **#67777** (11 comments) both concern subagent completion silently lost on timeout/drain/orphan — a recurring theme. **#48788** (20 comments) asks for a centralized filename-encoding utility for multi-encoding Content-Disposition across channels.

**Underlying needs:** users are pushing for deterministic session/agent lifecycle (no silent message loss), stronger security boundaries (memory trust, config redaction), and better observability (trace contexts, resolved-model exposure, health summaries).

## 5. Bugs & Stability

Ranked by severity (P0 first), with fix status:

**P0**
- **#103804** — *service-env generator double-quotes values, breaking `AWS_REGION` hostname* — auth-provider, release-blocker severity (diamond lobster). A PR is open (#108979 is unrelated; this has a linked PR per labels). Configuration breaking is high-impact but narrow.

**P1 (session-state / message-loss cluster)** — several have linked open PRs:
- **#116277** (closed) — DeepSeek v4 Flash silent reply failure — likely fixed (linked PR open).
- **#116022** — `/new` reuses stable session ID, cannot recover retired Codex binding tombstone (2026.7.2-beta.5) — linked PR open.
- **#114234** — Usage-cost refresh lock never released after restart reusing owner PID in containers; permanently freezes cache — linked PR open.
- **#116010** — All persistent sessions capped at 128k context regardless of model (2026.7.x) — linked PR open. This is a severe regression for large-context models.
- **#115700** — `chat.send` rejected with "thread switched branches" after model completes (stale `expectedLeafEntryId`) — 2026.7.2 — linked PR open.
- **#115037** — Synthetic "No response requested." on resume triggers model fallback; user turn silently served by downgraded model — linked PR open.
- **#84516** — Codex app-server replies silently truncated at ~1000–1100 chars (stop=null, aborted=false) — no fix PR; awaiting maintainer + live repro.
- **#87744** — Codex-backed Telegram turns repeatedly time out waiting for `turn/completed` (2026.5.27) — no fix; awaiting maintainer/live-repro.
- **#52249** — ACP parent session stuck until refresh when child completes — no maintainer decision yet.
- **#44925 / #67777** — Subagent completion lost on timeout/drain/orphan — both diamond lobsters, no fix PR.

**P1 (other)**
- **#45494** — Cron jobs silently time out during sustained LLM API outages instead of fast-failing — regression, awaiting maintainer.
- **#44502** — Discord routing/mention-gating regression — awaiting maintainer.
- **#53408** — Write/exec tool parameters silently dropped after long conversations — awaiting maintainer.

**P2 notable regressions**
- **#112906** — `` (collapsible) tags render broken in v2026.7.1/v2026.7.1-2 with richMessages — a visible UX regression in the latest release; no linked fix yet.

**Fix PRs in flight (good news):** Several fixes are circulating with "ready for maintainer look": `#117887` (proxy SSE body close), `#117998` (tlon SSE watchdog), `#117339` (reject non-binary video downloads), `#118211` (redact signed cloud credential params — security), `#94299` (codex root memory in bootstrap), `#81185` (redact exec result payloads — long-running, security).

## 6. Feature Requests & Roadmap Signals

Active requests with traction (by comments/reactions):

- **#7707** — *Memory Trust Tagging by Source* (24 comments) — security-motivated; would prevent memory poisoning. Diamond-lobster rated; likely a candidate for next major.
- **#42840** — *MathJax/LaTeX rendering in Control UI* (👍10) — clear user desire for math support; low-risk UI addition, plausible for a near-term release.
- **#45508** — *Self-hosted STT/TTS provider support in webchat* (👍2) — route webchat through gateway instead of browser APIs; aligns with self-hosting posture.
- **#51441** — *Expose resolved backend model in session_status* — observability win, small surface; likely to land.
- **#47910** — *Provider fallback by failure class (quarantine auth-broken providers)* — reduces latency/cost; architecture-adjacent, product decision needed.
- **#91044 / #91144 (Windows)** — Windows native CLI gateway scheduled task doesn't stay running; community request for Windows parity.
- **#46058** — *Chat-first Android surface* (discussion) — user is building a fork; maintainers may upstream pieces.
- **#73537** — *Production-readiness stability labels on releases* (👍2) — user (family/business assistant) wants clearer stability signals.

**Prediction:** The next minor or patch likely includes: `#118275` (MCP projected names), `#118998` (TUI terminal-control blocking, security), `#119006` (thinking-level change for non-owners, has security-boundary risk so may need review), and `#119040` (cron wake-only payload). Memory-trust tagging (#7707) is a strong candidate for the next feature-minor given its security framing and community interest.

## 7. User Feedback Summary

**Positive sentiment:** Users continue to rely on OpenClaw for family/business automation (Telegram, cron, Home Assistant; see #73537) and express appreciation for the project. The maintainer team's rapid release cadence (two patches in a day) is responsive to regressions.

**Pain points (recurring):**
1. **Silent message loss** — the dominant theme across top issues (#116277, #44925, #67777, #84516, #87744, #44502). Users repeatedly report the bot does nothing (or posts a generic fallback) without warning, eroding trust.
2. **Session-state fragility** — the "thread switched branches" (#115700), `/new` tombstone (#116022), and context-cap regression (#116010) show persistent-state management is fragile across restarts and model fallbacks.
3. **Observability gaps** — users cannot tell why a session is stuck, what backend model served them (#51441), or why health reports say "unavailable" while the gateway works (#57256).
4. **Configuration friction** — double-quoted env values breaking `AWS_REGION` (#103804, P0), `OPENCLAW_HOME` nested-dir regression (#45765, closed), and `replyToMode` overrides rejected across eight bundled channels (#119030, PR open).

**Satisfaction signals:** Users provide detailed repro guides and even audit logs (e.g., #44134 Google ban, #116201 realtime voice) — indicating deep engagement and willingness to help. The diamond-lobster rating system (community-tagged severity) suggests users feel heard, but the volume of P1s awaiting maintainer review indicates a review bottleneck.

## 8. Backlog Watch

Long-standing, high-importance items needing maintainer attention (older than 30 days, no linked fix):

- **#7707** (Feb 3) — *Memory Trust Tagging* — 24 comments, security; needs product decision.
- **#44925** (Mar 13) — *Subagent completion silently lost* — 23 comments, diamond lobster, P1; no fix PR. This is the single most-echoed reliability bug.
- **#48788** (Mar 17) — *Centralized filename encoding utility* — 20 comments, P3; needs a maintainer to greenlight the cross-channel refactor.
- **#40786** (Mar 9) — *`.gitignore`-like excludes for backup CLI* — 10 comments, security (can't exclude `.env`); needs security review + product decision.
- **#45494** (Mar 13) — *Cron jobs time out on sustained API outages* — regression, P1; needs maintainer to confirm fast-fail behavior.
- **#53408** (Mar 24) — *Write/exec params silently dropped after long conversations* — P1, 9 comments; no repro from maintainers.
- **#50291** (Mar 19) — *Plugin hooks missing trace context* — P2, observability; no maintainer decision.
- **#44134** (Mar 12) — *Google Antigravity ban due to tool-schema reload spam* — P1, has product/security implications; 7 comments.
- **#46031** (Mar 14) — *`auth.order` ignored for GitHub Copilot provider* — P2, linked PR open; needs review.

**PRs waiting on author (stale but important):** `#81185` (exec redaction, security), `#118862`, `#118813` (QA), `#111609` (reef JSONL OOM guard), `#94299` (codex memory bootstrap).

**Health verdict:** OpenClaw is shipping fast and its maintainers are actively closing QA gaps, but the backlog of P1 session-state/message-loss bugs — many months old — suggests the core runtime needs a sustained reliability pass, not just patch fixes. The community is engaged and technical, and the diamond-lobster tagging system is surfacing the right priorities; the bottleneck is maintainer review capacity, not reporter diligence.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — AI Agent & Personal Assistant Open-Source Ecosystem
**Date: 2026-08-04**

---

## 1. Ecosystem Overview

The open-source personal AI assistant landscape is characterized by high-velocity development across a spectrum of projects ranging from large, feature-complete frameworks (OpenClaw, Hermes Agent, CoPaw) to nimble, focused tools (NanoBot, PicoClaw, NullClaw). A dominant theme across all active projects is **reliability hardening** — particularly around silent message loss, session-state integrity, and provider interoperability — as users increasingly deploy these systems for production and family/business automation. Security is emerging as a second major axis, with projects like ZeroClaw and Hermes Agent shipping dedicated hardening sprints (SSRF gates, credential redaction, API-key migration). The ecosystem is bifurcating: large projects are formalizing release cadences and architectural RFC processes, while smaller projects are consolidating rapid community-contributed fixes. Cross-cutting user demands include deterministic lifecycle behavior, observability (trace contexts, resolved-model exposure), and config-driven flexibility across an expanding multi-channel (Telegram, Discord, Slack, Mattermost, Signal) and multi-provider (Anthropic, OpenAI, DeepSeek, Gemini, Ollama) landscape.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed PRs | Release Status | Health Score* | Notes |
|---|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 168 | v2026.7.1-2 (2 patches today) | ⭐⭐⭐⭐ | Very high activity; production-hardening wave |
| **Hermes Agent** | 50 | 50 | 4 | v0.20.0 "Herald" (Aug 3) | ⭐⭐⭐⭐ | Post-release triage; 1,200 issues closed in cycle |
| **IronClaw** | 45 | 50 | 18 | Pre-release; PR #5598 pending | ⭐⭐⭐ | Intense "Reborn" refactoring; CI churn |
| **CoPaw (QwenPaw)** | 22 | 50 | 24 | v2.1.0-beta.1 (Aug 3) | ⭐⭐⭐⭐ | Fast cadence; contributor diversity strong |
| **ZeroClaw** | 50 | 50 | 3 | Consolidating for v0.9.0 | ⭐⭐⭐ | RFC-heavy; security-focused |
| **NanoBot** | 1 (new bug) | 36 | 25 | No release; consolidating | ⭐⭐⭐⭐ | High merge velocity; WebUI/UX polish |
| **PicoClaw** | 8 | 6 | 3 | 0.3.1 (stable) | ⭐⭐⭐ | Moderate; MCP hang critical |
| **NanoClaw** | 1 | 9 | 6 | No release | ⭐⭐⭐⭐ | Healthy; image repin prep |
| **NullClaw** | 1 | 5 | 2 | No release | ⭐⭐⭐ | Focused; proxy/streaming work |
| **LobsterAI** | 2 | 11 | 6 | No release | ⭐⭐⭐ | 4 stale PRs; feature dev active |
| **Moltis** | 0 | 1 | 0 | No release | ⭐⭐ | Single-feature focus |
| **TinyClaw / ZeptoClaw** | 0 | 0 | 0 | No activity | ⭐ | Inactive |

*Health Score: composite of activity, responsiveness, fix velocity, and backlog health (5-star scale).

---

## 3. OpenClaw's Position

**Advantages over peers:**
- **Scale of activity:** 500 issues/PRs updated and 168 PRs merged in 24h dwarfs all competitors (next closest: IronClaw and CoPaw at ~50). OpenClaw is the clear ecosystem leader in community engagement.
- **Release cadence:** Two patch releases in a single day demonstrates exceptional responsiveness to regressions — unmatched in this cohort.
- **Community severity-tagging system:** The "diamond lobster" rating mechanism enables community-driven prioritization that other projects lack, surfacing P0/P1 bugs with remarkable clarity.
- **QA investment:** A wave of dedicated coverage PRs (#118813, #118862, etc.) signals production-readiness maturity beyond most peers.

**Technical approach differences:**
- OpenClaw's architecture spans gateway, MCP integration, memory core, and provider routing with deep plugin support — broader surface area than NanoBot or PicoClaw, positioning it as a full-stack assistant rather than a channel adapter.
- Explicit "session-state integrity" as a first-class concern (context caps, tombstone recovery) contrasts with smaller projects that treat sessions as ephemeral.

**Community size comparison:** OpenClaw's 500/500 issue/PR volume is ~10x IronClaw and CoPaw, ~50x NanoBot, and >500x Moltis. It is the clear reference implementation for the ecosystem.

**Weakness:** The P1 backlog (session-state/message-loss cluster) is larger than peers, suggesting the maintainer review capacity is the bottleneck — a challenge smaller projects have not yet hit at this scale.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|---|---|---|
| **Silent message/subagent loss prevention** | OpenClaw (#116277, #44925), CoPaw (#6614), Hermes (#67498) | Deterministic lifecycle; no generic fallbacks; visible delivery status |
| **Session-state integrity / context management** | OpenClaw (#115700, #116010), CoPaw (#6588), PicoClaw (#3301) | Context caps per model; tombstone recovery; auto-compaction for routed agents; batch placeholder normalization |
| **Provider interoperability & fallback** | OpenClaw (#118275), NanoBot (#5214), CoPaw (#6659), NullClaw (#964), ZeroClaw (#9419) | Model-specific parameter validation (Opus 5 temperature); fallback with cooldown; credential rotation; streaming tool-call deltas |
| **Security hardening** | ZeroClaw (SSRF, approval auth), Hermes (API keys → .env, NUL-byte exploit), OpenClaw (#7707 memory trust), CoPaw (#6657) | Memory-poisoning prevention; credential redaction; sensitive-path guards; config validation |
| **Observability & transparency** | ZeroClaw (OTel trace), OpenClaw (#51441 resolved-model), Hermes (#78087) | Trace contexts; resolved-backend exposure; health summaries; structured telemetry events |
| **WebUI/UX polish & i18n** | NanoBot (#5226–5229), PicoClaw (#3273 Japanese), CoPaw (inbox UI), Hermes (pt-BR, #78081) | Mobile UX; IME handling; localization; slow-network resilience |
| **Channel parity & lifecycle** | PicoClaw (#3315 Telegram topics), CoPaw (WeChat), Hermes (Telegram hang), ZeroClaw (Nextcloud Talk), NullClaw (proxy) | Per-channel policies; topic support; proxy routing; gateway lifecycle handoff |
| **Self-hosted deployment & Windows parity** | Hermes (Windows bugs), OpenClaw (#91044), PicoClaw (systemd) | Native Windows support; headless deployment guides; installer reliability |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | CoPaw | ZeroClaw | NanoBot | PicoClaw |
|---|---|---|---|---|---|---|
| **Primary focus** | Full-stack assistant framework | Desktop-first agent with skills ecosystem | Desktop app + multi-agent missions | Architecture-hardening + RFC-driven | Lightweight multi-channel gateway | Self-hosted multi-agent router |
| **Target user** | Power users, family/business automation | Enterprise/desktop users, Obsidian/Notion users | Chinese-speaking desktop users, API integrators | Security-conscious, RFC-engaged developers | Developers wanting quick multi-channel deployment | Raspberry Pi/self-hosters |
| **Architecture** | Monolithic with plugin/MCP ecosystem | Desktop app + gateway + skills | Desktop app + SSE API | Layered (WS2/WS3) refactoring | Gateway with provider adapters | Dispatch-rule routing |
| **Key strength** | Scale, community severity tagging | Skills marketplace, credential pool | Fast desktop cadence, API automation | Security-first design process | Merge velocity, i18n polish | Lightweight, privacy-focused |
| **Key weakness** | P1 backlog bottleneck, maintainer capacity | Windows parity gap, Telegram regressions | agentscope dependency fragility | Decision queue congestion, slow releases | No major release yet; small community | MCP hang bug; single maintainer fatigue |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapid iteration / high momentum:**
- **OpenClaw** (500 issues/PRs, 2 patches/day) — Production hardening; the reference project.
- **CoPaw** (50 PRs, 24 merged, beta release) — Fastest feature cadence; contributor diversity (first-timers active).
- **NanoBot** (25 PRs merged) — Consolidating a large batch toward imminent release.

**Tier 2 — Active development / architectural shifts:**
- **IronClaw** — High churn but focused on internal refactoring (WS2/WS3); user-facing features temporarily secondary.
- **ZeroClaw** — Security/architecture hardening with RFC queue; release paused for v0.9.0 consolidation.
- **Hermes Agent** — Post-v0.20.0 triage; massive release scale (~3,650 commits) suggests ongoing stabilization.

**Tier 3 — Steady but moderate:**
- **PicoClaw, NanoClaw, NullClaw, LobsterAI** — Healthy community contributions but smaller scale; some stale-backlog risks.
- **Moltis** — Quiet; single-feature focus.

**Tier 4 — Inactive:**
- **TinyClaw, ZeptoClaw** — No activity; possibly dormant.

---

## 7. Trend Signals

**For AI agent developers, the following industry trends emerge from community feedback:**

1. **Reliability is the new feature.** The #1 cross-project complaint is silent failure (no output, generic fallbacks, lost subagent results). Users are demanding deterministic behavior over novel capabilities. *Action:* Instrument all failure paths; fail loudly with actionable context.

2. **Context management is a first-class engineering problem.** Session-state fragility (tombstones, context-cap regressions, route-specific compression) spans OpenClaw, CoPaw, PicoClaw. The era of "infinite context" is over; explicit lifecycle management is table-stakes.

3. **Provider abstraction is brittle.** Model-specific quirks (DeepSeek reasoning malformed, Opus 5 temperature deprecation, Gemini replay errors) break clients. *Signal:* The industry needs declarative provider capability manifests, not hardcoded validation.

4. **Security is shifting from network to prompt/memory.** Memory-poisoning prevention (OpenClaw #7707), credential redaction (Hermes, OpenClaw), and approval audit integrity (ZeroClaw) indicate a move toward defending the agent's data plane, not just the control plane.

5. **Observability is a competitive moat.** Users increasingly demand trace contexts, resolved-model exposure, and structured telemetry to debug complex multi-turn loops. Projects with strong OTel integration (ZeroClaw) are ahead.

6. **i18n and channel parity are growth drivers.** Japanese localization (PicoClaw), pt-BR (Hermes), and Mattermost/Telegram topic support signal global adoption and production diversity. Non-English users are active, detailed reporters.

7. **Windows and self-hosted parity remain underserved.** Native Windows bugs (Hermes, OpenClaw) and headless/serenity deployment guidance (PicoClaw, OpenClaw) represent a persistent gap — and an opportunity for projects that invest here.

8. **The "assistant" is becoming a "multi-agent orchestrator."** Cross-session memory (NanoBot #5211), goal mode (ZeroClaw #8303), and routed-agent context management (PicoClaw #3316) all point toward agents that manage tasks and sub-agents autonomously over time — with the ecosystem still converging on safe patterns.

---

*Report generated 2026-08-04 from public GitHub activity data.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest - 2026-08-04

## Today's Overview

NanoBot is experiencing a substantial development spike, with 36 pull requests updated in the past 24 hours—the majority (25) being merged or closed, indicating a healthy, fast-moving merge pipeline. Activity is clustered around cross-cutting fixes for the WebUI (i18n, mobile keyboard, IME input), provider interoperability (DeepSeek reasoning, Gemini replay), and resource lifecycle management. A single new bug was opened today concerning Anthropic's newly released Opus 5 model, while one older MIME-type frontend issue was resolved. No new releases were published today, suggesting the project is consolidating a large batch of work toward an upcoming version.

## Releases

No new releases were published in the last 24 hours. The high volume of merged PRs (25) suggests a significant release may be imminent.

## Project Progress

A wide-ranging set of fixes and features were merged today across several key areas:

**WebUI Polish (PRs #5226–#5229):** A concentrated push by contributor `chengyongru` addressed mobile UX and internationalization. These fixes include dismissing the mobile keyboard after message send (#5226), completing a full i18n audit with corrected Simplified/Traditional Chinese terminology (#5227), showing actual local trigger messages in the session popover (#5228), and stabilizing the thread scroll position during IME composition input (#5229).

**Provider Reliability (PRs #5214, #5230, #5204):** Significant work was done to harden provider interoperability. A high-priority fix keeps DeepSeek reasoning items wire-valid for the OpenAI Responses API (#5214), while another drops unsigned tool calls when replaying history to Gemini models to avoid `400 INVALID_ARGUMENT` errors (#5230). A separate open PR declares Responses capabilities declaratively for OpenAI, GitHub Copilot, and DeepSeek (#5204).

**Lifecycle & Infrastructure (PRs #5213, #5215, #5141):** Resource and teardown stability was improved—the gateway now closes agent resources deterministically on stop, preventing asyncio noise (#5215). Plugin installation now falls back to `uv` when `pip` is unavailable in `uv tool` environments (#5213), and cron expressions are now validated at creation time to fail fast with clear `ValueError` messages (#5141).

**Memory & Data Integrity (PR #5221):** The memory store's efficient tail-read of `history.jsonl` was hardened against invalid UTF-8 splits mid-character.



**Documentation & New Providers:** ModelScope (魔搭) provider documentation was added (#5038), and Eden AI was merged as a built-in OpenAI-compatible gateway provider (#4861).

## Community Hot Topics

The most active PRs today (all with minimal comment counts but high structural interest) show a clear pattern of community-driven multi-provider expansion and configuration flexibility:

- **[PR #5233/#5232: feat(mattermost): separate group policy for threads and expose in WebUI](https://github.com/HKUDS/nanobot/pull/5233)** — A follow-up to the Mattermost channel support, this seeks to give admins distinct mention-requirement policies (`groupPolicyInThread`) for threads versus main channels, exposed in the WebUI. The duplicate open/closed pairing suggests rapid iteration.
- **[PR #5234: feat(agent): integrate mst-python as a metasearch provider](https://github.com/HKUDS/nanobot/pull/5234)** — Adds the Meta-Search Tool, which aggregates results from DuckDuckGo, Google, Brave, and Bing using Reciprocal Rank Fusion, pointing to user demand for richer, aggregated web search results.
- **[PR #5211: feat(session): add cross-session search and mentions](https://github.com/HKUDS/nanobot/pull/5211)** — Introduces bounded, read-only access to persisted conversations, letting users mention and cite other sessions—a strong signal of users wanting better multi-turn/multi-context continuity and citation ability.

**Underlying Need:** The pattern of these PRs—thread-specific policies, aggregated search, cross-session references, and dual-mode provider auth (see #1550)—reveals a user base deploying NanoBot in increasingly complex, production-grade multi-channel environments, demanding finer-grained control and higher autonomy.

## Bugs & Stability

One new bug was reported today, and several critical stability fixes were merged.

**New Issue (High Severity):**
- **[Issue #5235: Anthropic Opus 5 configuration always rejected](https://github.com/HKUDS/nanobot/issues/5235)** — The newly released `claude-opus-5` (2026-07-24) has fully deprecated the `temperature` parameter, but NanoBot's client-side `omit_temperature` substring list still lacks `"opus-5"`, causing every request to Opus 5 to be rejected by the API. This is an urgent compatibility issue for users adopting the latest Anthropic model.

**Fixes Merged (High Severity):**
- **[PR #5215: fix(gateway): close agent resources deterministically](https://github.com/HKUDS/nanobot/pull/5215)** — Addresses shutdown hangs and `RuntimeError: Event loop is closed` noise when stopping with running exec sessions or MCP subprocesses.
- **[PR #5214: fix(providers): keep DeepSeek reasoning wire-valid](https://github.com/HKUDS/nanobot/pull/5214)** — Fixes a serde-style deserialization rejection from the OpenAI Responses API when DeepSeek reasoning strings are malformed.

**Fixes Merged (Medium Severity):**
- **[PR #5221: fix(memory): harden history tail read against invalid UTF-8](https://github.com/HKUDS/nanobot/pull/5221)** — A subtle but important crash fix that could occur when history files exceed 4KiB and contain multi-byte characters.
- **[PR #5222 (Open): fix(telegram): keep fenced code intact with special chars](https://github.com/HKUDS/nanobot/pull/5222)** — An open PR addressing corrupted code block rendering for languages like `c++` and `objective-c` in Telegram due to a regex stopping at the first non-word character.

## Feature Requests & Roadmap Signals

Several features merged or in-flight today signal strong directionality for near-term releases:

- **Enhanced Multichannel Policy Granularity:** The Mattermost `groupPolicyInThread` feature (#5233/#5232) signals that per-channel, per-thread permissioning will be a theme, likely expanding to other channels.
- **Rich Web Search Transparency:** The MST metasearch integration (#5234) is aimed at giving users broader, fusion-based search results, likely as a competitive answer to single-engine limitations.
- **Cross-Session Memory & Continuity:** PR #5211 (cross-session search and mentions) and PR #5231 (archiving idle sessions for the "Dream" feature) both focus on making long-term memory and session persistence far more useful and actionable—a core value-add for personal AI assistants.
- **Provider Breadth and Dual-Mode Auth:** The long-running PR #1550 that supports both OAuth and custom API-key modes for OpenAI Codex remains flagged as `conflict` but was updated today, indicating continued community interest in hybrid auth modes.

**Prediction:** The next NanoBot release will likely bundle the substantial WebUI/UX polish (#5226–#5229) with the provider reliability fixes (#5214, #5230) and the new gateway-provider addition (Eden AI). The Opus 5 temperature bug (#5235) is urgent enough likely to be hot-fixed quickly.

## User Feedback Summary

- **Pain Point—Model Compatibility:** The Opus 5 issue (#5235) reflects immediate user pain when adopting the newest model versions. The fact that validation is hard-coded into the client is a broader design concern—users expect new models to "just work."
- **Pain Point—Provider Switch Hazards:** Several fixes today (Gemini replay without signatures #5230, DeepSeek reasoning malformed input #5214) point to real user frustration when switching models mid-conversation or using fallback routing. The hard `400 INVALID_ARGUMENT` errors are an unpleasant, opaque experience.
- **Satisfaction—Fast Iteration:** The sheer volume of WebUI fixes (5 merged in one day) and the "complete i18n audit" (#5227) demonstrate maintainers responding quickly to detailed feedback, which should boost satisfaction for non-English and mobile users.
- **Positive Adoption Signals:** Users are actively building and submitting integrations (Eden AI, ModelScope documentation, MST metasearch), a strong sign of developer satisfaction and ecosystem momentum.

## Backlog Watch

- **[PR #1550: feat(codex): 支持 OAuth 与自定义 Responses 双模式 (Conflicting)](https://github.com/HKUDS/nanobot/pull/1550)** — This PR, open since early March, remains flagged with a `conflict` label. It is the single oldest item updated today. It attempts to give OpenAI Codex dual-mode operation (OAuth vs. custom API base/key). Without resolution, users with enterprise API-key setups remain forced into the OAuth flow. Maintainer guidance on conflict resolution would be valuable here.
- **[PR #5204: refactor(providers): declare Responses capabilities (Open, flagged `conflict`)](https://github.com/HKUDS/nanobot/pull/5204)** — Another `conflict`-flagged PR. This declarative refactor simplifies how providers express their ability to route/reason/downcast to the Responses API. As it is foundational and touches OpenAI, Copilot, and DeepSeek, it seems long overdue for review and could unblock further provider work.

---

*Generated 2026-08-04 | Source data: HKUDS/nanobot GitHub repository*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** August 4, 2026

---

## 1. Today's Overview

Hermes Agent is in an active development cycle with 50 issues and 50 PRs updated in the last 24 hours, signaling a healthy and engaged community. The project just shipped **v0.20.0 "The Herald Release"** (v2026.8.3) with a staggering ~3,650 commits, ~1,400 merged PRs, and ~1,200 issues closed since v0.19.0, reflecting massive momentum. Activity is split between post-release bug triage (particularly around Telegram gateway hangs, Windows path handling, and config/session integrity) and a steady stream of feature development (i18n, skills visibility states, and security hardening). The maintainer team is actively closing duplicates and engaging with new reports, indicating a responsive governance model. Issue volume skews toward bugs (P1-P2) rather than feature requests, suggesting the release brought some regressions that are being quickly swept up.

---

## 2. Releases

### v2026.8.3 — Hermes Agent v0.20.0 (The Herald Release)
- **Released:** August 3, 2026
- **Scope:** ~3,650 commits, ~1,400 merged PRs, ~5,200 files changed, ~559K insertions, ~405K deletions, **~1,200 issues closed**, 650+ contributors

While the release notes are truncated, the "Herald Release" marks a major milestone in the project's evolution. Given the scale (1,200 issues closed), this version likely includes significant architectural changes across the agent core, gateway, plugins, and desktop app.

**⚠️ Migration/Compatibility Watch:** The release has introduced several reported regressions, including:
- **Telegram gateway hangs** on connect (issues #78052, #67498, #72454) — likely related to python-telegram-bot initialization changes
- **`read_file` binary detection regression** (#76886) where UTF-8 text with multibyte chars is misclassified as binary
- **Schema migration concerns** around session `chat_id` backfill (issue #71322) — already patched but indicates boundary conditions in the v23 migration

**Recommendation:** Users upgrading to v0.20.0 should watch for gateway connectivity issues and file-tool regressions; the Telegram connection problem appears to affect both v0.18.2 and v0.19.0/0.20.0 paths, suggesting a deeper upstream dependency issue.

---

## 3. Project Progress

**Merged/Closed PRs (4 total in last 24h):**
- **#77944** `fix(session): drop empty tool_calls in repair_message_sequence` — Critical fix for the "Invalid 'messages[N].tool_calls': empty array" HTTP 400 on strict providers (DeepSeek v4, Kimi), resolving long-session failures. Seen as a follow-through to the #59110 chokepoint fix.
- **#78005** `feat(skills): add index-excluded visibility state` — New third visibility state for skills: hidden from discovery indexes but still exact-loadable; applied consistently across prompt assembly, list, slash-command discovery, and forced preload.
- **#78071 (closed)** — `sanitize_api_messages` fix for tool messages with missing/empty `tool_call_id`, submitted as a follow-up finding from #78063.
- **#78057 (closed)** — Duplicate issue closed; gateway startup notice interfering with A2A tasks.

**Active Open PRs Gaining Traction (may merge soon):**
- **#78086** `fix(security): keep webhook and model API keys out of config.yaml` — Security hardening routing API keys through `.env` with `key_env` references.
- **#78082** `fix(skills): restore bundle/installed content-hash symmetry on Windows` — Addresses hash comparison contract for skill update checks on Windows.
- **#78083** `fix(cron): check binary magic bytes instead of bare NUL for lifecycle guard` — Security fix for NUL-byte bypass in cron script scanning.

---

## 4. Community Hot Topics

### Most Discussed Issues (by comment count, 7 comments each):

1. **[#30220] Background Self-Improvement Review misclassifies content** [OPEN, P2]
   https://github.com/NousResearch/hermes-agent/issues/30220
   The `_spawn_background_review` system misfiles learnings between memory/skill/user stores. This long-running issue (since May) touches core agent self-improvement architecture — a high-impact area that hasn't seen a fix in months.

2. **[#76886] `read_file` misclassifies valid UTF-8 as binary (regression in 0.19.1)** [OPEN, P2]
   https://github.com/NousResearch/hermes-agent/issues/76886
   The 1000-byte sample cuts a multibyte character, triggering binary detection. **Critical regression** affecting Obsidian users; trivial to fix but highly disruptive.

3. **[#67498] Telegram gateway hangs at 'Connecting to Telegram (attempt 1/8)'** [CLOSED, P1]
   https://github.com/NousResearch/hermes-agent/issues/67498
   Despite `TELEGRAM_FALLBACK_IPS` workaround, gateway hangs with all threads idle. Closed after tracking a persistent upstream issue affecting multiple Telegram-related problems.

4. **[#39043] Signal adapter: complete native quote/reply, edit, delete support** [OPEN, P3, 👍2]
   https://github.com/NousResearch/hermes-agent/issues/39043
   The most-upvoted open feature request: users want full signal-cli capability exposure (timestamp IDs, edits, remote delete, read receipts).

### Analysis:
The community is split between **enterprise/power users** demanding gateway reliability (Telegram hangs, webhook reconnects) and **feature-completeness seekers** wanting platform-native capabilities (Signal, Matrix threads). The Telegram issue cluster (multiple duplicate reports) indicates the maintainers are converging on a single root cause, but the volume of duplicates (~4-5) suggests comms friction around the workaround.

---

## 5. Bugs & Stability

### Critical (P0/P1):

1. **Telegram Gateway Hang (Multiple Reports: #78052, #67498, #72454)** [CLOSED/OPEN]
   - https://github.com/NousResearch/hermes-agent/issues/78052
   - https://github.com/NousResearch/hermes-agent/issues/67498
   - https://github.com/NousResearch/hermes-agent/issues/72454
   - **Symptom:** Gateway process hangs forever on `attempt 1/8`; standalone adapter connects fine. All threads idle (py-spy).
   - **Impact:** High — affects all self-hosted Telegram bot users. One issue closed, but regression persists in v0.20.0, implying a fix may be incomplete or mis-diagnosed.

2. **`/resume` blocked for pre-v23-migration sessions (#71322)** [CLOSED]
   - https://github.com/NousResearch/hermes-agent/issues/71322
   - NULL `chat_id` causes IDOR guard to fail closed; migration didn't backfill. **High impact** for long-standing Discord users with session history.

### High (P2):
| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#69216](https://github.com/NousResearch/hermes-agent/issues/69216) | uv installed but not found on native Windows 11 | ⚠️ None identified |
| [#77618](https://github.com/NousResearch/hermes-agent/issues/77618) | Desktop app fails on macOS 15 despite "12+" requirement | None — needs investigation |
| [#67498](https://github.com/NousResearch/hermes-agent/issues/67498) | Telegram gateway hang (closed) | Duplicate — tracked with #63309 |
| [#60551](https://github.com/NousResearch/hermes-agent/issues/60551) | `hermes config set` writes string scalar for list keys | None |
| [#68559](https://github.com/NousResearch/hermes-agent/issues/68559) | Multiplexed gateway ignores routed profile's terminal backend | None |
| [#76886](https://github.com/NousResearch/hermes-agent/issues/76886) | `read_file` binary misclassification (UTF-8 regression) | None yet — simple fix |
| [#78079 PR](https://github.com/NousResearch/hermes-agent/pull/78079) | Sensitive-path write guard silently no-ops on Windows | ✅ PR open |
| [#78083 PR](https://github.com/NousResearch/hermes-agent/pull/78083) | Cron lifecycle guard bypassable with single NUL byte | ✅ PR open |

### Platform-Specific Cluster (Windows):
Notable recurrence of **native Windows** bugs (no WSL): `search_files` path rewrite fails (#67629), uv-not-found (#69216), `.env` BOM drops first key (has fix PR #65124), sensitive-path guard no-op (PR #78079), skill content-hash asymmetry (PR #78082), and duplicate sidebar lanes (PR #71889). This indicates a systemic Windows QA gap that deserves maintainer attention.

---

## 6. Feature Requests & Roadmap Signals

### Active Feature Requests (high engagement):
- **[#39043] Signal adapter completeness** (👍2, 7 comments) — quote/edit/delete/read-receipt support. Likely candidate for v0.21.0.
- **[#29771] Extend credential pool to search backends** (5 comments) — Tavily/Exa credential management; logical follow-on to existing provider credential pool work.
- **[#78061] Tool-to-tool binary output passing** (new, 2 comments) — Let local tools consume MCP tool binary output without model re-emitting; addresses a core agent-efficiency gap.
- **[#77744] Incremental status bar context % during tool loops** (new) — TUI polish for long-running tasks.

### Roadmap Signals from PRs:
- **Security hardening is a theme:** Two new PRs (#78086 API keys → `.env`; #78083 NUL-byte exploit fix) suggest a security-focused sprint.
- **i18n momentum:** PR #78081 brings complete pt-BR translation (~2,500 keys) to the desktop app. Expect more locale PRs to follow.
- **Desktop is maturing:** Diagram preservation (PR #78080), non-git project chats (PR #68414), macOS spawn-helper chmod fix (PR #63789) — the desktop experience is catching up to the CLI.
- **Skills ecosystem:** PR #52107 adds bundled Box productivity skill; PR #78005 adds index-excluded visibility state. The skills marketplace/hub is an active area.

### Predictions for v0.21.0:
High likelihood: Telegram gateway connect fix (dedicated upstream patch or dependency bump), `read_file` binary-detection fix, skills index-excluded state, and at least one Windows path normalization fix. The API-key-to-`.env` migration may be a breaking change requiring migration notes.

---

## 7. User Feedback Summary

### Pain Points:
- **Telegram reliability is the #1 frustration:** Multiple duplicates (5+ issues) across version ranges indicate users feel unresolved; one commenter noted "I tried the workaround, still hangs." Tone is frustrated but not hostile.
- **Windows users are underserved:** Repeated native-Windows-only bugs (paths, uv, permissions) suggest the project's primary dev environment is POSIX. Users are manually working around with MSYS/Cygwin conversions.
- **Configuration pitfalls:** `hermes config set` semantics for list keys, `disabled_toolsets` unexpectedly removing `web_search`, and provider display-name vs runtime-name confusion (#78072) point to config UX debt.
- **Session/memory corruption anxieties:** Issues around session stack recovery (#78087 PR), empty `tool_calls` (fixed in #77944), and pre-migration `/resume` blocks show users rely on long-running sessions and are sensitive to data loss.

### Positive Signals:
- PRs are being submitted quickly with high-quality root cause analysis (e.g., #78082 documents the exact contract broken; #76886 identifies the sampling bug precisely).
- Users appreciate the credential-pool and provider routing improvements, engaging constructively with proposals.
- The very detailed bug reports (with py-spy traces, reproduction steps, environment configs) signal a technically sophisticated user base that trusts the project.

### Satisfaction:
Mixed-to-negative on gateway platforms (Telegram, webhook) and Windows; positive on core agent capabilities (skills, delegation, compression) and the desktop app's trajectory.

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention:

1. **[#30220] Background Self-Improvement Review misclassifies content** (P2, since 2026-05-22, 7 comments)
   https://github.com/NousResearch/hermes-agent/issues/30220
   Oldest major unresolved issue. Core architectural bug in self-improvement system; no maintainer response visible in last 24h. **High priority** for agent autonomy story.

2. **[#10376] Profile isolation incomplete: `--clone` copies memory; cross-profile reads possible** (P2, since 2026-04-15)
   https://github.com/NousResearch/hermes-agent/issues/10376
   Two months old with 4 comments. Security/stability boundary issue; contradicts documented "fully isolated" promise. Needs a decision (accept as documented? or fix?).

3. **[#68859] Define explicit tool retry semantics for lifecycle hooks** (P3, since 2026-07-21)
   https://github.com/NousResearch/hermes-agent/issues/68859
   One comment only. Telemetry/observability gap that blocks safe custom hooks for retry logic.

4. **[#64392] Duplicate skill names disagree across list/prompt/skill_view** (P2, since 2026-07-14, needs-decision)
   https://github.com/NousResearch/hermes-agent/issues/64392
   Three inconsistent behaviors for the same input; needs design decision on canonical resolution.

5. **[#69216] uv installed but not found (Windows)** (P1, since 2026-07-22)
   https://github.com/NousResearch/hermes-agent/issues/69216
   **P1 with zero fix PRs.** Blocks new users on the second most common desktop OS. This should be escalated.

6. **[#78022] Webhook platform reconnect loop on port collision** (P2, since 2026-08-03)
   https://github.com/NousResearch/hermes-agent/issues/78022
   Silent recurring failure mode; no maintainer response yet.

### PRs Awaiting Review/Decision:
- **#53958** `feat(compression): configurable warn_after_compressions` — Open for 5+ weeks despite being a small, clear improvement.
- **#65102** `feat(api): resolve configured session identities early` — Feature with broad impact (sessions, toolsets, prompt context); massive blast radius may be causing hesitation.
- **#65124** `fix(cli): read .env as utf-8-sig so a BOM doesn't drop the first key` — Open 2+ weeks; simple fix with Windows-wide benefit.
- **#65824** `fix(delegation): preserve redacted output on timeout` — Small fix that prevents loss of completed research results; stale.
- **#63789** `fix(desktop): chmod 755 spawn-helper after staging` — Fixes a show-stopping macOS 26 desktop issue; should be fast-tracked.

---

*Digest generated from public GitHub data on 2026-08-04. All links point to NousResearch/hermes-agent.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-04

## 1. Today's Overview
PicoClaw saw a moderate spike in activity: **8 issues and 6 PRs were updated in the last 24 hours**, signaling an active community and responsive maintainers. **5 issues and 3 PRs were closed/merged today**, indicating good triage throughput, while **3 issues and 3 PRs remain open/active**. The day's updates cluster around **agent routing/context management**, **Telegram/Discord channel handling**, and **MCP server resilience** — a strong signal that production users are hitting real integration pain points as PicoClaw scales beyond simple single-agent use. No new releases were published. Overall, the project appears **healthy and genuinely community-driven**, though the persistence of a stale-issue backlog and several open bugs (notably the MCP hang in #3269) points to areas where maintainer bandwidth is stretched thin.

## 2. Releases
**No new releases were published this period.** The most recent stable version remains **0.3.1** (the version cited in all current bug reports). The "nightly" channel (git `2cf030d2`) is actively used by the community, suggesting users are willingly testing pre-release builds to get new features — but also that they are encountering regressions in that nightly stream.

## 3. Project Progress
Three PRs were merged/closed today, representing concrete fixes to known issues:

- **[PR #3267 — fix scope bug for refresh agy token](https://github.com/sipeed/picoclaw/pull/3267)** *(merged)* — Fixes a critical auth bug for the Antigravity provider where token refresh passed an incorrect scope, causing hard `PERMISSION_DENIED` failures mid-session. Closes a long-standing reliability gap for that provider.
- **[PR #3273 — feat(webui): add Japanese (ja) localization](https://github.com/sipeed/picoclaw/pull/3273)** *(merged)* — Adds full Japanese localization to the WebUI (968-line translation file), fulfilling feature request #3272 and expanding the product's global reach.
- **[PR #3202 — fix(routing): strip leading/trailing underscores in ID normalization](https://github.com/sipeed/picoclaw/pull/3202)** *(merged)* — Fixes a routing edge case where underscores in agent/account IDs violated the documented `^[a-z0-9]...` regex contract, breaking ID normalization for certain custom agent names.

**Notable open PRs advancing major features:**
- **[PR #3316 — fix: routed-agent context management](https://github.com/sipeed/picoclaw/pull/3316)** *(open, by j-v)* — A substantial fix addressing a serious bug where agents routed via dispatch rules failed to persist history and never triggered auto-compaction. This directly addresses long-standing issue #3301. Expect this to be a high-priority merge candidate.
- **[PR #3315 — Support topics in private bot chats](https://github.com/sipeed/picoclaw/pull/3315)** *(open, by genuss)* — Extends Telegram topic support to private bot chats (not just forum supergroups), fixing a behavior gap where `IsTopicMessage` was ignored when `Chat.IsForum` was false.
- **[PR #3314 — Fix: agent not able to execute shell command added to customAllowPatterns](https://github.com/sipeed/picoclaw/pull/3314)** *(open, by j-v)* — Fixes a security-configuration bug where default deny patterns always overrode user-defined `customAllowPatterns`, making the allow list silently ineffective. Critical for power users automating workflows via `exec`.

## 4. Community Hot Topics
The most discussed and commented items this cycle reveal three distinct user communities: self-hosters, automation-heavy power users, and non-English speakers.

- **[Issue #3281 — Web UI chat input is very laggy with long history](https://github.com/sipeed/picoclaw/issues/3281)** *(3 comments, open)* — UI performance degradation in the web client. Reporters note session-long histories make the input box crawl, likely an unoptimized re-render on every keystroke in the frontend. The underlying need is for **virtualized history rendering or lazy state updates**. No fix PR open yet.
- **[Issue #3269 — MCP server connection failure hangs the agent loop](https://github.com/sipeed/picoclaw/issues/3269)** *(2 comments, 1 👍, open)* — A serious reliability issue. When an MCP server fails, the entire agent stalls and the chat interface stops responding. Signals a missing timeout/backoff wrapper around MCP calls. **No fix PR exists yet.**
- **[Issue #3301 — /clear and auto-compression broken for routed agents](https://github.com/sipeed/picoclaw/issues/3301)** *(1 comment, open)* — Dispatch-rule users report that `/clear` and token-based session compression are silently ignored for routed conversations, causing runaway context growth. **PR #3316 appears to be a direct fix for this.**
- **[Issue #3272 — Japanese localization request](https://github.com/sipeed/picoclaw/issues/3272)** *(2 comments, closed)* — Strong demand for i18n; closed by the merged PR #3273. The brisk close suggests the maintainers are responsive and prioritize internationalization.

## 5. Bugs & Stability
Three active bugs are ranked below by severity:

1. **[Issue #3269 — MCP connection failure hangs agent loop](https://github.com/sipeed/picoclaw/issues/3269)** — **Critical**. A transient MCP failure permanently wedges the agent, killing all downstream user replies. No retry/timeout logic in the MCP wrapper. **No fix PR open.** This is the single highest-risk stability item in the current tracker.
2. **[Issue #3301 — Routed agents ignore /clear and auto-compression](https://github.com/sipeed/picoclaw/issues/3301)** — **High**. The feature is silently non-functional for a supported configuration (dispatch rules), leading to context blow-up and cost escalation. **Fix available in open PR #3316.**
3. **[Issue #3281 — Web UI lag with long history](https://github.com/sipeed/picoclaw/issues/3281)** — **Medium**. Degrades UX gradually; not a hard failure, but makes sustained sessions painful.

**Fixed today (regression resolution):** PR #3267 (Antigravity scope bug) and PR #3202 (routing ID normalization) were merged, removing two known landmines for enterprise and custom-agent users.

**Security note:** Open PR #3314 fixes a `customAllowPatterns` bypass that could let the agent run disallowed commands, highlighting a reliability/security tradeoff worthy of maintainer review given the MCP hang issue.

## 6. Feature Requests & Roadmap Signals
Strong signals emerged for the next minor release (0.4.x):

- **Internationalization is now a priority**: Japanese (`ja`) localization shipped today via PR #3273. Expect additional languages (Spanish, Portuguese, Korean) in this cycle, given PicoClaw's global adoption.
- **Telegram topic support in private chats** (PR #3315) will likely land soon, as multi-channel production users are clearly driving channel-parity fixes.
- **Routed-agent context management** (PR #3316) is the most user-urgent open feature; expect it to be merged and backported quickly.
- **External gateway management via systemd** (#3276, closed) suggests the maintainers are leaning toward a "launcher should not own gateway lifecycle" philosophy — likely leading to a **best-practices guide for headless deployment** rather than code changes.
- **Exec tool `action` defaulting to `"run"`** (#3268, closed) points to a broader reliability goal: making tool schemas less brittle for downstream LLM callers.

## 7. User Feedback Summary
User sentiment this cycle is **positive toward responsiveness but concerned about reliability**.

- **Pain point: session context management.** Users setting up routed multi-agent systems (Discord/Telegram) are hitting walls: routed agents forget earlier messages (#3301) and fail to auto-compress, making long-running conversations impractical. These are users doing real production deployments (Raspberry Pi + DeepSeek via OpenCode Go is a notable stack).
- **Pain point: fragile external integrations.** The MCP hang (#3269) and Antigravity token scope failure (#3267, now fixed) show that non-native provider/extension failures take down entire sessions. Users expect graceful degradation, not hard-stops.
- **Satisfaction signal: issue/wish fulfillment speed.** The #3272 → #3273 Japanese localization pair was closed within days; the #3268 exec-tool proposal was also resolved quickly. Users see their detailed reports acted on fast, which bolsters community trust.
- **Low signal but notable:** The `git push` allow-pattern failure (#3314) implies a cohort of users are leveraging `exec` for sophisticated git workflows — a power-user use case PicoClaw should actively support.

## 8. Backlog Watch
Several issues that were updated today carry the **`stale` label**, indicating they have not seen maintainer action for some time:

- **[Issue #3276 — Launcher/gateway lifecycle handoff](https://github.com/sipeed/picoclaw/issues/3276)** — Closed today but originally raised on 07-20; it took two weeks and two comments to resolve. The systemd use case is common; worth codifying in docs.
- **[Issue #3265 — Gateway fails on 'unknown type deltachat'](https://github.com/sipeed/picoclaw/issues/3265)** — Closed, but the underlying pattern (gateway hard-fails on a channel type not present in config) may warrant a defensive guard to prevent a single bad channel from tanking the entire gateway.
- **[Issue #3264 — SplitMessage hangs on oversized fenced-code info string](https://github.com/sipeed/picoclaw/issues/3264)** — Closed, but the underlying algorithmic fragility in message splitting could resurface; a fuzz test on `SplitMessage` would harden this path.
- **Open PRs needing review:** [#3314](https://github.com/sipeed/picoclaw/pull/3314) (exec allow-pattern bypass) and [#3315](https://github.com/sipeed/picoclaw/pull/3315) (Telegram private topic) are both clean, well-scoped, and should be prioritized for review to keep community momentum.

---

*Digest generated from public GitHub activity for sipeed/picoclaw, 2026-08-04.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-04

## Today's Overview

NanoClaw is in a healthy, high-velocity state. The project saw 9 pull requests updated within the last 24 hours, with 6 of those being merged or closed — indicating strong momentum in the contribution pipeline. Activity centered on bug fixes around session resume and retention cleanup, infrastructure hardening (image repinning), and one notable feature PR for remote Streamable HTTP MCP servers that remains open. Only one new issue was reported (a Node.js compatibility error), suggesting the current codebase is relatively stable. The mix of core-team and community contributions, all following contribution guidelines, points to a well-governed and actively maintained project.

## Releases

No new releases were published during the reporting window. The project is, however, actively preparing infrastructure changes via PR #3182, which repins the agent image, signaling an upcoming deployment rather than a user-facing version update.

## Project Progress

Six pull requests were merged or closed today, reflecting meaningful forward movement:

- **[#3182] versions: repin the agent image to hardened-2026-08-02** — Core team repinned the agent image to a hardened build. While NanoClaw content is identical (same upstream digest), the refreshed base improves security posture. Merged.
- **[#3180] fix(update): surface hardened image migration** — An operational skill improvement to ensure users are properly informed about the hardened image migration path, complementing the image repin. Merged.
- **[#3137] Fix engagement consistency and expose self-serve wiring controls** — A significant merged PR that allows agents to inspect their wirings, request engagement-policy updates, and rejects invalid JavaScript engagement regexes, preventing warm-container follow-up turns. Merged.
- **[#3143] Preserve resolved approval card content** — Fixes a UX issue where resolved approval cards lost their title and request details; they now retain the original body and display a muted decision/actor or timeout status. Merged.
- **[#3181] fix(imessage): opt in via first message to the assigned line** — Fixes iMessage channel behavior so agents opt in via the first message to the assigned line. Merged.
- **[#3178] Closed — opened against wrong repository** — A contributor's PR was correctly identified as targeting the wrong repo and closed without upstream change.

A notable open PR, **[#3092] feat: support remote Streamable HTTP MCP servers**, advanced and remains open, tracking toward a potentially significant feature addition.

## Community Hot Topics

The most active community engagement today centers on:

- **[#3179] SyntaxError: The requested module 'node:util' does not provide an export named 'styleText'** — This new issue already has 1 comment, indicating rapid community response. The error stems from `@clack/core@1.2.0` importing `styleText` from `node:util`, which is only available in Node.js 20.12+/21.7+. Users are likely hitting this due to an older Node runtime. This is the only active issue and represents the primary community concern today.
- **[#3183] fix(group-init): pin cleanupPeriodDays so retention cleanup can't reap cold sessions** — While a PR, its subject matter (cold sessions being deleted after 30+ days of inactivity) reflects a real community pain point around data retention and unexpected session loss.

## Bugs & Stability

Two bugs were actively addressed today, both with fix PRs already in place:

1. **Session resume failure on missing transcript (Severity: High)** — PR #3184 addresses a bug where continuing a stored session whose transcript file no longer exists results in a hard failure (`No conversation found with session ID: <uuid>`). The fix rotates to a new session instead of dying. This is a critical reliability issue for long-running conversations.
2. **Retention cleanup reaping cold sessions (Severity: High)** — PR #3183 fixes a bug where the group-init `cleanupPeriodDays` was not pinned, causing the retention cleanup to delete sessions for users messaging after 30+ days of inactivity. This causes the same raw session-not-found errors as above. The fix pins the cleanup period to prevent session reaping.
3. **Node.js version incompatibility (Severity: Medium)** — Issue #3179, the `styleText` SyntaxError, is a runtime compatibility issue. No fix PR exists yet, but the workaround is to upgrade Node. This affects the CLI (dev tooling) rather than the production server, mitigating severity.

## Feature Requests & Roadmap Signals

- **Remote Streamable HTTP MCP servers (PR #3092)** — This open feature PR, tagged `core-team` and `follows-guidelines`, would extend NanoClaw's MCP support to remote Streamable HTTP transport. Given its age (since 2026-07-19) and continued activity, it is a strong candidate for inclusion in the next minor release.
- **Self-serve wiring controls (PR #3137, merged)** — Agents gaining the ability to inspect and adjust their engagement policies signals a roadmap direction toward more agent autonomy and decentralized control, which may lead to further self-management features.

## User Feedback Summary

- **Satisfaction**: Contributors are actively following contribution guidelines and submitting high-quality fixes, indicating a healthy, well-documented contribution process. The rapid merging of 6 PRs suggests maintainers are responsive and supportive.
- **Pain points**: The most immediate user pain is the **Node.js compatibility issue** (`styleText` error), which blocks the CLI for users on Node < 20.12. The **session loss after inactivity** bugs (fixed by #3183, #3184) reflect significant user frustration with losing long-running session context, though they were quickly addressed. The **resolved approval cards losing content** (#3143) was a smaller UX annoyance that has been fixed.

## Backlog Watch

- **[#3092] feat: support remote Streamable HTTP MCP servers** — Open since 2026-07-19, this feature PR has not received maintainer merge. Given its scope and core-team interest, it warrants attention to determine if it will land soon or needs further review.
- No other issues or PRs appear to be languishing without response; the project's triage and response cadence today is excellent, with no signs of neglect.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-08-04

## 1. Today's Overview

NullClaw is in an active development phase with moderate activity: 5 PRs updated in the last 24 hours and 1 issue receiving attention, though no new releases were cut. The project shows a healthy balance of community contributions and maintainer review — two significant PRs addressing proxy/curl transport handling for both providers and Telegram are open and appear to be part of a coordinated stability push. Two PRs related to structured streaming tool-call support were closed, indicating progress has been made on that front. The only open issue, a scheduler unauthorized bug, has been active for nearly 3 months with 4 comments, suggesting it may require maintainer attention. Overall, the project is progressing steadily with focused work on networking reliability and streaming tool-call capabilities.

## 2. Releases

No new releases were published in the last 24 hours. There is no release-related information to report for this digest period.

## 3. Project Progress

Two PRs were closed (merged) in the last 24 hours, both authored by mtdphn and both focused on enabling native API-level tool calls during streaming:

- **[PR #964 — Enable native API-level tool calls during streaming](https://github.com/nullclaw/nullclaw/pull/964)** (closed, created 2026-06-18): This PR addresses the root cause of streaming tool-call issues by preserving structured tool-call deltas in `StreamChatResult`. Previously, even though streaming requests could include API-level tools, the agent could not execute pure streamed tool responses because the deltas were lost. This is a foundational fix that enables provider-wide capability checks for streaming tool calls.

- **[PR #965 — Structured streaming tool-call support for SSE parser](https://github.com/nullclaw/nullclaw/pull/965)** (closed, created 2026-06-18): A companion fix to #964, this PR adds structured tool-call parsing for SSE (Server-Sent Events) streams, specifically handling servers that emit model-generated XML within `delta.content`. Together with #964, this closes the gap for providers that don't natively support structured tool-call deltas.

These merges represent a meaningful advancement in NullClaw's streaming capabilities, enabling more reliable tool-call execution during streaming responses.

## 4. Community Hot Topics

The most active discussion this period is the long-standing scheduler issue:

- **[Issue #915 — [bug] Problem with scheduler unauthorized](https://github.com/nullclaw/nullclaw/issues/915)** — 4 comments, 1 reaction. Opened by scabros on 2026-05-15, this issue describes a broken scheduler in both Telegram chat and other contexts. The user runs NullClaw on Ubuntu with an external Ollama host (qwen3.6:27b on an RTX 3090). Notably, the LLM itself works fine and tool calling generally functions — the problem is specifically with the scheduler component. The fact that this issue has received comments over a 2.5-month span but remains open suggests it's a real pain point that hasn't been fully resolved, though it may be low-priority compared to other work.

Two PRs from the same author (ArcanePivot) also drew attention, both addressing proxy handling:

- **[PR #982 — fix(telegram): use curl transport for explicit proxies](https://github.com/nullclaw/nullclaw/pull/982)**
- **[PR #983 — fix(providers): use pinned curl path for proxied requests](https://github.com/nullclaw/nullclaw/pull/983)**

## 5. Bugs & Stability

**Moderate severity:**

- **[Issue #915 — [bug] Problem with scheduler unauthorized](https://github.com/nullclaw/nullclaw/issues/915)** — The scheduler component fails with what appears to be an authentication/authorization issue ("unauthorized") in both Telegram chat and other contexts. The LLM works fine and tool calling is functional, isolating the problem to the scheduler subsystem specifically. Severity: **Medium** — the core LLM functionality still works, but a key automation feature is broken for this user. **No fix PR is currently open** for this issue. The issue has been open since May 15, 2026 (nearly 3 months), with 4 comments but no clear resolution path visible.

**Potential stability concerns (from PRs):**

- PRs #982 and #983 suggest existing bugs in proxy handling — specifically that the live channel probe already routes through curl transport (per PR #982 description), but the main POST path did not, indicating an inconsistency that may have caused proxy-related connection failures. These PRs are still open.

## 6. Feature Requests & Roadmap Signals

The following signals from PRs and issues suggest where NullClaw is heading:

- **Native streaming tool calls** (from PRs #964, #965): The merged PRs enable API-level tool calls during streaming, and the companion SSE parser enhancement supports servers that output XML in `delta.content`. This means NullClaw is becoming more robust for a wider range of LLM providers and configurations — a clear roadmap direction toward broader provider compatibility.

- **Enhanced proxy support** (from PRs #982, #983): The consistent approach using pinned curl paths and secure temporary header files for proxied requests suggests a roadmap push toward improved network reliability, credential security (keeping headers out of argv), and consistent behavior across provider and Telegram channels.

These PRs suggest the next versions will likely include improved streaming tool-call reliability and more robust proxy handling — both significant stability improvements for users behind firewalls or using remote LLM hosts.

## 7. User Feedback Summary

- **Positive signals:** The user reporting issue #915 notes that "tool calling in nullclaw in general also works mostly fine," indicating the core tool-calling functionality is generally working well. The active PR work on streaming tool calls and proxy handling suggests the maintainers are addressing advanced use cases that community members care about.

- **Pain points:** The scheduler issue (#915) seems to be a genuine frustration — the user tried it in multiple contexts (Telegram and others) and it consistently fails with an "unauthorized" error. Despite being open for ~3 months with 4 comments, there's no clear resolution, which may indicate either low maintainer priority or difficulty reproducing the issue.

- **Use case insight:** The affected user runs NullClaw on Ubuntu with an external Ollama instance on the same network — a common self-hosted deployment pattern. The fact that this works fine for the LLM but fails for the scheduler highlights how edge-case components can be unreliable even when core functionality is solid.

## 8. Backlog Watch

- **[Issue #915 — Scheduler unauthorized](https://github.com/nullclaw/nullclaw/issues/915)** — Open since **2026-05-15** (~3 months). This is the longest-standing open issue visible in the current data. With 4 comments and a 👍 reaction, it has community engagement but no resolution. Given that the scheduler is likely a key feature for automation-focused users, this deserves maintainer attention. Recommended action: reproduce with an external Ollama host configuration, or at minimum provide a status update to the reporter.

- **[PR #956 — ci(deps): bump alpine from 3.23 to 3.24](https://github.com/nullclaw/nullclaw/pull/956)** — Open since **2026-06-15** (~7 weeks). A routine Dependabot dependency bump that has been sitting unmerged. While low-risk, leaving dependency bumps stale can lead to accumulating version drift in Docker images. Maintainers should either merge or close this to keep the backlog clean.

No other significant stale items were identified in the current data window.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-04

## 1. Today's Overview

IronClaw is in a period of intense architectural refactoring, driven by the multi-wave "Reborn" restructuring initiative. Activity is very high, with 45 issues and 50 PRs updated in the last 24 hours; however, only 18 PRs were merged or closed, indicating a large volume of open, in-flight work. The project's focus is clearly on internal code health, with the majority of activity centered on the WS2/WS3 re-layering efforts, dependency boundary enforcement, and CI reliability. A significant portion of the churn stems from a few core contributors (BenKurrek, henrypark133, serrrfirat) executing a large, pre-planned refactoring roadmap, producing both structural progress and a wave of follow-up issues around tooling gaps. While no releases were cut today, a release PR (#5598) remains open, and the project is operating under a newly documented weekly Wednesday release strategy.

## 2. Releases

No new releases were published in the last 24 hours. A release PR (#5598) is open and was last updated on 2026-08-03; it details breaking API changes for `ironclaw_common` (0.4.2 -> 0.5.0) and `ironclaw_skills` (0.3.0 -> 0.4.0). Notably, a documentation PR (#7049) was merged that establishes a **weekly Wednesday release strategy**, aligning Monday-to-Monday sprints with Monday RC cuts and Tuesday QA, indicating the project is formalizing its release cadence.

## 3. Project Progress

Today's merged work was dominated by the execution and follow-up of the "Reborn" wave plan, with a focus on fixing regressions and closing out smaller workstreams:

- **CI and E2E Stability (High Priority):** PR #7070 (merged) unblocked main E2E coverage by fixing five failing Reborn WebUI v2 tests. The fixes included an SSE `keep_alive` cursor bug and an admin load-more retry, both of which were user-facing correctness issues.
- **Extension Registry Re-layering (WS2):** PR #7040 (merged) closed the final open WS2 rows, correcting the stale claims in the documentation and re-verifying the current state of the architecture.
- **Documentation and Process:** PR #7049 (merged) added the weekly Wednesday release strategy, providing a clear process for release ownership, blocker fixes, and emergency handling.
- **Auth Fixes:** PR #7024 (merged) resolved custom MCP authentication during registration, ensuring that `Auto` auth performs a proper, credential-free initialization handshake and only resolves to OAuth when a usable client path exists.

A significant number of large (XL-sized) refactoring PRs remain open, including the `wit/` move (#7084), the sandbox lane merge (#7065), and several WS3 re-layering efforts (#7090, #7094, #7096, #7080), all of which are part of the current wave.

## 4. Community Hot Topics

The most engaging discussion this week centered on the project's **error-recoverability endgame**, which is the top-level goal for the agent's runtime resilience.

- **[#6284: [EPIC] error-recoverability endgame — the model recovers from 100% of the errors it sees (CLOSED)](https://github.com/nearai/ironclaw/issues/6284)** — 15 comments
  This closed epic defines a strict contract for every mid-run error: the run must survive, the model must see it, the error must carry both the cause and the path to success, and the model must get a turn to act. Its closure suggests the team believes this core stability goal has been met.

- **[#6524: Epic: Hermetic capability and journey testing platform (CLOSED)](https://github.com/nearai/ironclaw/issues/6524)** — 4 comments
  This closed epic focused on describing a platform to mechanically answer whether every supported capability has deterministic coverage, highlighting the project's strong emphasis on automated verification.

The high level of activity from core contributors on tightly-scoped architecture issues (e.g., #7091, #7092, #7093) indicates a highly structured and disciplined approach to code health, likely driven by automated checks and an explicit planning document (`docs/reborn/target-architecture/`). The needs behind these discussions are not user-facing features but rather a sustained push for maintainable, well-layered code to prevent future regressions.

## 5. Bugs & Stability

A significant volume of bugs were reported today from both internal QA and the user-facing bug bash, ranging from critical authentication failures to CI tooling gaps. Below are the most notable issues, ranked by severity:

- **[#7069: Google services require repeated authentication (OPEN) — bug_bash_P1](https://github.com/nearai/ironclaw/issues/7069)**
  Users are forced to re-authenticate for every Google service (Calendar, Docs, etc.) even after completing the OAuth flow. This is a critical user-experience blocker. While the issue is open, PR #7077 is open and claims to fix it by making one vendor authorization cover every installed extension sharing the account.

- **[#7078: Shared-vendor OAuth scope ceiling is store-wide, not caller-scoped (OPEN)](https://github.com/nearai/ironclaw/issues/7078)**
  This issue was split out of the review for #7077 and represents a structural flaw in how OAuth scopes are determined. The resolver unions vendor recipes across all manifests, meaning the scope requested is the union of *all* extensions, not just the one being called. This is a follow-up architecture issue that could cause sub-optimal or failed authorization flows.

- **[#7082: builtin.skill_install: inline multi-file installs are unreachable... (OPEN)](https://github.com/nearai/ironclaw/issues/7082)**
  The skill install input gate rejects valid shapes and silently drops others (files/source/source_url) for URL installs. This is a functional bug in a core tool, but with no fix PR yet.

- **[#7075: Agent ignores follow-up question after failed run (OPEN) — bug_bash_P2](https://github.com/nearai/ironclaw/issues/7075)**
  After a run fails (e.g., provider unavailable), the agent resumes the failed task instead of addressing the user's new request. This is a conversational-loop bug that degrades the core assistant experience.

- **[#7068: Hosted MCP: omitted destructiveHint defaults to false vs spec default of true (OPEN)](https://github.com/nearai/ironclaw/issues/7068)**
  A subtle but important correctness bug where the MCP spec's default for `destructiveHint` is `true`, but the code treats absence as `false`. This could lead to destructive actions not being UI-blocked as intended.

**CI/Infrastructure Reliability:** There are also several critical internal tooling bugs hampering the development workflow:
- **[#7087: Reborn PR test planner hard-fails on Dockerfile, .githooks/, .claude/, etc. (OPEN)](https://github.com/nearai/ironclaw/issues/7087)** — The CI planner fails on any PR touching these files, blocking a whole class of changes.
- **[#7081: Docker fail-closed test gate is wired to nothing (OPEN)](https://github.com/nearai/ironclaw/issues/7081)** — The `IRONCLAW_REQUIRE_DOCKER_TESTS` env var is never set, meaning the fail-closed gate is effectively dead code.
- **[#7083: Coverage is dark for crates/extensions/ family (OPEN)](https://github.com/nearai/ironclaw/issues/7083)** — A recent directory move has made five crates invisible to the coverage tooling, weakening a key safety net.

Several of these (e.g., #7087, #7085, #7081, #7083) were filed by BenKurrek as blocking issues found while executing the refactoring waves, highlighting that the CI tooling is struggling to keep up with the architectural changes.

## 6. Feature Requests & Roadmap Signals

User-facing feature work is currently focused on improving the "first-run" experience and making the system more configurable through natural language:

- **[#7044: Onboarding to channel-first approach (OPEN)](https://github.com/nearai/ironclaw/issues/7044)** — This epic addresses the blank-slate problem of the WebUI. The focus is on the "General Assistant" use case, guiding users through their first use case. This includes the OOBE prototype in PR #6994, which is a UI-only prototype for a carousel-based onboarding flow.
- **[#7046: Configure all tools, channels, and extensions from AI chat (OPEN)](https://github.com/nearai/ironclaw/issues/7046)** — This epic aims to allow users to configure everything via chat rather than navigating the WebUI, aligning with the "channel-first" approach and simplifying the setup process.
- **[#7097: Add billing support escalation pathways to billing page (OPEN)](https://github.com/nearai/ironclaw/issues/7097)** — A simple usability request from a user uncertain about who handles billing issues.

The "channel-first onboarding" likely to be a major driver for the next few releases. Given the active OOBE prototype (#6994) and the epic tracking it (#7044), we can predict that the next version will feature a guided onboarding experience for the WebUI. Similarly, the push to make configuration chat-driven (#7046) suggests we will see more `builtin.*` lifecycle tools exposed to the model.

## 7. User Feedback Summary

Real user feedback is primarily coming from a **bug bash** initiative, revealing both functional and systemic issues:

- **Authentication friction:** The most critical issue is the repeated Google authentication (#7069). This is a direct contradiction of the "it just works" goal and is a top priority.
- **Systemic conversational failures:** users frequently encounter errors where the assistant gets stuck in a loop, ignores new queries (#7075), or tries to call unavailable functions (#7074), leading to failed complex tasks.
- **Poor UX and presentation:** This includes confusing connection status indicators that flash "Reconnecting" (#7071), raw Markdown being shown instead of formatted text in Telegram (#7072), and the assistant leaking internal "tool names" and "delivery routing logic" instead of giving simple answers (#7073). The later issue suggests the model's prompt or output filtering needs significant work to provide a more polished, user-friendly interface.
- **Usability gaps:** Users want clear billing pathways (#7097) and guidance on how to use the system (#7044).

Overall, the sentiment from the bug bash indicates that while the core engine may be stable (per the closed error-recoverability epic), the **user-facing experience is currently rough**, with authentication, conversation flow, and presentation all needing iteration.

## 8. Backlog Watch

The following items are important but show no recent activity or are in need of maintainer attention:

- **[#5598: chore: release (OPEN)](https://github.com/nearai/ironclaw/pull/5598)** — This release PR has been open for over a month (since 2026-07-03) and includes breaking changes to two crates. While the team has adopted a Wednesday release strategy, this stale PR needs to be resolved, either by being superseded or merged. It appears to have been set aside for a while.
- **[#6957: feat(reborn-ironhub): manage installed package lifecycle (OPEN)](https://github.com/nearai/ironclaw/pull/6957)** — This PR adds persistence for installation receipts and new `ironhub.status` and `ironhub.update` model tools. It was created on 2026-07-31 and updated on 2026-08-03, but its merge may be blocked by the ongoing wave of architectural changes.

- **[#5598: chore: release (OPEN)](https://github.com/nearai/ironclaw/pull/5598)** — This release PR has been open for over a month (since 2026-07-03) and includes breaking changes to two crates. While the team has adopted a Wednesday release strategy, this stale PR needs to be resolved, either by being superseded or merged. It appears to have been set aside for a while.
- **[#6957: feat(reborn-ironhub): manage installed package lifecycle (OPEN)](https://github.com/nearai/ironclaw/pull/6957)** — This PR adds persistence for installation receipts and new `ironhub.status` and `ironhub.update` model tools. It was created on 2026-07-31 and updated on 2026-08-03, but its merge may be blocked by the ongoing wave of architectural changes.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest
**Date: 2026-08-04**

---

## 1. Today's Overview

LobsterAI shows moderate activity today with 2 issues and 11 PRs updated in the last 24 hours. The majority of recent PR activity (6 items) was closed or merged, indicating productive development cycles, particularly around Windows installer fixes, UI improvements, and feature additions. Notably, 4 stale PRs from April remain open and unaddressed, suggesting potential maintainer bandwidth constraints on older contributions. No new releases were published this period. The project continues to demonstrate healthy feature development momentum, with activities such as a startup credit campaign and multi-agent task filtering moving forward.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Project Progress

Six PRs were closed/merged today, reflecting meaningful progress across several areas:

| PR | Description | Impact |
|---|---|---|
| [#2418](https://github.com/netease-youdao/LobsterAI/pull/2418) | **feat(sidebar): add multi-agent task activity filter** | Adds Codex-inspired task activity filter to sidebar for quickly finding tasks needing attention across multiple agents; includes filter button, hide-when-collapsed behavior, and blue indicator |
| [#2419](https://github.com/netease-youdao/LobsterAI/pull/2419) | **feat(activity): add startup credit campaign** | Adds configurable startup credit campaign experience for NetEase user acquisition, including popup, persistent new-conversation-page entry, and login continuation |
| [#2420](https://github.com/netease-youdao/LobsterAI/pull/2420) | **fix(nsis): re-kill survivor processes on every stop poll round** | Fixes Windows uninstall issue where processes surviving the stop gate could persist; now re-issues Stop-Process every poll round with detailed logging |
| [#2421-2423](https://github.com/netease-youdao/LobsterAI/pull/2423) | **fix(btw tools) + revert** | A fix for "btw tools" was merged then reverted, suggesting an issue was discovered and rolled back |

---

## 4. Community Hot Topics

The most active discussions this period center on document processing reliability and export functionality:

**[Issue #1206: kimi2.5 model duplicate processing/replies during document analysis](https://github.com/netease-youdao/LobsterAI/issues/1206)**
- ⚠️ Open for 4+ months (created April 1, updated August 3)
- **1 comment** — User reports kimi2.5 model repeats the same action notification multiple times during document analysis on Windows 10 (v2026.3.30), with the issue being reproducible 100% of the time on current tasks. Switching models resolves it. A stale label suggests this might not have received recent maintainer attention.
- **Underlying need:** Reliability in document analysis workflows; users need clear, non-duplicated progress signals to avoid uncertainty about whether the task is still executing.

**[Issue #1213: Export session details as Markdown](https://github.com/netease-youdao/LobsterAI/issues/1213)**
- ⚠️ Open for 4+ months (created April 1, updated August 3)
- **1 comment** — User requests Markdown export for conversation details, citing that image-only export is inconvenient for editing, searching, and sharing.
- **Underlying need:** Text-based portability and archivability of AI conversations for documentation, knowledge management, and collaboration. Notably, a PR ([#1214](https://github.com/netease-youdao/LobsterAI/pull/1214)) exists but remains open since April.

---

## 5. Bugs & Stability

| Severity | Issue | Description | Fix Status |
|---|---|---|---|
| 🟠 **Medium** | [#1206](https://github.com/netease-youdao/LobsterAI/issues/1206) | kimi2.5 model repeats action notifications during document analysis (100% reproducible on current tasks) | No fix PR identified; stale for 4+ months |
| 🟡 **Low** | [#2420](https://github.com/netease-youdao/LobsterAI/pull/2420) | Windows uninstall could leave survivor processes running | ✅ Fixed in PR #2420 (closed today) |
| 🟡 **Low** | [#2421-2423](https://github.com/netease-youdao/LobsterAI/pull/2423) | "btw tools" fix was merged and then reverted | ⚠️ Rolled back — potential regression or incomplete fix |

---

## 6. Feature Requests & Roadmap Signals

**Actively developed features (likely in next release):**
- **Startup credit campaign** ([PR #2419](https://github.com/netease-youdao/LobsterAI/pull/2419)) — closed today, likely shipping soon
- **Multi-agent task activity filter** ([PR #2418](https://github.com/netease-youdao/LobsterAI/pull/2418)) — closed today, likely shipping soon

**Pending feature requests awaiting implementation:**
- **Markdown export for session details** ([Issue #1213](https://github.com/netease-youdao/LobsterAI/issues/1213)) — PR [#1214](https://github.com/netease-youdao/LobsterAI/pull/1214) exists but is stale (4+ months); strong candidate for next release if maintainers pick it up

**Potential roadmap signals:**
- **Custom provider expansion** ([PR #1212](https://github.com/netease-youdao/LobsterAI/pull/1212), stale) — Increasing custom model providers from 10 to 20 suggests growing user demand for model flexibility
- **Error retry mechanism** ([PR #1208](https://github.com/netease-youdao/LobsterAI/pull/1208), stale) — Inline retry button for transient errors (429, network) would significantly improve user experience for Cowork sessions

---

## 7. User Feedback Summary

**Pain Points:**
- **Document analysis reliability** (Issue #1206): Duplicate progress notifications create confusion — users can't distinguish between bugs and ongoing execution, leading to wasted waiting time or premature task abandonment
- **Session export limitations** (Issue #1213): Image-only export is cumbersome for workflows requiring text manipulation, search, or archival; users resort to manual copying/screenshots

**Positive Signals:**
- The project is actively shipping UI improvements (sidebar filters) and commercial features (credit campaigns), suggesting healthy product investment
- Windows installer robustness fix (PR #2420) demonstrates attention to platform-specific reliability

**Satisfaction Indicators:**
- Issue #1206 notes that "switching models resolves the issue," suggesting the kimi2.5 integration specifically needs attention rather than the core platform

---

## 8. Backlog Watch

⚠️ **Items needing maintainer attention:**

| Item | Age | Concern |
|---|---|---|
| [PR #1208](https://github.com/netease-youdao/LobsterAI/pull/1208) — Manual retry button for Cowork session errors | 4+ months | Valuable UX improvement; inactive conversation suggests review bottleneck |
| [PR #1209](https://github.com/netease-youdao/LobsterAI/pull/1209) — Fix web-search unsupported Chrome flags | 4+ months | Addresses real-world deployment issue with Chrome 130+ compatibility |
| [PR #1212](https://github.com/netease-youdao/LobsterAI/pull/1212) — Allow up to 20 custom providers | 4+ months | Directly addresses user configurability need; API-clean solution |
| [PR #1214](https://github.com/netease-youdao/LobsterAI/pull/1214) — Markdown export feature | 4+ months | Implements requested feature (#1213); comprehensive implementation |
| [Issue #1206](https://github.com/netease-youdao/LobsterAI/issues/1206) — kimi2.5 duplicate processing bug | 4+ months | 100% reproducible bug on a documented model; stale label applied |
| [Issue #1213](https://github.com/netease-youdao/LobsterAI/issues/1213) — Markdown export request | 4+ months | Popular request with pending PR; user likely waiting for resolution |

**Analysis:** The cluster of 4+ month-old stale PRs suggests older contributions may be deprioritized in favor of newer work. With 6 closed PRs today (all from August 3), the team is active but may benefit from a **backlog triage session** to either merge or explicitly close these older contributions to reduce community uncertainty and contributor frustration.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for **2026-08-04**.

---

# Moltis Project Digest — 2026-08-04

## 1. Today's Overview
Moltis is currently in a low-activity phase, with zero issues updated and zero releases published in the last 24 hours. Developer focus is singularly directed toward **PR #1183**, which introduces managed Git repository bundles for MCP servers—a substantial backend and onboarding feature. The project is stable but quiet; no bugs or community-reported issues surfaced today, indicating a healthy maintenance state rather than a crisis. The single open PR suggests active engineering work, but the lack of merged PRs or new releases means short-term momentum is resting on the review and merge of this one significant change.

## 2. Releases
None. No new versions of Moltis were published in the last 24 hours.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. The sole piece of forward progress is the open **PR #1183 (feat(mcp): add managed repository bundles)** by `penso`. This PR advances the MCP (Model Context Protocol) infrastructure by adding:
- A lifecycle for managed Git repositories (discover, preview, install, update, rollback, remove).
- Support for HTTPS credentials and a pinned managed SSH transport.
- Vault lifecycle integration for secure credential handling.
- Imported repository-backed MCP configurations, simplifying the web onboarding flow.

While not yet merged, this represents the core feature pipeline currently being pushed toward the codebase.

## 4. Community Hot Topics
The only active item is **PR #1183**, which currently has no comments or reactions. This makes it difficult to gauge community engagement; however, the underlying need is clear: users require a more robust, credential-aware, and lifecycle-managed way to handle MCP servers. The shift from manual configuration to a managed repository bundle system indicates a demand for **GitOps-style versioning and rollback** within MCP tooling, as well as **secure, non-interactive authentication** (HTTPS/SSH) for production environments. The "simplify web onboarding" goal also signals a push to reduce friction for non-technical evaluators.
🔗 [View PR #1183](https://github.com/moltis-org/moltis/pull/1183)

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The project exhibits no new stability concerns today.

## 6. Feature Requests & Roadmap Signals
While no formal feature requests were filed, **PR #1183** is a strong roadmap signal. It suggests the next minor release will likely focus on:
- **Operational MCP management** (install/rollback/update) rather than just static configuration.
- **Security hardening** via Vault integration, which hints at enterprise or multi-tenant use cases.
- **Simplified UX** for importing and onboarding new MCP configurations.

Given the file and engineering weight of this PR, it is plausible that this feature is earmarked for the immediate next version (e.g., v0.x.1), though no release date is visible.

## 7. User Feedback Summary
There is no explicit user feedback (issues, comments, or reactions) captured in the last 24 hours. The absence of negative reports suggests general satisfaction or a lull in active usage. However, the existence of PR #1183 implies prior user pain points surrounding manual MCP server setup and credential management are being proactively addressed by the maintainers.

## 8. Backlog Watch
**No items currently require maintainer attention.** There are zero open issues and zero unanswered PRs beyond the actively updated #1183. The backlog is effectively clean, allowing maintainers to focus entirely on reviewing and landing the pending MCP feature.
🔗 [Moltis Issues](https://github.com/moltis-org/moltis/issues) | [Moltis Pull Requests](https://github.com/moltis-org/moltis/pulls)

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-04

## 1. Today's Overview

CoPaw (QwenPaw) maintains a **high-velocity development cadence** heading into the v2.1.0-beta.1 release. Activity is intense: 50 PRs updated in the last 24h (26 open, 24 merged/closed) and 22 issues touched (16 open/active, 6 closed). The new beta release ships with fixes for stale channel identity in chats and inbox UI improvements. The most significant ongoing work clusters around **API stability and compatibility with agentscope 2.0.4.post1**, **shell command reliability (timeouts, output handling, subprocess cleanup)**, and **infrastructure fixes to the CI pipeline** (the "Real behavior proof" gate is being iterated on heavily). Contributor diversity is strong, with multiple first-time contributors submitting PRs this week, indicating a healthy community funnel. However, a backlog of **silent failure bugs** (WeChat cron ret=-2, console approvals not rendering) suggests systematic gaps in observability for certain channel paths.

## 2. Releases

**v2.1.0-beta.1** was published (2026-08-03, 4-hour verification window).
- `fix(chat)`: prevent stale channel identity leaking into new chats
- `feat(inbox)`: wobble sidebar inbox on new approvals & color-code badge dot

This is a **beta release** — no breaking changes or migration notes highlighted in the changelog snippet. The release verification issue (#6656) required installation checks across platforms within a 4-hour deadline, indicating a time-boxed release-validation process. Note the release PR URL references the `QwenPaw` repo path; there may be a repo rename occurring (agentscope-ai/CoPaw vs agentscope-ai/QwenPaw), which is worth tracking.

## 3. Project Progress

**Merged/Closed PRs (24 total in last 24h)** show a focus on hygiene and infrastructure:

- **CI pipeline fixes** — Several closed PRs address the `real-behavior-proof` gate: `#6653` (fence-aware section extraction, fixes #6626), `#6646` (fetch PR body via API for fork PRs, fixes #6563), `#6654` (cap playwright below 1.62 to fix macOS desktop verify timeout). These unblock external contributors.
- **`spawn_subagent` schema fix** — `#6609` (closed) replaces `Optional[list | str]` with `list | str | None` to correct schema inference (fixes #6588). A follow-up PR `#6658` (open) further normalizes empty placeholders.
- **Desktop Python execution** — `#6579` (closed) addresses the bundled Python interpreter for script execution, directly responding to Issue #6160.
- **Windows liveness probe** — `#6203` (closed) fixes the `tasklist` probe in `command_runner.py` (bound + hide the tasklist window).
- **`batch` placeholder normalization** — `#6658` (open) handles empty `batch=[]`, `""`, or `"[]"` placeholders from OpenAI Responses-compatible endpoints.

**Open PRs of note (feature work):**
- `#5930` — structured run outcome to SSE response for API automation (open since July 10, significant for Java-service integrations).
- `#6659` / `#2199` — model fallback with cooldown mechanism. Two PRs exist for the same feature; `#6659` is a newer implementation by a different author; the older `#2199` has been open since March and is still unmerged — a sign of review friction.
- `#6302` — unify provider discovery, model metadata, routing, and agent controls (large architectural PR, open since July 21).
- `#6650` — skill loading redundancy: separates lightweight list summaries from on-demand detail responses, directly addressing the slow-network UI timeouts (Issues #6633, #6635).
- `#6651` — file/folder management REST API for the `/files` page (6 missing operations, reuses FileGuard security model).
- `#6652` — enforce `max_iterations` server-side in MissionGate (fixes #6505 where controller LLM produced 54+ sub-sessions instead of configured 20).
- `#6616` — fix CLI headless task command building invalid user message for agentscope 2.0.4.post1.
- `#6657` — report sandbox constraints the backend cannot enforce, eliminating silent config gaps (e.g., `deny_paths` not applied by `NoneSandbox`).
- `#6623` — prevent final text loss in ACP when notifications race prompt response (fixes #6625).

## 4. Community Hot Topics

The most actively discussed items (by comment count) reveal three pain clusters:

1. **Skill tags regression** — Issue #6537 (closed, 11 comments): Skill tags disappear on restart; regression of #3270. High user impact since data is saved correctly but lost during manifest reconciliation. The fix path is unclear from the issue, but the closure suggests resolution.

2. **GPT-5.6 prompt caching** — Issue #6649 (open, 8 comments): Support for `prompt_cache_key`, `prompt_cache_options`, `prompt_cache_breakpoint` in the Responses API provider to enable prefix caching in multi-turn agent loops. This is a clear roadmap signal — reducing latency/cost is a priority for the Chinese-speaking user base.

3. **`spawn_subagent` batch placeholder bug** — Issue #6588 (open, 6 comments): Three-step failure chain when LLMs pass empty placeholders. Multiple PRs (#6609, #6658, #6595) address different angles, showing active but somewhat fragmented fixes.

Other significant threads: Issue #6160 (standalone Python environment for desktop, 4 comments), Issue #6655 (console channel silently fails on security approvals, 3 comments), Issue #6608 (long-running shell commands bypass timeout, 3 comments).

## 5. Bugs & Stability

Ranked by severity:

**Critical (silent failures / data loss):**
- **Issue #6614** — WeChat cron pushes **never delivered** but reported success (ret=-2, `context_token` invalid). ~44M tokens burned in retries. This is a costly silent failure eroding trust.
- **Issue #6655** — Console channel does not render security approval prompts; blocked commands silently time out after 300s with zero user visibility. This is a security UX failure — users may think a command executed.
- **Issue #6608** — Long-running shell commands bypass `shell_command_timeout`, blocking Feishu sessions for 1.5 hours; orphan subprocess on cancel; no per-channel total timeout.

**High (crashes / freezes):**
- **Issue #6647** — Desktop UI goes fully black when WebView2 browser process crashes (STATUS_IN_PAGE_ERROR 0xc0000006); no recovery path, forcing app restart.
- **Issue #6589** (closed) — `execute_shell_command` with tens of thousands of stdout lines freezes the UI (fixed? closure suggests a fix landed).
- **Issue #6619** — `"ToolCallBlock" object has no field "extra_content"` crash in `openai_chat_model_compat._parse_stream_response` — agentscope 2.0.4.post1 compatibility break.
- **Issue #6612** — QwenPaw 2.0.1 incompatible with agentscope 2.0.4.post1: proactive subsystem crashes and tool-permission deadlock. This is a **dependency-version landmine** — a common but dangerous failure mode.

**Medium (functional regressions):**
- **Issue #6537** (closed) — Skill tags disappear on restart (regression of #3270).
- **Issue #6588** — `spawn_subagent` empty batch placeholders treated as batch mode. Fix PRs exist: #6609 (closed), #6658 (open), #6595 (open).
- **Issue #6565** — Multi-line shell commands: newlines outside quotes collapsed to spaces breaking syntax; Linux PIPE mode background processes hang.
- **Issue #6635 / #6633** — Console pages and Skills/Skill Pool fail to load on slow networks; MB-level uncompressed API responses vs fixed 30s frontend timeout. Fix PR #6650 open.

**Low (UX polish):**
- **Issue #6547** (closed) — Misplaced cursor in Coding Mode editor.
- **Issue #6624** — Auto-compaction (Scroll) does not trigger `summarize_when_compact` memory flow; manual `/compact` works. User flagged as possibly by-design.

## 6. Feature Requests & Roadmap Signals

The following requests are strong candidates for next releases:

1. **Model fallback with cooldown** (PRs #6659, #2199): Multiple users requesting automatic failover on rate limits/timeouts. Two competing PRs suggest maintainers should consolidate. Long-open #2199 (since March) implies priority might be rising.

2. **Task-scoped output directories** (Issue #6643): Users want a dedicated directory per task instead of dumping all artifacts into `media/`. Simple to implement, high UX value.

3. **Direct file path reading on drag-drop** (Issue #6642): Users want to read original file paths instead of uploading/copying to media. Privacy- and clutter-motivated.

4. **GPT-5.6 prompt caching** (Issue #6649): Cost/latency optimization; likely to be picked up quickly given the author's detailed parameter spec.

5. **Structured SSE run outcomes** (PR #5930): Proposed by a Java-service integrator; extends the SSE stream with explicit run termination reasons. This is an API-surface evolution that needs maintainer sign-off.

6. **Unified provider discovery/metadata/routing** (PR #6302): Large architectural PR; if merged, it changes how providers are configured. High impact, likely a v2.2+ roadmap item.

7. **WeChat push reliability** (Issue #6614): Though reported as a bug, the underlying ask is reliable OAuth token refresh and visible delivery status. Expect this to be prioritized given the token burn.

**Prediction for v2.1.0 stable:** The beta already contains the chat identity fix and inbox UI. Likely additions before stable: spawn_subagent empty-batch fix (#6658), CLI task message fix (#6616), and possibly the sandbox constraint reporting (#6657). The skill payload reduction (#6650) may also make it in if testing goes well.

## 7. User Feedback Summary

**Satisfaction drivers:**
- The project is responsive to regression reports — Issues #6537 and #6589 were closed quickly with fixes.
- API-driven automation (SSE, Java services) is being actively enhanced, indicating B2B/integration usage growth.
- The desktop app is on a fast release cadence (v2.0.1 → v2.1.0-beta.1 in days).

**Pain points (recurring themes):**
- **Silent failures frustrate trust**: WeChat push reports success but never delivers (#6614); console channel swallows approval prompts (#6655); mission mode doesn't enforce max_iterations (#6652). Users repeatedly discover failures only after significant token/time burn.
- **Dependency management**: `agentscope` upgrades breaking QwenPaw is a top pain point (#6612, #6619). The project ships with a pinned older agentscope, creating an upgrade cliff for users who install latest from PyPI.
- **Shell command execution is fragile**: three separate bugs (#6565, #6608, #6589) around newlines, timeouts, and output handling — this is the most frequent technical complaint this week.
- **Slow-network UX**: MB-level uncompressed API responses causing 30s timeouts (#6633, #6635) — real pain for users on WAN/VPN links.
- **Onboarding gap for multi-agent**: A user (Issue #6621) invested 50+ conversations before discovering that Default Agent doesn't auto-invoke other agents without explicit PROFILE.md instructions. This is a documentation/discoverability failure.

**Satisfaction signal**: The shift from "I can't use this" to "this behavior is suboptimal and here's my suggested fix" indicates increasing user sophistication and product maturity. Chinese-language users are active and contributing detailed, well-structured reports (often in Chinese, with English summaries).

## 8. Backlog Watch

Issues and PRs that need maintainer attention (long-open, important, or stalled):

- **PR #2199** — Automatic model fallback with cooldown (open since 2026-03-24, 133 days). With a newer duplicate #6659 now open, this needs consolidation. Very high user value; two implementations signal demand, but neither has reached merge.

- **Issue #6614** — WeChat cron silent delivery failure (updated 2026-08-03, open since July 31). Token burn is severe; no visible fix PR yet.

- **PR #5930** — Structured SSE run outcome (open since July 10, 25 days). This is a significant API enhancement for automation users; needs a maintainer to review and shepherd.

- **Issue #6621** — Multi-agent coordination discoverability (open since Aug 1). Not a bug, but a UX/documentation gap; requires product-level decision on default behavior (proactive agent invocation).

- **Issue #6160** — Bundled Python for desktop (open since July 16, closed today but likely needs documentation of the fix). The fix PR #6579 is merged, so the issue closure is expected. Watch for regressions.

- **PR #6658 vs #6595** — Two open PRs for the same bug (#6588) — maintainers should pick one and close the other to avoid review split.

- **Issue #6608** — Long-running shell commands bypassing timeout — no fix PR yet. This is a high-severity bug affecting channel reliability, not just UX.

- **WebView2 black-screen crash** (#6647) — No fix PR yet. For a desktop app, an uncrashable UI shell is table-stakes; this regression should be prioritized.

---

**Health assessment**: CoPaw is a **fast-moving, contributor-friendly project** with a strong community in both English and Chinese. The main risks are: (1) dependency-version fragility with `agentscope`, (2) a pattern of silent failures in channel integrations (WeChat, Console, Feishu) that erodes user trust, and (3) review backlog on high-value PRs (#2199, #5930). The CI tooling is consuming maintainer attention this week, which is healthy in the short term (enabling fork contributions) but should not distract from runtime reliability fixes. Overall trajectory is positive; the v2.1.0-beta.1 release is on schedule with meaningful UX improvements.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-04

## 1. Today's Overview

ZeroClaw is in an intensive stabilization and architecture-hardening phase, with 50 issues and 50 PRs updated in the last 24 hours. The project shows strong momentum toward the v0.9.0 milestone, with significant activity clustered around security (SSRF gates, approval authorization, credential rotation), observability (OTel trace correlation, DORA telemetry retirement), and configuration migration. Maintainer attention is heavily consumed by a large queue of high-priority RFCs and design decisions, many of which are still awaiting review — indicating a potential bottleneck in the decision-making pipeline. The release cadence has paused (0 new releases), suggesting the team is consolidating breaking changes for the next major version rather than shipping incrementally.

## 2. Releases

No new releases were published in the last 24 hours. The project appears to be in a pre-release consolidation phase, with a substantial queue of breaking-change PRs and RFCs targeting v0.9.0 (tracked in [#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432)). Users should expect a substantial release with breaking changes when it lands.

## 3. Project Progress

Three PRs were closed/merged today, though the project's primary progress is visible through active high-priority PRs:

**Active High-Impact PRs:**

- **Security hardening:**
  - [PR #9574](https://github.com/zeroclaw-labs/zeroclaw/pull/9574) — Authorize approval responders for Telegram, Slack, Lark, and Matrix channels (size:L, risk:high, priority:p1). Addresses critical audit-trail integrity concerns.
  - [PR #9720](https://github.com/zeroclaw-labs/zeroclaw/pull/9720) — Enforce response cache request boundaries; restricts caching to deterministic requests (size:L, risk:high, priority:p1).
  - [PR #9606](https://github.com/zeroclaw-labs/zeroclaw/pull/9606) — Honor runtime proxy for OpenAI Responses API path (size:M, risk:high, priority:p1).
  - [PR #8713](https://github.com/zeroclaw-labs/zeroclaw/pull/8713) — Add `allowed_private_hosts` opt-in to `file_download` SSRF gate (size:XL, risk:high).

- **Provider reliability:**
  - [PR #9419](https://github.com/zeroclaw-labs/zeroclaw/pull/9419) — Rotate live credentials after rate limits; cool only the credential that returned a retryable 429 (size:XL, risk:high).
  - [PR #9404](https://github.com/zeroclaw-labs/zeroclaw/pull/9404) — Accept data-wrapped compatible chat responses for external providers.

- **CI and build:**
  - [PR #9637](https://github.com/zeroclaw-labs/zeroclaw/pull/9637) — Guard temporary React Router RSC npm advisory exception (priority:p1).
  - [PR #9514](https://github.com/zeroclaw-labs/zeroclaw/pull/9514) — Add opt-in multi-arch Alpine image using cargo-zigbuild.

## 4. Community Hot Topics

The most active discussions center on architectural direction and security design:

1. **[RFC: Goal mode v1 — bounded foreground Matrix work](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)** (11 comments, 1 👍) — The most-discussed item. Proposes a durable way to pursue bounded user objectives across multiple agent turns. The discussion highlights the project's ambitious scope for agentic behavior and the fine line between control-plane and data-plane responsibilities.

2. **[Maintainer decision queue tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)** (8 comments) — A meta-issue tracking RFCs and design decisions awaiting maintainer action. Its very existence signals a backlog of decisions that need resolution before v0.9.0 can ship.

3. **[RFC: Unified attachment architecture for web chat and channels](https://github.com/zeroclaw-labs/zeroclaw/issues/9488)** (8 comments) — Proposes consolidating file/attachment handling across web chat and all channel backends. Underlying need: inconsistent UX and duplicated logic in how different channels handle uploads.

4. **[RFC: Structured Observability Enhancement](https://github.com/zeroclaw-labs/zeroclaw/issues/7232)** (5 comments) — Rich events, OTel trace correlation, and bridge refactoring. Community is pushing for better production debuggability without exposing sensitive prompt/tool content in telemetry.

5. **[RFC: Schema-validated memory consolidation](https://github.com/zeroclaw-labs/zeroclaw/issues/6998)** (3 comments, updated today) — Fragile JSON parsing for memory consolidation across providers; proposes schema validation with bounded fallback.

## 5. Bugs & Stability

**Critical/S1:**

- **[MacOS desktop app can reopen blank or without window](https://github.com/zeroclaw-labs/zeroclaw/issues/7527)** (priority:p1, needs-repro) — Blank window on relaunch, permission detection issues on macOS 15.7.7. No fix PR yet; blocked on reproduction.

**High (S2/S3, with fixes in progress):**

- **[Telegram delivers duplicate messages when model emits tool_call + content](https://github.com/zeroclaw-labs/zeroclaw/issues/9718)** (new today, priority:bug) — Defensive handling needed when LLM returns both `tool_calls` and populated `content`. No PR yet.

- **[Approval timeout recorded as explicit operator denial](https://github.com/zeroclaw-labs/zeroclaw/issues/9642)** (priority:p1, closed) — Audit-trail falsification: timed-out Telegram approval cards are logged as human denial. Closed as in-progress; likely fixed via [PR #9574](https://github.com/zeroclaw-labs/zeroclaw/pull/9574).

- **[Nextcloud Talk uses wrong bot message API](https://github.com/zeroclaw-labs/zeroclaw/issues/6157)** (risk:high, blocked) — Bot secret passed incorrectly in URL construction. Blocked on maintainer decision.

- **[vi_verify registered as model-callable tool](https://github.com/zeroclaw-labs/zeroclaw/pull/9472)** — Removed: `vi_verify` deserialized constraints and fulfillment from model-supplied args with no signature verification. Security-sensitive fix in review.

**Stability improvements in flight:** [PR #9722](https://github.com/zeroclaw-labs/zeroclaw/pull/9722) preserves timeout error context (Uno Q connect), [PR #9721](https://github.com/zeroclaw-labs/zeroclaw/pull/9721) gates SIGTERM cleanup to Unix for Windows Clippy lane.

## 6. Feature Requests & Roadmap Signals

Strong signals for v0.9.0 features:

- **Goal mode** ([#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)) — Multi-turn bounded objective pursuit. Likely a headline feature but still in RFC; uncertain for next release.
- **SOP capability permission contract** ([#9598](https://github.com/zeroclaw-labs/zeroclaw/issues/9598)) — Target v0.9.0; make `required_permissions` authoritative via shared security pipeline.
- **Session persistence contract** ([#9600](https://github.com/zeroclaw-labs/zeroclaw/issues/9600)) — Four independent workstreams touch the same contract; ownership tracker in place.
- **Turn-level OTel trace correlation** ([#6641](https://github.com/zeroclaw-labs/zeroclaw/issues/6641), merged) — Nest `llm.call` / `tool.call` / `memory.*` under single turn trace. Shipped.
- **Session TTL enforcement** ([#8134](https://github.com/zeroclaw-labs/zeroclaw/issues/8134)) — Implement `session_ttl_hours` to auto-truncate stale channel history. Accepted, no PR yet.
- **Gateway WebSocket decoupling** ([#7759](https://github.com/zeroclaw-labs/zeroclaw/issues/7759)) — Priority:p1; run turns in background, resume on reconnect. Accepted, no PR.
- **Rust→Wasm web UI** ([#8132](https://github.com/zeroclaw-labs/zeroclaw/issues/8132)) — Replace React/Vite with Dioxus/Leptos/Yew. Priority:p3, needs author action; likely deferred.

## 7. User Feedback Summary

Real user pain points emerging from issues:

- **Security trust:** Users are actively testing and reporting security issues (XOR cipher critique [#1](https://github.com/zeroclaw-labs/zeroclaw/issues/1), SSRF gaps, approval-timeout audit issues). The community is security-conscious and expects rapid hardening.
- **Configuration complexity:** Multiple issues related to config migration and alias handling ([#9246](https://github.com/zeroclaw-labs/zeroclaw/issues/9246), [#9707](https://github.com/zeroclaw-labs/zeroclaw/pull/9707)) suggest the V3 config migration is causing friction.
- **Channel UX:** Users report inconsistent behavior across channels — Telegram duplicates ([#9718](https://github.com/zeroclaw-labs/zeroclaw/issues/9718)), Slack silence during long tasks ([#7113](https://github.com/zeroclaw-labs/zeroclaw/issues/7113)), and Nextcloud Talk API issues ([#6157](https://github.com/zeroclaw-labs/zeroclaw/issues/6157)).
- **Attribution and transparency:** Requests for structured observability ([#7232](https://github.com/zeroclaw-labs/zeroclaw/issues/7232)) and harness context injection ([#9005](https://github.com/zeroclaw-labs/zeroclaw/issues/9005)) show users want to understand *why* the agent behaves as it does.
- **Process fatigue:** The large number of RFCs and trackers (decision queue [#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)) may be slowing perceived progress, but also shows a healthy, transparent governance model.

## 8. Backlog Watch

Issues/PRs needing maintainer attention (high importance, long-open, or stale):

- **[RFC: Replace React/Vite with Rust→Wasm](https://github.com/zeroclaw-labs/zeroclaw/issues/8132)** — Opened 2026-06-22, priority:p3, needs-author-action, 1 👍. Long-running architectural discussion; if seriously considered it's a multi-month effort.
- **[ [Bug]: macOS blank window](https://github.com/zeroclaw-labs/zeroclaw/issues/7527)** — Opened 2026-06-12, priority:p1, needs-repro. Critical desktop UX bug unanswered for over a month.
- **[RFC: Workspace-relative forbidden path patterns](https://github.com/zeroclaw-labs/zeroclaw/issues/8424)** — Opened 2026-06-28, risk:high, needs-author-action. Security-relevant (protecting `.env`, `config.yaml`); important for enterprise adoption.
- **[PR: SSRF gate for file_download](https://github.com/zeroclaw-labs/zeroclaw/pull/8713)** — Size:XL, risk:high, needs-author-action, opened 2026-07-04. Critical security PR flagged stale-candidate; needs maintainer review or revision.
- **[RFC: Staged opt-in product telemetry](https://github.com/zeroclaw-labs/zeroclaw/issues/9621)** — Newer (2026-08-01) but directly addresses maintainer blind spots on feature usage; high architectural importance.
- **[CI: Validate Containerfile changes in PR CI](https://github.com/zeroclaw-labs/zeroclaw/issues/9456)** — Opened 2026-07-27, risk:high. Prevents container-build regressions; approved-labor but no PR yet.

---

*Digest generated from ZeroClaw GitHub activity on 2026-08-04. All items sourced from [ZeroClaw repository](https://github.com/zeroclaw-labs/zeroclaw).*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*