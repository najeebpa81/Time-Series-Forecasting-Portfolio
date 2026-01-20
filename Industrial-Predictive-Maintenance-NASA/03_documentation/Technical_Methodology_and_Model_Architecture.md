# Technical Methodology & Model Architecture

## 1. Executive Summary of Approach
This project utilizes a supervised learning regression framework to estimate the Remaining Useful Life (RUL) of industrial turbofan engines. The solution's success is rooted in a **Piecewise Linear Target** strategy combined with high-fidelity temporal feature engineering.

## 2. Data Engineering & Signal Processing
Raw sensor data from the NASA CMAPSS dataset is inherently noisy. To extract a reliable "degradation signal," the following transformations were applied:

### A. Temporal Feature Extraction (Rolling Windows)
We shifted from "point-in-time" readings to "trend-based" readings using a **10-cycle rolling window**.
* **Rolling Mean:** Smoothes high-frequency sensor noise to reveal the underlying wear trend.
* **Rolling Standard Deviation:** Captures increasing sensor volatility (vibration/instability) as the engine nears failure.



### B. Lagged Features
A **5-cycle lag** was implemented for all primary sensors. This allows the XGBoost model to "see" the velocity of degradation by comparing current sensor values to their state 5 cycles prior.

## 3. The "Secret Sauce": Piecewise Linear RUL
In real-world industrial assets, the initial phase of operation shows no measurable wear. Predicting a declining RUL during this "healthy" phase introduces noise into the model.
* **Strategy:** RUL values are capped at **125 cycles**. 
* **Mathematical Rationale:** The model treats all cycles > 125 as a constant "Healthy" state. This forces the Gradient Boosting algorithm to focus its mathematical "attention" strictly on the final 125 cycles where the degradation signatures are most distinct.
* **Impact:** This strategy was the primary driver in achieving the final **MAE of 13.76**.



## 4. Model Architecture: XGBoost Regressor
The core engine is an **eXtreme Gradient Boosting (XGBoost)** regressor. 
* **Objective Function:** `reg:squarederror`
* **Why XGBoost?** It excels at capturing non-linear relationships between multiple sensors (e.g., how a simultaneous spike in Temperature and Pressure indicates a specific failure mode) that standard linear models would miss.
* **Handling Nulls:** XGBoost natively handles the constant sensors we excluded (S1, S5, etc.) by assigning them zero importance.

## 5. Model Interpretability (Explainable AI)
To ensure the model is "trustworthy" for maintenance technicians, we utilize:
1. **Global Pareto Analysis:** Identifying the 20% of sensors that provide 80% of the predictive signal.
2. **Local SHAP Waterfall Charts:** Decomposing individual predictions to show the exact contribution of each rolling mean and lag feature.

---
**Najeeb P.A** | *Senior Industrial AI Consultant*
Singapore (Remote Freelance covering UAE & SEA)
Expertise: Analytical Chemistry | Precision Engineering | Quality Management
