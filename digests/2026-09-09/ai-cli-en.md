# AI CLI Tools Community Digest 2026-09-09

> Generated: 2026-09-09 09:31 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report — AI CLI Developer Tools
**Coverage window:** 2026-09-09 community digests for Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI. Digests for OpenCode, Pi, Qwen Code, and DeepSeek TUI were unavailable (summary generation failed) and are excluded from quantitative comparisons.

---

## 1. Ecosystem Overview

The AI CLI tool landscape is in a phase of rapid, security-focused iteration. Anthropic, OpenAI, and Google all shipped releases within 24 hours, with OpenAI's Codex alone publishing four alpha builds. Community attention is concentrated on infrastructure reliability — sandboxing, credential handling, session continuity, and Windows/WSL parity — rather than raw model capability. A significant cross-tool pattern is emerging: as agents gain autonomy (subagents, background skills, Computer Use), users are demanding honest status reporting, interruption-safe state, and transparent security boundaries. Extension and plugin models (Claude Code's Function Hooks proposal at 150 comments; Gemini's skills system) are becoming the key differentiator battleground.

## 2. Activity Comparison

Counts reflect **highlighted items in each digest** (hot issues / key PRs), not full GitHub totals. All figures are for the 2026-09-09 window.

| Tool | Issues Highlighted | PRs Highlighted | Releases | Release Notes |
|---|---|---|---|---|
| Claude Code | 10 | 1 | 2 | v2.1.266 (gateway hotfix), v2.1.265 (telemetry, `--plugin-dir`) |
| OpenAI Codex | 10 | 10 | 4 | `rust-v0.154.0-alpha.7` / alpha.8 / alpha.10.2 / alpha.11 |
| Gemini CLI | 10 | 10 | 3 | v0.61.0-nightly, v0.60.0-preview.0, v0.59.0 stable |
| GitHub Copilot CLI | 3 (section truncated) | 0 listed | 2 | v1.0.84-3, v1.0.84-2 (Vim mode GA) |
| Kimi Code CLI | 3 | 2 | 0 | — |
| OpenCode / Pi / Qwen Code / DeepSeek TUI | n/a | n/a | n/a | Digest generation failed |

## 3. Shared Feature Directions

Several requirements recur across tool communities, independently:

- **Subagent reliability & honest status reporting.** Gemini CLI users report MAX_TURNS and Wayland failures being misreported as "GOAL success" (#22323, #21983); generalist agent hangs force workarounds (#21409). Claude Code shows adjacent symptoms: `--resume` renders stale messages after compaction (#46603). Across tools, users want visible subagent trajectories and truthful termination reasons — not silent masking.
- **Windows/WSL parity.** Codex has four of ten hot issues rooted in WSL path-mapping and sandbox failures (#41290, #29639, #42501, #25178); Copilot CLI's truncated issue list begins with a Windows desktop regression (#4756); Gemini's latest nightly includes NTFS short-name mitigation (#29116). Cross-platform execution remains the largest single source of friction.
- **Sandboxing without collateral damage.** Gemini PR #29156 reverts an over-aggressive sandbox

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

⚠️ Skills summary generation failed.

---

# Claude Code Community Digest — 2026-09-09

## Today's Highlights

Anthropic shipped two quick releases to address a gateway/proxy regression: v2.1.265 introduced telemetry fields and folder-based `--plugin-dir` support, while v2.1.266 fixed a 2.1.265 regression where the `CLAUDE_CODE_USE_GATEWAY` env var forced Cloud sign-in prematurely. On the community side, the Function Hooks proposal (#91870) is the dominant discussion (150 comments), and the long-running copy/paste whitespace bug (#18170) crossed 292 👍, making it the most-voted open issue. Several data-loss and correctness bugs in Desktop session transcripts and `--resume` also gained attention.

## Releases

**v2.1.266** — Hotfix for a 2.1.265 regression: the undocumented `CLAUDE_CODE_USE_GATEWAY` env var, previously only honored when both `ANTHROPIC_BASE_URL` and `ANTHROPIC_AUTH_TOKEN` were set, began forcing Cloud-gateway sign-in on its own. LLM-gateway and proxy setups should restore their previous behavior.
[Release v2.1.266](https://github.com/anthropics/claude-code/releases/tag/v2.1.266)

**v2.1.265** — Two changes: (1) `user.email` and `user.groups` are now included in telemetry forwarded through a Claude apps gateway, matching terminal sessions; (2) `--plugin-dir` can now point at a folder of plugins — every child folder with a manifest loads, and children added/removed are picked up dynamically.
[Release v2.1.265](https://github.com/anthropics/claude-code/releases/tag/v2.1.265)

## Hot Issues

1. **[#91870 — Function Hooks: make plugins 10x more powerful](https://github.com/anthropics/claude-code/issues/91870)** — *150 comments, 88 👍* · The week's highest-engagement discussion proposes a deep plugin extension model with a parameterized `$` object, side-effect tracking, and an Express/Koa-style `next()` continuation model. If adopted, this could substantially reshape the plugin ecosystem.

2. **[#18170 — Copy/paste from terminal includes unwanted indentation/trailing spaces](https://github.com/anthropics/claude-code/issues/18170)** — *135 comments, 292 👍* · The most-upvoted open issue. Copied code retains prompt-alignment indentation and trailing whitespace, corrupting pasted snippets. A daily annoyance for heavy TUI users that has now drawn sustained community pressure.

3. **[#65961 — Claude writes verbose code comments by default, ignoring instructions to stop](https://github.com/anthropics/claude-code/issues/65961)** — *31 comments, 205 👍* · A model-behavior complaint: explicit prompts to avoid comments are repeatedly ignored. High 👍 count signals broad frustration with comment verbosity.

4. **[#83033 — Sonnet 5 corrupts Hangul in tool-call parameters via mis-spelled \uXXXX escapes](https://github.com/anthropics/claude-code/issues/83033)** — *6 comments, 134 👍* · A root-caused, 100%-repro bug where Korean text in tool parameters is written as Unicode escapes with corrupted hex, breaking `AskUserQuestion`/`TodoWrite`. Likely the cause behind earlier Korean-corruption reports.

5. **[#86928 — Sandboxed Bash intermittently fails: unshare(CLONE_NEWUSER): Invalid argument](https://github.com/anthropics/claude-code/issues/86928)** — *14 comments, 8 👍* · With `sandbox: { enabled: true }` on Linux, roughly 1 in 10 Bash calls fails in seccomp setup. Reproduced; impacts anyone relying on sandboxing for safety.

6. **[#76694 — Cowork macOS: "Choose a folder" lost after Chat/Cowork merge](https://github.com/anthropics/claude-code/issues/76694)** — *16 comments, 20 👍* · A UX regression where new projects can no longer pick a folder — the context menu was replaced by a chat-style upload-only knowledge menu.

7. **[#29415 — GitHub connector missing from /mcp despite being connected in settings](https://github.com/anthropics/claude-code/issues/29415)** — *12 comments, 14 👍* · GitHub silently fails to appear in the MCP list while all 19 other connectors sync. Likely a connector-sync bug specific to GitHub.

8. **[#92825 — Desktop session transcripts silently become permanently unavailable](https://github.com/anthropics/claude-code/issues/92825)** — *7 comments* · A follow-up to #79044: `cliSessionId` is nulled and transcripts are lost with no local recovery path. Data-loss severity; notable because it's a recurrence.

9. **[#46603 — `--resume` shows stale messages after context compaction](https://github.com/anthropics/claude-code/issues/46603)** — *7 comments* · Compaction creates messages with `parentUuid` references to deleted history, so resumes display days-old conversations and appear to lose recent work.

10. **[#93043 — statusLine goes blank under cmux after 2.1.263](https://github.com/anthropics/claude-code/issues/93043)** — *new today, 0 comments* · A freshly filed regression: the status line renders nothing in new sessions under cmux after the 2.1.263 auto-update, with no errors. Likely a rendering-path regression worth watching.

## Key PR Progress

Only one PR was updated in the 24-hour window, so this section is limited.

**[#63686 — Bump stale and autoclose timeouts from 14 to 90 days](https://github.com/anthropics/claude-code/pull/63686)** — *closed* · A long-dormant lifecycle PR (opened May, closed Sept 8) that would extend both the "stale

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-09-09

## Today's Highlights

Release activity continues with four new `rust-v0.154.0` alpha builds, while pull request momentum is concentrated on credential brokering, Python SDK publishing, and release/packaging hardening. On the issue side, Windows/WSL workspace and Computer Use failures dominate community discussion, with several high-traffic threads crossing 50 comments.

## Releases

Four Rust pre-release builds shipped in the last 24 hours:

- [rust-v0.154.0-alpha.7](https://github.com/openai/codex/releases/tag/rust-v0.154.0-alpha.7)
- [rust-v0.154.0-alpha.8](https://github.com/openai/codex/releases/tag/rust-v0.154.0-alpha.8)
- [rust-v0.154.0-alpha.10.2](https://github.com/openai/codex/releases/tag/rust-v0.154.0-alpha.10.2)
- [rust-v0.154.0-alpha.11](https://github.com/openai/codex/releases/tag/rust-v0.154.0-alpha.11)

No detailed changelogs were attached; these appear to be iterative fixes leading toward a stable `0.154.0`.

## Hot Issues

Top issues by community engagement and impact:

- [Windows][WSL] Project creation and removal fail after switching Agent Environment to WSL — 51 comments, 37 👍  
  https://github.com/openai/codex/issues/41290  
  A major workflow blocker for Windows users relying on WSL workspaces.

- Windows Computer Use screenshot fails on Windows 10 22H2 with `SetIsBorderRequired` error — 50 comments, 23 👍  
  https://github.com/openai/codex/issues/25178  
  Computer Use can list and activate windows but cannot capture screenshots, crippling the core experience.

- Computer Use Chrome extension unavailable in Chrome Web Store; offline installer needed — 29 comments, 25 👍  
  https://github.com/openai/codex/issues/21700  
  Distribution/availability problem blocking browser automation features.

- Paginated thread history projection stops at a `token_count` record — 24 comments  
  https://github.com/openai/codex/issues/40342  
  Long-session thread history renders incorrectly after pagination.

- Browser Use Node REPL fails in Windows Desktop with WSL workspace due to unmapped `sandboxCwd` — 22 comments  
  https://github.com/openai/codex/issues/29639  
  Path-mapping mismatch between Windows app and WSL filesystem breaks MCP tooling.

- Windows app fails to launch UI when `cua_node` staging cannot copy `node_repl.exe` — 13 comments  
  https://github.com/openai/codex/issues/42501  
  Recent update can leave Codex Desktop stuck without a visible window.

- Reopen #19464 and support 1M context — 11 comments, 8 👍  
  https://github.com/openai/codex/issues/30910  
  Continued demand for larger context windows beyond the current 272k.

- Invalid prompt: flagged as potentially violating usage policy — 11 comments  
  https://github.com/openai/codex/issues/43058  
  Users hit false policy blocks on ordinary prompts, hurting reliability.

- False “Cyber Abuse” Policy Flag for legitimate reverse engineering work — 8 comments  
  https://github.com/openai/codex/issues/30271  
  Safety over-blocking affecting verified security researchers.

- macOS “Open in” submenu stays on “Loading available apps…” indefinitely — 5 comments, 7 👍  
  https://github.com/openai/codex/issues/41480  
  Desktop integration regression on macOS.

## Key PR Progress

Important merged/closed PRs from the last 24 hours:

- [Support credential brokering in plaintext HTTP tunnels](https://github.com/openai/codex/pull/44089)  
  Extends credential interception to HTTP `CONNECT` and SOCKS5 tunnels, not just TLS.

- [Add untrusted external messages to the Python SDK](https://github.com/openai/codex/pull/44086)  
  Exposes `ExternalMessage` for sync and async `run(...)`, enabling tool-level content delivery without user-authorization semantics.

- [Expose Python SDK history selection and per-turn options](https://github.com/openai/codex/pull/44084)  
  Adds response-history control and per-turn service-tier overrides with runtime compatibility checks.

- [Publish Python packages after stable CLI releases](https://github.com/openai/codex/pull/44067)  
  Adds a downstream workflow to publish and verify Python SDK/runtime on PyPI from stable CLI commits.

- [Raise Guardian's action review limit to 200,000 bytes](https://github.com/openai/codex/pull/44060)  
  Increases action review capacity from 8 KB to 200 KB, while keeping stdin approvals capped separately.

- [Add configurable credential providers to the network proxy](https://github.com/openai/codex/pull/44056)  
  Introduces environment-variable-based credential providers with bearer/token/Basic/custom header auth.

- [Fix voice runtime release builds and packaging](https://github.com/openai/codex/pull/44062)  
  Builds voice runtimes with `-c opt`, fixes path resolution, and seals release archives correctly.

- [Harden credential handling in shell snapshots and replay](https://github.com/openai/codex/pull/44040)  
  Decodes shell literals safely and prevents startup files from restoring real credentials after dummy replacement.

- [Use `StartThreadOptions` across thread fork APIs](https://github.com/openai/codex/pull/44043)  
  Unifies thread-fork configuration and startup arguments into one options structure.

- [Reject empty audio payloads in data URLs](https://github.com/openai/codex/pull/44070)  
  Returns a clear `AudioPreparationError::InvalidDataUrl` instead of proceeding with invalid input.

## Feature Request Trends

The most requested feature directions from recent issues:

- **Larger context windows** — Continued pressure to raise the 272k context limit, with calls to reopen previous 1M-context requests.
- **Better long-thread navigation** — Requests for message bookmarks and minimap improvements to handle long Codex App sessions.
- **Restored desktop “Open with” workflows** — macOS users want a one-click top-right menu for opening the current workspace in editors like VS Code and Cursor.
- **Offline and alternative distribution** — The missing Chrome Web Store extension has users asking for offline installers.
- **Improved WSL integration** — Users want seamless path mapping, sandbox behavior, and project lifecycle management when Codex switches between Windows and WSL environments.

## Developer Pain Points

Recurring frustrations across recent issues:

- **Windows + WSL path mismatches** are causing sandbox setup failures, MCP tool breakage, and project creation/removal errors.
- **Computer Use reliability** is a top concern: screenshot capture, Chrome extension availability, and `node_repl.exe` staging all fail in different Windows configurations.
- **Desktop regressions after updates** — Windows and macOS builds are frequently reported with launch hangs, reconnecting loops, or missing UI elements.
- **Thread/history migration bugs** — Paginated threads, subagent histories, and migrated rollouts show empty or truncated projections.
- **False-positive policy flags** on legitimate prompts and security work are eroding trust in model-behavior guardrails.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-09-09

## 1. Today's Highlights

The project shipped three releases in the last 24 hours, headlined by nightly v0.61.0 with Windows NTFS path mitigation and sandbox container isolation fixes. Meanwhile, a critical PR landed to prevent session context poisoning on interrupted agent turns, addressing a long-standing frustration for developers who frequently Ctrl-C long-running agent tasks. The issue tracker continues to spotlight subagent reliability — misreported MAX_TURNS terminations, generalist agent hangs, and a lack of autonomous skill usage remain the loudest community complaints.

## 2. Releases

**v0.61.0-nightly.20260909.ged2ac40df** — Latest nightly
- `fix(core)`: Mitigate NTFS 8.3 short name (SFN) path issues ([#29116](https://github.com/google-gemini/gemini-cli/pull/29116))
- `fix(cli)`: Isolate settings directory inside sandbox containers ([#29216](https://github.com/google-gemini/gemini-cli/pull/29216))

**v0.60.0-preview.0** — Preview release
- `fix(core)`: Improve destination validation and connection routing in web fetch utilities ([#29120](https://github.com/google-gemini/gemini-cli/pull/29120))
- `fix(core)`: Enforce RFC 9207 issuer identification in the MCP OAuth flow

**v0.59.0** — Stable release
- Changelog for v0.58.0-preview.0, version bumps, and ongoing core stability fixes.

## 3. Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** · 13 comments · `p1` bug
   The `codebase_investigator` subagent reports `status: "success"` with `Termination Reason: "GOAL"` even when it hit MAX_TURNS before doing any analysis. This silently masks interruptions and has drawn sustained community attention — a top correctness concern for multi-agent workflows.

2. **[#19873 — Zero-Dependency OS Sandboxing & Post-Execution Intent Routing](https://github.com/google-gemini/gemini-cli/issues/19873)** · 9 comments · `p2` enhancement
   Proposes letting Gemini 3's native bash affinity run freely inside OS-level sandboxes, then routing command intent post-execution. Backed by the maintainer team, this could meaningfully change the shell-execution security model.

3. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** · 8 comments · 8 👍 · `p1` bug
   Simple tasks like folder creation hang indefinitely when deferred to the generalist agent — users report waiting up to an hour. The only workaround today is explicitly instructing the model to avoid subagents. High community resonance given the 👍 count.

4. **[#22745 — AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** · 7 comments · `p2` feature/EPIC
   Tracks whether AST-aware tools can reduce token noise, improve method-bound reads, and sharpen code navigation. Companion issue [#22746](https://github.com/google-gemini/gemini-cli/issues/22746) suggests `tilth` or `glyph` as starting points.

5. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** · 6 comments · `p2` bug
   Anecdotal but widely echoed: Gemini ignores custom skills and sub-agents unless explicitly instructed. Users with `gradle` and `git` skills report the model rarely self-triggers them, undermining the extensibility story.

6. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** · 5 comments · `p2` security bug
   Auto Memory sends transcript content to an extraction model *before* prompt-based redaction occurs, and the service can log skill content. A security-relevant concern for teams using the memory system with sensitive codebases.

7. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** · 4 comments · `p2` bug
   Sessions the extractor deems low-signal are never marked processed, so they resurface repeatedly. Part of a broader cluster of Auto Memory quality issues ([#26516](https://github.com/google-gemini/gemini-cli/issues/26516), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523)).

8. **[#25166 — Shell command gets stuck with "Waiting input" after completing](https://github.com/google-gemini/gemini-cli/issues/25166)** · 4 comments · 3 👍 · `p1` bug
   After trivial CLI commands finish, the shell tool can hang showing "Awaiting user input." Highly disruptive for automation-heavy usage; an `effort/medium` fix is in the maintainer backlog.

9. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** · 4 comments · `p1` bug
   Browser Agent terminates with "GOAL" despite failing under Wayland, another instance of misleading success reporting. Linux desktop users are affected disproportionately.

10. **[#20079 — Symlinked agent files in ~/.gemini/agents are not recognized](https://github.com/google-gemini/gemini-cli/issues/20079)** · 4 comments · `p2` bug
   `filename.md` symlinks in the agents directory are ignored, breaking common dotfile-management setups (e.g., chezmoi, GNU Stow). A small but quality-of-life issue for power users.

## 4. Key PR Progress

1. **[#29265 — Prevent session context poisoning on interrupted turns](https://github.com/google-gemini/gemini-cli/pull/29265)** · OPEN · `p2` · `area/agent`
   Fixes a critical issue where SIGINT, timeouts, or aborted tool executions corrupt in-memory session history and break subsequent prompt execution. Directly targets the interruption pain echoed across several top issues.

2. **[#29248 — Avoid duplicate history and telemetry after confirmation](https://github.com/google-gemini/gemini-cli/pull/29248)** · OPEN · `area/core`
   Stops slash-command history and telemetry from being inserted twice when a confirmation dialog overlaps with an incoming message — e.g., `/resume save <tag>` with an overwrite prompt.

3. **[#29163 — Prevent crash during authentication in git repositories](https://github.com/google-gemini/gemini-cli/pull/29163)** · OPEN · `p1` · `area/security`
   Fixes startup crashes when `useGitBranchName` runs inside a macOS Seatbelt-restricted `.git` directory. Important for users in hardened or sandboxed environments.

4. **[#29156 — Stop nullifying user git config in shell executions](https://github.com/google-gemini/gemini-cli/pull/29156)** · OPEN · `area/core`
   Reverts an over-aggressive sandboxing change ([#28792](https://github.com/google-gemini/gemini-cli/pull/28792)) that pointed `GIT_CONFIG_GLOBAL`/`GIT_CONFIG_SYSTEM` at `/dev/null`, silently hiding `user.name`, `user.email`, and credential helpers from every shell command.

5. **[#29155 — Decode BOM-encoded content correctly in `isEmpty`](https://github.com/google-gemini/gemini-cli/pull/29155)** · OPEN · `area/core`
   Fixes UTF-16/UTF-32 whitespace-only plan files being treated as non-empty — NUL-decoded bytes tripped `trim()` and broke `validatePlanContent`.

6. **[#29151 — Handle skill precedence and active state case-insensitively](https://github.com/google-gemini/gemini-cli/pull/29151)** · OPEN · `p1` · `area/agent`
   Fixes a case-sensitivity mismatch in `SkillManager` where workspace skills failed to override built-in/extension skills if names differed only in casing.

7. **[#29067 — Remove misleading security schemes and hardcoded credentials from a2a-server](https://github.com/google-gemini/gemini-cli/pull/29067)** · CLOSED · `area/security`
   Cleans up `coderAgentCard` and `customUserBuilder`, removing fake `securitySchemes` and hardcoded credentials. Closes [#29001](https://github.com/google-gemini/gemini-cli/issues/29001).

8. **[#29089 — Forward abortSignal to retryWithBackoff in BaseLlmClient](https://github.com/google-gemini/gemini-cli/pull/29089)** · CLOSED · `area/core`
   Ensures `SessionSummaryService`, chat compression, and the classifier actually respect abort signals during retry backoff — previously a cancellation could still burn through retries.

9. **[#29088 — Resolve VSCode IDE companion `stop()` with an MCP stream open](https://github.com/google-gemini/gemini-cli/pull/29088)** · CLOSED · `area/core`
   Fixes `IdeServer.stop()` deadlocking because a long-lived MCP streaming response on `GET /mcp` prevented the HTTP server from draining. Resolves extension deactivation hangs ([#28785](https://github.com/google-gemini/gemini-cli/issues/28785)).

10. **[#29063 — Stop Plan Mode from waiting on user feedback in non-interactive sessions](https://github.com/google-gemini/gemini-cli/pull/29063)** · CLOSED · `p1` · `area/non-interactive`
    Fixes `gemini -p "..." -y` Plan Mode runs hanging forever on a user turn that never arrives. Closes the well-known [#28913](https://github.com/google-gemini/gemini-cli/issues/28913) and its predecessor [#26004](https://github.com/google-gemini/gemini-cli/issues/26004).

Also notable: **[#29087 — Prevent concurrent extension install races](https://github.com/google-gemini/gemini-cli/pull/29087)** (CLOSED), which uses `proper-lockfile` to stop two CLI processes from corrupting the same extension installation.

## 5. Feature Request Trends

- **AST-aware code intelligence**: Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) push for method-bound reads, precise search, and codebase mapping via AST tooling to cut token waste and turn counts.
- **Surgical / token-frugal context loading**: The "Tactful Extraction" proposal ([#19561](https://github.com/google-gemini/gemini-cli/issues/19561)) — a grep-first discovery hierarchy — complements the AST work and targets the ~36.6k-token baseline context bloat.
- **OS-level sandboxing for shell execution**: [#19873](https://github.com/google-gemini/gemini-cli/issues/19873) wants zero-dependency sandboxing plus post-execution intent routing, leaning into the model's native bash fluency without the security risk.
- **Subagent observability & governance**: Requests include visible subagent trajectories via `/chat share` ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)), included subagent context in `/bug` reports ([#21763](https://github.com/google-gemini/gemini-cli/issues/21763)), and persistent file-based task tracking to replace in-context `WriteToDo` ([#18836](https://github.com/google-gemini/gemini-cli/issues/18836)).
- **Browser agent resilience**: Automatic session takeover and lock recovery for persistent profiles ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232)), plus honoring `settings.json` overrides ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)).

## 6. Developer Pain Points

- **Misleading success reporting**: Subagents terminating on MAX_TURNS or Wayland failures report "GOAL success," eroding trust in autonomous workflows ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323), [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)).
- **Hangs and stuck states**: Generalist agent hangs ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), shell "Waiting input" deadlocks ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and interactive-prompt traps during scaffolding ([#22465](https://github.com/google-gemini/gemini-cli/issues/22465)) remain the most disruptive day-to-day failures.
- **Auto Memory system trust**: The memory subsystem generates a steady stream of bug reports — low-signal retries ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)), silent invalid patch skips ([#26523](https://github.com/google-gemini/gemini-cli/issues/26523)), and pre-redaction secret exposure ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)).
- **Agents not using user configuration**: Skills and

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-09-09

## 1. Today's Highlights

Two patch releases shipped today: **v1.0.84-2** makes Vim mode generally available and adds Windows sandbox blocked-access recording, while **v1.0.84-3** fixes `/copy` task-completion output and OAuth-authenticated MCP startup reliability. The issue tracker remains dominated by session-resume failures, MCP configuration friction, and Windows-specific desktop app regressions.

## 2. Releases

**v1.0.84-3**
- **Fixed:** `/copy` now includes task completion messages when available.
- **Fixed:** OAuth-authenticated MCP servers connect reliably during session startup.

**v1.0.84-2**
- **New:** Vim mode is available to everyone. Enable it with `/vim` or by setting `editorMode` to `vim`; the current mode is shown while typing.
- **Improved:** On supported Windows sandbox policies, interactive shell commands now record blocked accesses.

See the [release page](https://github.com/github/copilot-cli/releases) for details.

## 3. Hot Issues

1. **[#13 — CLI input should have a vi/vim input mode](https://github.com/github/copilot-cli/issues/13)**  
   Closed after shipping in v1.0.84-2. This was the community’s most-upvoted open feature request with **76 👍** and 11 comments.

2. **[#4742 — Desktop app: cannot create a second Local session while one is running](https://github.com/github/copilot-cli/issues/4742)**  
   After desktop app 1.1.15, creating a second Local session fails with “This project already has an active Local workspace.” High-impact regression for parallel working sessions; 10 comments.

3. **[#4612 — Runaway FileWatch host-event loop freezes TUI and grows debug log to 13 GB](https://github.com/github/copilot-cli/issues/4612)**  
   Long-running sessions can enter a tight loop that makes the terminal UI unresponsive and writes massive debug logs. Serious stability issue; 9 comments.

4. **[#4756 — Windows app

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-09-09

## Today's Highlights

No new releases landed in the past 24 hours. The main community signal is an open, high-severity auth regression: `/login` device flow succeeds in the browser but then fails with HTTP 500 on macOS, affecting both the CLI and the VS Code extension. On the engineering side, two PRs target data integrity and fetch reliability — refusing to edit non-UTF-8 files and suppressing duplicated extracted comments.

## Releases

No releases in the last 24 hours.

## Hot Issues

Only 3 issues were updated in the last 24h; all are listed below.

- [#2638 [OPEN] /login device auth fails with HTTP 500 after successful browser approval (CLI v0.42.0, macOS)](https://github.com/MoonshotAI/kimi-cli/issues/2638)  
  A fresh blocker for macOS users on the free plan. The browser approval succeeds, but the CLI then receives HTTP 500, and the same failure is reproducible from the VS Code extension. Since login is the entry point, this is likely the most urgent item today. No comments or reactions yet.

- [#1270 [CLOSED] VSCode extension: after typing @, open files should be displayed first](https://github.com/MoonshotAI/kimi-cli/issues/1270)  
  A UX enhancement request from v0.4.3: when users type `@` in the dialog, already-open files should be prioritized because they are the most likely targets for analysis/operations. The issue is now closed, but it reflects a common desire for tighter editor-context integration.

- [#2601 [CLOSED] Quote & Reply: comment on any selected part of an AI response in Kimi Web](https://github.com/MoonshotAI/kimi-cli/issues/2601)  
  Requests the ability to select any text span in an assistant response — a paragraph, code block, step, or diff line — and attach a follow-up question/comment directly to that selection. Useful for precise conversational continuation. Closed, likely superseded by product changes.

## Key PR Progress

Only 2 PRs were updated in the last 24h; both are included.

- [#1863 [CLOSED] fix(fetch): suppress duplicated extracted comment text](https://github.com/MoonshotAI/kimi-cli/pull/1863)  
  Fixes `FetchURL` output where Trafilatura extraction can duplicate GitHub issue comments alongside the main body. The change inspects main text and comments separately, suppresses comments that normalize to the same content, and adds a regression test. This improves reliability when the CLI fetches web pages or issue URLs.

- [#2595 [OPEN] fix(StrReplaceFile): refuse to edit files that are not valid UTF-8](https://github.com/MoonshotAI/kimi-cli/pull/2595)  
  Addresses a silent-corruption bug: `StrReplaceFile` currently decodes files with `errors="replace"`, applies an edit, then writes everything back — turning any invalid UTF-8 byte into `U+FFFD` and corrupting bytes unrelated to the edit. The fix refuses to edit non-UTF-8 files instead, protecting file integrity.

## Feature Request Trends

From the small issue sample, two directions stand out:

- **Editor-context awareness**: Users expect the CLI/extension to prioritize already-open files in `@` mentions for faster analysis workflows.
- **Conversational precision**: Users want to quote and reply to specific segments of AI-generated responses, especially for following up on code blocks or plan steps.
- **Cross-surface consistency**: Issues appearing in both CLI and VS Code extension highlight that users expect the same behavior and reliability across all surfaces.

## Developer Pain Points

- **Auth reliability**: Device-code login breaking after browser approval is a critical workflow blocker, especially when it spans multiple client surfaces.
- **File-encoding safety**: Editing files with non-UTF-8 bytes can silently corrupt them via replacement characters — developers need fail-fast behavior rather than data loss.
- **Noisy fetched content**: Duplicate extracted comments from fetched GitHub/web URLs reduce trust in the fetch tool.
- **Context-selection friction**: Both open-file prioritization and quote-and-reply requests reflect a common pain point: maintaining precise context while interacting with AI output.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

⚠️ Summary generation failed.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

⚠️ Summary generation failed.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

⚠️ Summary generation failed.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

⚠️ Summary generation failed.

</details>