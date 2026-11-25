# Roster

This file tells which model does which role. The orchestrator reads it before each delegation. With T3 Code, it gives
the provider, the model and the option to `delegate_task` (`target.providerInstanceId`, `target.model`,
`target.options`). Without T3 Code, refer to "Delegation" in `workflow.md`.

The section "Roster changes" in the project settings changes this file for one project. A change that the owner gives
with a command changes it for one run.

## Roles

The models are in order. Each model has its default effort.

| Role | First | Second | Third |
| --- | --- | --- | --- |
| Orchestrator | Opus 5.5, medium | | |
| Planner | Fable 5.2, high | GPT-6.2 Astra, high | Gemini 4 Neon, high |
| Designer, test author | Opus 5.5, high | GPT-6.2 Astra, high | Gemini 4 Neon, high |
| Implementer | Grok 4.7, xhigh | GPT-6.2 Sol, high | DeepSeek V4.1 Flash, max |
| Reviewer | Gemini 4 Neon, high | GPT-6.2 Astra, high | Opus 5.5, high |
| Tester | Hy4 Flash Free, high | DeepSeek V4.1 Flash, max | Haiku 5.5, medium |
| Explorer, researcher, other | DeepSeek V4.1 Flash, max | Haiku 5.5, medium | |

The orchestrator is the thread itself. Its row tells which model to start the thread with.

## Providers

The providers for each model are in order. Each cell is: `provider` / `model id` / the name of the effort option.

| Model | First | Second | Third | Fourth |
| --- | --- | --- | --- | --- |
| Opus 5.5 | `claudeAgent` / `claude-opus-5-5` / `effort` | `antigravity` / `claude-opus-5-5` / `thought_level` | `cursor` / `claude-opus-5-5` / `effort` | `pi` / `anthropic/claude-opus-5-5` / `thinking` |
| Fable 5.2 | `claudeAgent` / `claude-fable-5-2` / `effort` | `cursor` / `claude-fable-5-2` / `effort` | `pi` / `anthropic/claude-fable-5-2` / `thinking` | |
| Haiku 5.5 | `claudeAgent` / `claude-haiku-5-5` / `effort` | `cursor` / `claude-haiku-5-5` / `reasoning_effort` | `pi` / `anthropic/claude-haiku-5-5` / `thinking` | |
| Gemini 4 Neon | `antigravity` / `gemini-4-neon` / `thought_level` | `cursor` / `gemini-4-neon` / `reasoning_effort` | |
| Grok 4.7 | `cursor` / `grok-4.7` / `reasoning_effort` | | |
| GPT-6.2 Astra | `codex` / `gpt-6.2-astra` / `reasoningEffort` | | |
| GPT-6.2 Sol | `codex` / `gpt-6.2-sol` / `reasoningEffort` | | |
| DeepSeek V4.1 Flash | `pi` / `opencode-go/deepseek-v4.1-flash` / `thinking` (only `low`, `high`, `max`) | | |
| Hy4 Flash Free | `pi` / `opencode-go/hy4-flash-free` / `thinking` (only `off`, `high`) | | |

Cursor has none of the GPT models in this table. A machine can have fewer providers than this table. The fallback
rule covers this.

## Rules

- **Fallback.** If a provider is not available, or the task fails because of the provider (limit, outage, refusal),
  use the next provider of the same model. If the model has no provider left, use the next model of the role. Do not
  change the model because the result is bad. Send the task back with the findings. If a role has no model left,
  stop and ask the owner.
- **Effort.** The effort in the table is the default. Use one step more for an issue that has the `invariant` flag,
  that touches stored data or money, that is long or complex, or that failed one review round. Also use one step
  more when a run stops before the work is done and names no stop condition. For example, GPT-6.2 Sol goes from
  high to xhigh. Use one step less for a small mechanical issue. If a provider does not have the level, use the
  nearest level below it.
- **Independent review.** The reviewer must not be the model that wrote the code. If a fallback makes them the same,
  stop and ask the owner.
- **Independent test.** The tester must not be the model that wrote the code, if possible. If it is the same model,
  use the next tester in the roster that is available, and comment this on the issue.
- **Record.** Each stage comment on the issue names the model that did the stage.
