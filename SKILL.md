---
name: codex-model-routing
description: Recommend a suitable available Codex Desktop model and reasoning effort for a new task, a material change in scope or risk, or a reported model fallback. Balance task quality against subscription usage and credits while preserving the user's chosen settings and avoiding unnecessary interruptions.
---

# Codex Model Routing

## Purpose

Recommend a model and reasoning effort that meet the task's quality and verification needs. Optimize usage only after protecting correctness and completeness. A recommendation does not change the active chat's settings.

## Establish what is actually available

- Honor the user's explicit model, effort, speed, and quality preferences. Do not silently switch them.
- Use current host capabilities or the actual Desktop picker to establish selectable models and efforts. Tool metadata for creating another chat or a subagent establishes options for that operation, not the active chat's model or picker.
- Report the effective model and effort only when reliable runtime metadata or the UI identifies this chat's settings. A saved configuration, model cache, documentation page, or the assistant's general identity does not prove the active selection.
- If current settings are unknown, say so briefly when relevant and continue authorized work unless a concrete capability gap prevents a reliable result. Do not inspect unrelated chats, logs, or private account files just to identify the model.
- Consult current official Codex documentation when availability or pricing affects a decision. API model availability and prices do not establish Desktop availability or subscription usage. If sources conflict, disclose the uncertainty and use the current host's supported options.

## Choose the quality tier

Classify the cost of an error, ambiguity, task breadth, and available verification. Keep a stronger model when a downgrade could materially compromise the result. Production changes, migrations, authentication, payments, security, destructive operations, unfamiliar code, and hard-to-verify decisions warrant particular care; a small, well-understood change does not automatically require maximum effort.

The following is a dated baseline, checked on **2026-10-27**, not a fixed allowlist. Use only options available to the current account and client. Refresh this baseline when the catalog changes.

| Task profile | Preferred model | Starting effort, if offered |
| --- | --- | --- |
| Exceptionally difficult reasoning, engineering, or research where stronger judgment materially changes the outcome | GPT-6 Astra | High or Very High; Max only with a concrete benefit |
| Complex coding, difficult debugging, serious review, or high-impact decisions | GPT-6.1 Sol | High; Very High or Max when deeper reasoning is useful |
| Normal implementation, research, or analysis requiring several steps | GPT-6.1 Sol | Medium; High when ambiguity warrants it |
| Everyday writing, visual interpretation, or work in supported apps with clear checks | GPT-6.1 Terra | Client default; increase only when planning or analysis warrants it |
| Small, bounded, repeatable work with clear acceptance criteria and inexpensive verification | GPT-6 Luna | Light or Medium |

GPT-6.1 Terra is a distinct option for writing, visual understanding, and computer use; do not replace Sol automatically for complex coding, difficult debugging, or serious review. Prefer Luna for focused, repeatable extraction or transformation when it meets the quality bar.

GPT-6 Sol and the GPT-5.6 Sol, Terra, and Luna models may remain available during rollout. Use them as availability fallbacks or when the user prefers them; compare capability and current usage terms rather than assuming older models save limits. GPT-5.5 retired from Codex with ChatGPT sign-in on October 14, 2026; API-key sessions are a separate case. Do not recommend it as a ChatGPT-sign-in fallback. Do not infer availability of GPT-5.4 or Mini from this older skill's catalog.

A higher effort on a weaker model is not automatically equivalent to a stronger model. Escalate from Sol to Astra when the task's difficulty justifies it, rather than making Astra the universal default.

## Select reasoning effort and speed separately

Use only the effort choices exposed for the selected model on the current surface. On **2026-10-25**, the user reported that their Desktop picker offers `Ultra` / `Ультра` for the models below except both Luna models. That historical screenshot established model names only; Ultra availability came from the user's clarification:

| Model in the Desktop picker | Ultra shown |
| --- | --- |
| GPT-6.1 Sol | Yes |
| GPT-6 Astra | Yes |
| GPT-6 Sol | Yes |
| GPT-6 Luna | No |
| GPT-5.6 Sol | Yes |
| GPT-5.6 Terra | Yes |
| GPT-5.6 Luna | No |

GPT-6.1 Terra was not covered by this historical snapshot. Its Desktop effort choices, including Ultra, remain unverified; inspect the current picker before recommending a specific effort. Availability in chat-creation or subagent tool metadata does not establish the Desktop picker.

This user-reported snapshot covers only Ultra's presence or absence in their picker. Inspect the picker for other effort choices or changed availability; do not infer their per-model availability. Desktop effort labels may include `Light` / `Лёгкий`, `Medium` / `Среднее`, `High` / `Высокое`, `Very High` / `Очень высокое`, `Max` / `Макс.`, and `Ultra` / `Ультра`. Internal values such as `low`, `medium`, `high`, `xhigh`, and `max` belong to runtime/API interfaces; do not assume their UI mapping without evidence.

- Start at Medium for ordinary work and Light for trivial, easily verified work.
- Use High for substantial planning, debugging, implementation, or analysis. Use Very High or Max when additional reasoning is likely to improve the outcome materially.
- Ultra uses subagents, rather than simply increasing a single agent's reasoning budget. Consider it only for substantial work that benefits from independent parallel subtasks, when available and consistent with the user's delegation and usage preferences. Its presence in a picker does not authorize creating separate user-owned chats.
- Effort and speed are distinct controls: **Ultra reasoning is not Ultrafast speed**. Keep the user's speed choice; recommend Standard for economy when no speed preference is given.

As checked on 2026-10-27, Fast consumes included subscription usage at **2.5 times** Standard, but purchased credits and Enterprise pay-as-you-go usage at **2 times** Standard. Fast supports GPT-6.1 Terra where offered. Ultrafast supports Astra and GPT-6.1 Sol on eligible plans, using **8 times** included usage or **6 times** paid credits. Do not infer Ultrafast support for Terra from its Fast support. Verify current eligibility and multipliers before recommending a speed change.

## Evaluate economy with the right evidence

Distinguish included subscription usage, purchased ChatGPT credits, and API-key billing. Credit rates alone do not determine included task counts. Context, reasoning, caching, tools, and retries affect task consumption.

When a user asks about remaining limits, use the available usage tool or dashboard. `usedPercent` is consumed usage; remaining is `100 - usedPercent`, clamped to zero through 100. Missing values are unknown. Do not infer the user's plan, exact message allowance, or reset time from generic examples.

For credit comparisons, this Standard-speed snapshot was checked on **2026-10-27** against [Codex pricing](https://learn.chatgpt.com/docs/pricing):

| Model | Input credits per million tokens | Cached input | Output |
| --- | --- | --- | --- |
| GPT-6 Astra | 250 | 25 | 1,250 |
| GPT-6.1 Sol | 50 | 2.5 | 250 |
| GPT-6.1 Terra | 25 | 1.25 | 125 |
| GPT-6 Sol | 50 | 5 | 250 |
| GPT-6 Luna | 2.5 | 0.25 | 12.5 |

At these Standard credit rates, GPT-6.1 Terra costs half as much per token as GPT-6.1 Sol in each listed category. This does not establish half the included subscription usage or half the total task cost.

Refresh rates when economy affects the recommendation; do not present this snapshot as a perpetual rate card or derive exact task costs from it. Do not consume a usage reset, buy credits, or change a subscription without explicit authorization.

## Communicate without blocking routine work

At the start of a genuinely new task, give one brief recommendation in the user's language, with the relevant reason. Include an economy alternative only when useful. For example:

> Рекомендация: GPT-6.1 Sol + High — задача требует анализа связанных компонентов. Текущие модель и effort не подтверждены; это рекомендация, настройки чата не менялись.

Proceed with authorized work when the current setting is adequate or no concrete limitation is evident. Do not require a switch or confirmation just because the recommendation differs, settings are unknown, or a new task starts. Re-evaluate when scope or risk materially changes, without repeating the announcement on every follow-up.

Use a native model/effort control only when available and the change is authorized; verify its result before claiming success. Otherwise, when a switch is needed or requested, point to the Desktop picker or `/model` and `/reasoning` if available. Editing configuration defaults does not prove that an already-open chat switched.

For a reported rate-limit fallback, disclose it when relevant and reassess the remaining work. Continue bounded work if verification still supports a reliable result. Pause only the steps that require unavailable capability or a user decision about a material quality or cost tradeoff; continue independent safe work. Never claim a fallback is equivalent merely because the user accepts it.

At completion, focus on the result and verification. Mention the effective model or a fallback only when known and useful or explicitly requested. Do not invent a next task or end with an automatic question about switching models.

## Official references

- [Codex and Work models](https://learn.chatgpt.com/docs/models) — product recommendations, availability, retirement, and Ultra behavior.
- [Codex pricing and usage](https://learn.chatgpt.com/docs/pricing) — subscription limits and credit rates.
- [Speed modes](https://learn.chatgpt.com/docs/agent-configuration/speed) — Fast and Ultrafast eligibility and billing.
- [Desktop slash commands](https://learn.chatgpt.com/docs/reference/slash-commands) — current chat controls.
- [OpenAI API model catalog](https://developers.openai.com/api/docs/models) — API models only; not proof of Desktop availability.
