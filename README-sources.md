# Sources — everything the four guides are built on

These are all the sources behind the repo's four guides, condensed into one place. Each entry says what we took from it, and which guide uses it.

Guides: [README.md](README.md) (how to prompt) · [README-coding-models.md](README-coding-models.md) (model chart) · [README-v4-vs-v4.1-flash.md](README-v4-vs-v4.1-flash.md) (DeepSeek comparison) · [README-benchmarks-explained.md](README-benchmarks-explained.md) (benchmarks explained).

*Snapshot: 2026-10-29. Links can move; the notes record what each source contributed at the time.*

## Prompting and working with AI

- **OpenAI — Prompt Engineering guide** — https://platform.openai.com/docs/guides/prompt-engineering — Roles and a structured prompt (identity → instructions → examples → context), few-shot examples, XML tags, and supplying context. *(Prompting guide)*
- **Anthropic — Best practices for Claude Code** — https://code.claude.com/docs/en/best-practices — Writing specific prompts, giving the agent a check it can run, asking for evidence, the unattended-run checklist, and which older habits are now obsolete. *(Prompting guide)*
- **DAIR.AI — Prompt Engineering Guide (techniques)** — https://www.promptingguide.ai/techniques — Zero-shot vs few-shot, chain-of-thought, prompt chaining, RAG, ReAct. *(Prompting guide)*
- **Codex paper (Chen et al., 2021)** — https://arxiv.org/abs/2107.03374 — The 28.8% one-shot HumanEval figure, the documented limitations, and the repeated-sampling idea; also the origin of the HumanEval benchmark. *(Prompting guide, Benchmarks)*

## FRC and WPILib

- **WPILib docs (stable)** — https://docs.wpilib.org/en/stable/ — The docs root we tell you to cite in prompts so the model uses the current season's API. *(Prompting guide)*
- **WPILib — What is WPILib?** — https://docs.wpilib.org/en/stable/docs/software/what-is-wpilib.html — Why Java is chosen for new users, and that API names are identical across languages. *(Prompting guide)*
- **WPILib — Creating a Robot Program** — https://docs.wpilib.org/en/stable/docs/software/vscode-overview/creating-robot-program.html — Base classes, the project templates, and the Command Robot recommendation. *(Prompting guide)*
- **WPILib — What Is Command-Based Programming?** — https://docs.wpilib.org/en/stable/docs/software/commandbased/what-is-command-based.html — The recommended programming style for new teams. *(Prompting guide)*
- **WPILib Java API reference** — https://github.wpilib.org/allwpilib/docs/release/java/ — The exact class and method names to cite in prompts. *(Prompting guide)*

## DeepSeek models and OpenRouter pricing

- **DeepSeek API docs** — https://api-docs.deepseek.com/ — Model names and aliases, thinking mode, `reasoning_effort`, system prompts, and agent integrations. *(Prompting guide, Model chart, DeepSeek comparison)*
- **OpenRouter — models & prices** — https://openrouter.ai/models — The list prices behind every row of the chart and the blended-price maths. *(Model chart)*
- **OpenRouter — rankings** — https://openrouter.ai/rankings — Weekly token usage, e.g. that DeepSeek V4.1 Flash 1017 is the most-used model. *(Model chart)*
- **OpenRouter — DeepSeek V4 Flash 0731** — https://openrouter.ai/deepseek/deepseek-v4-flash-0731 — The exact model ID and price for the team's current model. *(DeepSeek comparison)*
- **OpenRouter — DeepSeek V4.1 Flash 1017** — https://openrouter.ai/deepseek/deepseek-v4.1-flash-1017 — The exact model ID and price for the recommended upgrade. *(DeepSeek comparison)*

## Artificial Analysis (scores, prices, benchmarks)

- **AA — Coding Agent Benchmarks** — https://artificialanalysis.ai/agents/coding-agents — The Coding Agent Index (an equal-weight average of FrontierCode v1.1, Terminal-Bench 4.0 and SWE-Atlas-QnA-AA) and each component's task count. *(Model chart, Benchmarks)*
- **AA — model page: DeepSeek V4 Flash 0731** — https://artificialanalysis.ai/models/deepseek-v4-flash — Terminal-Bench 4.0 score, speed, model size, and the deprecation notice. *(Model chart, DeepSeek comparison)*
- **AA — model page: DeepSeek V4.1 Flash 1017** — https://artificialanalysis.ai/models/deepseek-v4-1-flash-1017 — Intelligence Index 32, Terminal-Bench 33.8%, FrontierCode 43.7%, speed and size. *(DeepSeek comparison)*
- **AA — Intelligence Benchmarking methodology** — https://artificialanalysis.ai/methodology/intelligence-benchmarking — Every benchmark definition, the Intelligence Index weights, the general testing parameters (temperature, retries, pass@1) and the version history. *(Benchmarks)*

## Benchmark primary sources

- **Terminal-Bench 4.0** — https://www.tbench.ai/?version=4 — The 66-task set and the public leaderboard. *(Benchmarks)*
- **Terminal-Bench dataset** — https://github.com/harbor-framework/terminal-bench — The task repository behind the harness. *(Benchmarks)*
- **Terminal-Bench paper** — https://arxiv.org/abs/2601.11868 — How the task suite and its verifiers are built. *(Benchmarks)*
- **Cognition — FrontierCode 2.0** — https://cognition.com/blog/frontier-code-2.0 — What the benchmark is and how merge-worthiness is graded. *(Benchmarks)*
- **Cognition — FrontierCode 1.1** — https://cognition.com/blog/frontier-code-1.1 — The version used in the Coding Agent Index. *(Benchmarks)*
- **SWE-Atlas-QnA-AA** — https://huggingface.co/datasets/ArtificialAnalysis/SWE-Atlas-QnA-AA — The dataset and grading behind the repository-Q&A component. *(Benchmarks)*
- **SciCode** — https://scicode-bench.github.io/ — The 288-sub-problem scientific-coding benchmark. *(Benchmarks)*
- **SciCode paper** — https://arxiv.org/abs/2407.13168 — How the problems and step-by-step grading work. *(Benchmarks)*
- **Zapier — AutomationBench** — https://zapier.com/benchmarks — The SaaS-workflow benchmark AA runs as AutomationBench-AA. *(Benchmarks)*
- **Surge AI — GDP.pdf** — https://surgehq.ai/benchmarks/gdp-pdf — The long-professional-document benchmark behind AA's GDP.pdf. *(Benchmarks)*
- **HLE-Diamond** — https://lastexam.ai/blog/hle-diamond — The refined 1,000-question Humanity's Last Exam set. *(Benchmarks)*
- **CritPt** — https://critpt.com/ — The research-level physics benchmark. *(Benchmarks)*
- **Terminal-Bench-Science** — https://terminal-bench-science.ai/ — The expert-curated scientific terminal benchmark. *(Benchmarks)*

## Model weights and tooling

- **Hugging Face — DeepSeek V4 Flash 0731 weights** — https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731 — The open weights for the team's current model. *(DeepSeek comparison)*
- **Hugging Face — DeepSeek V4.1 Flash 1017 weights** — https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash-1017 — The open weights for the recommended upgrade. *(DeepSeek comparison)*
- **e2b** — https://e2b.dev/ — The sandbox provider Artificial Analysis uses for its agentic benchmarks. *(Benchmarks)*
