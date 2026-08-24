# Deterministic Calculation Skill

`DETERMINISTIC_CALCULATION_SKILL` is a reusable instruction set for LLM-assisted workflows that contain numeric calculations.

Core rule:

```text
LLM_WRITES_TEXT=yes
LLM_AS_NUMERIC_SOURCE=no
CALCULATION_DELEGATION_REQUIRED=when_numeric_result_requires_calculation
```

The model may explain, structure, and validate a calculation, but computed numeric results should come from a deterministic calculation mechanism whenever one is available: calculator, Python/code execution, spreadsheet formulas, or another formal numeric engine.

## Why this exists

Large language models can produce internally inconsistent numeric tables even when the governing formulas are stated correctly. A visible formula is therefore not sufficient evidence that all derived values were actually computed from it.

The skill separates two responsibilities:

1. **LLM layer** — interpret the task, select the confirmed formula, explain assumptions, and present the result.
2. **Calculation layer** — produce numeric values deterministically and reproducibly.

## When to use

Use the skill for arithmetic, percentages, ratios, engineering formulas, conversions, tabular calculations, normalized scores, weighted sums, rankings, min/max checks, and any other value that must be computed rather than generated as text.

## Minimal integration contract

```text
DETERMINISTIC_CALCULATION_REQUIRED=yes
LLM_AS_NUMERIC_SOURCE=no
TOOL_CALCULATION_REQUIRED=when_tool_available
FORMAL_ALGORITHM_REQUIRED=when_tool_unavailable
INTERMEDIATE_ROUNDING=forbidden_unless_requested
```

For large tabular calculations, a stricter workflow may forbid language-model fallback entirely and require an external calculation tool.

## Files

- [`SKILL.md`](SKILL.md) — full skill specification.
- [`examples/mcda_chat_free_case.md`](examples/mcda_chat_free_case.md) — application to an MCDA workflow where a chat model produced inconsistent normalized and final scores.
- [`examples/alt_s12_s14_integration.md`](examples/alt_s12_s14_integration.md) — minimal integration into gates S12–S14.

## Scope

The skill does not choose decision criteria, weights, formulas, time horizons, or business preferences. Those remain part of the governing decision procedure. The skill only controls **how numeric consequences of confirmed rules are computed and checked**.
