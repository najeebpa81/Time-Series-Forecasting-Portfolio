# 05 Visual Insights: Interpreting the Maintenance Alerts

This folder contains high-resolution exports of the analytical charts that drive the decision-making process in this Predictive Maintenance framework.

## 1. Fleet-Level Priority: Pareto Analysis
**File:** `sensor_importance_pareto.png`

This chart identifies the "Vital Few" sensors. By applying the 80/20 rule, we identified that **Sensors S3, S2, and S15** are responsible for the vast majority of degradation signals.
* **Business Use:** Allows maintenance departments to optimize sensor calibration schedules and focus hardware inspections on the most critical components first.



## 2. Individual Asset Diagnostic: SHAP Waterfall Chart
**File:** `unit_82_diagnostic_waterfall.png`

For every RUL prediction, the system generates a "biopsy" of the decision. This waterfall chart shows exactly which sensor values (e.g., a spike in HPC Outlet Temp) pushed the specific engine's health score down.
* **Business Use:** Provides "Explainable AI" (XAI) for technicians. Instead of just seeing a "Danger" alert, the technician sees exactly *which* parameter is failing.



## 3. Prediction Accuracy: RUL vs. Cycle Trend
**File:** `rul_prediction_accuracy_trend.png`

This visualization compares the **Actual RUL** against the **Predicted RUL** for a test engine. It highlights the model's high precision in the critical "Late-Life" phase (the final 50 cycles).
* **Business Use:** Demonstrates the reliability of the **13.76 MAE** result and builds trust in the model's ability to catch failures before they happen.



## 4. Operational Urgency Leaderboard
**File:** `maintenance_urgency_leaderboard.png`

A snapshot of the final output table, ranking all engines in the fleet by their remaining life.
* **Business Use:** This is the primary "Action List" for a Maintenance Manager to plan the next 48 hours of hangar operations.

---
**Najeeb P.A** | *Senior Industrial AI Consultant*
Singapore (Remote Freelance covering UAE & SEA)
