# 🛡️ FakeGuard AI — Fake News Detection
### NeuroLogic 26 Datathon Submission

> Binary classification: **Real (TRUE)** vs **Fake (FALSE)** news articles

---

## 🎯 Competition Objective

Build a model that classifies news articles as real or fake using the reduced version of the [Fake and Real News Dataset](https://www.kaggle.com/datasets/clmentbisaillon/fake-and-real-news-dataset).

| Label | Meaning | Count |
|-------|---------|-------|
| TRUE  | Real news | 15,438 |
| FALSE | Fake news | 8,455 |
| **Total** | | **23,893** |

**Evaluation Metric:** Accuracy

---

## 🗂️ Repository Structure

```
neurologic26-datathon-fakenews/
├── notebook/
│   └── fakeguard_solution.ipynb   ← Main Kaggle notebook (run this)
├── instructions/
│   └── dataset_info.md            ← Competition dataset documentation
├── README.md
└── .gitignore
```

---

## 🚀 How To Run (Kaggle Notebook)

1. Go to [Kaggle](https://kaggle.com) → **New Notebook**
2. Add dataset: search `clmentbisaillon fake-and-real-news-dataset`
3. Set Accelerator: **GPU T4 x1**
4. Upload `notebook/fakeguard_solution.ipynb`
5. Run cells **one at a time**, top to bottom

### Cell Flow

| Cell | Task | Time |
|------|------|------|
| 1 | Install/fix packages | 30 sec |
| 2 | Restart kernel | instant |
| 3 | GPU check | instant |
| 4 | Load competition dataset | instant |
| 5 | Explore data | instant |
| 6 | Clean + deduplicate + split | 1 min |
| 7 | TF-IDF Baseline (honest ~88-92%) | 1 min |
| 8 | RoBERTa fine-tune (anti-overfit) | 30–40 min |
| 9 | Evaluate + confusion matrix | 2 min |
| 10 | Generate submission.csv | instant |

---

## 🧠 Model Strategy

### Why Not Just Use Subject/Date?
The raw dataset has a `subject` column (`politicsNews`, `News`, `left-news`) that perfectly correlates with labels. We **intentionally drop** it to build a model that genuinely understands language — not dataset shortcuts.

### Pipeline
```
title + text → clean → TF-IDF (baseline ~90%)
           ↓
title + text → RoBERTa fine-tune → Target ~94-97%
```

### Anti-Overfitting Techniques
- `weight_decay = 0.10` (strong L2 regularization)
- `hidden_dropout_prob = 0.2`
- `attention_probs_dropout_prob = 0.2`
- `warmup_steps = 1000`
- `max_grad_norm = 1.0` (gradient clipping)
- `EarlyStoppingCallback(patience=2)`

---

## 📊 Results

| Model | Val Accuracy | Notes |
|-------|-------------|-------|
| TF-IDF + LR (baseline) | ~90% | Honest, no leakage |
| RoBERTa (fine-tuned) | ~94-97% | Target |

---

## 📁 Dataset

- **Source:** [Kaggle — Fake and Real News Dataset](https://www.kaggle.com/datasets/clmentbisaillon/fake-and-real-news-dataset)
- **Competition version:** Reduced single CSV (23,893 rows)
- **Columns used:** `title`, `text` only (subject + date dropped to prevent leakage)

---

## 👤 Author

**Archi Jain** — NeuroLogic 26 Datathon
