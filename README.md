# Predicting Workforce Layoff Risks in the Corporate Industry

**Student:** Rishinath S Kurup &nbsp;|&nbsp; **Register Number:** CB.SC.U4CSE23741 &nbsp;|&nbsp; **Section:** H
**Business Domain:** Human Resource Analytics / Corporate Workforce Management

## Problem Statement

Corporate organizations frequently undergo workforce layoffs due to economic downturns, mergers
and acquisitions, automation, changes in business strategy, and financial instability. Most
organizations recognize these risks only after they become severe, resulting in financial
losses, reduced employee morale, and operational disruption. This case study predicts
company-level workforce layoff risk using leading business and workforce indicators, so that HR
managers and business leaders can make proactive workforce-planning decisions.

## Objectives

- Identify the major business and workforce factors that contribute to layoffs.
- Build and analyze a structured dataset covering the required business attributes.
- Perform data preprocessing and exploratory data analysis (EDA).
- Develop a predictive classification model to estimate layoff risk (Low / Medium / High).
- Provide business recommendations to reduce unnecessary layoffs and improve workforce planning.

## Data Collection Source / Method

The dataset's structural schema (company, industry, country, layoff count, funding stage, and
funding raised) follows the format used by publicly accessible tech-layoff tracking sites such
as **Layoffs.fyi**, which aggregate layoff announcements from company press releases, business
news portals, and layoff-tracking coverage. The additional HR/finance attributes required by the
case study proposal (Company Size, Funding Status, Revenue Trend, Hiring Status, Profit/Loss
Indicator, Business Growth Rate, and Layoff Risk Label) were engineered following the fill-rules
defined for this project (e.g., Company Size random 100-10,000; Funding Status
Funded/Bootstrapped/Public; Revenue Trend Increasing/Decreasing/Stable, etc.).

Because compiling several thousand individually verified, named-company layoff records was
outside the practical scope of this exercise, a **4,215-record synthetic dataset** was generated
programmatically to match the statistical structure, category distributions, and value ranges
observed on public layoff trackers, with randomized/noisy relationships between features so the
prediction task is realistic rather than trivial. Company names are synthetic (e.g.,
"NovaDynamics") rather than references to real organizations, so no unverified layoff figures
are attributed to any real company. **This is disclosed transparently for academic integrity**;
the same cleaning/EDA/modeling pipeline in `analysis.ipynb` can be re-pointed at a genuinely
scraped dataset of the same shape (e.g., collected with a tool such as Apify against
Layoffs.fyi or similar public sources) for a fully compliant final submission.

- **Records:** 4,215 (raw) / 4,200 (cleaned)
- **Attributes:** 15
- **Time period:** 2022-2026
- **Coverage:** 18 industries, 15 countries

## Analytics Methods Used

Layoff Risk is framed as a **multi-class classification problem** (Low / Medium / High).
Three models were trained and compared on leading, pre-layoff indicators only (Company Size,
Funding Status, Total Funding Raised, Revenue Trend, Hiring Status, Profit/Loss Indicator,
Industry, Country, Business Growth Rate):

- Logistic Regression (linear baseline)
- Decision Tree Classifier (non-linear baseline)
- **Random Forest Classifier (primary / best-performing model)**

Evaluation used accuracy, macro-precision, macro-recall, macro-F1, a confusion matrix, and
one-vs-rest ROC curves.

## Key Results

| Model | Accuracy | Precision (macro) | Recall (macro) | F1 (macro) |
|---|---|---|---|---|
| Logistic Regression | 0.627 | 0.558 | 0.534 | 0.483 |
| Decision Tree | 0.602 | 0.522 | 0.538 | 0.523 |
| **Random Forest (best)** | **0.638** | 0.551 | 0.563 | **0.547** |

- **Business Growth Rate** and **Company Size** are the leading predictive drivers, followed by
  Revenue Trend and Profit/Loss Indicator.
- **Hiring Freeze** status is a useful secondary/confirming signal, clearly visible in the raw
  EDA but with less unique contribution once growth rate, size, revenue trend and profitability
  are already in the model.
- Funding stage and country contribute the least incremental predictive value.
- **Recommendation:** track a combined quarterly layoff-risk score (growth rate + company size +
  revenue trend + profit/loss) and pair any Medium/High model output with human review before
  acting on it.

## Repository Structure

```
├── README.md                  # this file
├── data/
│   ├── layoff_risk_raw.csv       # dataset as generated
│   └── layoff_risk_cleaned.csv   # cleaned dataset used for analysis
├── analysis.ipynb              # preprocessing, EDA, modeling, evaluation
└── Case_Study_Report.pdf       # full report (Section A format)
```

## References

1. Mansor, N., Sani, N. S., & Aliff, M. (2021). Machine Learning for Predicting Employee
   Attrition. *International Journal of Advanced Computer Science and Applications (IJACSA)*,
   12(11), 435-445.
2. Nayak, S., & Palai, P. (2023). Employee Attrition System Prediction using Random Forest
   Classifier. *International Journal of Computer & Communication Technology (IJCCT)*.
   https://doi.org/10.47893/ijcct.2023.1445
3. Guerranti, F., & Dimitri, G. M. (2023). A Comparison of Machine Learning Approaches for
   Predicting Employee Attrition. *Applied Sciences*, 13(1), 267.
   https://doi.org/10.3390/app13010267
4. Layoffs.fyi - Tech Layoffs Tracker. Publicly accessible layoff-tracking website used as the
   structural reference for the dataset schema.
5. Pedregosa, F., et al. (2011). Scikit-learn: Machine Learning in Python. *Journal of Machine
   Learning Research*, 12, 2825-2830.
