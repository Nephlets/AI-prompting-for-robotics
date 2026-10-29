# The Benchmarks, Explained

Every score our readmes quote comes from a public benchmark. This page explains what each one tests, how it is run, and how it is scored — so you can tell a real capability difference from a formatting change.

Companion guides: [README.md](README.md) (how to prompt) · [README-coding-models.md](README-coding-models.md) (model chart) · [README-v4-vs-v4.1-flash.md](README-v4-vs-v4.1-flash.md) (DeepSeek comparison).

*Snapshot: 2026-10-29. Benchmark suites change; the version history and links below track that.*

## How to read a benchmark score

- **pass@1** means the model must get it right on its *first* try — most benchmarks here use it. Where a benchmark runs several attempts (3, 5 or 10), the pass@1 figures are averaged across all attempts.
- **The harness matters.** Agentic benchmarks give the model a shell and tools. The same model can score very differently under different harnesses, turn limits and prompts.
- **Composites are weighted.** The AA Intelligence Index is four categories at 25% each — don't compare a single benchmark to an index.
- **Versions change.** Scores are only comparable within the same version of a benchmark (e.g. HLE and HLE-Diamond are different tests).
- On this page, **higher is better** for every metric except cost, time and hallucination.

## The two composite indexes

### Artificial Analysis Intelligence Index v5.0

One number for "how smart overall" — a weighted average of nine evaluations across four categories, 25% each:

| Category (25% each) | Evaluation | Index weight | What it is |
|---|---|---|---|
| Knowledge work | AA-Briefcase v1.1 | 15% | Multi-week business projects with file deliverables |
| | AutomationBench-AA | 5% | SaaS workflows driven through REST APIs |
| | GDP.pdf | 5% | Reasoning over long professional PDFs |
| Coding | FrontierCode 2.0 | 15% | Merge-worthy changes to real open-source repositories |
| | Terminal-Bench 4.0 | 10% | Agentic coding and terminal use |
| Science | Terminal-Bench-Science 0.1 | 15% | Scientific research workflows in a terminal |
| | CritPt v2 (Hard) | 10% | Research-level physics problems |
| General | AA-Omniscience v1.1 | 15% | Factual accuracy (10%) + non-hallucination (5%) |
| | HLE-Diamond | 10% | 1,000 hard reasoning and knowledge questions |

It is a mainly text-based, English-language suite; models that take images also receive the image questions. For reference, the strongest models today sit in the high 50s.

### Artificial Analysis Coding Agent Index v2.0

The headline on AA's coding-agents leaderboard — an **equal-weight average of three** coding benchmarks:

| Component | Tasks | By |
|---|---|---|
| FrontierCode v1.1 | 100 | Cognition |
| Terminal-Bench 4.0 | 66 | Laude Institute |
| SWE-Atlas-QnA-AA | 124 | Scale AI (grading adjusted by AA) |

Each component score is the mean over three attempts per task. The same page also reports cost per task, token use, wall-clock time, safety refusals and reward hacking.

## The coding benchmarks

### Terminal-Bench 4.0
**Tests:** whether an agent can finish hard, realistic work in a computer terminal — software engineering, machine learning, data processing, science, operations, security, hardware and media. 66 tasks.
**How it's run:** each task ships its own environment, human-written solution and test suite. The agent works in a shell through the `mini-swe-agent` harness (up to 500 steps, full transcript, no compaction). Grading runs in a separate verifier container, and a verifier timeout counts as a failure.
**How it's scored:** pass@1, averaged over three repeats per task. A task passes only if *every* test passes.
**Where it fits:** 10% of the Intelligence Index, and one of the three components of the Coding Agent Index.
**Source:** [tbench.ai](https://www.tbench.ai/?version=4) · [dataset](https://github.com/harbor-framework/terminal-bench) · [paper](https://arxiv.org/abs/2601.11868)

### FrontierCode 1.1 / 2.0
**Tests:** whether an agent's change to a real open-source repository is good enough that a maintainer would merge it.
**How it's run:** in AA's `Stirrup` harness, with shell commands that keep running in the background and long wall-clock limits. FrontierCode 2.0 has 132 tasks; FrontierCode 1.1 (the one used in the Coding Agent Index) runs its 100-task "main" set. Three attempts per task.
**How it's scored:** held-out tests plus a rubric of *blocking* and *non-blocking* checks. An attempt that fails any blocking check — or is flagged for looking up the solution — scores 0; otherwise it scores 70–100%. An LLM judge (GPT-6 Luna, medium effort) reviews the criteria.
**Where it fits:** 15% of the Intelligence Index (v2.0); a component of the Coding Agent Index (v1.1).
**Source:** [v2.0 announcement](https://cognition.com/blog/frontier-code-2.0) · [v1.1 announcement](https://cognition.com/blog/frontier-code-1.1)

### SWE-Atlas-QnA-AA
**Tests:** repository understanding — reading a codebase and producing a correct technical answer about it. 124 tasks.
**How it's run and scored:** binary pass/fail per attempt, aligned with Scale AI's Task Resolve Rate methodology, with AA adjusting the grading. Three attempts per task.
**Where it fits:** one of the three components of the Coding Agent Index.
**Source:** [dataset and grading](https://huggingface.co/datasets/ArtificialAnalysis/SWE-Atlas-QnA-AA)

### SciCode
**Tests:** Python code for scientific computing — 288 sub-problems drawn from 80 laboratory problems across 16 scientific disciplines.
**How it's run:** no agent tools. The model is asked for the *next step's* complete function (following a supplied header); the code is extracted from a Python code block and run in an isolated executor.
**How it's scored:** sub-problem-level pass@1, with a 300-second execution timeout.
**Where it fits:** was part of the Intelligence Index until v5.0; still reported, and used in our DeepSeek comparison.
**Source:** [scicode-bench.github.io](https://scicode-bench.github.io/) · [paper](https://arxiv.org/abs/2407.13168)

### The classic: HumanEval (historical)
Our prompting guide cites the Codex paper's **HumanEval** result. It is 164 hand-written Python problems, each with unit tests, scored with pass@k. It was the standard coding benchmark of its era but is now saturated (frontier models solve nearly all of it), which is why current leaderboards use the harder, agentic benchmarks above.
**Source:** [Codex paper, arXiv:2107.03374](https://arxiv.org/abs/2107.03374)

## The rest of the Intelligence Index

### AA-Briefcase v1.1 — agentic knowledge work
Realistic multi-week business scenarios (91 tasks across 4 scenarios; 2–5 tasks per week) with deliverable files. Run in a sandboxed agent harness (up to 500 turns, no internet). Graded by a three-judge panel: binary rubric checks plus pairwise comparisons for analytical and presentation quality. Headline metric is AA-Briefcase Elo. **15% of the Index.**

### AutomationBench-AA — SaaS workflows
657 tasks across Finance, HR, Marketing, Operations, Sales and Support, run in simulated apps (Gmail, Sheets, Slack, Salesforce, Zendesk, Jira, HubSpot) through REST API tool calls, up to 50 turns each. Grading is fully programmatic against the final environment state: a task scores 0 if any *guardrail* is broken, otherwise it earns the share of *objectives* completed. **5% of the Index.** [Zapier's AutomationBench](https://zapier.com/benchmarks).

### GDP.pdf — long professional documents
100 tasks across 10 domains, grounded in 4,592 PDF pages. The model answers in a single turn from the full extracted text (plus page images when it supports them); every task is attempted five times. GPT-5.6 Luna (medium) judges each criterion independently, and the headline is the All-pass rate. **5% of the Index.** [Surge AI's GDP.pdf](https://surgehq.ai/benchmarks/gdp-pdf).

### AA-Omniscience v1.1 — knowledge and hallucination
3,000 questions across 42 topics. Each answer is graded CORRECT, INCORRECT, PARTIAL or NOT_ATTEMPTED — **abstaining is neutral, guessing wrong is penalised**. It contributes two parts to the Index: accuracy (10%) and non-hallucination rate (5%). This is the metric behind the "makes things up often" warning in our model chart.

### HLE-Diamond — hard reasoning and knowledge
A cleaned-up 1,000-question version of Humanity's Last Exam (500 reasoning + 500 knowledge questions, 272 of them with images). Answered without tools and graded by an equality-checker LLM (GPT-5.6 Luna, medium). **10% of the Index.** [lastexam.ai](https://lastexam.ai/blog/hle-diamond).

### CritPt v2 (Hard Subset) — physics
40 of the 70 research-level physics problems that frontier models did *not* all solve. Models work with a code-execution tool in an offline sandbox; answers may be numbers, symbolic expressions or Python functions, checked by the official grading server. pass@1 over five repeats. **10% of the Index.** [critpt.com](https://critpt.com/).

### Terminal-Bench-Science 0.1 — scientific workflows
70 expert-curated terminal tasks across the life (19), physical (17), mathematical (17), engineering (9) and earth (8) sciences, each with its own test suite. Same `mini-swe-agent` setup as Terminal-Bench 4.0, but with up to 1,000 steps. **15% of the Index.** [terminal-bench-science.ai](https://terminal-bench-science.ai/).

## Other benchmarks you might see

| Benchmark | Tests | How it's scored |
|---|---|---|
| GPQA Diamond | Graduate-level biology, physics, chemistry (198 questions) | 4-option multiple choice, pass@1 |
| MMLU-Pro | Graduate-level knowledge (10 answer options) | Regex extraction, pass@1 |
| LiveCodeBench | Competitive-programming problems, harvested continuously to stay contamination-free | pass@1 |
| AIME 2025 | Olympiad mathematics (30 problems) | Integer answer, pass@1 over 10 repeats |
| MATH-500 | 500 competition-mathematics problems | — |
| AA-LCR v1.1 | Long-context reasoning across ~100k-token documents | Equality-checker LLM, pass@1 |
| HLE (original) | 2,158 text-only frontier questions | Equality-checker LLM, pass@1 |
| Terminal-Bench 2.1 / Hard | Older terminal-agent suites (89 / 44 tasks) | pass@1 over 3 repeats |
| τ²-Bench Telecom / τ³-Banking | Conversational support with tool calls, graded on the final account state | pass@1 over 3–5 repeats |
| AA-PersonalityBench | How a model communicates (style), not whether it is correct | Judged trait scores (1–100) |

All are Artificial Analysis evaluations unless noted; descriptions and prompts are in the [methodology](https://artificialanalysis.ai/methodology/intelligence-benchmarking).

## How Artificial Analysis runs them

- **Standard conditions:** the same prompts for every model; temperature 0 for non-reasoning models and 0.6 for reasoning models (unless the model's maker recommends otherwise). Maximum output is 16,384 tokens for non-reasoning models and the model's own maximum for reasoning models.
- **Zero-shot, instruction-prompted:** clear instructions, no worked examples.
- **pass@1, with repeats** where noted. Up to 30 retries on API errors, and every failed question is reviewed by hand.
- **Agent harnesses:** `mini-swe-agent` (Terminal-Bench 4.0, Terminal-Bench-Science), `Stirrup` (AA-Briefcase, FrontierCode, GDPval-AA) and `Terminus 2` (older Terminal-Bench 2.1/Hard) — each in an isolated sandbox ([e2b](https://e2b.dev/)).
- **Independent:** AA keeps its own copies of the datasets and runs the evaluations itself, rather than trusting vendor-reported numbers.

## Benchmarks don't tell you everything

- **A benchmark is a sample.** It measures a task family, not your robot code.
- **Harness and settings matter** as much as the model: turn limits, tools and prompts can swing scores.
- **Suites change.** The Intelligence Index swapped several components in v5.0; scores from different versions are not comparable.
- **Saturation and contamination:** older tests (HumanEval, MMLU) are largely saturated, while newer ones (Terminal-Bench 4.0, FrontierCode) resist it better.
- **Cost is part of capability.** AA reports cost and tokens per task next to every score — see the model chart for the price side of the trade-off.

## Links

- **Artificial Analysis — intelligence methodology:** https://artificialanalysis.ai/methodology/intelligence-benchmarking
- **Artificial Analysis — coding agents (Coding Agent Index):** https://artificialanalysis.ai/agents/coding-agents
- **Terminal-Bench 4.0:** https://www.tbench.ai/?version=4
- **FrontierCode (Cognition):** https://cognition.com/blog/frontier-code-2.0
- **SciCode:** https://scicode-bench.github.io/
- **HLE-Diamond:** https://lastexam.ai/blog/hle-diamond
- **AutomationBench (Zapier):** https://zapier.com/benchmarks
- **GDP.pdf (Surge AI):** https://surgehq.ai/benchmarks/gdp-pdf
- **Codex / HumanEval paper:** https://arxiv.org/abs/2107.03374
