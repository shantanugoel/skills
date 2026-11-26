# Roster

Model and provider lookup for subagent delegation. Override order: this file < `.agents/forge.md` ("Roster changes") < one-run command overrides.

## Roles

Ordered by preference, with default effort.

| Role | First | Second | Third |
| --- | --- | --- | --- |
| Orchestrator | Opus 5.5, medium | | |
| Planner | Fable 5.2, high | Gemini 4 Neon, high | GPT-6.2 Astra, high |
| Designer, UX/UI designer, test author | Opus 5.5, high | GPT-6.2 Astra, high | Gemini 4 Neon, high |
| Implementer | GPT-6.2 Sol, high | Grok 4.7, high | DeepSeek V4.1 Flash, max |
| Reviewer | Gemini 4 Neon, high | Opus 5.5, high | GPT-6.2 Astra, high |
| Tester | Hy4 Flash Free, high | DeepSeek V4.1 Flash, high | Haiku 5.5, medium |
| Explorer, researcher, other | DeepSeek V4.1 Flash, max | Haiku 5.5, medium | |

The Orchestrator row indicates which model to start the thread with.

## Providers

Ordered by preference. Cell format: `provider` / `model id` / `effort option`.

| Model | First | Second | Third | Fourth |
| --- | --- | --- | --- | --- |
| Opus 5.5 | `claudeAgent` / `claude-opus-5-5` / `effort` | `antigravity` / `claude-opus-5-5` / `thought_level` | `cursor` / `claude-opus-5-5` / `effort` | `pi` / `anthropic/claude-opus-5-5` / `thinking` |
| Fable 5.2 | `claudeAgent` / `claude-fable-5-2` / `effort` | `cursor` / `claude-fable-5-2` / `effort` | `pi` / `anthropic/claude-fable-5-2` / `thinking` | |
| Haiku 5.5 | `claudeAgent` / `claude-haiku-5-5` / `effort` | `cursor` / `claude-haiku-5-5` / `reasoning_effort` | `pi` / `anthropic/claude-haiku-5-5` / `thinking` | |
| Gemini 4 Neon | `antigravity` / `gemini-4-neon` / `thought_level` | `cursor` / `gemini-4-neon` / `reasoning_effort` | | |
| Grok 4.7 | `cursor` / `grok-4.7` / `reasoning_effort` | | | |
| GPT-6.2 Astra | `codex` / `gpt-6.2-astra` / `reasoningEffort` | | | |
| GPT-6.2 Sol | `codex` / `gpt-6.2-sol` / `reasoningEffort` | | | |
| DeepSeek V4.1 Flash | `pi` / `opencode-go/deepseek-v4.1-flash` / `thinking` (`low`, `high`, `max` only) | | | |
| Hy4 Flash Free | `pi` / `opencode-go/hy4-flash-free` / `thinking` (`off`, `high` only) | | | |

Cursor does not provide the GPT models above. Machines with fewer providers rely on fallback.

## Selection rules

- **Fallback:** On unavailable provider or provider failure (rate limit, outage, refusal), try the next provider for the same model, then the next model for the role. Never switch models due to poor output—send findings back instead. If no model remains, stop and ask the owner.
- **Effort:** Raise one step for: `invariant` issues (build and review), stored data or money, high complexity, retry after a failed review round, or a run that stopped prematurely without a stop condition (e.g., `high` → `xhigh`). Lower one step for small mechanical work. If a provider lacks the requested level, use the nearest supported level below it.
- **Independence:** Reviewer and Test author must not use the same model as Implementer; if fallback causes a collision, stop and ask the owner. Tester should also differ from Implementer—if they collide, pick the next available Tester and note it on the issue.
