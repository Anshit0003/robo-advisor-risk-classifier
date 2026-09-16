# robo-advisor-risk-classifier
# Robo-Advisor Risk-Profile Classifier

**Student:** Anshit Jindal
**Course:** Introduction to Artificial Intelligence and Machine Learning — BBA (FinTech)
**Assessment:** AI Business Case Study, Prompt Research & Presentation

## Project Overview
This project applies supervised Machine Learning to a real robo-advisor use case: automatically classifying a client's investment risk tolerance (Conservative / Moderate / Aggressive) so the platform can recommend an appropriate asset allocation without manual review.

## Business Problem
Robo-advisors need to assign every client a risk category before recommending a portfolio. Doing this manually, or with a fixed rule-based questionnaire, doesn't scale and produces inconsistent results across clients with similar profiles. A supervised classification model can learn the relationship between client characteristics and risk category, producing faster and more consistent risk-profiling.

## Company / Industry Selected
FinTech — Robo-Advisory / Automated Investment Platforms.

## Data Used
Client questionnaire-style data:
- Age
- Annual Income
- Investment Horizon (years)
- Monthly Savings Capacity (% of income)
- Loss Tolerance Score (1–10, from risk questionnaire)
- Investment Experience (Beginner / Intermediate / Expert)
- Number of Dependents

**Target variable:** Risk Category (Conservative / Moderate / Aggressive)

> Note: This version uses a synthetic dataset built to reflect realistic robo-advisor questionnaire logic, since no real client database was available. The pipeline is designed to be reused directly with real client data.

## AI/ML Solution Proposed
**Supervised Classification.** Three algorithms were built and compared:
- Logistic Regression
- Decision Tree
- Random Forest

Logistic Regression was selected as the recommended model — not because it scored highest on every metric, but because it is the most interpretable of the three, which matters for a regulated financial-advisory use case where a client can reasonably ask *why* they were classified a certain way.

## How the Solution Works
```
Client Inputs (age, income, horizon, loss tolerance, experience, dependents)
        ↓
Trained Classification Model
        ↓
Predicted Risk Category (Conservative / Moderate / Aggressive)
        ↓
Mapped Asset Allocation (Equity : Debt : Gold)
        ↓
Robo-Advisor Recommendation to Client
```

## Results

| Model | Accuracy | Precision | Recall | F1-Score |
|---|---:|---:|---:|---:|
| Logistic Regression | 0.807 | 0.808 | 0.807 | 0.807 |
| Random Forest | 0.787 | 0.792 | 0.787 | 0.784 |
| Decision Tree | 0.713 | 0.712 | 0.713 | 0.707 |

## Key Findings
- Investment Horizon and Loss Tolerance Score were the two strongest predictors of risk category (Random Forest feature importance).
- Investment Experience contributed the least — suggesting the questionnaire could potentially be shortened.
- All three models handled the "Moderate" class best; "Aggressive" and "Conservative" (minority classes) had lower recall, meaning some clients at the extremes may be misclassified toward the middle.

## Business Impact
- Faster, consistent client onboarding — no manual risk scoring needed.
- Model output feeds directly into portfolio allocation logic, connecting risk-profiling to actual investment recommendations.
- Removes subjectivity between different advisors/reviewers assigning risk categories manually.

## Risks, Ethics & Responsible AI
- **Misclassification risk:** A wrong risk category could lead to an inappropriate allocation for the client's actual risk capacity.
- **Data bias:** The current model is trained on synthetic data reflecting assumed relationships; a real deployment requires validation against actual client outcomes.
- **Regulatory limitation:** In India, SEBI's investment-advisory suitability requirements mean this model can *support* an advisor's risk assessment but should not be the sole basis for a client's final risk categorization.
- **Human oversight:** Edge cases (unusually high loss tolerance with a short horizon, for example) should be flagged for manual advisor review rather than auto-approved.

## Recommendation
Pilot the Logistic Regression model as a decision-support tool alongside the existing questionnaire, with human review required before the recommended allocation is finalized for the client. Track real classification outcomes over time to replace the synthetic training data with real client data once available.

## AI Tools Used
- Claude — model design, code generation, evaluation, and this documentation

## Tools Used
- Python (scikit-learn, pandas, matplotlib)
- Google Colab

## Skills Demonstrated
- Supervised Machine Learning (Classification)
- Model comparison and evaluation (Accuracy, Precision, Recall, F1-score, Confusion Matrix)
- Feature importance / explainability
- Business-focused model interpretation
- Responsible AI considerations in a regulated financial context

## Limitations
- Trained on synthetic, not real, client data.
- Predictions do not establish causation between client characteristics and actual investment behaviour.
- Model performance should be re-evaluated once real client outcome data is available.
- Not a substitute for regulatory-compliant suitability assessment.

## Repository Contents
- `robo_advisor_risk_classifier.py` — standalone Python script
- `Robo_Advisor_Risk_Classifier.ipynb` — Google Colab notebook (pre-executed)
- `model_comparison.csv` — evaluation metrics for all three models
- `confusion_matrix.png` — confusion matrix for the best-performing model
- `feature_importance.png` — feature importance chart

## AI Usage Declaration
Generative AI (Claude) was used to design the model pipeline, generate code, and draft this documentation. All metrics and outputs shown were produced by actually running the code — none were invented or manually edited. Final interpretation, business recommendations, and evaluation of the results were reviewed by the student.
