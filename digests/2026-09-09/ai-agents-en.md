# OpenClaw Ecosystem Digest 2026-09-09

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-09-09 09:31 UTC

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

# OpenClaw Project Digest — 2026-09-09

## 1. Today's Overview

OpenClaw shows very high activity: 500 issues and 500 PRs were updated in the last 24 hours, with **217 issues closed** and **206 PRs merged/closed** — indicating strong triage throughput. A new patch release, **v2026.9.3**, shipped with a focus on safer self-update mechanics (candidate-state rehearsal and abandoned-update recovery), directly targeting a cluster of update-path regressions reported in 2026.8.x/9.x. Despite the volume of closed work, several **P0 release-blockers remain open**, notably Codex OAuth refresh timeouts ([#89278](https://github.com/openclaw/openclaw/issues/89278)), a Windows de-DE upgrade maintenance block ([#136203](https://github.com/openclaw/openclaw/issues/136203)), and Feishu plugin tools being silently dropped ([#140971](https://github.com/openclaw/openclaw/issues/140971), fix PR open). Community reporting continues to concentrate on regressions introduced in the 2026.8.1–2026.9.2 range, with auth-provider and message-loss impact areas dominating.

## 2. Releases

**v2026.9.3** ([release](https://github.com/openclaw/openclaw/releases/tag/v2026.9.3)) — openclaw 2026.9.3

Highlights:
- **Safer updates:** core and plugin changes are now rehearsed in an isolated candidate state before activation.
- **Migration support:** eligible 2026.9.2 migrations are supported.
- **Recovery:** abandoned update records can be recovered without stopping a healthy matching Gateway (related [#136997](https://github.com/openclaw/openclaw/issues/136997)).

No breaking changes or explicit migration steps were announced. The release appears designed to address the update-path pain visible in the tracker: stuck npm updates ([#141617](https://github.com/openclaw/openclaw/issues/141617)), core/plugin version skew after `openclaw update` ([#135776](https://github.com/openclaw/openclaw/issues/135776)), and Windows upgrade maintenance locks ([#136203](https://github.com/openclaw/openclaw/issues/136203)).

## 3. Project Progress

**Merged/closed today: 206 PRs; 217 issues closed.**

Notable PRs currently in the pipeline (updated in last 24h):

- **Discord presence fix — merged/closed:** [#141218](https://github.com/openclaw/openclaw/pull/141218) — show member presence immediately after reconnect (fixes [#141054](https://github.com/openclaw/openclaw/issues/141054)).
- **Feishu tool siloing fix (P0 regression):** [#141984](https://github.com/openclaw/openclaw/pull/141984) — avoids collateral drop of non-restricted Feishu tools; closes [#140971](https://github.com/openclaw/openclaw/issues/140971).
- **iMessage bridge recovery:** [#142626](https://github.com/openclaw/openclaw/pull/142626) — restores typing indicators/read receipts after bridge recovery; automerge armed.
- **Memory recall reliability:** [#142693](https://github.com/openclaw/openclaw/pull/142693) — continues memory recall when optional trigger lookup times out; closes [#142479](https://github.com/openclaw/openclaw/issues/142479).
- **OpenAI-compatible provider text doubling:** [#142888](https://github.com/openclaw/openclaw/pull/142888) — fixes live assistant text duplicating when providers resend full content in one delta; closes [#136262](https://github.com/openclaw/openclaw/issues/136262).
- **Image job lifecycle:** [#142991](https://github.com/openclaw/openclaw/pull/142991) — keeps accepted `image_generate` jobs alive through provider cleanup (related [#140674](https://github.com/openclaw/openclaw/issues/140674)).
- **Documentation restructure:** a sustained effort by vincentkoc to split oversized docs pages (ledger findings) — gateway CLI ([#143005](https://github.com/openclaw/openclaw/pull/143005)), browser tools ([#142984](https://github.com/openclaw/openclaw/pull/142984)), subagents ([#142999](https://github.com/openclaw/openclaw/pull/142999)), Ollama provider ([#143004](https://github.com/openclaw/openclaw/pull/143004)), Matrix channel ([#142996](https://github.com/openclaw/openclaw/pull/142996)), TTS ([#142992](https://github.com/openclaw/openclaw/pull/142992)), and the Updating guide ([#142993](https://github.com/openclaw/openclaw/pull/142993)).
- **Mobile/edge surfaces

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — Personal AI Assistant / Agent Open-Source Ecosystem
**Date:** 2026-09-09 | **Source:** Community digest summaries for 10 projects (2 unavailable)

---

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem remains dominated by OpenClaw-derived or OpenClaw-compatible architectures, with the core reference project processing an extraordinary ~1,000 items/day of issue+PR activity and shipping regular patch releases. The broader landscape shows a two-speed dynamic: a few high-throughput projects (OpenClaw, LobsterAI, NanoBot, Hermes Agent) are absorbing large volumes of triage and compatibility work, while a long tail of smaller forks (PicoClaw, NanoClaw, IronClaw, ZeptoClaw) iterate on niche channel integrations and edge deployments. Across all active projects, the dominant themes are update-path reliability, IM channel compatibility after upstream upgrades, provider/routing flexibility, and security hardening — indicating an ecosystem maturing from "demo-ware" into production operations. Notably, CoPaw and ZeroClaw failed digest generation this cycle, and three projects (NullClaw, TinyClaw, Moltis) recorded zero activity, suggesting consolidation or stalled maintenance in parts of the ecosystem.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release (24h) | Health Score¹ | Notes |
|---|---|---|---|---|---|
| **OpenClaw** | 500 updated / 217 closed | 500 updated / 206 merged-closed | ✅ v2026.9.3 | **9/10** | Extreme throughput; P0 blockers remain (OAuth, Windows upgrade, Feishu tools) |
| **LobsterAI** | 20 updated / 4 closed | 14 touched / 12 merged-closed | ❌ | **7/10** | High merge velocity; 5 open security advisories; compatibility-fix driven |
| **NanoBot** | 2 updated | 27 touched / 8 closed | ❌ | **8/10** | Fast, focused WebUI/TUI fixes; healthy maintainer cadence |
| **Hermes Agent** | 50 updated / 11 closed | 50 updated / **0 merged** | ❌ | **6/10** | Heavy triage but review/landing backlog; no code landed |
| **IronClaw** | 2 open | 11 touched / 5 merged-closed | ❌ | **7/10** | Focused MCP catalog work; security issue open since July |
| **PicoClaw** | 3 updated / 1 closed | 8 touched / 1 closed | ❌ | **6/10** | Good contributor output; maintainer review lagging |
| **NanoClaw** | 2 open | 10 touched / 2 merged | ❌ | **7/10** | Active, targeted fixes; 2 operational bugs without fix PRs |
| **ZeptoClaw** | 1 open | 1 open | ❌ | **5/10** | Light activity; security fix pending review |
| **NullClaw** | — | — | ❌ | **1/10** | No activity |
| **TinyClaw** | — | — | ❌ | **1/10** | No activity |
| **Moltis** | — | — | ❌ | **1/10** | No activity |
| **CoPaw** | — | — | — | **N/A** | Digest generation failed |
| **ZeroClaw** | — | — | — | **N/A** | Digest generation failed |

¹ Composite of activity volume, merge velocity, issue closure rate, and blocker severity. Qualitative estimate for decision-making, not a formal metric.

---

## 3. OpenClaw's Position

OpenClaw is the undisputed ecosystem hub: its 24-hour throughput (500 issues, 500 PRs, 217 issue closures, 206 PRs merged/closed) exceeds the combined activity of all other tracked projects by an order of magnitude. Its technical leadership rests on three pillars: (1) a **safer self-update mechanism** (candidate-state rehearsal, abandoned-update recovery in v2026.9.3) that directly addresses the ecosystem's most painful failure mode; (2) **breadth of channel/provider support** — Discord, Feishu, iMessage, Matrix, OpenAI-compatible providers — while smaller projects handle one or two channels; and (3) **release discipline**, shipping versioned patches while most peers remain unreleased on `main`. Its main vulnerabilities are the cluster of open P0 regressions (Codex OAuth refresh timeouts, Windows de-DE upgrade maintenance lock, Feishu tool siloing) — all concentrated in the 2026.8.1–2026.9.2 range, which is precisely the upgrade wave now breaking across downstream projects like LobsterAI. Community-size comparison is stark: OpenClaw's 217 closed issues in one day exceeds the total open+closed item count of all smaller projects combined.

---

## 4. Shared Technical Focus Areas

Cross-project requirements emerging independently across multiple codebases:

| Focus Area | Projects Affected | Specific Needs |
|---|---|---|
| **Update/upgrade path reliability** | OpenClaw, LobsterAI, NanoClaw, PicoClaw | Stuck npm updates, core/plugin version skew, Windows upgrade locks, upgrade-triggered channel breakage, broken `/update-nanoclaw`, config schema mismatch after nightly builds |
| **IM channel integration robustness** | OpenClaw, LobsterAI, PicoClaw, NanoClaw, IronClaw | Feishu tools silently dropped; Telegram reply/mention handling, runaway edit loops, document context loss; WhatsApp JID filtering; DingTalk/Lark/NIM/QQ compatibility after upstream bump; IRCv3 multiline |
| **Provider/routing flexibility** | ZeptoClaw, NanoClaw, Hermes Agent, OpenClaw | OrcaRouter support; OpenCode provider contracts; OpenAI-compatible text doubling; streaming SSE fixes; provider-agnostic session headers |
| **Context & memory management** | OpenClaw, Hermes Agent, NanoClaw, IronClaw, LobsterAI | Memory recall timeouts, unbounded conversation archive growth, prompt-context token budget overrides, pointer mode for document inlining, persistent cross-session memory |
| **Security & authentication** | ZeptoClaw, LobsterAI, IronClaw, OpenClaw | WebSocket bearer-token exposure, unauthenticated local token proxy, symlink file disclosure, cross-user MCP metadata leakage, OAuth refresh timeouts |
| **MCP / tool catalog lifecycle** | IronClaw, Hermes Agent | Per-principal catalog isolation (not per-extension), profile-scoped MCP reliability, catalog merge vs. replace semantics |
| **Task scheduling correctness** | NanoClaw, LobsterAI | Recurrence changes not rescheduling next fire time; cron run-history duplication after upgrades |
| **WebUI/desktop stability** | NanoBot, LobsterAI | UI freezes, skill picker refresh, project-selection races, backup deadlocks |

---

## 5. Differentiation Analysis

| Project | Core Focus | Target Users | Architecture / Notable Traits |
|---|---|---|---|
| **OpenClaw** | Full-featured reference assistant; update safety; broad channel support | General developers, self-hosters | Gateway + plugins + candidate-state rehearsal; largest contributor base |
| **Hermes Agent** | Research-grade agent runtime (NousResearch) | AI researchers, multi-profile deployments | Multiplexed gateway, compute-host PID supervision, vision format breadth (HEIC/AVIF), profile-scoped MCP |
| **LobsterAI** | Desktop app for Chinese ecosystem | NetEase Youdao users; China market | Bundles OpenClaw core; QQ/DingTalk/Lark/NIM/Bee channels; i18n; Windows desktop UX |
| **NanoBot** | Lightweight agent with strong WebUI/TUI | Hobbyists, local-first users | Focus on UI polish; streaming math rendering; TUI `/usage`; skill picker |
| **IronClaw** | Hosted-MCP & extension system | Multi-tenant server operators | Rust/crate-based extension packaging; per-principal tool catalog keying; SEP-414 attribution |
| **PicoClaw** | Channel-reliability specialist (Sipeed) | Hardware/edge users, IRC/Telegram communities | Small-footprint; phone-pairing adapter; IRCv3 multiline; Telegram mention-only workflows |
| **NanoClaw** | Community/ops-focused agent (Echo/Slack portal) | Self-hosters, WhatsApp users | Community-cell setup in browser; thread-per-invocation routing; WhatsApp edge cases |
| **ZeptoClaw** | Ultra-lightweight Rust binary (~6MB, ~50ms startup) | Edge/IoT, constrained environments | Minimal footprint as value proposition; needs broader provider support |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapid iteration / shipping:** OpenClaw is the only project shipping releases this cycle and sustaining four-digit monthly throughput; its v2026.9.3 release marks a stabilizing phase after the 2026.8.x regression wave. LobsterAI is iterating fastest per-capita — 12 PRs merged in one day — but is in a reactive compatibility-fix mode with an accumulating security-debt backlog.

**Tier 2 — Active but backlog-bound:** NanoBot shows the healthiest maintainer cadence (small fixes closed quickly, no release needed). Hermes Agent is in a "review bottleneck": 50 PRs touched, zero merged — strong contributor interest but poor landing velocity. NanoClaw and IronClaw are steadily landing targeted fixes; IronClaw shows healthy refinement loops, though repeated rework on the same MCP catalog bug signals weak upfront design specification.

**Tier 3 — Contributor-led, maintainer-starved:** PicoClaw has engaged contributors submitting real bug fixes (Telegram runaway animation, IRC multiline) but no merges this cycle; several PRs risk staleness. ZeptoClaw has a high-value security fix waiting for review.

**Tier 4 — Dormant/failed:** NullClaw, TinyClaw, Moltis had zero activity; CoPaw and ZeroClaw digest generation failed — ecosystem consolidation appears underway.

---

## 7. Trend Signals

1. **Update mechanics are the new moat.** Three separate projects (OpenClaw, LobsterAI, NanoClaw) are actively fixing upgrade-induced breakage. OpenClaw's candidate-state rehearsal will likely become the reference pattern; downstream projects must design for upstream-version skew as a first-class concern.

2. **Multi-tenant isolation is the next security frontier.** IronClaw's cross-user MCP metadata exposure (#6778) and LobsterAI's five open security advisories signal that single-user assumptions are breaking as agents move to shared servers. Per-principal keying, ticket-based WebSocket auth, and SSRF guard defaults will be differentiators.

3. **Context-window economics are driving architecture.** Independent signals: IronClaw's pointer/reference mode for document inlining, prompt-context limit overrides, NanoClaw's unbounded archive complaint, and LobsterAI's token-waste reports all point to the same conclusion — token/context management is becoming a user-visible product feature, not just an internal detail.

4. **Provider agnosticism is table stakes.** OpenClaw fixes OpenAI-compatible duplication, ZeptoClaw users request OrcaRouter, NanoClaw integrates OpenCode, Hermes Agent fixes Gemini SSE. Agents that lock to a single provider will lose mindshare

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

## 1. Today’s Overview

NanoBot showed a high level of activity on 2026-09-09: 27 pull requests were updated in the last 24 hours, with 8 moving to closed status and 19 remaining open. The bulk of closed work centered on WebUI stability and UX fixes — project selection, skill picker refresh, streaming math rendering, activity layout, and performance — plus a new TUI `/usage` feature. Only 2 issues were updated, one closed feature request and one open WebUI bug. No new releases were published. Overall project health looks strong: maintainers are closing small, focused fixes quickly while continuing to iterate on larger WebUI settings/sidebar and TUI onboarding efforts.

## 2. Releases

No new NanoBot releases were published in this window. There are no changelog entries, breaking changes, or migration notes to report.

## 3. Project Progress

Eight PRs moved to closed status in the last 24 hours. These represent the main landed/closed work:

- [PR #5717](https://github.com/HKUDS/nanobot/pull/5717) — `fix(webui): preserve project when creating a topic from its menu`  
  Fixes a race where changing the URL hash cleared the selected project after creating a topic from a project context menu.

- [PR #5703](https://github.com/HKUDS/nanobot/pull/5703) — `perf(webui): reduce repeated work and bound history rendering`  
  Reduces repeated DOM scans, bounds expensive rendering/caching paths for long conversations and tool-heavy responses.

- [PR #5716](https://github.com/HKUDS/nanobot/pull/5716) — `fix(webui): refresh skill suggestions when opening the picker`  
  Ensures newly installed agent skills appear in the WebUI picker without requiring a page reload.

- [PR #5714](https://github.com/HKUDS/nanobot/pull/5714) — `fix(webui): keep edit diffs outside reasoning folds`  


</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-09-09

## 1. Today's Overview

Hermes Agent is in a high-activity triage window: 50 issues and 50 PRs were updated in the last 24 hours, with 11 issues closed and 39 still open/active. No PRs were merged or closed during the window, and no new releases were published. The busiest threads are dominated by automation health (#66616, 183 comments), session/time awareness (#10421), and profile-scoped MCP reliability (#106005). Contributor activity is strong, with several new PRs salvaging older community fixes, but zero merged PRs means the project is still in a review/landing backlog rather than a fast-shipping phase.

## 2. Releases

No new releases in this window.

## 3. Project Progress

No PRs were merged or closed in the last 24 hours, so no confirmed code changes landed from PRs today.

However, 11 issues were closed, mostly triage/duplicate cleanup. Notable closed bugs include:
- [Issue #105892](https://github.com/NousResearch/hermes-agent/issues/105892) — Ollama/OpenAI-compatible provider dropping conversation history (closed P1).
- [Issue #105670](https://github.com/NousResearch/hermes-agent/issues/105670) — WAL generation split-brain / state.db corruption (closed P1).
- [Issue #105396](https://github.com/NousResearch/hermes-agent/issues/105396) — Multiplexed gateway starving non-default profiles of MCP servers (closed; related #106005 remains open).
- [Issue #96742](https://github.com/NousResearch/hermes-agent/issues/96742) — SSH-only connection.json not reconciled into v2 connections registry.

Active PRs show strong forward progress, especially “salvage” PRs that revive older community work:
- [PR #106419](https://github.com/NousResearch/hermes-agent/pull/106419) — zombie-safe, Windows-safe compute-host PID supervision.
- [PR #106404](https://github.com/NousResearch/hermes-agent/pull/106404) — proxy-mode/Gemini SSE stream fix, keeping final frames and surfacing mid-stream drops.
- [PR #106408](https://github.com/NousResearch/hermes-agent/pull/106408) — HEIC/HEIF/AVIF support for `vision_analyze`.
- [PR #106409](https://github.com/NousResearch/hermes-agent/pull/106409) — preserve SSL/PQ hints in Codex device-login failures.
- [PR #106417](https://github.com/NousResearch/hermes-agent/pull/106417) — V4A Add File no longer overwrites existing files.

## 4. Community Hot Topics

- [Issue #66616 — skills index is stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616)  
  183 comments · 0 👍  
  Automated freshness probe has

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-09-09

## Today's Overview

PicoClaw showed moderate-to-high community activity on 2026-09-09: 3 issues were updated (2 still open, 1 closed as stale) and 8 pull requests were touched (7 open, 1 closed). No new releases were published. Contributor focus is heavily on channel reliability: Telegram reply handling, runaway feedback animations, IRCv3 multiline support, and a new provider integration. Maintainers closed an older skills CLI PR and a stale DeltaChat startup bug report. The project is healthy overall, but the growing stack of open PRs needs maintainer review, especially PRs that directly fix active bugs.

## Releases

No new releases were published during the report window.

## Project Progress

- [#714 [closed] skills: install/reinstall CLI and refactor into skillsCmd](https://github.com/sipeed/picoclaw/pull/714) — Closed after a long lifecycle; it proposed `ParseInstallSpec`, `InstallFromGitHubEx`, `reinstall` subcommand support, and a GitHub Trees API-based install flow.
- [#3265 [closed] Gateway startup fails with 'channel deltachat has unknown type deltachat'](https://github.com/sipeed/picoclaw/issues/3265) — Closed as stale; no active code change tied to it in this window.

No PRs were merged in the last 24 hours, so no confirmed feature/landed code progress to report beyond the closed PR above.

## Community Hot Topics

- [#3265 — Gateway startup fails with 'channel deltachat has unknown type deltachat'](https://github.com/sipeed/picoclaw/issues/3265) — Most-commented item with 4 comments and 1 👍. Although closed as stale, it highlights user confusion when an unconfigured channel still causes startup failures.
- [#3343 — Tool feedback animation can edit a Telegram message indefinitely after a failed turn](https://github.com/sipeed/picoclaw/issues/3343) — Active bug report with 3 comments; documents 228,000 edit attempts and Telegram rate limiting.
- [#3355 — config.json contains unknown field(s): channel_list.feishu.app_id](https://github.com/sipeed/picoclaw/issues/3355) — Feishu configuration error; likely a schema/versioning mismatch, with no maintainer response yet.

Underlying need: users want predictable gateway startup, clear configuration errors, and no runaway background behavior on messaging channels.

## Bugs & Stability

Ranked by severity:

1. **High — Telegram tool feedback animation runaway loop**  
   [#3343](https://github.com/sipeed/picoclaw/issues/3343) — A tool feedback animation kept calling `editMessageText` every 3 seconds for days, causing over 228,000 attempts and Telegram server-side rate limiting.  
   **Fix PR exists:** [#3353](https://github.com/sipeed/picoclaw/pull/3353) bounds animation lifetime and stops on first edit error.

2. **Medium — Feishu config validation rejects valid-looking config**  
   [#3355](https://github.com/sipeed/picoclaw/issues/3355) — Nightly build with `channel_list.feishu.app_id` reports "unknown field(s)." Needs maintainer clarification on expected schema.

3. **Low / Closed — DeltaChat startup error when not configured**  
   [#3265](https://github.com/sipeed/picoclaw/issues/3265) — Gateway failed with "unknown type deltachat" even without DeltaChat configuration. Closed as stale, but the report was never explicitly resolved.

## Feature Requests & Roadmap Signals

No new feature-request issues were filed in the window, but several open PRs signal roadmap direction:

- [#3354 — feat(irc): assemble IRCv3 multiline messages](https://github.com/sipeed/picoclaw/pull/3354) — Adds `draft/multiline` receive support so long IRC messages arrive as one message.
- [#3357 — fix(telegram): treat replies to the bot's own messages as implicit mentions](https://github.com/sipeed/picoclaw/pull/3357) — Important for `mention_only: true` group workflows.
- [#3356 — fix(telegram): re-attach quoted documents when replying to a file message](https://github.com/sipeed/picoclaw/pull/3356) — Restores document context in quoted replies.
- [#3371 — feat(providers): add opencode-go provider with session header support](https://github.com/sipeed/picoclaw/pull/3371) — Adds a dedicated provider for OpenCode Go with model-based routing and session headers.
- [#3344 — Add Build Remote Agent phone pairing (gbr/1)](https://github.com/sipeed/picoclaw/pull/3344) — New phone pairing adapter for remote spectation.

Likely next-version candidates: the Telegram fix set (#3353, #3356, #3357), IRC multiline support, and possibly the OpenCode Go provider, assuming maintainer review proceeds.

## User Feedback Summary

- **Telegram users** are frustrated by ignored replies in `mention_only` groups when replying directly to a bot message; the workaround requiring an explicit @mention breaks natural conversation flow.  
- **Telegram document context loss** is another concrete pain point: quoted replies to files only send `[file]` to the agent, losing the actual document.  
- **Runaway tool feedback animation** caused external API abuse/rate limiting and made the system appear unhealthy to users.  
- **Feishu users** hit config validation errors that should ideally be caught by clear schema/docs.  
- **IRC users** need multiline messages preserved; contributor activity suggests this is a desired capability.  
- Overall, contributors are actively submitting targeted fixes for existing bugs, indicating an engaged but somewhat frustrated user base dealing with channel-integration edge cases.

## Backlog Watch

- [#3222 — refactor(deltachat): cleanup implementation, documentation -200LOC](https://github.com/sipeed/picoclaw/pull/3222) — Open since July 3; large refactor waiting for maintainer review. May risk becoming stale.
- [#3344 — Add Build Remote Agent phone pairing (gbr/1)](https://github.com/sipeed/picoclaw/pull/3344) — Open since August 23; no visible maintainer response. Needs triage.
- [#3355 — Feishu config unknown field](https://github.com/sipeed/picoclaw/issues/3355) — Open since September 1 with one comment; no maintainer acknowledgment yet.
- [#3353 / #3356 / #3357](https://github.com/sipeed/picoclaw/pull/3353) — Telegram fix PRs opened Aug 31–Sep 1; each targets a real reported bug and should be prioritized for review/merge.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-09-09

## 1. Today's Overview
NanoClaw showed strong short-term activity: 10 pull requests were updated in the last 24 hours, 2 of them now closed/merged, while 2 issues remain open and active. No new release was published in this window, so recent fixes and features are still landing on `main` rather than reaching users via a versioned release. Development is concentrated on agent-runner threading/routing correctness, WhatsApp channel behavior, and a significant OpenCode provider integration effort. Overall project health looks healthy: contributors are actively fixing bugs and iterating on feature PRs, though two open operational/scheduling issues still lack fix PRs.

## 2. Releases
No releases were published in this cycle.

## 3. Project Progress
Two pull requests were closed/merged among the PRs updated in the last 24 hours:

- **PR #3738** — `fix(agent-runner): thread replies from the message being answered`  
  Fixes `send_message`, `send_file`, and `<message to>` replies so they land in the correct thread instead of the main channel.  
  [nanocoai/nanoclaw PR #3738](https://github.com/nanocoai/nanoclaw/pull/3738)

- **PR #3729** — `feat(setup): connect the host to its community cell and manage perks in the browser`  
  Moves Echo and Slack setup into the community portal with a single browser visit and keeps the running host linked to its account cell.  
  [nanocoai/nanoclaw PR #3729](https://github.com/nanocoai/nanoclaw/pull/3729)

Also notable: multiple open PRs show continued work on OpenCode integration, context-preview revival, WhatsApp fixes, and thread-per-invocation agent handling.

## 4. Community Hot Topics
The most-discussed items in this window are both open bug reports:

- **Issue #3735** — `conversations/ archives grow without bound — no retention, no cap` (2 comments)  
  Reports that `archiveTranscriptFile()` writes permanent markdown archives under `groups/<folder>/conversations/`, with no retention, rotation, or cap. This is an operational pain point with fleet-level impact.  
  [nanocoai/nanoclaw Issue #3735](https://github.com/nanocoai/nanoclaw/issues/3735)

- **Issue #3705** — `ncl tasks update --recurrence doesn't recompute the next scheduled fire (process_after)` (1 comment)  
  Changing a task’s cron via `--recurrence` leaves `process_after` on the old schedule, causing users to miss expected task firing times.  
  [nanocoai/nanoclaw Issue #3705](https://github.com/nanocoai/nanoclaw/issues/3705)

The underlying needs are clear: production users want bounded storage/hygiene for agent transcripts, and task scheduling must react immediately to recurrence changes.

## 5. Bugs & Stability
Ranked by estimated severity:

- **High — Unbounded conversation archive growth (#3735)**  
  Archive files accumulate forever for every agent group. This can cause disk exhaustion on long-running fleets. No fix PR is linked yet.  
  [nanocoai/nanoclaw Issue #3735](https://github.com/nanocoai/nanoclaw/issues/3735)

- **Medium — Task recurrence update does not reschedule next fire time (#3705)**  
  A stale `process_after` can make agents run too late or not at all after a cadence change. No fix PR is linked yet.  
  [nanocoai/nanoclaw Issue #3705](https://github.com/nanocoai/nanoclaw/issues/3705)

- **Medium — Replies dropped when trigger messages from multiple threads land in the same processing window (#3749)**  
  Open fix PR processes one agent invocation per thread so every thread receives its reply.  
  [nanocoai/nanoclaw PR #3749](https://github.com/nanocoai/nanoclaw/pull/3749)

- **Medium — Threaded replies routed to main channel (#3738)**  
  Addressed by the closed PR #3738.  
  [nanocoai/nanoclaw PR #3738](https://github.com/nanocoai/nanoclaw/pull/3738)

- **Medium — `/update-nanoclaw` broken because `scripts/provider-contract-verifier.ts` is omitted (#3750)**  
  The update controller crashes at module load; open fix extracts the full `scripts/` tree.  
  [nanocoai/nanoclaw PR #3750](https://github.com/nanocoai/nanoclaw/pull/3750)

- **Medium/Low — WhatsApp handling issues (#3751, #3752)**  
  One fix ignores `@newsletter` JIDs at the inbound boundary; another keeps every pending question answerable in a chat.  
  [nanocoai/nanoclaw PR #3751](https://github.com/nanocoai/nanoclaw/pull/3751)  
  [nanocoai/nanoclaw PR #3752](https://github.com/nanocoai/nanoclaw/pull/3752)

- **Low — Provider cancellation, failure delivery, and skill file preservation (#3746)**  
  Open fix preserves cancellation signals, failed-turn status, and existing skill files across provider operations.  
  [nanocoai/nanoclaw PR #3746](https://github.com/nanocoai/nanoclaw/pull/3746)

## 6. Feature Requests & Roadmap Signals
The main roadmap signal is **OpenCode provider integration**, represented by two large open PRs:

- **PR #3733** — `feat(add-opencode): implement provider contracts and host authentication`  
  Runs OpenCode through NanoClaw’s provider contracts using a self-contained, manually installed skill.  
  [nanocoai/nanoclaw PR #3733](https://github.com/nanocoai/nanoclaw/pull/3733)

- **PR #3747** — `feat(add-opencode): integrate setup and host assistance`  
  Adds OpenCode to the interactive setup flow and routes authentication/host assistance through provider-owned adapters.  
  [nanocoai/nanoclaw PR #3747](https://github.com/nanocoai/nanoclaw/pull/3747)

Other roadmap signals include:

- **PR #3745** —

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-09-09

## 1. Today's Overview

Moderate activity with a clear thematic focus: fixing the hosted-MCP tool catalog lifecycle. 11 PRs were updated in the last 24h (6 open, 5 closed/merged) and 2 issues remain open, with the long-running cross-user metadata exposure issue (#6778, open since 2026-07-28) finally drawing direct fix attempts. The merged set includes an env-var semantics fix, first-party agent-market packaging, and a catalog-merge fix that is already being superseded by a more precise per-caller keying approach. No new releases were cut this cycle. Overall the project shows healthy iteration velocity, though the repeated refinement on the same MCP catalog bug suggests the underlying design needs stronger upfront specification.

- Open issues: 2 | Open PRs: 6 | Merged/closed PRs: 5 | Releases: 0

---

## 2. Releases

No new releases published in this window.

---

## 3. Project Progress

Five PRs were merged or closed in the last 24h:

- **[PR #8088 — feat(common): distinguish a set-but-empty env var from an unset one](https://github.com/nearai/ironclaw/pull/8088)** *(merged)* — Fixes a quiet configuration hazard where `FOO=` and an absent `FOO` were treated identically by `env_or_override`, which could turn an operator typo into a silent fallback to defaults for deployment-critical overrides.
- **[PR #8089 — feat(extensions): bundle the agent-market hosted-MCP provider package](https://github.com/nearai/ironclaw/pull/8089)** *(merged)* — Adds a first-party package for the agent.market provider with manifest, per-tool input schemas, and static tool declarations acting as a pre-discovery fallback.
- **[PR #8083 — fix(extensions): merge discovered hosted-MCP catalogs instead of replacing them](https://github.com/nearai/ironclaw/pull/8083)** *(merged)* — Fixes a data-loss bug where one user's `tools/list` discovery on a multi-tenant MCP server deleted previously discovered tools from the shared per-extension registry slot.
- **[PR #6760 — feat(extensions): bundle the agent-market marketplace extension](https://github.com/nearai/ironclaw/pull/6760)** *(closed, superseded — size XL)* — Env-configurable marketplace server URL; superseded in shape by the newer bundled-extension crate structure, but its intent carried into #8089.
- **[PR #6759 — feat(mcp): SEP-414 _meta attribution on outbound hosted-MCP tools/list + tools/call](https://github.com/nearai/ironclaw/pull/6759)** *(closed, needs rebase — size L)* — Opt-in principal attribution for multi-tenant MCP servers; closed without merge but re-implemented in smaller form in #8084.

The through-line: the hosted-MCP extension system is maturing from "works for one user" to "correct for multi-principal, multi-tenant deployments," with bundling, attribution, and catalog isolation all landing in the same cycle.

---

## 4. Community Hot Topics

The most active item by comments is the hosted-MCP catalog isolation problem, which spans one issue and two PRs:

- **[Issue #6778 — Hosted-MCP: discovered tool catalogs are published per extension id, not per installation — cross-user metadata exposure on multi-principal servers](https://github.com/nearai/ironclaw/issues/6778)** — 2 comments, open since 2026-07-28. The core concern is both a correctness bug (users overwrite each other's tools) and a security/privacy issue (the discovered catalog is keyed only by extension id while installations are per-user, so tool surfaces and their metadata leak across principals). This is the most discussed item and is actively being worked: #8083 merged a merge-based fix, and **[PR #8090 (open)](https://github.com/nearai/ironclaw/pull/8090)** replaces it with per-caller keying.

- **[PR #8090 — fix(mcp): key discovered hosted-MCP catalogs per caller, not per extension](https://github.com/nearai/ironclaw/pull/8090)** *(open)* — The more surgical follow-up to #8083: instead of merging catalogs into one shared slot, key the published catalog by the calling principal. Directly addresses the cross-user exposure dimension that merging alone cannot fully solve.

**Underlying need:** Multi-tenant hosted-MCP deployments require first-class principal isolation — both for tool availability and for metadata confidentiality. The community is effectively pushing the design from a single-extension namespace toward a per-installation/per-principal namespace.

---

## 5. Bugs & Stability

Ranked by severity:

1. **[#6778 — Cross-user metadata exposure on multi-principal hosted-MCP servers](https://github.com/nearai/ironclaw/issues/6778)** — **High severity (security/privacy).** Active discovery under one user's credential publishes tools into a shared per-extension slot, so any user's discovery can both overwrite and expose another user's tool surface. Open since July; fix in progress via #8083 (merged, partial) and #8090 (open, preferred approach).

2. **[#8085 — fix(extensions): treat operator-installed packages like host-bundled ones](https://github.com/nearai/ironclaw/pull/8085)** *(open)* — **Medium severity (functional regression).** An operator-installed package can be built but not used because `from_host_bundled_manifest_with_inline_dynamic_schemas` and `validate_consistency` disagree about which manifest sources may carry inline dynamic descriptor schemas (constructor stricter one way, validator the other). Fix PR is open.

3. **[#8086 — `ironclaw skills list` cannot see skills that the runtime writes](https://github.com/nearai/ironclaw/issues/8086)** — **Medium severity (developer UX / debuggability).** Agent-installed skills and skills belonging to other configured users are invisible to the CLI tool that a developer would naturally use to debug "why can't my agent see its skill," actively misdirecting diagnosis. New issue, no fix PR yet.

4. **[#8088 — Set-but-empty env var silently selects defaults](https://github.com/nearai/ironclaw/pull/8088)** — **Low-to-medium severity (configuration safety), already fixed.** Now merged.

No crashes or regressions reported in this window beyond the above.

---

## 6. Feature Requests & Roadmap Signals

Several forward-looking features are in flight, mostly as open PRs:

- **[PR #8087 — feat(loop): make the prompt-context limit an override instead of a constant](https://github.com/nearai/ironclaw/pull/8087)** *(open)* — `PromptContextTokenBudget::DEFAULT_CONTEXT_LIMIT_TOKENS` is hardcoded at 128k; deployments with larger-window models must patch the constant. Expect this to land soon; it is a small, low-risk configurability win.

- **[PR #8084 — feat(mcp): opt-in SEP-414 caller attribution on outbound hosted-MCP calls](https://github.com/nearai/ironclaw/pull/8084)** *(open)* — Lets hosted MCP servers distinguish per-conversation callers and recognize retries, enabling per-conversation state and avoiding double-charging on side-effecting retries. Strictly opt-in per provider manifest. A narrower reincarnation of the closed #6759.

- **[PR #8082 — feat(attachments): opt-in pointer mode for document text in model context](https://github.com/nearai/ironclaw/pull/8082)** *(open)* — Addresses context-budget exhaustion from inlined document text (~25k tokens per PDF, re-incurred every turn) by allowing pointer/reference mode instead of full inlining. Likely to be popular for RAG-heavy and document-heavy workloads.

- **[PR #8072 — feat(telegram): register the Bot API command menu at activation](https://github.com/nearai/ironclaw/pull/8072)** *(open, author thisisjoshford)* — Registers the channel's declared commands (`/model`, `/status`, `/new`, `/stop`, `/interrupt`) with Telegram's `setMyCommands` at activation, with best-effort cleanup at deactivation. A user-facing polish feature from an experienced contributor.

**Prediction:** #8087 and #8084 are the most likely to merge next, given the active MCP workstream; #8082 addresses a widely felt pain point (context budget) and could land in the next release if review bandwidth allows.

---

## 7. User Feedback Summary

Pain points expressed through issues and PR descriptions this cycle:

- **MCP catalog overwrite/leakage is the dominant complaint.** Both the issue and multiple PRs describe the same scenario from different angles: "user A's turn → A's tools in the registry; user B's turn → B's tools replace A's" — plus the privacy concern that one principal can observe the surface discovered by another. Users need predictable, isolated tool discovery on shared servers.
- **Configuration footguns are resurfacing.** The empty-vs-unset env var issue (#8088) reflects a broader user need: deployments want explicit, fail-loud configuration rather than silent fallback to defaults — especially for endpoint overrides and similar operator-controlled settings.
- **Debugging tooling lags behind runtime behavior.** Issue #8086 is a concrete developer-experience regression: the natural CLI diagnostic returns an empty list for skills the runtime actually wrote, leading users to chase the wrong problem.
- **Context-window economics are a real constraint.** PR #8082 (pointer mode) and #8087 (context-limit override) both respond to users running larger models or attaching many documents, where the 128k budget and per-turn re-inlining become blockers.
- **Telegram users want discoverable commands.** PR #8072's command-menu registration is a UX request from a channel-integration user base — minor, but a sign of growing non-CLI adoption.

Overall sentiment is constructive; users are filing precise, well-scoped reports with reproduction-style detail, and maintainers are responding with fixes within the same cycle.

---

## 8. Backlog Watch

Items that need maintainer attention:

- **[Issue #6778 — Cross-user metadata exposure (hosted-MCP catalog keying)](https://github.com/nearai/ironclaw/issues/6778)** — Open since 2026-07-28 with only 2 comments and no maintainer response recorded in the data. While #8083 and #8090 make progress, the security dimension (metadata exposure, not just overwrite) should be explicitly acknowledged and tracked to closure. Highest-priority backlog item.

- **[PR #8072 — Telegram command menu registration](https://github.com/nearai/ironclaw/pull/8072)** — Open since 2026-09-04 from a non-primary contributor (thisisjoshford), size L, no comment activity visible. Untended external contributions risk going stale; needs a maintainer review pass.

- **[PR #8085 — Operator-installed packages can be built but not used](https://github.com/nearai/ironclaw/pull/8085)** — A functional bug fix currently open with no merge; given it blocks a legitimate deployment path (operator-installed packages), it should be prioritized alongside the MCP work.

- **Closed-but-not-merged PRs #6760 and #6759** — Both closed after long lifetimes (since 2026-07-28) without merging. Their intent was partially reimplemented, but the closure process (supersede/rebase notices) could be made more explicit to avoid contributor confusion — relevant for community trust and future contributions.

---

*Digest generated from IronClaw GitHub activity for 2026-09-09. All item counts reflect the last 24h update window; links point to the canonical issue/PR pages.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-09-09

## 1. Today's Overview

LobsterAI saw a maintenance-heavy day: 20 issues were updated (16 still open/active, 4 closed) and 14 PRs were touched, with 12 merged or closed and only 2 still open. No new releases were published. The main focus was compatibility and regression-fixing around the bundled OpenClaw v2026.8.1 upgrade, especially for IM channels (Discord, QQ, DingTalk, Lark, NIM, NetEase Bee), gateway config handling, and scheduled tasks. Community reports continue to highlight performance, token consumption, installer reliability, and an accumulating set of open security advisories. Project activity is healthy, but several important user-facing issues remain unresolved after weeks or months.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

Twelve PRs were merged/closed today. The majority are OpenClaw v2026.8.1 compatibility fixes and infrastructure updates:

- **[#2637](https://github.com/netease-youdao/LobsterAI/pull/2637)** — Bundle Discord with trusted plugin origin to fix OpenClaw plugin registration failure.
- **[#2636](https://github.com/netease-youdao/LobsterAI/pull/2636)** — Fix i18n bug where the About update label did not refresh on language switch.
- **[#2635](https://github.com/netease-youdao/LobsterAI/pull/2635)** — Avoid gateway restarts on stale config hashes by adding bounded retry logic.
- **[#2634](https://github.com/netease-youdao/LobsterAI/pull/2634)** — Restore QQ shutdown cleanup and desktop IM sync after gateway restarts.
- **[#2633](https://github.com/netease-youdao/LobsterAI/pull/2633)** — Update Discord DM config fields to match the new OpenClaw schema.
- **[#2632](https://github.com/netease-youdao/LobsterAI/pull/2632)** — Preserve IM/agent/gateway config during logout, and stop Windows gateway gracefully via IPC.
- **[#2631](https://github.com/netease-youdao/LobsterAI/pull/2631)** — Fix cron run-history duplication and failure-state persistence after OpenClaw upgrade.
- **[#2630](https://github.com/netease-youdao/LobsterAI/pull/2630)** — Restore DingTalk and Lark inbound message dispatch.
- **[#2629](https://github.com/netease-youdao/LobsterAI/pull/2629)** — Restore NIM and NetEase Bee plugin loading.
- **[#2628](https://github.com/netease-youdao/LobsterAI/pull/2628)** — Fix DingTalk and Lark plugin compatibility with OpenClaw v2026.8.1.
- **[#2166](https://github.com/netease-youdao/LobsterAI/pull/2166)** — CI dependency bump: `dorny/paths-filter` from v3 to v4.
- **[#2294](https://github.com/netease-youdao/LobsterAI/pull/2294)** — Docs: add TakoAPI directory badge.

Two PRs remain open and appear stale: **[#2358](https://github.com/netease-youdao/LobsterAI/pull/2358)** (session rename feedback) and **[#2373](https://github.com/netease-youdao/LobsterAI/pull/2373)** (image attachments vs. model vision capability).

## 4. Community Hot Topics

The most-commented issues updated today focus on user-facing reliability and product direction:

- **[#1903 — 会员登录频繁失败 (Login failures)](https://github.com/netease-youdao/LobsterAI/issues/1903)** — 4 comments. Closed as stale. Users report being unable to log in / use paid NetEase models.
- **[#2046 — Agent memory system proposal](https://github.com/netease-youdao/LobsterAI/issues/2046)** — 3 comments. Closed as stale. Detailed proposal for persistent session memory, metadata storage, and cross-session recall.
- **[#2079 — Result window freeze when scrolling to top](https://github.com/netease-youdao/LobsterAI/issues/2079)** — 3 comments. Reproducible UI hang on 2026.5.27.
- **[#2120 — Product suggestions: task queue, longer runtime, skills UI](https://github.com/netease-youdao/LobsterAI/issues/2120)** — 3 comments. Users want to pre-queue tasks, extend monitoring runtime, and improve skills layout.
- **[#2121 — Repeated output may waste tokens](https://github.com/netease-youdao/LobsterAI/issues/2121)** — 3 comments. User suspects duplicated output consumes excessive tokens; asks whether it is a Claw bug.
- **[#2131 — Hermes agent support request](https://github.com/netease-youdao/LobsterAI/issues/2131)** — 3 comments. Interest in supporting `hermes` agent.

Security-related issues from YLChen-007 also draw attention, though with fewer comments: #2176, #2181, #2286, #2287, #2288.

## 5. Bugs & Stability

Several serious bugs and regressions are open. Security issues rank highest by severity.

### Critical / Security
- **[#2286 — Unauthenticated local token proxy allows API replay](https://github.com/netease-youdao/LobsterAI/issues/2286)** — Any local process can replay authenticated server-model API capability. Open.
- **[#2287 — NIM outbound media flow allows local file exfiltration](https://github.com/netease-youdao/LobsterAI/issues/2287)** — Assistant-generated absolute paths can exfiltrate local files. Open.
- **[#2288 — HTML preview server follows symlinks, discloses local files](https://github.com/netease-youdao/LobsterAI/issues/2288)** — Lexical path check bypassable via in-root symlinks. Open.
- **[#2176 — Automatic artifact loading allows arbitrary local file reads](https://github.com/netease-youdao/LobsterAI/issues/2176)** — Message-derived `MEDIA:` references forwarded to privileged Electron code. Open.
- **[#2181 — Private-network browser access restored by default, weakens SSRF guard](https://github.com/netease-youdao/LobsterAI/issues/2181)** — Default `ProxyCompatible` mode bypasses OpenClaw SSRF protection. Open.

### High Severity — Functional
- **[#2214 — Desktop "data backup" deadlocks main process (100% reproducible)](https://github.com/netease-youdao/LobsterAI/issues/2214)** — User must force-kill; no fix PR seen today.
- **[#2230 — Same model much slower and token-hungry in LobsterAI vs CodeBuddy](https://github.com/netease-youdao/LobsterAI/issues/2230)** — Reported: 25 min / 60M tokens vs. 2m24s / 67k tokens. No fix identified yet.
- **[#2215 — Installer repeatedly fails: "Resource extraction failed: could not start extractor process"](https://github.com/netease-youdao/LobsterAI/issues/2215)** — Detailed investigation by user; still unresolved.
- **[#2216 — Memory Search cannot switch embedding provider; DB lock EBUSY](https://github.com/netease-youdao/LobsterAI/issues/2216)** — Provider fixed to OpenAI; unusable when API quota is exhausted.

### Medium Severity
- **[#2079 — Execution result window freezes when scrolled to top](https://github.com/netease-youdao/LobsterAI/issues/2079)** — Reproducible UI hang.
- **[#2121 — Duplicate text output may waste tokens](https://github.com/netease-youdao/LobsterAI/issues/2121)** — User suspects repeated output is consuming tokens.
- **[#1152 — Corporate IMAP connection failure (closed/stale)](https://github.com/netease-youdao/LobsterAI/issues/1152)** — Old bug, no clear resolution.

### Fixes merged today for recent regressions
- DingTalk/Lark transport restored: [#2630](https://github.com/netease-youdao/LobsterAI/pull/2630), [#2628](https://github.com/netease-youdao/LobsterAI/pull/2628)
- NIM/NetEase Bee restored: [#2629](https://github.com/netease-youdao/LobsterAI/pull/2629)
- QQ shutdown/IM sync restored: [#2634](https://github.com/netease-youdao/LobsterAI/pull/2634)
- Discord DM config fixed: [#2633](https://github.com/netease-youdao/LobsterAI/pull/2633)
- IM config preservation / graceful Windows shutdown: [#2632](https://github.com/netease-youdao/LobsterAI/pull/2632)
- Gateway restart loop fixed: [#2635](https://github.com/netease-youdao/LobsterAI/pull/2635)
- Cron history fix: [#2631](https://github.com/netease-youdao/LobsterAI/pull/2631)

## 6. Feature Requests & Roadmap Signals

High-signal feature requests from users include:

- **[#2046 — Agent memory system](https://github.com/netease-youdao/LobsterAI/issues/2046)** — Persistent, cross-session memory with metadata stored to filesystem so agents can retrieve/history-link. This was closed stale, but the demand is clear.
- **[#2180 — "AI Collaborator" natural-language command bar and task dispatch](https://github.com/netease-youdao/LobsterAI/issues/2180)** — Proposal for cross-model orchestration and project-level memory.
- **[#2120 — Task queue, longer monitoring runtime, better skills UI](https://github.com/netease-youdao/LobsterAI/issues/2120)** — Practical workflow improvements for continuous work.
- **[#2239 — Programming tools "OpenClaw-ification" and ecosystem integration](https://github.com/netease-youdao/LobsterAI/issues/2239)** — Suggests MCP-native integration with OpenCode/CodeBuddy and full workflow automation.
- **[#2243 — Make skills.load.watch manual / add UI toggle](https://github.com/netease-youdao/LobsterAI/issues/2243)** — Performance pain with 174 skills; watch mode is protected and not configurable.
- **[#2131 — Hermes agent support](https://github.com/netease-youdao/LobsterAI/issues/2131)** — Simple compatibility request.

Likely next-version candidates: continued OpenClaw v2026.8.x stabilization, configurable skill watch mode, and possibly memory-system groundwork. Security fixes should be prioritized, but no PRs for them have appeared yet.

## 7. User Feedback Summary

Real user pain points across recent issues:

- **Login / auth reliability**: Paid NetEase model access is failing for some users ([#1903](https://github.com/netease-youdao/LobsterAI/issues/1903)).
- **Memory and continuity**: Users are frustrated by session isolation and lack of agent-accessible memory ([#2046](https://github.com/netease-youdao/LobsterAI/issues/2046)).
- **Performance and cost**: Extremely high latency and token consumption compared to alternatives ([#2230](https://github.com/netease-youdao/LobsterAI/issues/2230)); duplicate output wasting tokens ([#2121](https://github.com/netease-youdao/LobsterAI/issues/2121)).
- **Stability**: UI freezes, backup deadlocks, installer failures, and Windows process shutdown issues ([#2079](https://github.com/netease-youdao/LobsterAI/issues/2079), [#2214](https://github.com/netease-youdao/LobsterAI/issues/2214), [#2215](https://github.com/netease-youdao/LobsterAI/issues/221

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

⚠️ Summary generation failed.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-09-09

## 1. Today's Overview
ZeptoClaw is in a lightly active state with **1 open issue** and **1 open pull request** updated in the last 24 hours, and **no new releases**. The only new issue, #675, requests broader provider support via OrcaRouter, signaling continued community interest in making the assistant work with more backends. The one active PR, #674, is a security hardening change for panel WebSocket authentication that has not yet been merged. No PRs were merged or closed today, so no committed feature or fix progress landed upstream. Overall, the project is moving at a measured pace with a promising security improvement pending review.

## 2. Releases
**None.** No new versions, pre-releases, or tags were published in the last 24 hours.

## 3. Project Progress
No PRs were merged or closed today, so no completed features or fixes landed upstream. The single open PR remains under review:

- **#674 [OPEN] fix(panel): replace websocket bearer URLs with tickets** — [qhkm/zeptoclaw PR #674](https://github.com/qhkm/zeptoclaw/pull/674)  
  Improves WebSocket authentication for the panel by replacing long-lived bearer tokens in URL query strings with short-lived, CSRF-protected tickets. This is a meaningful security fix, but it is still unmerged.

No other project advancement was recorded in the last 24 hours.

## 4. Community Hot Topics
With only one issue and one PR active, there are no heavily commented or reacted threads. The main community signal is the new feature request:

- **#675 [OPEN] OrcaRouter provider support for ZeptoClaw** — [qhkm/zeptoclaw Issue #675](https://github.com/qhkm/zeptoclaw/issues/675)  
  Author: putraperdana1207-pixel | Created: 2026-09-09 | Comments: 0 | Reactions: 0  
  The requester highlights ZeptoClaw’s core value proposition: a ~6MB Rust binary with ~50ms startup, capable of running where container runtimes cannot. The ask is to add **OrcaRouter as a provider**, indicating that users see ZeptoClaw as an efficient local/edge AI runtime but need more routing/provider integrations to fit existing infrastructure.

Underlying need: users want ZeptoClaw to work with more channels/providers without sacrificing its small footprint. This also suggests the community values the project as a lightweight alternative to heavier agent frameworks.

## 5. Bugs & Stability
No new bugs, crashes, or regressions were reported in the last 24 hours.

However, the open PR #674 addresses an existing security issue: WebSocket connections previously exposed long-lived API tokens or JWTs in `?auth=` parameters, which could leak credentials via access logs and browser history. The proposed fix replaces those tokens with 30-second single-use tickets.

**Severity assessment:** High severity from a security standpoint, but the fix is already proposed and needs review/merge. No other stability issues are currently visible.

## 6. Feature Requests & Roadmap Signals
The clearest roadmap signal is:

- **OrcaRouter provider support** — [Issue #675](https://github.com/qhkm/zeptoclaw/issues/675)  
  Users want ZeptoClaw to integrate with OrcaRouter, likely for flexible routing across AI providers. Given the project’s emphasis on lightweight deployment, a provider abstraction that supports OrcaRouter could be a likely next-version candidate if maintainers prioritize ecosystem compatibility.

The PR #674 work around ticketed WebSocket auth may also land in the next release as part of a stability/security pass. Expect future releases to potentially include:
- Additional provider/router integrations
- Improved panel authentication and security hardening
- Continued focus on low-footprint, fast-startup operation

## 7. User Feedback Summary
The single user submission this period expresses a positive view of ZeptoClaw’s architecture, explicitly noting the value of packing tools, memory, channels, providers, and sandboxed autonomy into a small Rust binary that starts in milliseconds. The pain point is **missing provider support**: the user wants OrcaRouter, implying that ZeptoClaw’s built-in provider set is not sufficient for their routing needs. Overall sentiment appears constructive and feature-oriented rather than critical.

## 8. Backlog Watch
No long-unanswered issues or PRs are currently visible in the last 24-hour window. The only item that needs maintainer attention is:

- **PR #674 [OPEN] fix(panel): replace websocket bearer URLs with tickets** — [qhkm/zeptoclaw PR #674](https://github.com/qhkm/zeptoclaw/pull/674)  
  Opened 2026-09-08, still unmerged. Because it addresses credential exposure, maintainers should review and merge it promptly.

The new issue #675 is not yet backlogged, but it may become a roadmap item if provider support continues to be requested.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

⚠️ Summary generation failed.

</details>