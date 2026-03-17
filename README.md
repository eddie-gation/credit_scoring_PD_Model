# 💳 End-to-End Credit Risk Scorecard Development
> **Predicting Probability of Default (PD) and Constructing an Operational Scorecard using LendingClub Data**

This project demonstrates a rigorous financial risk modeling pipeline, transitioning from raw data to a production-ready **Credit Scorecard (300-850 range)**. It covers the entire lifecycle of PD modeling, emphasizing statistical validity, feature engineering (WoE), and business strategy formulation.

---

## 📊 Executive Summary
* **Model**: Logistic Regression with custom P-value significance testing.
* **Performance**: AUC-ROC **~0.702**, Gini Coefficient **~0.404**.
* **Key Methodology**: Weight of Evidence (WoE) Binning, Information Value (IV) Analysis, and Scorecard Scaling (PDO 20).
* **Business Output**: Optimal Cut-off strategy based on the trade-off between Approval Rate and Bad Rate.

---

## 🔍 1. Data Engineering & Risk Analysis (`preprocessing.ipynb`)

To handle non-linear relationships and enhance model interpretability, I utilized **Weight of Evidence (WoE)** as the primary transformation strategy.

* **Variable Selection via IV**:
    * Identified high-impact predictors like `grade` (IV: >1.0), `home_ownership`, and `annual_inc`.
    * Performed **Monotonicity Checks**: Visualized WoE trends to ensure that risk scores correlate logically with feature bins (e.g., lower grades consistently show higher default risk).
* **Feature Engineering**:
    * Converted date-based variables (`issue_d`, `earliest_cr_line`) into "months since" features to capture the maturity of a borrower's credit history.
    * Systematically managed **Reference Categories** to avoid the dummy variable trap and provide a baseline for risk comparison.

---

## 📉 2. Statistical Modeling & Validation (`PD_Modeling.ipynb`)

Beyond predictive power, this project focuses on the **statistical rigor** required by financial regulators.

* **Custom Logistic Regression**:
    * Implemented a `LogisticRegression_with_p_values` class to calculate the p-value for each coefficient, a feature not natively available in `scikit-learn`.
* **Backwards Elimination**:
    * Refined the model by iteratively removing features with p-values > 0.05 (e.g., `purpose:educational`), ensuring a parsimonious and stable model.
* **Validation Metrics**:
    * **AUC-ROC & Gini**: Confirmed strong discriminatory power.
    * **KS Statistic**: Verified the maximum separation between 'Good' and 'Bad' populations.

---

## 🎯 3. Scorecard Scaling & Business Strategy

The final stage involved translating abstract probabilities into an intuitive **Credit Score**.

* **Scaling Logic (PDO 20)**:
    * **Target Score**: 600 points at 19:1 Odds.
    * **Points to Double Odds (PDO)**: Set to 20, meaning a score increase of 20 points halves the probability of default.
    * **Result**: Generated a score distribution ranging from **350 to 840**, following a near-normal distribution.

* **Optimal Cut-off Strategy**:
    * **Trade-off Analysis**: Analyzed the relationship between **Approval Rate** and **Bad Rate**.
    * **Strategic Recommendation**: Based on the trade-off curve, I analyzed how changing the Cut-off score (e.g., to 620 points) impacts both the business volume (Approval Rate) and risk level (Bad Rate).

---

## 🛠️ Tech Stack
* **Language**: Python 3.x
* **Data Analysis**: Pandas, NumPy
* **Modeling/Stats**: Scikit-learn, SciPy
* **Visualization**: Matplotlib, Seaborn

## 💡 Key Learnings (Internship Focus)
1. **Domain Expertise**: Learned how WoE binning and Scaling make models "auditable" and "interpretable" for financial institutions.
2. **Decision Science**: Realized that a modeler's job is not just to predict, but to provide the **trade-off insights** necessary for executive decision-making.

---

## 📷 Visualizations
*(Note: Please replace the placeholders below with your actual exported image paths)*

### 1. Score Distribution
Describes how the final credit scores are distributed among the test population.
![Score Distribution](path/to/your/score_dist_hist.png)

### 2. Good vs Bad Customer Separation
KDE plot showing the separation between actual defaulters and non-defaulters.
![Good vs Bad KDE](path/to/your/kde_plot.png)

### 3. Approval Rate vs. Bad Rate Trade-off
Strategic tool used to determine the optimal cut-off score.
![Trade-off Curve](path/to/your/tradeoff_plot.png)

---
**Contact**: [Seonghyuek Kim] | [seonghyuek.kim@gmail.com] |
