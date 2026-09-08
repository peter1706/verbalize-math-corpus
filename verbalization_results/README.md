# Verbalization results

This folder stores LLM verbalizations of Wikipedia-sourced formulas and **lexical confusions** between alternative spoken realizations of the same mathematical construct.

Formulas were taken from English Wikipedia articles in six domains (Chemistry, Computer Science, Economics, Mathematics, Physics, Statistics). They are stratified by token length (`1-10`, `11-20`, `21-30`, `31-40`). A 24-formula subset of this corpus was used in the listening study documented under [`../survey_results/`](../survey_results/).

Confusion pairs (in [`confusion_pairs/`](confusion_pairs/)) come from comparing verbalizations of the same formula and counting how often one wording is used where another reading uses a different phrase. Files exist for each of the four prompt conditions plus an overall aggregate.

## Files

### `transcriptions_with_bleu_export_complete.csv`

One row per formula (**120 rows**, 20 per domain, 30 per token-range bin). Each row stores the source article, the LaTeX formula, surrounding article context, spoken transcriptions from five models, and BLEU scores.

**Source and formula metadata**

| Column | Description |
| --- | --- |
| `url` | Wikipedia article URL from which the formula was extracted. |
| `date` | Article snapshot / crawl date. |
| `text` | Article text used as context (may be long; two rows have a missing `text` field). |
| `metadata` | JSON string with extraction diagnostics (MathML / MathJax / annotation counts, and similar). |
| `length_text` | Length of the article text. |
| `category` | Domain: Chemistry, Computer Science, Economics, Mathematics, Physics, or Statistics. |
| `latex_formula` | Original LaTeX (often wrapped in `\displaystyle`). |
| `parsed_formula` | Flattened / tokenized reading of the formula used as an intermediate representation. |
| `token_count` | Number of formula tokens (range 1–39 in this export). |
| `token_range` | Length bin: `1-10`, `11-20`, `21-30`, or `31-40`. |
| `context_before`, `context_after` | Article text immediately before and after the formula. |
| `image_path` | Relative path to a rendered formula image (not included in this repository). |

**Verbalizations**

Spoken transcriptions are provided for five models — **Gemini, DeepSeek, OpenAI, Claude, and Grok** — in four prompt settings:

| Setting (column infix) | Prompt |
| --- | --- |
| `no_context_no_info` | Formula only; literal spoken form. |
| `no_context_add_info` / `no_context_with_info` | Formula only, plus extra explanatory wording (units, names of symbols, and similar). |
| `with_context_no_additional_info` / `with_context_no_info` | Formula plus surrounding Wikipedia context; still a relatively literal reading. |
| `with_context_and_additional_info` | Context plus extra explanatory wording. Columns named `extended_transcription_*` are the raw extended readings. |

Columns without a `_validated` suffix are the raw model output. Columns ending in `_validated` are normalized versions of the same reading (punctuation, spelling, and similar cleanup) used for comparison.

**Agreement and BLEU**

| Column | Description |
| --- | --- |
| `n_unique_variants_standard_validated` | How many distinct validated *standard* (no extra explanation) readings the five models produced (1–5). |
| `n_unique_variants_extended_validated` | Same count for *extended* (with extra information) readings. |
| `bleu_*` | BLEU score for that model and prompt condition. Scores are typically higher for literal readings and lower when extra explanatory text is added, because n-gram overlap with a more compact reference decreases. |

The first column (`Unnamed: 0`) is a leftover row index from the CSV export.

### `confusion_pairs/`

Cleaned directed substitution pairs, one CSV per prompt condition plus `overall_cleaned_confusion_pairs.csv`. See [`confusion_pairs/README.md`](confusion_pairs/README.md) for columns, row counts, and group breakdowns.
