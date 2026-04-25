# Fake News Detection Dataset (Binary Classification — Competition Use)

## Overview

This competition uses data derived from the **Fake and Real News Dataset**.

**We are not the creators or owners of the original dataset.**
The data has been sourced from Kaggle and **preprocessed into a single unified CSV file** for this competition.

The task is to classify news articles as **real or fake**.

---

## Dataset Source

Original dataset available at:
[https://www.kaggle.com/datasets/clmentbisaillon/fake-and-real-news-dataset](https://www.kaggle.com/datasets/clmentbisaillon/fake-and-real-news-dataset)

The provided dataset is a **reduced form** of the above dataset.

---

## Task Definition

Participants must build a **binary classification model**:

### Labels

* **TRUE** — Real news
* **FALSE** — Fake news

---

## Dataset Statistics

| Label     | Count      |
| --------- | ---------- |
| FALSE     | 8,455      |
| TRUE      | 15,438     |
| **Total** | **23,893** |

---

## Dataset Format

The competition dataset is provided as a **single CSV file**.

### Columns

* `title` — Headline of the article
* `text` — Full news content
* `subject` — Topic/category (⚠️ DROP THIS — leaks label)
* `date` — Publication date (⚠️ DROP THIS — not generalizable)
* `label` — Target label (`TRUE` or `FALSE`)

---

## ⚠️ Critical Warning: Subject Column Leaks Labels

The `subject` column contains values like:
- `politicsNews`, `worldnews` → almost always **TRUE (real)**
- `News`, `left-news`, `Government News` → almost always **FALSE (fake)**

**DO NOT use `subject` or `date` as model features.**
Using them will give artificially high accuracy (close to 1.0) but the model will fail on real-world unseen data.

**Allowed features: `title` + `text` only.**

---

## Label Mapping

| Label | Numeric |
| ----- | ------- |
| TRUE  | 1       |
| FALSE | 0       |

```python
df["label_num"] = df["label"].map({"TRUE": 1, "FALSE": 0})
```

---

## Evaluation Metric

* **Accuracy** (primary)

---

## Important Disclaimer

* This dataset is **not originally created by the competition organizers**
* It has been **reformatted and labeled for competition use**
* Original credit belongs to the dataset creator on Kaggle

---

## Citation

> Fake and Real News Dataset
> Available at: [https://www.kaggle.com/datasets/clmentbisaillon/fake-and-real-news-dataset](https://www.kaggle.com/datasets/clmentbisaillon/fake-and-real-news-dataset)
