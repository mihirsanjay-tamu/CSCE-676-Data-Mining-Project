# Mining the Hidden Structure of Jeopardy!
### CSCE 676 — Data Mining and Analysis | Texas A&M University | Spring 2026

---

## 👉 Start here: [`main_notebook.ipynb`](main_notebook.ipynb)

---

## 🎥 Project Video

**[Watch the project walkthrough on YouTube](https://www.youtube.com/watch?v=1Xdq9jJE9pk)**

---

## Overview

Jeopardy! has been on air since 1984, producing over 216,000 question-answer pairs spanning every domain of human knowledge. Despite the richness of this archive, its hidden structure has never been fully mapped — the show's own category labels are inconsistent, redundant, and semantically fragmented; the evolution of knowledge themes across decades has never been systematically tracked; and the factors that determine what makes a question worth the money remain largely unexplored.

This project applies data mining techniques — clustering, topic modeling, and supervised classification — to uncover what lies beneath the surface of this dataset. It asks three connected questions: can we automatically discover semantic groupings that the show's manual labels never captured? Do thematic patterns shift across three decades of episodes? And can dollar value be predicted from question text and metadata?

---

## Research Questions

- **RQ1:** Can we automatically group Jeopardy! questions into meaningful semantic clusters beyond the show's manually assigned categories?
- **RQ2:** How do themes and knowledge domains in Jeopardy! questions evolve over time, and what latent topic structures emerge across decades of episodes?
- **RQ3:** To what extent can the dollar value of a Jeopardy! question be predicted from its textual content and metadata — and how much does each contribute?

---

## Results Summary

K-Means clustering on the full 213k dataset discovered interpretable semantic clusters (music, geography, science, literature, politics) that the show's 26,000+ fragmented category labels never explicitly captured — with Sentence Transformer embeddings outperforming TF-IDF (NMI: 0.397 vs 0.298 at k=30). Topic modeling and TF-IDF trend analysis independently identified the same primary temporal finding: the growth of multimedia-linked vocabulary post-2001, aligned precisely with the introduction of the Jeopardy! Clue Crew in September 2001 — while the show's core knowledge portfolio remained remarkably stable across 28 years. For value prediction, text carries weak but real signal (LR: 39.84% on 3-tier, baseline 33.3%), but structural metadata — particularly Round — explains more variance than question content; simpler TF-IDF models consistently outperformed all deep learning approaches.

---

## Dataset

**Source:** [200,000+ Jeopardy Questions — Kaggle](https://www.kaggle.com/datasets/tunguz/200000-jeopardy-questions)

**File:** `JEOPARDY_CSV.csv`

**Description:** 216,930 question-answer pairs with 7 columns: Show Number, Air Date, Round, Category, Value, Question, Answer. Spans 1984–2012.

**Preprocessing steps (all handled in `main_notebook.ipynb`):**
- `Value` column parsed from currency string to numeric; 3,634 unparseable rows dropped (~1.7%)
- `Air Date` parsed to datetime; `year` extracted
- Categories normalized (uppercase, whitespace stripped, trailing punctuation removed)
- Text cleaned: lowercased, punctuation removed, stopwords stripped, tokens < 2 chars filtered
- `text_combined` field created by concatenating `category_clean` + `question_clean` + `answer_clean`

> **Note:** The dataset file is not included in this repository due to its size. Download it directly from the Kaggle link above and place `JEOPARDY_CSV.csv` in `/content/` before running in Colab.

---

## How to Reproduce

This project was built entirely in **Google Colab**.

1. Download `JEOPARDY_CSV.csv` from [Kaggle](https://www.kaggle.com/datasets/tunguz/200000-jeopardy-questions) and upload it to `/content/` in your Colab session
2. Open `main_notebook.ipynb` in Google Colab
3. Install dependencies: `pip install -r requirements.txt`
4. **Run all cells from top to bottom** — the notebook is self-contained and handles all preprocessing, modeling, and visualization internally

> **GPU recommended:** The Sentence Transformer encoding and BiLSTM training sections require GPU acceleration. In Colab: `Runtime → Change runtime type → T4 GPU`

> **Note on reproducibility:** K-Means random initialization behaves differently across CPU and GPU backends even with `random_state=42`. Cluster label assignments may vary between runs, but semantic themes remain consistent. Labels are remapped by cluster size for consistent ordering.

---

## Key Dependencies

| Package | Version |
|---|---|
| Python | 3.11 |
| pandas | 2.2.0 |
| numpy | 1.26.4 |
| scikit-learn | 1.4.1 |
| tensorflow | 2.16.1 |
| sentence-transformers | 2.7.0 |
| matplotlib | 3.8.0 |
| seaborn | 0.13.2 |
| lime | 0.2.0.1 |

Full environment: [`requirements.txt`](requirements.txt)

---

## Repo Structure

```
jeopardy-data-mining/
│
├── main_notebook.ipynb          # 👉 Main deliverable — start here
├── requirements.txt             # Full Colab environment
├── README.md
├── .gitignore
│
├── checkpoints/
│   ├── checkpoint_1.ipynb       # Project Checkpoint 1
│   └── checkpoint_2.ipynb       # Project Checkpoint 2
│
└── assets/                      # Figures and visualizations (optional)
```

---

## Acknowledgements

This project builds on a hw6 submission for CSCE 676 that explored K-Means and DBSCAN on a 20k sample of this dataset. The main notebook extends that baseline substantially — full dataset metric evaluation, TruncatedSVD visualization, Sentence Transformer embeddings, LDA temporal analysis, multiple supervised classifiers, ablation studies, per-round models, and LIME explainability — none of which appeared in the checkpoint work.

Dataset: [JEOPARDY_CSV.csv via Kaggle (tunguz)](https://www.kaggle.com/datasets/tunguz/200000-jeopardy-questions)
