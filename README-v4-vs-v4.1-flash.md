# DeepSeek V4 Flash vs V4.1 Flash — which should the team use?

**Short answer: DeepSeek V4.1 Flash 1017.** It costs about **1.7× more** but scores about **2.8× higher on agentic code reasoning** (Terminal-Bench 4.0: 12% → 34%), and it's the version DeepSeek still supports. Details below.

Companion guides: [README.md](README.md) (how to prompt) · [README-coding-models.md](README-coding-models.md) (full model chart).

*Snapshot: 2026-10-29. Prices and lineups change; all links are at the end.*

## Side by side

| | **DeepSeek V4 Flash 0731** (team's current) | **DeepSeek V4.1 Flash 1017** (recommended) |
|---|---|---|
| OpenRouter ID | `deepseek/deepseek-v4-flash-0731` | `deepseek/deepseek-v4.1-flash-1017` |
| Released | 2026-07-31 | 2026-10-17 |
| OpenRouter price /1M (in · out) | $0.12 · $0.24 | $0.15 · $0.60 |
| Blended price /1M (3 in : 1 out) | **$0.15** | **$0.26** |
| Context window | 1M tokens | 1M tokens |
| Input | text | text + image |
| Size | 284B total / 13B active | 552B total / 16B active |
| License | MIT (open weights) | MIT (open weights) |
| **Terminal-Bench 4.0** (agentic coding) | **12%** | **34%** |
| **FrontierCode** (fixing real bugs) | not run | **44%** (v2.0: 28%) |
| AA Intelligence Index | not scored | **32** (#1 of 19 in its class) |
| Output speed | 113 tokens/s | 179 tokens/s |
| Status | **deprecated** — superseded by V4.1 Flash | current |

## Is the upgrade worth the price?

| | V4 Flash 0731 | V4.1 Flash 1017 | Change |
|---|---|---|---|
| Blended price /1M | $0.15 | $0.26 | **1.8× more** |
| Typical task (100k in + 20k out) | ≈$0.02 | ≈$0.03 | **1.6× more** |
| **Agentic code reasoning — Terminal-Bench 4.0** | 12% | 34% | **2.8× better** |
| Code generation — SciCode | 50% | 56% | 1.1× better |
| Real bug fixing — FrontierCode | not run | 44% | — |

Plainly: **≈1.7× the price for ≈2.8× the agentic-coding capability**, and the whole gain is in code reasoning — the kind of work Kilo Code does. (Single-shot code generation, SciCode, was already close at 1.1×, so a plain average of the two code benchmarks is a more modest ≈1.4×. The upgrade pays off on long, multi-step coding tasks, which is what this team does.) With V4 Flash deprecated, the upgrade is the clear call anyway.

## Why V4.1 Flash 1017 wins

1. **Much stronger at agentic coding.** Terminal-Bench 4.0 — tasks where the model edits files, runs commands and fixes its own errors, exactly what Kilo Code does — jumps from **12% to 34%**. On FrontierCode (fixing real bugs in real repositories) it scores **44%**, while the older model was never benchmarked.
2. **It's the supported model; the old one is deprecated.** Artificial Analysis flags V4 Flash 0731 as deprecated and points to V4.1 Flash, so don't expect further fixes or improvements.
3. **Faster:** ~179 tokens/s vs ~113 tokens/s.
4. **More capable overall:** AA Intelligence Index **32** (well above the ~23 median for its class), and it accepts **images** as well as text — handy for screenshots of build errors or field diagrams.

## When V4 Flash 0731 is still fine

- Quick, simple edits or "explain this code" questions.
- If you truly want the cheapest option, note that **GLM-5.3 Flash ($0.05/1M, score 37)** is cheaper *and* scores higher than either DeepSeek Flash — see the [model chart](README-coding-models.md).

## Which "V4.1 Flash" revision?

Two V4.1 Flash snapshots exist on OpenRouter:
- `deepseek/deepseek-v4.1-flash` (Sept 10) — deprecated in favour of the newer revision (Terminal-Bench 26.8%, FrontierCode 44%).
- `deepseek/deepseek-v4.1-flash-1017` (Oct 17) — **use this one** (Terminal-Bench 33.8%, FrontierCode 43.7%).

## Switch in Kilo Code

Open the model selector, search **`deepseek/deepseek-v4.1-flash-1017`**, and select it. Keep the usual rule: paste the real WPILib docs and build after every change.

## Links

- **OpenRouter** — [V4 Flash 0731](https://openrouter.ai/deepseek/deepseek-v4-flash-0731) · [V4.1 Flash 1017](https://openrouter.ai/deepseek/deepseek-v4.1-flash-1017)
- **Artificial Analysis** — [V4 Flash 0731](https://artificialanalysis.ai/models/deepseek-v4-flash) · [V4.1 Flash 1017](https://artificialanalysis.ai/models/deepseek-v4-1-flash-1017)
- **Model weights (Hugging Face)** — [V4 Flash 0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) · [V4.1 Flash 1017](https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash-1017)
- **DeepSeek docs** — https://api-docs.deepseek.com/

*Prices are OpenRouter's listed rates at snapshot time and can differ by provider/region. Benchmark scores are from Artificial Analysis.*
