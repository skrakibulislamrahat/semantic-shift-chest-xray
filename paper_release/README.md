# Reproducibility files for the chest radiograph transport analysis

This folder contains the analysis notebook, aggregated outputs, and figures for the manuscript *Cross-Dataset Reliability of Chest Radiograph Models: Provenance-Aware Analytics and Implications for Microbiology*.

## What is included

- `Full_research_analysis_patient_bootstrap.ipynb`: Colab notebook for calculating the five-seed ensemble metrics, patient-cluster bootstrap intervals, operating-point flag counts, and figures from saved per-image predictions.
- `data/`: the analysis manifest and aggregated result tables used to report the 16 source-to-target comparisons. These files contain summary results, not image files or per-image predictions.
- `figures/`: four aggregate heatmaps for AUROC, AUPRC, ECE15, and threshold flags.

The notebook is the post-training analysis step. It does **not** train models or run image inference. The reusable model-training and transfer-evaluation scripts are in [`../src/`](../src/). To reproduce the reported tables, users must first obtain the datasets from their providers, follow their access terms, create the task splits, train the source models, and generate the saved prediction CSVs and source-validation threshold CSV described below. Raw radiographs, model checkpoints, and patient-level predictions are not redistributed here.

## Run the notebook in Colab

1. Download this repository or open the notebook in Colab.
2. Obtain the datasets from the original providers and prepare the project files using the repository's training/evaluation workflow.
3. In the notebook's configuration cell, set `PROJECT` to the Google Drive project directory containing:
   - `predictions/cross_dataset/`, with one file per source-target-seed named `{source}__to__{target}__seed_{seed}.csv`;
   - `source_validation_operating_points_seedwise.csv`, with source-validation Youden thresholds.
4. Run all cells. The notebook writes summary tables and heatmaps to the configured output folder.

Each prediction CSV must contain `source_task`, `target_task`, `seed`, `target_subset`, `image_id`, `patient_id`, `true_label`, and `pred_prob`. The target subset used for evaluation is `test_split`. The operating-points file must include `threshold_policy`, `source_task`, `seed`, and `threshold`; the notebook selects `source_youden` rows only. The notebook checks for all four tasks and five seeds, matching image/label rows across seeds, and applies source thresholds without tuning on target labels.

## Analysis protocol

The notebook averages the five saved seed probabilities for the primary ensemble estimates, calculates AUROC, AUPRC, balanced accuracy, Brier score, ECE15, negative log-likelihood, high-confidence coverage/errors, and flags per 1,000 images. It uses 500 percentile-bootstrap replicates per comparison, resampling patients when identifiers are available and images otherwise. Since Kaggle/Kermany has no usable patient identifier in this project, comparisons with it as the target use image-level resampling. Bootstrap intervals condition on the saved five-seed ensemble; they are not estimates of site-to-site or prospective clinical performance.

## Data, licensing, and responsible use

The source datasets have separate access and reuse terms; users must obtain them directly from their providers. No raw images or patient-level predictions are included. The CSV outputs here are aggregate task-level summaries. This repository is for research reproducibility and is not a clinical diagnostic system. The results do not identify pathogens or validate a microbiology-testing workflow.

The code is released under the MIT License; third-party dataset terms remain applicable to those datasets.

