# deterministic-calculation-skill

A small experimental LLM skill for safer numerical work in ordinary chat.

It is designed for tasks where the language model can understand the problem correctly but a numerical mistake in arithmetic, normalization, scoring, or ordering can invalidate the result.

## Use in ChatGPT Work / Skills

If your ChatGPT account exposes **Skills**, the file can be installed as a native skill:

1. Download `SKILL.md`.
2. Open **Plugins → Skills**.
3. Select **+ → Upload from computer**.
4. Upload `SKILL.md`.
5. In ChatGPT Work, select the installed skill when needed, for example from the `@` skill list when that option is available.

In the tested ChatGPT Work setup, the uploaded skill was installed successfully and was available for explicit use. Interface details and feature availability may vary by account and product configuration.

## Use in ordinary Chat / ChatGPT Free

If native skill installation is unavailable, attach `SKILL.md` directly to the chat and give a short instruction such as:

> For all calculations in this chat, use the attached Deterministic Calculation Skill as a mandatory local instruction. Do not generate computed numerical values from the language model alone. If a deterministic calculation mechanism is available, use it. If reliable deterministic calculation is unavailable, stop and report that limitation.

Then send the task normally.

In this mode, `SKILL.md` is used as an attached instruction file; it is not installed as a persistent native skill.

No separate coding environment is required just to **attach and invoke the skill as an instruction file**. Whether the chat product actually provides a deterministic calculation mechanism is platform-dependent.

## What the skill does

It requires the assistant to:

- use deterministic calculation when available;
- stop when calculation-changing rules are missing;
- expose formulas, inputs, and intermediate values;
- keep raw, normalized, and weighted values separate;
- validate the final ordering and numerical result;
- avoid fabricating a result when reliable calculation is unavailable.

## Example

See [`Example_CHAT_FREE_MCDA.md`](Example_CHAT_FREE_MCDA.md).

The example is intentionally simple: one run without the skill produced an internally inconsistent calculation. After the skill was attached and deterministic calculation was required, the same decision model produced a final score and ranking that matched an independent arithmetic check.

The detailed example also records a limitation: one displayed intermediate value in the skill-assisted trace was not fully consistent with the stated formula, even though the independently checked final score and final ordering were correct.

## Limitation

This is an experimental instruction pattern, not a guarantee that every model, account, or product will expose or use the same calculation backend.

In the ChatGPT Free example, the assistant stated that it used a deterministic calculation mechanism, but the screenshots do not expose backend tool-call logs. The example therefore demonstrates an observed improvement in calculation discipline and final-result reliability, not a guarantee that every displayed intermediate value or every future run will be error-free.
