---
name: codex-model-routing
description: Choose and communicate the most suitable Codex Desktop model and reasoning effort for each new coding, research, review, debugging, or file-editing task, balancing quality against ChatGPT usage limits and credits. Use at the start of every new task, when a task materially changes scope or risk, and when Codex reports a rate-limit fallback or model change.
---

# Codex Model Routing

## Purpose

Select a model and reasoning effort before substantive work begins. Preserve quality whenever a cheaper setting could materially increase the chance of an incorrect, incomplete, unsafe, or hard-to-review result. Treat limit and credit savings as a secondary objective.

Use the model picker and `/reasoning` controls for the current Desktop chat when they are available. Do not claim that a model or effort changed unless the runtime or UI visibly confirms it.

## Workflow

### 1. Classify the request

Before acting, determine:

- Whether this is a new task or a continuation of the current deliverable.
- The cost of a wrong answer: low, moderate, high, or irreversible.
- The task shape: simple edit, routine implementation, multi-file engineering, difficult debugging, research, code review, security, migration, or other high-stakes work.
- Whether the user explicitly pinned a model, effort, speed, or quality preference. Honor an explicit choice unless the selected setting is unavailable; explain any limitation.
- Whether the task is clearly safe to run on a lower-cost setting without weakening the acceptance criteria.

Treat production changes, data migrations, authentication or payments, privacy-sensitive work, security reviews, destructive operations, public-facing deliverables, large refactors, unfamiliar repositories, and ambiguous high-impact decisions as quality-first tasks.

### 2. Choose the conservative quality tier

Use only models available in the user's current Codex Desktop picker. As of 2026-09-05, the known choices include:

- GPT-6 Astra
- GPT-5.6 Sol
- GPT-5.6 Terra
- GPT-5.6 Luna
- GPT-5.5
- GPT-5.4
- GPT-5.4 Mini

Use GPT-6 Astra selectively for the hardest end-to-end work where a marginal quality gain materially affects the outcome. OpenAI describes it as more capable than GPT-5.6 Sol for complex reasoning, software engineering, browsing, computer use, research, and professional work. Do not make Astra the universal default: it consumes included usage and credits substantially faster than Sol, even though its token efficiency can reduce total work on some difficult tasks.

Use GPT-5.6 Sol as the normal quality-first model, Terra for the everyday quality/limit balance, and Luna for bounded cost-sensitive work. Treat GPT-5.5 and GPT-5.4 as compatibility or availability fallbacks, not automatic economy choices; an older model is not necessarily cheaper against subscription limits. Use GPT-5.4 Mini only for clearly simple, low-risk work when its lower capability still meets the quality bar.

| Task profile | First choice | Effort | Economy rule |
| --- | --- | --- | --- |
| Exceptionally difficult end-to-end work where the best available judgment materially changes the outcome | GPT-6 Astra | High or Very High; Max or Ultra only with clear benefit | Accept higher limit use because quality takes priority |
| High-impact, irreversible, security-sensitive, or very difficult | GPT-5.6 Sol | Very High or Max; Ultra only when justified | Escalate to Astra when Sol creates a material quality risk |
| Complex coding, broad refactor, difficult debugging, or serious review | GPT-5.6 Sol | High or Very High | Compare Terra only when the quality bar can still be met |
| Normal multi-step implementation, research, or analysis | GPT-5.6 Terra | Medium or High | Use Sol when correctness or ambiguity matters more than limits |
| Small, bounded, low-risk edit or explanation | GPT-5.6 Luna | Light or Medium | Move to Terra if verification or judgment becomes nontrivial |
| Repetitive, trivial, and easily verified work | GPT-5.4 Mini | Light or the lowest available adequate effort | Use only when the subscription-limit saving is real and quality remains adequate |

Use a lower model only when the task is bounded, the acceptance criteria are clear, and the likely quality loss is immaterial. A higher effort on a weaker model is not automatically equivalent to a stronger model. When uncertain, keep the stronger model and reduce economy claims.

Do not recommend a model outside the seven known Desktop choices unless the picker changes. Availability can roll out by plan and account. If Astra or another recommended model is absent, choose the closest visible option and disclose the substitution.

Use these current limit and credit signals when economy matters:

- Plus local-message estimates per five-hour period: Astra 5 to 45, Sol 10 to 100, Terra 25 to 200, Luna 250 to 2,000. These are estimates, not fixed message caps.
- Credit rates per one million input/output tokens: Astra 250/1,250, Sol 100/500, Terra 50/300, Luna 5/30.
- Astra therefore costs about 2.5 times Sol per token. Do not infer exact per-task consumption because context, reasoning, tools, caching, and model token efficiency also affect usage.
- Keep Desktop speed at Standard unless latency matters enough to justify extra credits. Fast mode for Astra consumes credits at 2.5 times its Standard rate where available.

### 3. Select reasoning effort

Use the exact effort labels exposed by the Desktop UI:

- `Light` / `Лёгкий`: trivial, bounded, easily verified tasks.
- `Medium` / `Среднее`: the default balance for normal agentic coding, research, planning, and multi-step work.
- `High` / `Высокое`: complex debugging, planning, coding, and high-value work.
- `Very High` / `Очень высокое`: deep research, security, code review, long-running tasks, and unusually challenging engineering.
- `Max` / `Макс.`: the hardest quality-first tasks where deeper reasoning is likely to produce a material gain.
- `Ultra` / `Ультра`: the most limit-intensive mode shown by Desktop. Use only when the task is exceptionally difficult, maximum quality justifies faster limit consumption, and the user accepts that tradeoff.

The confirmed availability is:

| Model | Confirmed effort choices |
| --- | --- |
| GPT-6 Astra | Light, Medium, High, Very High, Max; use Ultra only if the current Desktop picker exposes it |
| GPT-5.6 Luna | Light, Medium, High, Very High, Max |
| GPT-5.6 Terra | Light, Medium, High, Very High, Max, Ultra |
| GPT-5.6 Sol | Light, Medium, High, Very High, Max, Ultra |

The screenshots do not establish the effort menus for GPT-5.5, GPT-5.4, or GPT-5.4 Mini. Inspect the actual picker before recommending a specific effort for those models; do not copy the Sol or Terra effort list by assumption.

Do not choose Very High, Max, or Ultra merely because the label sounds safer. Use them when additional reasoning is likely to improve the result or verification. Conversely, do not lower effort just to save credits when the acceptance criteria require deeper reasoning.

### 4. Announce the recommendation before starting

State the recommendation briefly before making substantive changes:

> Рекомендация перед началом: `<model> + <effort>`. Причина: `<task-risk and task-shape>`. Экономичный вариант: `<alternative>`, только если качество останется достаточным.

Also state whether the current model and effort are known. If the recommendation differs from the current setting, or the current setting is not visible and the distinction matters, stop before substantive work and ask the user to switch using `/model` and/or `/reasoning`.

If a native runtime action for changing the current model or effort is exposed, use it, then verify the result. Otherwise, ask the user to make the change in the picker. Never change a user's explicit selection silently and never pretend that editing a config file changed the already-open chat; configuration defaults may apply only to new threads.

If the current setting is adequate and the user has already accepted it for this task, proceed without an unnecessary confirmation loop.

### 5. Handle availability and fallbacks

When the recommended model is missing from the picker, choose the closest available model by capability and disclose the substitution. Do not use a deprecated model merely because its name is familiar.

When Codex reports a rate-limit or automatic fallback:

- For a low-risk, bounded task, explain the fallback and ask whether to continue if the user has not already allowed it.
- For a quality-first or high-impact task, pause and ask whether to restore the recommended setting or accept the lower-quality risk.
- Do not describe a fallback as equivalent to the original model unless the user has explicitly accepted that tradeoff.

### 6. Close the task and manage the next one

At completion, record the effective model and effort when known, the quality-sensitive reason for the choice, and any fallback that occurred. Before beginning a genuinely new task, ask the user whether to continue with the current setting or switch to the new recommendation.

Use a compact handoff such as:

> Задача завершена на `<model> + <effort>`. Следующая задача выглядит как `<profile>`; рекомендую `<new model> + <new effort>`. Продолжать на текущих настройках или переключить?

Do not ask to switch when the user is merely continuing the same deliverable, answering a follow-up, fixing a discovered regression, or requesting a verification pass that depends on the current context. Re-evaluate and ask again if the risk or scope materially increases.

## Quality and economy guardrails

- Optimize first for task success, correctness, safety, and verifiability; optimize limits and credits only after that bar is protected.
- Prefer a lower-cost recommendation only when the task is clearly low-risk and bounded.
- If the user rejects a suggested downgrade, continue with the user's chosen setting without repeatedly arguing for economy.
- If model availability, rate-limit behavior, or effort labels are uncertain, say so and consult current official OpenAI documentation when browsing is available.
- Keep API model names, Desktop picker labels, and effective fallback behavior distinct; do not infer one from another without evidence.

## Official references

Consult these sources when the model catalog or UI changes:

- [OpenAI model catalog](https://developers.openai.com/api/docs/models)
- [GPT-6 Astra model page](https://developers.openai.com/api/docs/models/gpt-6-astra)
- [OpenAI model guidance](https://developers.openai.com/api/docs/guides/latest-model)
- [Reasoning models and effort guidance](https://developers.openai.com/api/docs/guides/reasoning)
- [Codex pricing and usage limits](https://learn.chatgpt.com/docs/pricing)
- [Codex speed and Fast mode](https://learn.chatgpt.com/docs/agent-configuration/speed)
- [Codex Desktop slash commands](https://learn.chatgpt.com/docs/reference/slash-commands)
- [Codex configuration reference](https://learn.chatgpt.com/docs/config-file/config-reference)
