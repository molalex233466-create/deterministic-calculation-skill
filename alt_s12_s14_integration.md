# Minimal ALT integration: S12–S14

This patch preserves the existing route and adds only the calculation contract required by `DETERMINISTIC_CALCULATION_SKILL`.

## S12 — calculation capability gate

```text
DETERMINISTIC_CALCULATION_REQUIRED=yes // числовой расчёт должен быть детерминированным
LLM_AS_NUMERIC_SOURCE=no // LLM не является источником вычисленных чисел
TOOL_CALCULATION_REQUIRED=when_tool_available // при наличии инструмента расчёт выполняется им
LARGE_TABLE_LANGUAGE_FALLBACK=forbidden // большая расчётная матрица не считается генерацией текста
EXTERNAL_CALCULATION_REQUIRED=when_no_reliable_tool_for_large_table // без надёжного инструмента большой расчёт останавливается
```

S12 must set `calculation_allowed=true` only when a reliable deterministic calculation path exists for the requested numeric workload.

## S13 — deterministic calculation

```text
CALCULATION_SOURCE=deterministic_tool_or_formal_algorithm // источник числового результата
RAW_INPUTS_REQUIRED=yes // сохраняются исходные значения
FORMULA_SOURCE=confirmed_rule_only // используются только подтверждённые формулы
INTERMEDIATE_ROUNDING=forbidden_unless_requested // промежуточное округление запрещено
ROW_REPRODUCIBILITY_REQUIRED=yes // каждая строка должна воспроизводиться
```

The LLM may generate explanation and presentation. The numeric matrix must come from the deterministic calculation path.

## S14 — independent numeric validation

```text
INDEPENDENT_RECALCULATION_REQUIRED=yes // обязательный независимый пересчёт
ROW_LEVEL_COMPARISON_REQUIRED=yes // проверяется каждая строка
FINAL_SCORE_RECOMPUTE_FROM_COMPONENTS=yes // итог пересчитывается из компонент
SORT_AFTER_NUMERIC_VALIDATION_ONLY=yes // сортировка только после числовой проверки
ANY_MISMATCH_ACTION=CALCULATION_INVALID // любое расхождение блокирует рейтинг
```

S14 keeps its existing semantic checks: tie handling, double counting, proposed-rule dependency, sensitivity, and inadmissible alternatives. Numeric reproducibility is added as a separate mandatory check rather than substituted for those checks.
