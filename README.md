# SyriaTel Customer Churn Prediction

## 1. Project Overview

This project addresses a critical business challenge: identifying customers who are likely to discontinue their service. By leveraging machine learning, the goal is to predict churn behavior based on usage patterns and service interactions, allowing for targeted retention efforts that safeguard revenue.

## 2. Methodology

* **Data Preparation:** Verified data integrity (no missing values present in the dataset).
* **Feature Selection:** Analyzed feature correlations and removed redundant or low-impact variables to reduce noise and improve model generalization.
* **Imbalance Handling:** Utilized `class_weight='balanced'` and hyperparameter tuning to ensure the model could effectively identify the minority churn class.
* **Model Selection:** Evaluated multiple algorithms, ultimately selecting the **Random Forest Classifier** for its superior ability to handle non-linear relationships and its stability against outliers.

## 3. Key Findings: The Drivers of Churn

![FEATURE IMPORTANCE](Images/features.png)

The analysis identified four primary predictors that significantly influence a customer's decision to leave:

* **Customer Service Calls:** The strongest predictor; churn risk increases exponentially after a customer reaches **3 service calls**.
* **Total Day Minutes & Charges:** High-usage customers are significantly more likely to churn, indicating sensitivity to daytime pricing structures.
* **International Plan:** Customers with an active international plan churn at a disproportionately higher rate, suggesting a possible lack of competitive value in the current plan structure.

## 4. Final Model Performance (Random Forest)

![FEATURE IMPORTANCE](Images/evaluation.png)

The Random Forest model was chosen for deployment because it balances the need to catch churners (Recall) with the need to avoid wasting resources on loyal customers (Precision).

* **Accuracy:** 94.7%
* **Precision:** 84.4% (Minimizes "False Alarms" to loyal customers)
* **Recall:** 80.2% (Successfully captures 4 out of every 5 churners)
* **F1-Score:** 82.2%
* **ROC-AUC:** 0.932 (Excellent ability to distinguish between classes)

## 5. Model Context & Applicability

### Where to use this model:

* **Proactive Retention:** Identifying high-risk customers for monthly loyalty incentives.
* **Support Prioritization:** Routing customers with high churn probability scores to specialized retention teams.

### Where NOT to use this model:

* **New Customers:** The model relies on accumulated usage history; it cannot accurately predict behavior for customers with no historical billing data.
* **Drastic Market Shifts:** If the company changes its base pricing or introduces 5G technology, the model should be retrained to reflect new usage behaviors.

## 6. Strategic Recommendations

To achieve target results (lower churn), the business should consider modifying the following "input variables" through policy changes:

* **Lowering "Day Charge" Impact:** Introduce a daytime usage cap or flat-rate bundle. By effectively lowering the `total_day_charge` for high-volume users, the model suggests a significant increase in retention.
* **Capping "Service Call" Friction:** Modify the support workflow so that the `customer_service_calls` counter never reaches 4 without a mandatory resolution audit. Solving the underlying problem early "resets" the primary churn trigger.
* **International Plan Optimization:** Restructure the plan to include inclusive minutes rather than just a flat access fee, reducing the high correlation between plan ownership and departure.

