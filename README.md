# QMCF-Net: Study-Generated Derived Data

This repository directory provides stimulus-level audience-perception targets and rating-support counts for the study **“Quantum-Enhanced Communication Analytics Using a Hybrid Quantum Multimodal Fusion Network for Audience Trust and Sentiment Prediction.”**

## Dataset composition

The study uses 800 multimodal stimuli: 400 advertisement images selected from Pitt Ads and 400 paired image–text posts selected from MVSA-Single. Participants provide ratings of sentiment, trust, and engagement. These responses are aggregated at the stimulus level to construct the SEN, TRU, and ENG target variables used in QMCF-Net.

## Files

- `data/derived/stimulus_level_targets.csv` — stimulus-level target means, sample standard deviations, valid rating counts, source labels, and evaluation partitions.
- `data/derived/stimulus_rating_counts.csv` — target-specific rating counts, common valid-rating support, and the gap relative to the planned 36 valid ratings per stimulus.
- `data/derived/data_dictionary.md` — field definitions, scales, aggregation, partitioning, and data-use notes.

## Target definitions

- **SEN:** the participant's SEN1 response.
- **TRU:** participant-level mean of TRU1–TRU3, aggregated across valid raters.
- **ENG:** participant-level mean of ENG1–ENG3, aggregated across valid raters.

FAM1 is retained as a descriptive/control measure in the study protocol and is not a primary QMCF-Net prediction target.

## Evaluation protocol

The stimulus-level partition is provided in the data. Use only `DEVELOPMENT` stimuli for model fitting, feature selection, hyperparameter tuning, and cross-validation. Keep the `TEST` stimuli untouched until final evaluation. Within cross-validation, fit data-dependent preprocessing on the training fold only and apply it unchanged to the corresponding validation fold.

## Source datasets

1. Pitt Ads: https://people.cs.pitt.edu/~kovashka/ads/
2. MVSA sentiment analysis on multi-view social data (includes MVSA-Single information): https://mcrlab.net/research/mvsa-sentiment-analysis-on-multi-view-social-data/

The source datasets provide the stimuli; the SEN, TRU, and ENG targets documented here are generated from participant responses collected for this study. Original source annotations are not substituted for these participant-derived outcomes.

## Data and reuse notes

This directory contains aggregated stimulus-level summaries and counts. It does not include participant-level response records, original image files, or original social-media post text. Access to and redistribution of the original source assets are subject to the terms and permissions of their respective providers. Please cite the original datasets as required by their providers and cite the QMCF-Net study when using these derived data.

## Citation

Until a paper or repository DOI is assigned, cite the QMCF-Net manuscript using its final bibliographic details when available. The repository owner should add authorship, affiliation, funding, and the final citation to the repository metadata before publication.
