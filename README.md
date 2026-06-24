# 🥊 UFC Fight Outcome Predictor

A machine learning system that predicts UFC fight outcomes using historical fight data, betting market signals, and a custom-built ELO rating engine.

Trained on **7,169 UFC fights** spanning **March 2010 to March 2026**, this project combines fighter statistics, dynamic skill ratings, and betting market intelligence into a single prediction pipeline.

---

## 📊 Results

**69.3% accuracy** on completely unseen future fights (trained on 2010–2023, tested on 2023–2026).

This matches the historical accuracy of professional sports betting markets on MMA — where the inherent unpredictability of combat sports (one strike can end a fight) creates a hard ceiling around 68–70%.

---

## 🧠 Key Features

### Custom ELO Rating System
Every fighter starts at 1,500. Ratings update after every fight based on opponent strength, with a 1.2x multiplier for finishes (KO/TKO/Submission). The system **independently identified Jon Jones, Islam Makhachev, and Khabib Nurmagomedov as the top 3 rated fighters** — with zero manual input.

### Time-Aware Features
- Last-3-fight win rate
- Days since last fight
- Current win/loss streaks
- Recent finish rate

All built **chronologically** to prevent data leakage — a fight only "knows" about fights that happened before it.

### Betting Market Integration
American odds converted into implied win probabilities, blended with Expected Value (EV) and finish-method odds (KO/Decision/Submission odds).

### Style Matchup Modeling
Classifies fighters as strikers or grapplers based on finish history, then engineers interaction features for stylistic clashes (striker vs. grappler, two strikers, two grapplers).

### 4-Model Voting Ensemble
- Logistic Regression
- Random Forest (hyperparameter-tuned)
- LightGBM
- XGBoost

Combined via soft voting with a tuned decision threshold (optimal cutoff found through testing, not the default 0.5).

### Honest Evaluation Methodology
Trained on fights from **2010–2023**, tested only on fights from **2023–2026** — a true future holdout. This avoids the inflated accuracy numbers common in random-split sports prediction models, where the model can "see" patterns from fights chronologically after the ones it's tested on.

---

## 🛠️ Tech Stack

- **Python**
- **Pandas / NumPy** — data processing
- **Scikit-learn** — Logistic Regression, Random Forest, model evaluation
- **XGBoost / LightGBM** — gradient boosting models
- **Matplotlib / Seaborn** — visualizations

---

## 📁 Dataset

[UFC Complete Dataset (Kaggle)](https://www.kaggle.com/datasets/mdabbert/ultimate-ufc-dataset) — `ufc-master.csv`

7,169 fights, 2010–2026, including fighter physical stats, career records, betting odds, fighter rankings, and finish details.

---

## 🚀 What It Does

Given two fighters, the model predicts:
- Win probability for each fighter
- The predicted winner
- A confidence level (Strong / Moderate / Toss-up)

Built using fighter ELO ratings, recent form, and historical stats — no manual input needed once a fighter is in the dataset.

---

## 📈 What the Model Learned

Top predictive factors (in order of importance):
1. Betting market implied win probability
2. Strike differential between fighters
3. ELO rating difference
4. Reach and height differential
5. Recent fight form (last 3 fights)

---

## 🎯 Why Not Higher Accuracy?

MMA has a genuine unpredictability ceiling. A single strike, takedown, or submission attempt can end a fight regardless of career stats. Professional betting markets — with far more data (camp info, injury reports, insider knowledge) — also sit around 66-68% accuracy on UFC outcomes. This project's 69.3% is consistent with that real-world benchmark, evaluated honestly on a true future holdout rather than an inflated random split.

---

## 👤 About

Built as a first machine learning project, combining a personal background in MMA training with applied data science and sports analytics.

**Author:** Abhra — AI/ML Engineering student, Symbiosis Institute of Technology, Pune
