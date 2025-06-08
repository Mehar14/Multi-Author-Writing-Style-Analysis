# Multi-Author-Writing-Style-Analysis
This repository presents an approach to the Multi-Author Writing Style Analysis task, part of the PAN 2024 shared tasks.

## Overview

This project explores a method for identifying authorship changes in Reddit posts using a fine-tuned RoBERTa model enhanced with Low-Rank Adaptation (LoRA). The objective is to detect transitions in writing style between consecutive paragraphs.

---

## Proposed Method

### 1. Preprocessing

To prepare the dataset for training:

* **Paragraph Segmentation:** Documents were split into paragraphs using line breaks.
* **Pair Formation:** Consecutive paragraphs were grouped into pairs for model input.
* **Tokenization:** Paragraph pairs were tokenized using the RoBERTa tokenizer. Pairs exceeding 512 tokens were truncated to fit the model’s input limit.

### 2. Fine-Tuning with LoRA

We utilized **Low Rank Adaptation (LoRA)** to fine-tune RoBERTa efficiently:

* Only a subset of the model's weights was updated, reducing training overhead.
* LoRA modules were inserted into key layers to better capture stylistic patterns.

---

## Evaluation

The model was evaluated using datasets of varying difficulty:

* **Easy:** Paragraphs span multiple topics.
* **Medium:** Limited topical variation; relies more on style detection.
* **Hard:** Paragraphs are on the same topic, requiring deep stylistic analysis.

### F1 Score Calculation

The F1 score was used to assess performance:

```
F1 = 2 * (Precision * Recall) / (Precision + Recall)
```

---

## Results

| Difficulty Level | F1 Score |
| ---------------- | -------- |
| Easy             | 0.93     |
| Medium           | 0.82     |
| Hard             | 0.80     |

The model performed best on the **Easy** dataset due to topical clues aiding style detection. Performance decreased slightly as task difficulty increased due to reduced topical diversity.

---

## Comparison with Baseline Models

We compared our approach with traditional and transformer-based baselines:

| Model          | Easy | Medium | Hard |
| -------------- | ---- | ------ | ---- |
| RoBERTa + LoRA | 0.93 | 0.82   | 0.80 |
| BERT           | 0.91 | 0.63   | -    |
| TF-IDF         | 0.86 | 0.75   | -    |
| Similarity     | 0.95 | 0.72   | -    |

### Key Insights:

* **RoBERTa** outperformed **BERT** due to better pretraining and contextual modeling.
* **LoRA fine-tuning** enabled efficient, task-specific adaptation.
* Traditional methods (e.g., TF-IDF) lacked deep contextual understanding, limiting their effectiveness on more complex datasets.

---

## Conclusion

RoBERTa with LoRA offers a robust, efficient approach for multi-author style analysis. It significantly outperforms traditional methods and general-purpose transformers, especially when topical clues are limited and deeper stylistic cues must be extracted.
