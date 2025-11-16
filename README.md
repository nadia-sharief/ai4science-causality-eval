# AI4Science Causal Claim Detection — Evaluation Repository

## Overview

This repository contains all data, manual labels, model predictions, and evaluation outputs for a preliminary study on **causal claim detection** in scientific abstracts.  
The goal is to determine whether the extracted conclusion from a paper’s title and abstract expresses a **causal claim**, and if not, classify the type of relationship described.

This work is based on the dataset:

**AI4Science: A Large-Scale Benchmark for Scientific Text Understanding**  
<https://arxiv.org/abs/2412.09628>

---

## Project Objectives

1. Extract a concise one-sentence conclusion from each paper.  
2. Determine whether the conclusion expresses a **causal claim** (e.g., causes, leads to, induces, mediates, prevents).  
3. For non-causal conclusions, classify the relationship as one of:  
   *correlation, association, description, hypothesis, mechanistic/theory, measurement/method, other*.  
4. Evaluate multiple LLM models:
   - GPT-4o  
   - GPT-4o (few-shot)  
   - GPT-4o-mini  
   - GPT-4o-mini (post-processed)  
   - Regex / keyword baseline  
5. Compare performance across scientific disciplines.

---

## Project Notebook

The complete end-to-end pipeline, including preprocessing, sampling, manual label integration, inference, evaluation, and error analysis, is documented in the Jupyter notebook:

### **`A Multi-Model Evaluation Pipeline for Causal Conclusion Extraction in Scientific Literature.ipynb`**

This notebook includes:

- dataset loading and parsing  
- discipline extraction and sampling  
- manual label integration  
- creation of the final evaluation split  
- GPT-4o, GPT-4o-mini, few-shot, and baseline inference  
- post-processing and consistency checks  
- error inspection (FP/FN)  
- per-discipline evaluation  
- generation of all CSV/XLSX outputs in this repository  

This file serves as the **central reproducibility record** for the project.

---

## Dataset Source

The original dataset file (**AI4Science_Dataset.txt**) is **not included** because GitHub does not allow files larger than 100MB.

To reproduce preprocessing, download the dataset:

📥 <https://arxiv.org/abs/2412.09628>

---

## Repository Structure

```
ai4science-causality-eval/
│
├── manual_label_TARGET.xlsx
├── manual.xlsx
├── manual_label_271_CLEAN.xlsx
├── manual_label_expanded_clean (2).xlsx
│
└── llm_causality_eval/
    ├── TEST_SPLIT.xlsx
    ├── pred_gpt-4o.csv
    ├── pred_gpt-4o_fewshot.csv
    ├── pred_gpt-4o-mini.csv
    ├── pred_gpt-4o-mini_pp.csv
    ├── pred_baseline_regex.csv
    ├── model_comparison.csv
    ├── errors_FN_*.xlsx
    ├── errors_FP_*.xlsx
    ├── per_discipline_*.xlsx
```


---

## File Descriptions

### 1. Manual Labeling Files

- **manual_label_TARGET.xlsx**  
  Initial sample of 270 papers (9 disciplines × 30).  
  Last 3 columns are intentionally empty for annotation.

- **manual.xlsx**  
  Fully manually annotated dataset containing:  
  - `manual_conclusion`  
  - `manual_causal`  
  - `manual_relation_type`

- **manual_label_271_CLEAN.xlsx**  
  Cleaned and standardized version of manual labels.

- **manual_label_expanded_clean (2).xlsx**  
  Intermediate expanded sheet used during validation.

---

### 2. Evaluation Dataset

- **TEST_SPLIT.xlsx**  
  Final evaluation set of 114 papers, stratified by discipline and causal status.

---

### 3. Model Prediction Files

Contains outputs from all evaluated models:

- GPT-4o  
- GPT-4o (few-shot)  
- GPT-4o-mini  
- GPT-4o-mini (post-processed)  
- Regex keyword baseline  

Each includes generated conclusions, causal predictions, and relation types.

---

### 4. Error Analysis Files

Files prefixed with:

- `errors_FN_*` → false negatives (causal true, predicted non-causal)  
- `errors_FP_*` → false positives (non-causal true, predicted causal)

---

### 5. Per-Discipline Performance Files

Files beginning with `per_discipline_*` contain discipline-wise F1 scores for each model.

---

### 6. Model Comparison Summary

- **model_comparison.csv**  
  Contains accuracy, macro-F1, weighted-F1, and relation-type accuracy for all evaluated models.

---

## Methodology Summary

1. Sampled 9 disciplines using metadata (30 papers each → 270 total).  
2. Performed manual labeling for:  
   - conclusion extraction  
   - causal classification  
   - relationship type assignment  
3. Constructed a stratified 114-paper evaluation split.  
4. Conducted inference with zero-shot, few-shot, and post-processing prompts.  
5. Evaluated:  
   - causal classification F1  
   - relation-type accuracy  
   - discipline-level performance  
   - false positive / false negative patterns  

---

## Reproducibility

To reproduce results:

1. Download the original AI4Science dataset.  
2. Set your API key:

```bash
export OPENAI_API_KEY="your_key_here"
```

3.Run preprocessing and evaluation notebooks.
4.All intermediate outputs are provided in this repository.
