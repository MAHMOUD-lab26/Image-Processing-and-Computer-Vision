# Advanced Machine Learning — Spring 2026
### German International University of Applied Sciences
**Course:** Advanced Machine Learning | **Instructor:** Dr. Caroline Sabty | **TAs:** Merna Said, Nouran Khaled

---

## Project Overview

This project spans three progressive milestones, each building on core machine learning and deep learning concepts. Together, the milestones take us from unsupervised clustering, through supervised deep learning for vision-language tasks, and finally into a full comparative study of modern NLP paradigms — from scratch-built models to large language models.

---

## Milestone 1 — Comparative Analysis of Clustering Algorithms
**Due:** April 6, 2026

### Objective
Apply and compare multiple unsupervised clustering algorithms on a real-world dataset, and use internal validation metrics to evaluate and interpret the quality of the resulting clusters.

### Dataset
**Wholesale Customers Dataset** — [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/292/wholesale+customers)
A dataset of wholesale distributor clients described by annual spending across product categories.

### What We Did

**Data Preprocessing**
- Loaded and inspected the dataset (structure, feature types, sample count).
- Checked for and handled missing values and duplicates.
- Applied feature scaling (Standardization or Min-Max normalization).
- Detected outliers using statistical and visualization methods.
- Applied PCA for dimensionality reduction where appropriate.

**Exploratory Data Analysis**
- Distribution plots for all numerical features.
- Correlation heatmap to reveal inter-feature relationships.
- Pairwise feature plots and scatter plots between selected pairs.
- 2D visualization using PCA projection and t-SNE for non-linear structure.

**Clustering Algorithms Applied**
- **Elbow Method** — determined the optimal number of clusters by plotting inertia vs. K.
- **K-Means Clustering** — applied for K = 2, 3, 4; visualized cluster assignments and centroids.
- **Spectral Clustering** — applied for K = 2, 3, 4; compared structure to K-Means results.
- **Gaussian Mixture Models (GMM)** — applied for K = 2, 3, 4; compared probabilistic cluster boundaries.

**Evaluation Metrics**
- Dunn Index
- Davies–Bouldin Index (DBI)
- Silhouette Score
- Calinski–Harabasz Index

**Results Analysis**
- Compared all three algorithms across every K value.
- Analyzed the effect of varying K on cluster quality.
- Profiled each cluster by computing average feature values per cluster.
- Interpreted evaluation metric values to identify the best-performing configuration.

---

## Milestone 2 — Image Captioning with CNN–RNN Architecture
**Due:** April 27, 2026

### Objective
Design and train an end-to-end deep learning pipeline that generates natural language captions for images by combining a CNN (visual encoder) with an RNN (language decoder).

### Dataset
**MS COCO (Common Objects in Context)** — [Kaggle](https://www.kaggle.com/datasets/hariwh0/ms-coco-dataset)

| Split | Images | Captions |
|-------|--------|----------|
| Train | 118,000 | 590,000 |
| Val   | 5,000   | 25,000   |
| Test  | 5,000   | 25,000   |

At least 50% of the training data was used due to dataset size. Each image has five human-written captions, providing a richer supervisory signal.

### What We Did

**Data Preprocessing**
- **Caption Cleaning & Tokenization** — lowercasing, punctuation handling, and tokenization of raw captions.
- **Vocabulary Construction** — built a word-level vocabulary from the training captions with frequency thresholding.
- **Sequence Preparation** — padded and truncated caption sequences to a fixed length; added `<start>` and `<end>` tokens.
- **Image Feature Extraction** — passed images through the CNN encoder to produce fixed-length feature vectors.

**Model Architecture**
- **CNN Encoder** — a convolutional network (pretrained or custom) that compresses each image into a compact visual representation.
- **Embedding Layer** — maps vocabulary tokens to dense vector representations.
- **RNN Decoder** — an LSTM or GRU that generates captions word-by-word, conditioned on the CNN-extracted image features.
- **Final Dense Layer** — projects the RNN hidden state to a probability distribution over the vocabulary at each time step.
- **Auxiliary Classification Head** — an additional image classification branch included as auxiliary supervision to sharpen the visual features extracted by the CNN.

**Training & Evaluation**
- The full pipeline was trained end-to-end, jointly optimizing caption generation and auxiliary classification.
- The model was evaluated on the test split with caption quality metrics.

---

## Milestone 3 — Comparative Analysis of Learning Paradigms for Text Classification
**Due:** May 12, 2026

### Objective
Solve a six-class emotion classification task using three fundamentally different NLP paradigms — from-scratch RNNs, fine-tuned transformers, and zero/few-shot LLM prompting — and rigorously compare them to understand the real-world value of pretraining.

### Dataset
**dair-ai/emotion** — [Hugging Face Hub](https://huggingface.co/datasets/dair-ai/emotion)
Short English texts (tweet-length) labeled with one of six emotions: **joy, sadness, anger, fear, love, surprise**.

| Split      | Examples |
|------------|----------|
| Train      | 16,000   |
| Validation | 2,000    |
| Test       | 2,000    |

### What We Did

**Part 1 — Data Preprocessing & Exploration**
- Loaded the dataset via the `datasets` library and inspected all splits.
- Reported class distribution and text length statistics.
- Visualized class balance (bar chart) and text length (histogram).
- Built two tokenization pipelines: a custom vocabulary for the RNN, and a pretrained `AutoTokenizer` for the transformer and LLM.

**Part 2 — From-Scratch RNN Baseline**
- Built an LSTM/GRU classifier with a randomly initialized embedding layer and a softmax classification head.
- Trained on the full 16,000-example training set.
- Reported: accuracy, macro F1, per-class F1, confusion matrix, training time, and inference time.

**Part 3 — Transfer Learning with a Fine-Tuned Transformer**
- Loaded `bert-base-uncased` or `distilbert-base-uncased` with a classification head via `AutoModelForSequenceClassification`.
- Fine-tuned for 2–3 epochs with a learning rate in the range 2×10⁻⁵ to 5×10⁻⁵.
- Explained the model's pretraining objective (masked language modeling) and why it benefits the downstream task.
- Reported the same metrics as Part 2 for a direct comparison.

**Part 4 — LLM Prompting (No Training)**
- Used a pretrained instruction-tuned LLM (Phi-3-mini or Llama-3.2-3B) loaded with 4-bit quantization via `bitsandbytes`.
- Evaluated under three prompting strategies:
  - **Zero-shot** — task description and input text only.
  - **Few-shot** — 3 and 8 labeled examples in the prompt.
  - **Chain-of-Thought** — the model was asked to reason step-by-step before producing a label.
- Reported accuracy, macro F1, and confusion matrix for each setting, with example prompts and raw model outputs shown in the notebook.

**Part 5 — Data Efficiency Experiment**
- Constructed a balanced 500-example training subset (≈83 examples per class).
- Retrained the RNN and re-fine-tuned the transformer on this small subset.
- Produced a comparison plot: test accuracy at 500 examples vs. full training set, for all three paradigms.
- Discussed what the experiment reveals about the value of pretraining when labeled data is scarce.

**Part 6 — Comparative Analysis**
Concluded with a full comparison of all three paradigms across:
- Test accuracy and macro F1 (summary table).
- Training time and inference time.
- Data efficiency (from Part 5).
- Failure modes per class (from confusion matrices).
- A practical discussion: when to choose each paradigm in a real-world project.

---

## Tech Stack

| Tool / Library | Purpose |
|----------------|---------|
| Python | Core language |
| PyTorch / TensorFlow | Model training |
| Hugging Face `transformers` & `datasets` | Pretrained models and dataset loading |
| `bitsandbytes` | 4-bit LLM quantization |
| scikit-learn | Clustering, evaluation metrics |
| Matplotlib / Seaborn | Visualization |
| torchvision | CNN image processing (Milestone 2) |

---

## Repository Structure

```
├── milestone_1_clustering.ipynb       # Clustering analysis (Assignment 1)
├── milestone_2_image_captioning.ipynb # CNN-RNN image captioning (Assignment 2)
├── milestone_3_text_classification.ipynb # NLP paradigm comparison (Assignment 3)
└── README.md
```

---



---
