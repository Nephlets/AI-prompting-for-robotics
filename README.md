# Prompting AI for Java — FRC Robotics Research Report

**Who this is for:** A 5-person programming team on an FRC robotics team. Nobody on the team knows how to code yet, and nobody has prompted an AI to write code before.
**What we use:** DeepSeek V4 Flash through OpenRouter, inside the Kilo Code extension for VS Code.
**What we're writing:** Java (WPILibJ) for FRC robots.

This is a research report, not a tutorial. It explains what the reliable sources say about getting good Java out of an AI, and translates that for a team starting from zero.

---

## The short version

If you read nothing else, these are the findings that matter:

1. **Be specific, not polite.** Vague questions get wrong code. Say the file, the class, the method, what's broken, and what "fixed" looks like. ([Anthropic](#sources), [OpenAI](#sources))
2. **Give the prompt structure.** Use sections — role, task, rules, examples, context — instead of one run-on sentence. This is the single biggest improvement a beginner can make. ([OpenAI](#sources))
3. **Give the AI the real WPILib information.** AI models happily invent FRC methods that don't exist. You must paste the actual documentation or link it. ([WPILib — What is WPILib?](#sources))
4. **Make the AI check its own work.** Give it something that returns pass/fail — mostly, the build. Otherwise "looks done" is all you get. ([Anthropic](#sources))
5. **Show an example instead of describing one.** Two real examples of the style you want beat a paragraph of explanation. ([OpenAI](#sources), [DAIR](#sources))
6. **A first draft is not a finished robot program.** A human who can run the code must review it. This is the biggest risk for a team that can't yet read code — see [Failure modes](#failure-modes).
7. **DeepSeek specifics:** turn thinking mode on, set a system prompt, and keep one task per session. ([DeepSeek](#sources))

---

## Why normal prompting advice isn't enough for us

Three things make our situation different:

- **We're at true zero.** We can't yet tell correct Java from incorrect Java. Research on AI code writing ([Codex paper](#sources)) found the model makes errors that *look* fine but are wrong. We can't catch those by reading — we have to **run** the code.
- **WPILib is a niche library.** AI knows general Java far better than `edu.wpi.first.wpilibj2.command`. WPILib deliberately keeps class and method names identical across languages ([WPILib — What is WPILib?](#sources)), so the names must be exact. **Invented methods are the number-one failure mode.**
- **Kilo Code is an agent, not just a chat box.** It can read our project and edit files. So the useful thing is to tell it what it *can't* figure out by itself (our hardware, our team rules, what "done" means) — not to re-describe code it can already see. ([Anthropic](#sources))

---

## What the sources actually say

### Core principles (apply to any AI)

**OpenAI — Prompt Engineering guide** ([OpenAI](#sources))
This is the most directly useful source, because DeepSeek's API is built to match OpenAI's. Main points:
- Use a **system/developer instruction** for high-level behavior; it takes priority over the normal message.
- Build that instruction in order: **Identity → Instructions → Examples → Context.**
- Use **headings and lists** for structure, and **XML tags** to mark where pasted data starts and ends.
- **Few-shot examples:** give a few input/output examples rather than describing the pattern.
- **Include relevant context** (docs, code) so the model uses facts it wasn't trained on — exactly what we need for WPILib.
- Coding-specific: define the AI's role, require testing, and remember tools may say "done" even when they failed — so you check.
- Give **precise, explicit instructions.** Models like this behave like a "junior coworker" — explicit steps beat vague goals.

**Anthropic — Claude Code best practices** ([Anthropic](#sources))
Written for a coding agent, so it maps almost one-to-one onto Kilo Code:
- **Tell it what it can't see.** Only write down what it can't find by reading the project (team decisions, hardware, process). Don't re-describe the file layout.
- **Write a specific prompt.** The doc's own example: instead of *"fix the login bug"* write *"users report login fails after the session times out. look at token refresh in src/auth/, write a failing test that reproduces it, then fix it."*
- **Give the agent a check it can run** that returns pass/fail — a test, a build, a linter.
- **Ask for evidence:** the command it ran and the output, not just "it works."
- For long or unsupervised work: give it a **goal**, a way to **check itself**, limits on **what it may touch**, and a **human sign-off** at the end.
- Note: older habits like "think step by step" and ALL-CAPS emphasis matter far less with current models. The real control is the **effort** setting, not magic words.

**DAIR.AI — Prompt Engineering Guide** ([DAIR](#sources))
The standard reference guide. Techniques we can use:
- **Zero-shot** (just ask) vs **few-shot** (give examples) — start simple, add examples when the answer is wrong.
- **Chain-of-Thought** — ask it to reason step by step for logic problems (e.g. "explain the intake states before writing them").
- **Prompt chaining** — break one big job into a series of small prompts. Safest pattern for beginners.
- **RAG (retrieval-augmented generation)** — feed it the real docs. Directly useful for WPILib.
- **ReAct** — reason and act (read docs, then code) — relevant to agent mode.

### Java-specific findings

The guides above are language-agnostic. For Java, combined with the Java and WPILib docs:

- **Java is verbose and strictly typed — that's a gift.** The compiler catches a huge class of AI mistakes. So the most valuable "check to run" ([Anthropic](#sources)) is the **WPILib build task**. If it compiles, many hallucinations are already caught.
- **Always ask for imports and the package line.** Java code without correct imports doesn't compile.
- **Ask for the supported style.** WPILib recommends **Command-Based programming** for new teams ([WPILib — Creating a Robot Program](#sources), [WPILib — Command-Based](#sources)). Left alone, the AI may write the discouraged procedural style or a bare `main()`.
- **Pin the API version.** WPILib changes every season and old methods get removed. Always name the season (e.g. **2026**) and point the AI at the matching docs: `https://docs.wpilib.org/en/stable/` and the Java API index `https://github.wpilib.org/allwpilib/docs/release/java/`.
- **The WPILib templates are the ground truth for structure.** Tell the AI to follow the `TimedRobot` / Command Robot template shape ([WPILib — Creating a Robot Program](#sources)). The compiler and our mentors — not the AI — decide what's right.

### What the code-generation research warns about

**Codex / HumanEval paper** ([Codex paper](#sources)) — the foundational study of AI writing code:
- The base model solved only **28.8%** of problems in one try; repeated sampling with 100 attempts reached 70.2%. **Translation: one-shot output is often wrong, but re-prompting often fixes it.**
- Known weaknesses: "long chains of operations" and binding operations to variables — i.e. **multi-step robot logic is exactly the hard case.**
- **So: expect to iterate.** A rejected answer is normal, not a failure.

### DeepSeek and Kilo Code specifics

**DeepSeek API docs** ([DeepSeek](#sources)) — since we use DeepSeek Flash through OpenRouter:
- The current model name is `deepseek-flash` (now serving DeepSeek-V4.1-Flash-1017). Old names like `deepseek-v4-flash` still work but are retired. **In OpenRouter, pick the matching model — don't type an old name by hand.**
- DeepSeek has a **thinking** mode and a **`reasoning_effort`** setting (e.g. `high`). For robot logic that's easy to get subtly wrong, **turn thinking on and use high effort**; for trivial renames, leave it off to save time.
- It supports a **system prompt** that takes priority — this is where team rules belong ("always use Command-Based; always include imports; target WPILib 2026").
- DeepSeek is designed to sit behind agent tools like Claude Code / OpenCode ([DeepSeek](#sources)) — the same pattern as using it inside Kilo Code.

**Kilo Code (our extension):**
- Kilo can read our project, so put **team-only, non-obvious facts** in a project instruction file rather than retyping them every prompt.
- Use **Plan/Ask mode** to design before **Code mode** writes. This is the "write a spec first, then build" pattern ([Anthropic](#sources)) and the safest workflow for people who can't yet read code.
- **Use the diff/Changes pane** to see exactly what it changed before accepting, and **run the build** as the check.

---

## The rules (one line each)

Combined from everything above. These are findings, not a step-by-step guide.

1. **Give a role and a target** — "You are helping an FRC team write WPILib **Java**, Command-Based, for the **2026** season."
2. **Be specific** — name the file, class, method, inputs, outputs, and the symptom.
3. **Structure the prompt** — Identity → Task → Rules → Examples → Context, with headings and XML tags around pasted code.
4. **Supply the real WPILib facts** — paste the doc excerpt or link the exact version. Never assume it knows the API.
5. **Show, don't tell** — paste a working example and say "follow this pattern."
6. **One task per request** — break big features into a chain of small prompts; multi-step logic is the weak spot.
7. **Demand the check** — "include all imports and the package, then tell me the build command and what success looks like." Then actually run it.
8. **Ask it to reason first for logic** — "explain the states in plain English, wait for my OK, then code."
9. **Require evidence and iterate** — ask for the command and its output. If wrong, paste the real error. Wrong twice? Rewrite the prompt or start a fresh session.
10. **Stay in the supported lane** — push it to the WPILib templates and Command-Based design; forbid reinventing `main()`.
11. **Configure the model** — DeepSeek: thinking on + high effort for logic, off for trivia; set a system prompt with team rules.
12. **Keep a human in the loop** — nothing is accepted until a person builds it and watches the robot behave.

---

## Failure modes to expect

| What goes wrong | Why | The fix |
|---|---|---|
| Invented WPILib methods/classes | Niche API, weak training data | Rule 4 — paste the docs / link the version |
| Wrong style (procedural not Command-Based) | Model defaults to generic Java | Rules 1, 10 — state the paradigm |
| Won't compile (missing imports/package) | Java boilerplate | Rules 3, 7 — demand imports + build check |
| "Looks done" but is wrong | No runnable check | Rules 7, 9 — give a check, require output |
| Multi-step logic subtly wrong | Documented limitation (Codex) | Rules 6, 8 — chain + reason first |
| Deprecated/removed API methods | New WPILib every season | Rule 2 — pin the season/version |
| Confident but wrong answers to beginners | We can't judge the answer | Rule 12 — human runs the robot |
| Endless corrections in one session | Bad context piles up | Rule 9 — restart after 2 failures |

---

## Beginner guardrails

For a team that can't yet read code:

1. **Never accept code you haven't built.** The build is the only objective check we have.
2. **Always run it in simulation** before the real robot (WPILib supports desktop/simulator builds — [WPILib — Creating a Robot Program](#sources)).
3. **One change at a time**, then build and test.
4. **Keep prompts and their outcomes in a shared doc** so the team stops re-deriving the same fact.
5. **Use Plan mode to understand, Code mode to implement** — never let the agent decide scope we can't evaluate.

---

## Open questions for the team

These need deciding before anyone writes a workflow:

- **Who owns the WPILib-version pin** and the docs link the prompts cite?
- **What is "done" for a task** — does it compile? Does it run in sim? Does it work on the robot?
- **Where do team rules live** so every member's prompts inherit them?
- **DeepSeek thinking-mode cost/time** at our OpenRouter budget — always high effort, or only for logic?

---

## Sources

Each source has a short name (how it's cited above) and its link.

- **OpenAI** — *Prompt Engineering guide*: https://platform.openai.com/docs/guides/prompt-engineering
  Roles, prompt structure, few-shot, context, coding guidance, message format.
- **Anthropic** — *Best practices for Claude Code*: https://code.claude.com/docs/en/best-practices
  Specific prompts, checks to run, evidence, unattended-run checklist, what's now obsolete.
- **DeepSeek** — *API docs (Your First API Call)*: https://api-docs.deepseek.com/
  Model names, thinking mode, `reasoning_effort`, system prompt, agent integrations.
- **WPILib — What is WPILib?**: https://docs.wpilib.org/en/stable/docs/software/what-is-wpilib.html
  Java chosen for new users; exact API names; doc/source links.
- **WPILib — Creating a Robot Program**: https://docs.wpilib.org/en/stable/docs/software/vscode-overview/creating-robot-program.html
  Base classes, templates, Command Robot recommendation.
- **WPILib — Command-Based**: https://docs.wpilib.org/en/stable/docs/software/commandbased/what-is-command-based.html
  The recommended programming style.
- **WPILib Java API reference**: https://github.wpilib.org/allwpilib/docs/release/java/
- **DAIR** — *Prompt Engineering Guide (Techniques)*: https://www.promptingguide.ai/techniques
  Zero-shot, few-shot, chain-of-thought, prompt chaining, RAG, ReAct.
- **Codex paper** — Chen et al., *Evaluating Large Language Models Trained on Code*, arXiv:2107.03374: https://arxiv.org/abs/2107.03374
  The 28.8% one-shot figure and the documented limitations; repeated-sampling strategy.
