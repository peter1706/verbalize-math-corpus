# Survey results

This folder contains the merged listening-survey responses. Participants heard TTS audio of LLM-generated formula verbalizations and rated how well the speech matched the written formula, which constructs were hard to follow, and whether pauses, emphasis, speech rate, and extra explanation helped.

The spoken scripts come from a **24-formula subset** of the corpus in [`../verbalization_results/transcriptions_with_bleu_export_complete.csv`](../verbalization_results/transcriptions_with_bleu_export_complete.csv). Formulas were taken from English Wikipedia articles in six domains (Chemistry, Computer Science, Economics, Mathematics, Physics, Statistics) and stratified by token length (`1-10`, `11-20`, `21-30`, `31-40`).

## Files

### `survey_merged_with_audio_info.csv`

Listening-study data: **240 rows** = 24 formulas × 2 spoken modalities × 20 respondents.

Design:

- **4 surveys** (`survey_id` 1–4), each with **12 formulas** and **5 respondents**.
- Each respondent rated **12 items** (one audio clip per formula).
- **Modalities:** `standard` (literal spoken formula) vs. `extended` (spoken formula with extra explanatory information). Each modality has 120 ratings. The item-level question *explanatory information helpful* was asked only for `extended` clips (missing for all `standard` rows).
- All 24 formulas appear in the verbalization corpus (`transcriptions_with_bleu_export_complete.csv`).
- All 20 respondents reported nationality Germany.

**Stimulus columns**

| Column | Description |
| --- | --- |
| `formula_id` | Composite identifier (`article URL` + LaTeX). |
| `category`, `token_range`, `token_count`, `latex_formula`, `url` | Domain, length bin, token count, LaTeX, and Wikipedia source (same meaning as in the verbalization corpus). |
| `modality` | `standard` or `extended`. |
| `transcription_text` | Spoken script that was synthesized. |
| `ssml_text` | SSML used for TTS (rate, breaks, emphasis). |
| `survey_id` | Survey version (1–4). |
| `item_order` | Position of the item in that survey. |
| `formula_row` | Formula index within the 24-item survey set (1–24). |
| `audio_duration_sec` | Length of the audio clip in seconds (about 0.7–51 s). |

**Per-item ratings (typically 1–5 Likert)**

| Column | Description |
| --- | --- |
| `annotation` | Item / condition code used in the survey instrument. |
| `formula_match` | How well the speech matched the written formula. |
| `difficult_parts` | Which constructs were hard to follow (free / multi-select text, e.g. brackets, subscripts). |
| `pauses_helpful`, `emphasis_helpful`, `speech_rate_helpful` | Whether those TTS features helped. |
| `explanatory_info_helpful` | Whether extra explanation helped (`extended` only). |

**Session / voice quality** (same value repeated on every row of a respondent)

How clear, correctly pronounced, natural, comfortable, and “teacher-like” the voice sounded over the survey.

**Demographics** (same value repeated on every row of a respondent)

Gender, age group, nationality, highest degree, field of study, mathematical background, English proficiency, device, and audio equipment.

`respondent_id` values look like `study{1–4}_r{1–5}`. The first column (`Unnamed: 0`) is a leftover export index (related to the original formula table, not a unique key for this file).
