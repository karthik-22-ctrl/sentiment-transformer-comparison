# Transformer-Based Sentiment Analysis on SemEval18

This repository contains the experimental implementation for an NLP research poster comparing three transformer architectures for binary sentiment classification:

- BERT
- RoBERTa
- XLNet

The experiment is inspired by prior comparative research on transformer models for sentiment analysis, particularly Bashiri & Naderi (2024).

## Research Question

Do BERT, RoBERTa, and XLNet show similar relative performance patterns on the SemEval18 sentiment dataset when evaluated under a controlled and reproducible experimental setup?

## Dataset

The experiment uses the SemEval18 sentiment dataset containing short, informal social-media text.

Total samples: **1,859**

Labels:

- Negative
- Positive

The data was divided using a stratified split:

- Training: 70%
- Validation: 15%
- Test: 15%

Random seed: **42**

The test set was kept separate from training and model selection.

### Dataset Source

The SemEval18 dataset used in this experiment was obtained from the sentiment-analysis dataset repository associated with Bashiri & Naderi (2024):

https://github.com/hadis-1/Sentiment-Analysis-Datasets

The dataset file itself is not redistributed in this repository. To reproduce the experiment, download `SemEval18.csv` from the source repository and place it in the same directory as the notebook.

## Models

The following pretrained transformer models were fine-tuned:

- `bert-base-uncased`
- `roberta-base`
- `xlnet-base-cased`

## Experimental Setup

Common settings used for all three models:

- Maximum sequence length: 128
- Batch size: 8
- Learning rate: 2e-5
- Epochs: 3
- Weight decay: 0.01
- Random seed: 42
- Model selection metric: Validation Macro F1

The best checkpoint was selected based on validation Macro F1 and evaluated once on the held-out test set.

## Final Test Results

| Model | Accuracy | Macro F1 | Weighted F1 |
|---|---:|---:|---:|
| BERT | 91.40% | 91.33% | 91.38% |
| RoBERTa | **93.55%** | **93.51%** | **93.54%** |
| XLNet | 90.68% | 90.61% | 90.66% |

RoBERTa achieved the highest performance in our experimental setup.

## Error Analysis

Manual inspection of RoBERTa's misclassified examples showed recurring difficulties involving:

- sarcasm and irony
- informal language
- emojis and social-media expressions
- implicit or mixed sentiment
- context-dependent or ambiguous examples

## Repository Contents

- `sentiment_transformer_comparison.ipynb` – complete experimental notebook
- `model_macro_f1_comparison.png` – comparison of model performance
- `roberta_confusion_matrix.png` – confusion matrix for the best-performing model

## Reproducibility

The notebook contains the complete preprocessing, training, evaluation, comparison, and error-analysis pipeline.

The experiments were executed using Python and Hugging Face Transformers.

## Reference

Bashiri, H., & Naderi, H. (2024).  
*Comprehensive review and comparative analysis of transformer models in sentiment analysis.*  
Knowledge and Information Systems, 66, 7305–7361.
