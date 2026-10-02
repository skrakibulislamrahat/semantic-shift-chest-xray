# Historical Result Summary

> **This file describes an earlier exploratory analysis and is not the result table for the current manuscript.** The current manuscript's five-seed ensemble results, target-bootstrap intervals, and aggregate data files are in [paper_release/](paper_release/README.md), especially [the primary results CSV](paper_release/data/primary_patient_cluster_bootstrap_ensemble.csv).

The values below are retained for project history only. They include earlier analyses of CheXpert consolidation and should not be cited as results for *Cross-Dataset Reliability of Chest Radiograph Models: Provenance-Aware Analytics and Implications for Microbiology*.

## Earlier exploratory results

### Nominal pneumonia transport

**Kaggle Pneumonia → CheXpert Pneumonia**

- AUROC: **0.690**
- Balanced accuracy: **0.574**
- ECE-15: **0.234**
- HCER@0.90: **0.199**

### Earlier opacity/consolidation comparisons

**CheXpert Lung Opacity → CheXpert Consolidation**

- AUROC: **0.927**
- Balanced accuracy: **0.860**
- ECE-15: **0.069**
- HCER@0.90: **0.009**

**RSNA Lung Opacity → CheXpert Consolidation**

- AUROC: **0.885**
- Balanced accuracy: **0.737**
- ECE-15: **0.112**
- HCER@0.90: **0.026**

These exploratory analyses do not establish that similarly named labels are clinically interchangeable or that any model is ready for patient-care use.
