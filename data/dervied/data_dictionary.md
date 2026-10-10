# Data Dictionary: QMCF-Net Derived Stimulus Data

## Scope

These files contain stimulus-level audience-perception summaries for the 800 stimuli used in QMCF-Net: 400 stimuli selected from Pitt Ads and 400 from MVSA-Single. They contain aggregated labels and rating-support counts, not participant-level response records or original image/text assets.

## `stimulus_level_targets.csv`

One row per stimulus (800 rows).

| Field | Definition |
|---|---|
| `stimulus_id` | Unique study identifier for the stimulus. |
| `source_dataset` | Original source dataset: `Pitt Ads` or `MVSA-Single`. |
| `source_type` | Source-domain code: `AD` for Pitt Ads; `SM` for MVSA-Single. |
| `partition` | Prespecified evaluation partition: `DEVELOPMENT` or `TEST`. |
| `cv_fold` | Cross-validation fold assignment for development stimuli; blank where not applicable. |
| `SEN_MEAN` | Mean participant-reported sentiment score (SEN1), on a 1–7 scale. |
| `SEN_SD` | Sample standard deviation of valid SEN1 ratings for the stimulus. |
| `SEN_N` | Number of valid participant ratings contributing to the SEN summary. |
| `TRU_MEAN` | Mean stimulus-level trust score. For each participant, TRU is the mean of TRU1, TRU2, and TRU3; this field aggregates those participant-level scores across valid raters. |
| `TRU_SD` | Sample standard deviation of participant-level TRU scores for the stimulus. |
| `TRU_N` | Number of valid participant-level TRU scores contributing to the trust summary. |
| `ENG_MEAN` | Mean stimulus-level engagement score. For each participant, ENG is the mean of ENG1, ENG2, and ENG3; this field aggregates those participant-level scores across valid raters. |
| `ENG_SD` | Sample standard deviation of participant-level ENG scores for the stimulus. |
| `ENG_N` | Number of valid participant-level ENG scores contributing to the engagement summary. |
| `n_i_common` | Number of valid ratings common to all three target summaries for the stimulus. |

## `stimulus_rating_counts.csv`

One row per stimulus (800 rows); reports support counts and the gap relative to the planned 36 valid ratings per stimulus.

| Field | Definition |
|---|---|
| `stimulus_id` | Unique study identifier for the stimulus. |
| `source_dataset` | Original source dataset. |
| `partition` | Prespecified evaluation partition. |
| `cv_fold` | Cross-validation fold assignment for development stimuli; blank where not applicable. |
| `SEN_N`, `TRU_N`, `ENG_N` | Valid rating counts contributing to the corresponding target. |
| `n_i_common` | Number of valid ratings common to all three targets. |
| `deficit_to_36` | Number of additional valid ratings required to reach 36; zero if support is at least 36. |
| `current_rating_support_status` | `36_OR_MORE_VALID_RATINGS` or `FEWER_THAN_36_VALID_RATINGS`, based on `n_i_common`. |

## Scales and aggregation

- All target scores are oriented so larger values indicate more of the named response: higher perceived sentiment score, trust, or engagement likelihood.
- SEN1 uses an integer 1–7 response scale.
- Trust items use a seven-point scale from 1 (describes very poorly) to 7 (describes very well).
- Engagement items use a seven-point scale from 1 (very unlikely) to 7 (very likely).
- TRU and ENG are first averaged across their three items at the participant–stimulus level, then summarized across valid raters.
- `FAM1` is a descriptive/control measure and is not included as a primary prediction target.

## Partitioning and leakage prevention

Use `partition` to distinguish development stimuli from the held-out test stimuli. The `TEST` partition must not be used for feature selection, hyperparameter tuning, preprocessing fit, model selection, or threshold selection. Cross-validation is conducted within `DEVELOPMENT` according to `cv_fold`. Fit any data-dependent preprocessing using only the applicable training partition/fold and apply the fitted transformation unchanged to its validation/test counterpart.

## Privacy and source assets

These files are aggregated at stimulus level and do not include participant IDs, raw participant-level answers, original images, or original social-media post text. The source datasets remain governed by their own access and reuse terms. Do not redistribute source assets unless the relevant rights and terms expressly permit it.
