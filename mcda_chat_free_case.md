# MCDA Chat Free case

## Observed failure

In a Chat Free MCDA run, the model correctly surfaced the governing procedure and displayed raw criterion values, normalized scores, and final weighted scores. However, some displayed normalized scores were incompatible with the stated min–max formula, and some final scores were incompatible with the displayed component scores and weights.

The result therefore failed reproducibility even though the calculation trace looked structurally complete.

## Example

For a cost criterion where lower is better, the stated normalization rule was:

```text
score = (max_value - value) / (max_value - min_value)
```

For UPK-0067, with:

```text
min_loss = 730.00
max_loss = 7821.43
loss = 4977.27
```

the deterministic normalized loss score is approximately:

```text
0.4011
```

The run displayed a materially different value. Because the downtime criterion carried a 30% weight, the error propagated into the final ranking and changed the apparent winner.

## Required behavior with this skill

1. The LLM identifies the confirmed formula and inputs.
2. The numeric expression is delegated to a deterministic calculation mechanism.
3. The mechanism returns normalized scores and weighted totals.
4. The LLM may format and explain the table, but must not invent or interpolate numeric cells.
5. Before ranking, each final score is independently recomputed from raw values and confirmed weights.
6. Any mismatch blocks ranking with `CALCULATION_INVALID`.

## Architectural lesson

A procedural prompt can control **which rules are allowed**, but it does not by itself make the LLM a reliable numeric engine. Procedural validity and computational validity require separate checks.
