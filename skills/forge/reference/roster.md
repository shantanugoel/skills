# Roster

Model and provider lookup for subagent delegation. Override order: this file < `.agents/forge.md` ("Roster changes") < one-run command overrides. Map provider names and model IDs using the active runner (`<forge>/reference/runner-t3code.md`, `<forge>/reference/runner-rex.md`, or native subagent IDs).

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

Ordered by preference per model. Runner files map each common provider name (`claude`, `antigravity`, `cursor`, `codex`, `pi`) to its runner-specific target and effort option.

| Model | ID | Providers (in order) | Effort limits |
| --- | --- | --- | --- |
| Opus 5.5 | `claude-opus-5-5` | `claude`, `antigravity`, `cursor`, `pi` | |
| Fable 5.2 | `claude-fable-5-2` | `claude`, `cursor`, `pi` | |
| Haiku 5.5 | `claude-haiku-5-5` | `claude`, `cursor`, `pi` | |
| Gemini 4 Neon | `gemini-4-neon` | `antigravity`, `cursor` | |
| Grok 4.7 | `grok-4.7` | `cursor` | |
| GPT-6.2 Astra | `gpt-6.2-astra` | `codex` | |
| GPT-6.2 Sol | `gpt-6.2-sol` | `codex` | |
| DeepSeek V4.1 Flash | `opencode-go/deepseek-v4.1-flash` | `pi` | `low`, `high`, `max` only |
| Hy4 Flash Free | `opencode-go/hy4-flash-free` | `pi` | `off`, `high` only |

On `pi`, prefix `claude-*` model IDs with `anthropic/`. Cursor does not provide the GPT models above. Machines with fewer providers rely on fallback.

## Selection rules

- **Fallback:** On unavailable provider or runtime failure (rate limit, outage, refusal), try the next provider for the same model, then the next model for the role. Never switch models due to poor output—send findings back instead. If no model remains, stop and ask the owner.
- **Effort:** Raise one step for: `invariant` issues (build and review), stored data or money, high complexity, retry after a failed review round, or a run that stopped prematurely without a stop condition (e.g., `high` → `xhigh`). Lower one step for small mechanical work. If a provider lacks the requested level, use the nearest supported level below it.
- **Independence:** Reviewer and Test author must not use the same model as Implementer; if fallback causes a collision, stop and ask the owner. Tester should also differ from Implementer—if they collide, pick the next available Tester and note it on the issue.
