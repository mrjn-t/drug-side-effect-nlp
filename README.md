# Predicting High Side-Effect Burden Using NLP
## Overview
With a background in pharmacy, I was interested in whether basic prescribing information — therapeutic indications and active ingredients — already contains enough signal to approximate side-effect burden.

In this project, I treat side-effect burden as a proxy classification task and test whether simple NLP features (TF-IDF) can separate higher-burden drugs from lower-burden ones.

This is not a clinical prediction model.  
It is a structured NLP experiment on a public dataset.

---

## Dataset

**Medicine_Details.csv** containing:

- Medicine Name  
- Composition  
- Uses  
- Side_effects  

Many rows share the same composition (different brands or forms), which makes evaluation design especially important.

---

## Approach
### 1. Target Definition

- Side-effect burden approximated as the number of listed side effects  
- High burden = top 25% of the dataset  
- This is a count-based proxy, not a severity measure  

### 2. Text Preprocessing

- Combined *Uses* and *Composition*  
- Removed dosage numbers (e.g., “500mg”)  
- TF-IDF with uni-grams and bi-grams  

### 3. Model

- Logistic Regression with class balancing  

### 4. Evaluation

- Random train/test split  
- Leakage-aware group split by composition (GroupShuffleSplit)  

---

## Results

- Random split ROC-AUC ≈ 0.98  
- Group split ROC-AUC ≈ 0.93 ± 0.03  

Performance drops under group-based evaluation, highlighting how repeated compositions can inflate metrics if not handled properly.

---

## Key Insight

The most important lesson was methodological:

When multiple products share identical compositions, naive splitting leads to overly optimistic performance estimates.  
Group-based splitting provides a more realistic estimate of generalization.

---

## Limitations

- Side-effect burden is approximated by count, not severity or incidence  
- Dataset is not patient-level clinical data  
- Number of listed side effects may reflect pharmacovigilance depth  

---

## Tech Stack

- Python  
- Pandas  
- Scikit-learn  
- TF-IDF  
- Logistic Regression  

---

## Why This Project

This project reflects my interest in Data Science and my motivation to develop practical skills in analyzing real-world data.
It combines domain knowledge with applied machine learning and highlights the importance of careful evaluation design.

---

## Author

Self-initiated project as part of preparation for MSc in Data Science / AI.
