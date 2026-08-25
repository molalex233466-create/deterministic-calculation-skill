# Deterministic Calculation Skill

Version: v0.1  
Status: experimental

## Purpose

Use this skill when a task requires arithmetic, normalization, scoring, ranking, aggregation, or other numerical calculations where a wrong intermediate value can change the final result.

The goal is simple: **do not generate computed numerical values from the language model alone when a deterministic calculation mechanism is available.**

## Rules

1. **Use a deterministic calculation mechanism for computed values.**
   - Use an available calculator, code execution tool, spreadsheet engine, or other deterministic numerical tool.
   - Do not rely on language-model arithmetic for non-trivial calculations.

2. **Do not invent missing calculation rules.**
   - Before calculating, identify formulas, units, directions, normalization rules, weights, ranges, tie rules, and other decision-changing assumptions that are required.
   - If a required rule is materially missing, stop the calculation and request that rule.

3. **Preserve source values.**
   - Keep source units, signs, scales, and precision unless an explicit conversion is required.
   - Do not silently replace or “clean up” source numbers.

4. **Show a calculation trace.**
   For every material calculated result, expose enough information to reproduce it:
   - formula;
   - input values;
   - intermediate values when they affect the result;
   - final calculated value.

5. **Separate raw values from normalized or weighted values.**
   - Do not mix source values, normalized scores, weights, and weighted contributions.
   - Label each layer clearly.

6. **Validate the result after calculation.**
   Check at least:
   - ranking order versus final scores;
   - ties and tie rules;
   - boundary conditions;
   - obvious range or sign errors;
   - double counting of calculated components.

7. **Do not fabricate a numerical result when deterministic calculation is unavailable.**
   - If the task cannot be calculated reliably with an available deterministic mechanism, stop and state that limitation.
   - Do not produce a guessed ranking, score, or “optimal” result.

## Output expectation

When calculations are performed, return:

- calculation method;
- formulas and inputs;
- calculated intermediate values needed for verification;
- final values or ranking;
- validation result;
- any unresolved numerical limitations.

## Scope

This skill controls **how calculations are executed and checked**. It does not define the domain model, criteria, weights, formulas, or decision rules unless those are explicitly supplied by the user or another governing instruction.
