# Cheapest Good AI Models for FRC Robot Code (WPILib Java)

A short guide to the best price-for-performance models for coding with **Kilo Code → OpenRouter**.
Companion to the prompting guide in [Prompting-AI-for-FRC-robotics.md](Prompting-AI-for-FRC-robotics.md).

*Snapshot: 2026-10-29. Model lineups and prices change weekly — links are in [Sources](#sources).*

## TL;DR

- **Your team's current model is DeepSeek V4 Flash 0731 — the lowest scorer on this chart (12/100†).** The upgrade to make is **DeepSeek V4.1 Flash 1017** (score 39, $0.26/1M): its direct successor, and the most-used model on OpenRouter.
- **GLM-5.3 Flash** is the crazy-cheap pick: ~5× less expensive than V4.1 Flash, almost the same score.
- **Claude Haiku 5.5** is the best "smart but cheap" pick.
- **GLM-5.3** is the best cheap model for big agent jobs (multi-file changes, long refactors).
- **Avoid GPT-6 Luna and MiniMax M3.1 Flash for robot code** — cheap and popular, but weak at agentic coding and/or high rates of making things up.
- Free practice models exist (bottom of page). Don't run them on competition-critical code.

## The chart — models up to $1.50 per 1M tokens

**Price /1M** is one blended number: 3 parts input + 1 part output. **Score /100** grades agentic coding — [how to read it](#how-to-read-this).

| Model (OpenRouter ID) | Price /1M | Score /100 | Notes |
|---|---|---|---|
| `z-ai/glm-5.3-flash` | $0.05 | 37 | Cheapest good coder |
| `deepseek/deepseek-v4-flash-0731` | $0.15 | 12† | **Your team's current model** (deprecated) |
| `xiaomi/mimo-v2.6-flash` | $0.18 | 32 | New; very cheap, solid |
| `anthropic/claude-haiku-5.5` | $0.20 | 37 | Best cheap "brain" |
| `openai/gpt-6-luna` | $0.20 | 27 | ⚠ weak at agent work |
| `deepseek/deepseek-v4.1-flash-1017` | $0.26 | 39 | Best all-rounder — the upgrade to make |
| `minimax/minimax-m3.1-flash` | $0.26 | 32 | ⚠ makes things up often |
| `qwen/qwen3.8-27b` | $0.34 | 20 | Cheap in, weak agent |
| `z-ai/glm-5.3` | $0.40 | 41 | Best cheap agent coder |
| `stepfun/step-5-preview` | $1.43 | 36 | Popular; near the cap |

† FrontierCode has not been run on DeepSeek V4 Flash, so its score is Terminal-Bench 4.0 alone — every other score averages the two benchmarks.

### For reference — the ladder up to Claude Opus 5.5

| Model (OpenRouter ID) | Price /1M | Score /100 |
|---|---|---|
| `google/gemini-3.8-flash` | $1.65 | 28 |
| `openai/gpt-6.1-terra` | $2.00 | 46 |
| `x-ai/grok-4.7` | $3.00 | 30 |
| `moonshotai/kimi-k3.1-pro` | $4.00 | 57 |
| `anthropic/claude-sonnet-5.5` | $4.00 | 55 |
| `google/gemini-4-argon` | $4.00 | 50 |
| `anthropic/claude-opus-5.5` | $8.00 | 56 |

The best money can buy scores ~55–57 — roughly 15–20 points above the cheap winners — for 10–30× the price. Spending more doesn't always help: `x-ai/grok-4.7` ($3.00, score 30) is beaten by several $0.05–0.40 models.

### How to read this

- **Price /1M** = (3 × input + 1 × output) ÷ 4, in USD per million tokens — the blended rate you actually pay when a task is mostly input with some output.
- **Score /100** = the average of two Artificial Analysis agentic-coding benchmarks: **Terminal-Bench 4.0** (real work in a terminal: edit files, run commands, recover from errors) and **FrontierCode** (fixing real bugs in real open-source repos). A score of ~40 means it passes ~40% of tasks on average.
- Higher score = more likely to edit code, run the build, and fix its own errors without human help — exactly what Kilo Code asks of a model. Premium models are graded at their highest "effort" setting.
- **To switch in Kilo Code:** open the model selector and search the OpenRouter ID (e.g. `z-ai/glm-5.3-flash`).

## What actually matters for WPILib

- **All models here know Java; none of them knows WPILib well.** Expect any of them to occasionally invent methods that don't exist. Model choice can't fix this: **paste the real docs into the prompt and build after every change** (see the prompting guide).
- **The score measures "agentic coding"** — editing files, running builds, reacting to errors — exactly how you use Kilo Code.
- **Most have 1M-token context (Qwen 27B: 256k), all support tool calling** — plenty for the WPILib docs + your robot code.
- **Costs are small either way.** Optimize for fewer failed builds, not fractions of a cent.

## Free models for practice

| Model | Notes |
|---|---|
| `poolside/laguna-s-2.1:free` | From a coding-specialist lab. Good for practice questions. |
| `cohere/north-mini-code:free` | Small code-specialist. |

Free tiers are rate-limited, can be slow, and usually allow your data to be used for training — **never paste anything private**. Fine for "explain this code" practice, not for robot code you'll run.

## Let OpenRouter pick for you

`openrouter/pareto-code` is an automatic router: each request goes to a strong, price-efficient coding model (up to 2M context). If you don't want to think about the list above, try setting Kilo Code to this model — and fall back to the table if anything misbehaves.

## Sources

- **OpenRouter** — model list & prices: https://openrouter.ai/models · weekly usage rankings: https://openrouter.ai/rankings
- **Artificial Analysis** — coding-agent benchmarks: https://artificialanalysis.ai/agents/coding-agents · per-model pages: https://artificialanalysis.ai/models/deepseek-v4-flash *(swap the model name in the URL for the others)*
- **DeepSeek docs** — https://api-docs.deepseek.com/

*Prices are OpenRouter's listed rates at snapshot time and can differ by region/provider (e.g. GLM-5.3 Flash is listed from ~$0.03 up, and Z.ai's direct API price is higher). Check the model page before relying on exact costs.*
