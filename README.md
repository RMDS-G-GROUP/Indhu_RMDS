# Indhu-Data-Science-Hackathon-
Dataset B — H1N1 Vaccine Acceptance & Cost-Optimal Allocation
Team 11 — Data Science Challenge (Hackathon, 11 November 2026)
This repository contains our team's solution to the Data Science Challenge. We
predict individual H1N1 vaccine acceptance and use the predictions to make
cost-optimal vaccine allocation decisions, minimising the town's expected total
cost (vaccine purchases, compensation, and hospitalisations).
Links
•	Colab notebook: dataset_B_team11_notebook.ipynb
•	Submissions: submissions/ (5 files, ordered best-to-worst)
Problem
Item	Cost
Vaccine (per dose, sent to home)	$500
Hospitalisation for H1N1	$25,000

•	Everyone in the town is infected (100% infection probability).
•	Anyone who wants a vaccine must receive one; otherwise the town pays them
$500 compensation.
•	Vaccines are home-delivered and ruined if unused — so we must predict
exactly who accepts, not just the total number.
•	Target variable: h1n1_vaccine (binary). Test-set labels are hidden.
Data
•	dataset_B_training.csv — 4,756 respondents, 31 columns (29 predictors +
respondent_id + target).
•	dataset_B_testing.csv — 4,749 respondents, 30 columns (target hidden).
•	30 features: H1N1 concern/knowledge, behavioural flags, doctor
recommendation, opinions on vaccine effectiveness/risk/side-effects,
demographics, employment, household composition, and chronic medical
conditions.
Method overview
1.	EDA — target distribution, missing-data analysis, acceptance rates by
categorical/ordinal predictors, correlations, and visualisations.
2.	Data integrity — ID uniqueness, duplicate feature profiles,
train/test overlap checks.
3.	Preprocessing — leakage-safe scikit-learn Pipeline/ColumnTransformer:
median imputation + indicators for numeric features, one-hot encoding for
text features. Three preprocessing variants compared (baseline, explicit
missing category, ordinal encoding).
4.	Models compared — dummy baseline, logistic regression, random forest,
extra trees, histogram gradient boosting (5-fold stratified CV, log loss
as primary metric).
5.	Hyperparameter tuning — grid search for logistic regression and
HistGradientBoosting.
6.	Honest evaluation — 20% audit split reserved untouched until the final
model comparison.
7.	Cost-sensitive decisions — per-person decision rule derived from the
challenge's cost structure.
8.	Sensitivity analysis — risk assumptions varied (baseline risk
0.4–1.5%, vaccine risk reduction 25–75%).
9.	Explainable AI — SHAP values on the final model.
Key results
Model	Audit log loss	Audit ROC AUC	Expected cost (per-person rule)
HistGradientBoosting (tuned)	0.493	0.827	**$524,050**
Logistic regression (C=0.03)	0.493	0.826	$525,450
Random forest	0.502	0.833	$527,650

•	Acceptance is driven by doctor recommendation, perceived H1N1 risk,
and perceived vaccine effectiveness.
•	A per-person decision threshold (from the cost formula) beats any
single global threshold by ~$9,500 in expected cost: send vaccines to
high-risk people even at lower acceptance probability; send to low-risk
people only when acceptance is very likely.
•	Expected costs are highly sensitive to hospitalisation-risk assumptions;
the decision-rule structure is robust across all scenarios tested.
Submissions (ordered best-to-worst)
Order	Model	Decision rule
1	HistGradientBoosting	Per-person cost-optimal thresholds
2	Logistic regression	Per-person cost-optimal thresholds
3	Random forest	Per-person cost-optimal thresholds
4	HistGradientBoosting	Global threshold 0.65
5	Logistic regression	Global threshold 0.60

How to run
1.	Open the Colab notebook (link above) with Editor rights.
2.	Upload dataset_B_training.csv and dataset_B_testing.csv when prompted.
3.	Runtime → Run all. Submission files are written to submissions/.
Requires: Python 3, pandas, numpy, scikit-learn, matplotlib, seaborn
(pip install -r requirements.txt); shap for the XAI section.
Repository structure
├── README.md
├── data/                       # training & testing CSVs (not committed if large)
├── notebooks/
│   └── dataset_B_team11_notebook.ipynb
├── submissions/                 # 5 challenge submission files
└── docs/                        # cost-metric research notes

Team workflow
•	Shared Colab notebook linked to this GitHub repository (all members have
commit access).
•	Work divided across the hackathon: EDA & visualisation, preprocessing,
model development, cost analysis, submission generation, and XAI.
•	All code reviewed and understood by every member before the presentation.
Contact
Team 11 — RMDS Data Science Challenge
<img width="476" height="661" alt="image" src="https://github.com/user-attachments/assets/e2c615f1-631d-4542-94ff-f3bec7f04bf0" />
