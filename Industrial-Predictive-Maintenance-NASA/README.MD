# Industrial Predictive Maintenance: Turbofan RUL Estimation

## 📌 Project Overview
Unplanned downtime in high-value industrial assets—such as aircraft engines or power turbines—results in significant operational costs and safety risks. This project develops a high-precision **Predictive Maintenance (PdM)** framework using the NASA CMAPSS (Commercial Modular Aero-Propulsion System Simulation) dataset.

The goal is to predict the **Remaining Useful Life (RUL)** of turbofan engines, transitioning maintenance from a reactive/scheduled model to a data-driven, predictive model.

## 📊 Performance Results
- **Mean Absolute Error (MAE):** 13.76 cycles
- **RMSE:** 19.15
- **R2 Score:** 0.79
- **Confidence:** High (Model performance was consistent across both internal validation and blind testing).

## 🛠️ Technical Strategy

### 1. Advanced Feature Engineering
To capture the "physics" of engine degradation, raw sensor data was transformed into temporal features:
* **Rolling Statistics:** Calculated 10-cycle rolling means and standard deviations to smooth sensor noise and identify stability trends.
* **Lag Analysis:** Implemented 5-cycle lags to capture the rate of change in sensor signatures.
* **Target Capping:** Applied a **Piecewise Linear RUL (capped at 125 cycles)** to focus the model's intelligence on the critical degradation phase rather than early-life steady-state operation.

### 2. The Model: XGBoost Regressor
The system utilizes an optimized XGBoost Gradient Boosting framework. This was chosen for its ability to handle non-linear sensor interactions and its robustness against outliers in industrial time-series data.

## 🔍 Interpretability & Root Cause Analysis
For industrial applications, "When" is not enough; "Why" is critical. This project implements two layers of explainability:

### Fleet-Level: Pareto Analysis
Using a **Pareto Principle (80/20 rule)** approach, we identified the "Vital Few" sensors driving 80% of the predictive signals. 
* **Top Red Flags:** Sensors **S3 (HPC Temp)**, **S2 (LPC Outlet Temp)**, and **S15 (LPT Outlet Pressure)** were identified as the primary indicators of failure.

### Individual Unit-Level: SHAP Waterfall Diagnostics
We utilize SHAP (SHapley Additive exPlanations) Waterfall charts to provide a "diagnostic biopsy" for individual engines. This allows technicians to see exactly which sensor values are pushing a specific engine's RUL estimate down at any given cycle.

## 📂 Directory Structure
* `01_executive_summary/`: High-level business impact and performance metrics.
* `02_data_deliverables/`: Saved model (`.pkl`) and inference-ready feature lists.
* `03_documentation/`: Technical deep-dive into the piecewise strategy and sensor selection.
* `04_source_code/`: Clean, modular Python scripts for training and real-time inference.
* `05_visual_insights/`: High-resolution Pareto, Waterfall, and RUL Prediction charts.

## 🚀 Deployment Use-Case
This framework is designed to be integrated into a maintenance dashboard. By inputting the latest sensor snapshots, the system outputs an **Urgency Leaderboard**, allowing maintenance teams in sectors like Aviation or Oil & Gas to prioritize assets based on true failure risk rather than arbitrary schedules.



