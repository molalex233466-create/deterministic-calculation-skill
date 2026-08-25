# deterministic-calculation-skill

A small experimental LLM skill for safer numerical work in ordinary chat.

It is designed for tasks where the language model can understand the problem correctly but a numerical mistake in arithmetic, normalization, scoring, or ordering can invalidate the result.

## Simple use

Attach `SKILL.md` to the chat and give a short instruction such as:

> For all calculations in this chat, use the attached Deterministic Calculation Skill as a mandatory local instruction. Do not generate computed numerical values from the language model alone. If a deterministic calculation mechanism is available, use it. If reliable deterministic calculation is unavailable, stop and report that limitation.

Then send the task normally.

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

The example is intentionally simple: one run without the skill produced an internally inconsistent calculation; the same decision model was later calculated correctly after the skill was attached and deterministic calculation was required.

## Limitation

This is an experimental instruction pattern, not a guarantee that every model or product will expose or use the same calculation backend. In the example run, the assistant stated that it used a deterministic calculation tool; the screenshots do not expose backend tool-call logs.
