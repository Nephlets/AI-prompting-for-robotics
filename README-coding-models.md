# Cheapest Good AI Models for FRC Robot Code (WPILib Java)

A short guide to the best price-for-performance models for coding with **Kilo Code → OpenRouter**.
Companion to the prompting guide in [README.md](README.md).

*Snapshot: 2026-10-29. Model lineups and prices change weekly — links are in [Sources](#sources).*

## TL;DR

- **Your current model, DeepSeek V4.1 Flash 1017, is still the best all-rounder** in its price range — and the most-used model on OpenRouter. Nothing cheaper clearly beats it.
- **GLM-5.3 Flash** is the crazy-cheap pick: ~5× less expensive, almost the same scores on coding tests.
- **Claude Haiku 5.5** is the best "smart but cheap" pick.
- **GLM-5.3** is the best cheap model for big agent jobs (multi-file changes, long refactors).
- **Avoid GPT-6 Luna and MiniMax M3.1 Flash for robot code** — cheap and popular, but weak at agentic coding and/or high rates of making things up.
- Free practice models exist (bottom of page). Don't run them on competition-critical code.

## The short list

Prices are OpenRouter rates (USD per 1M tokens, in · out). "Cost/task" ≈ one typical Kilo Code task (100k tokens in, 20k out, no caching).

| Model (OpenRouter ID) | $/1M in · out | Cost/task | AA Index | Terminal-Bench 4.0 | FrontierCode 1.1 / 2.0 | Weekly use | Why |
|---|---|---|---|---|---|---|---|
| `z-ai/glm-5.3-flash` | 0.03 · 0.10 | ≈$0.005 | — | 33% | 41% / — | #3 (+32%) | Cheapest good coder |
| `openai/gpt-6-luna` | 0.10 · 0.50 | ≈$0.02 | 27.8 | 13% | 42% / 25% | #4 (+58%) | ⚠ weak at agent work |
| `anthropic/claude-haiku-5.5` | 0.10 · 0.50 | ≈$0.02 | 36.2 | 33% | 42% / 35% | — | Best cheap "brain" |
| `xiaomi/mimo-v2.6-flash` | 0.14 · 0.28 | ≈$0.02 | 26.7 | 23% | 42% / 22% | #10 (−52%) | New; very cheap, solid |
| `deepseek/deepseek-v4.1-flash-1017` | 0.15 · 0.60 | ≈$0.03 | 32.5 | 34% | 44% / 28% | **#1 (+140%)** | Current default — keep |
| `minimax/minimax-m3.1-flash` | 0.15 · 0.60 | ≈$0.03 | 28.9 | 26% | 39% / 21% | rising | ⚠ makes things up often |
| `qwen/qwen3.8-27b` | 0.04 · 1.25 | ≈$0.03 | 20.1 | 6% | 34% / 15% | — | Cheap in, weak agent |
| `z-ai/glm-5.3` | 0.07 · 1.40 | ≈$0.04 | 31.7 | **42%** | 40% / 22% | #8 | Best cheap agent coder |
| `stepfun/step-5-preview` | 1.00 · 2.70 | ≈$0.15 | 28.5 | 33% | 38% / 12% | #7 (+132%) | Popular; 4× DeepSeek price |
| `google/gemini-3.8-flash` | 0.85 · 4.13 | ≈$0.17 | 30.5 | 20% | 36% / 19% | — | Research-first |
| `openai/gpt-6.1-terra` | 1.00 · 5.00 | ≈$0.20 | **51.0** | **56%** | 36% / **42%** | new | "When you're stuck" (~8× price) |

**How to read this**
- **AA Index** = Artificial Analysis Intelligence Index v5.0 — the overall "smarts" score. For reference, the best premium models (Claude Opus 5.5, GPT-6 Astra) score ~55–58 at 10–50× the price. ("—" = AA hasn't published one for that model yet.)
- **Terminal-Bench 4.0** = can the model do real agent work in a terminal: edit files, run commands, fix its own errors. This is basically what Kilo Code does for you.
- **FrontierCode 1.1 / 2.0** = fixing real bugs in real open-source repositories (2.0 is newer and harder).
- **To switch in Kilo Code:** open the model selector and search the OpenRouter ID (e.g. `z-ai/glm-5.3-flash`).

## What actually matters for WPILib

- **All models here know Java; none of them knows WPILib well.** Expect any of them to occasionally invent methods that don't exist. Model choice can't fix this: **paste the real docs into the prompt and build after every change** (see the prompting guide).
- **The scores above measure "agentic coding"** — editing files, running builds, reacting to errors — exactly how you use Kilo Code.
- **Most have 1M-token context (Qwen 27B: 256k), all support tool calling** — plenty for the WPILib docs + your robot code.
- **Costs are small either way** — from half a cent to ~20¢ per task. Optimize for fewer failed builds, not fractions of a cent.

## Premium (only when you're stuck)

- `openai/gpt-6.1-terra` — 51 AA Index, 56% Terminal-Bench — but ~8× the blended price of DeepSeek. For the hardest bugs, not daily use.
- The top of the charts (Claude Opus 5.5, GPT-6 Astra, Claude Fable 5.1) score ~55–58 but cost 10–50× more. Overkill for FRC.

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
- **Artificial Analysis** — coding-agent benchmarks: https://artificialanalysis.ai/agents/coding-agents · per-model pages (Intelligence Index v5.0, Terminal-Bench 4.0, FrontierCode): https://artificialanalysis.ai/models/deepseek-v4-1-flash-1017 *(swap the model name in the URL for the others)*
- **DeepSeek docs** — https://api-docs.deepseek.com/

*Prices are OpenRouter's listed rates at snapshot time and can differ by region/provider (e.g. GLM-5.3 Flash is listed from ~$0.03 up, and Z.ai's direct API price is higher). Check the model page before relying on exact costs.*
