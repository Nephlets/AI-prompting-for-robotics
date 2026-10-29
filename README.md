# FRC Robotics AI Guides

Practical, beginner-friendly guides for an FRC robotics team using AI to write **WPILib Java**. Nobody on the team knows how to code yet, so everything here starts from zero.

**This knowledge base was gathered with DeepSeek V4.1 Flash** — every page was researched and written using DeepSeek V4.1 Flash running in Kilo Code (via OpenRouter). *Snapshot: 2026-10-29; prices and model lineups change.*

## What's in this repo

| File | What it covers |
|---|---|
| [Prompting-AI-for-FRC-robotics.md](Prompting-AI-for-FRC-robotics.md) | How to prompt AI to write WPILib Java: the rules, the failure modes, and the research behind them. |
| [README-coding-models.md](README-coding-models.md) | Price-vs-performance chart of coding models — blended $/1M against a single 0–100 coding score. |
| [README-v4-vs-v4.1-flash.md](README-v4-vs-v4.1-flash.md) | Direct comparison of DeepSeek V4 Flash and V4.1 Flash, with the price-vs-capability maths. |
| [README-benchmarks-explained.md](README-benchmarks-explained.md) | What every benchmark tests, how it is run, and how it is scored. |
| [README-sources.md](README-sources.md) | Every source used across the guides, with a short note on what was taken from each. |

## Rough outline of what each guide covers

### Prompting-AI-for-FRC-robotics.md
- Who it's for: a five-person FRC team starting from zero
- The short version: seven rules for prompting AI to write Java
- Why generic prompting advice isn't enough (niche WPILib API; Kilo Code is an agent)
- What the sources actually say (OpenAI, Anthropic, DAIR, the Codex paper)
- Java-specific findings: imports, Command-Based style, pinning the season
- Failure modes to expect, and beginner guardrails
- Open questions for the team

### README-coding-models.md
- How the price is blended (3 parts input : 1 part output)
- A single 0–100 coding score (Terminal-Bench 4.0 + FrontierCode)
- Models up to $1.50/1M, with notes, plus a premium reference table up to Claude Opus 5.5
- Free practice models and the `openrouter/pareto-code` auto-router
- What matters for WPILib specifically

### README-v4-vs-v4.1-flash.md
- Side-by-side spec table (price, context, size, scores, speed, status)
- Is the upgrade worth the price? ≈1.7× the cost for ≈2.8× the agentic-coding capability
- Why V4.1 Flash 1017 wins — and when V4 Flash is still fine
- Which "V4.1 Flash" revision to use, and how to switch in Kilo Code

### README-benchmarks-explained.md
- The two composite indexes: the AA Intelligence Index v5.0 and the Coding Agent Index v2.0
- The coding benchmarks in detail: Terminal-Bench 4.0, FrontierCode, SWE-Atlas-QnA-AA, SciCode, HumanEval
- The rest of the Intelligence Index, plus other benchmarks you may see
- How Artificial Analysis runs them, and why benchmarks don't tell you everything

### README-sources.md
- Every link used, grouped by topic
- A note next to each source saying what was taken from it, and which guide uses it

## Where to start

1. **Prompting-AI-for-FRC-robotics.md** — learn how to ask the AI for code.
2. **README-coding-models.md** — pick a cheap model for Kilo Code.
3. **README-benchmarks-explained.md** — understand what the scores mean.
4. **README-sources.md** — check the original sources.

Anything time-sensitive (prices, model IDs, benchmark versions) is a snapshot — verify it against the linked sources before relying on it.
