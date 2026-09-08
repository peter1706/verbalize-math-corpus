# Confusion pairs

Cleaned **directed substitution pairs** from comparing LLM verbalizations of the same formula: how often one spoken phrase appears where another reading uses a different phrase. Counts are useful for error analysis and for designing speech-style guidelines (for example, preferring a single convention for brackets).

The four condition files match the prompt settings in [`../transcriptions_with_bleu_export_complete.csv`](../transcriptions_with_bleu_export_complete.csv). `overall_cleaned_confusion_pairs.csv` aggregates pairs across conditions (after its own cleaning pass).

## Shared columns

| Column | Description |
| --- | --- |
| `group` | Linguistic / notational category (brackets, fractions, operators, and similar). |
| `reference` | Phrase on the reference side of the comparison. |
| `hypothesis` | Alternative phrase that appeared instead. |
| `count` | How often this pair was observed in that file. |

`reference` and `hypothesis` are **not** interchangeable: the same two words can appear in both directions as separate rows if both substitutions occurred. Column order is `group, reference, hypothesis, count` in the overall file and `reference, hypothesis, count, group` in the per-condition files.

Condition files also include groups that the overall file does not (`capitalization`, `latin letters`, and in the `*_with_info` files also `summations`). Fraction-group spelling is `Fractions/Divisions` in the condition files and `Fractions/Divisons` in the overall file.

## Files

| File | Prompt condition | Rows | Total counts | Most frequent pair |
| --- | --- | --- | --- | --- |
| `no_context_no_info_cleaned.csv` | Formula only; literal spoken form | 140 | 319 | *comma* → *and* (22) |
| `no_context_with_info_cleaned.csv` | Formula only, plus extra explanatory wording | 777 | 1067 | *open parenthesis* → *the quantity* (38) |
| `with_context_no_info_cleaned.csv` | Formula plus Wikipedia context; relatively literal | 209 | 470 | *open parenthesis* → *the quantity* (37) |
| `with_context_with_info_cleaned.csv` | Context plus extra explanatory wording | 600 | 857 | *open parenthesis* → *the quantity* (30) |
| `overall_cleaned_confusion_pairs.csv` | Pairs pooled across conditions | 203 | 493 | *open parenthesis* → *the quantity* (37) |

Extra explanatory wording (`*_with_info`) yields many more distinct pairs than the literal settings, especially for brackets, Latin/Greek letters, and basic operators.

### Group counts (overall file)

| Group | Rows | Typical example (`reference` → `hypothesis`) |
| --- | --- | --- |
| Brackets/grouping | 109 | *open parenthesis* → *the quantity* |
| punctuation/separators | 23 | *comma* → *and* |
| basic operators | 21 | *multiplied* → *times* |
| Fractions/Divisons | 17 | *divided* → *over* |
| Superscript/exponents | 12 | *to* → *squared* |
| greek letters | 8 | *alpha* → *beta* |
| optimization operators | 6 | *max* → *of* |
| integral | 5 | *d* → *dee* |
| Subscripts/indices | 2 | *with* → *sub* |

In the overall file, bracket and grouping wording accounts for more than half of the distinct pairs.
