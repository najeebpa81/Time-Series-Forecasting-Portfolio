# 03 Scaling & Preprocessing Parameters

To maintain the predictive integrity of the XGBoost model, all incoming raw sensor data must undergo the following transformations before inference. These parameters are fixed based on the training distribution of the NASA FD001 dataset.

## 1. Target Variable Strategy (RUL Capping)
The model utilizes a **Piecewise Linear RUL** strategy. 
* **Cap Value:** 125 cycles.
* **Rationale:** In industrial assets, degradation is not linear from day one. By capping the RUL at 125, we prevent the model from trying to predict "health" and force it to focus strictly on the "degradation" phase. 
* **Inference Note:** Any predicted value of 125 should be interpreted by the maintenance team as "Healthy / No immediate risk."

## 2. Feature Engineering Constants
The following window sizes must be used when generating features from raw sensor streams:
* **Rolling Window ($W$):** 10 cycles. (Used for `rolling_mean` and `rolling_std`).
* **Lag Interval ($L$):** 5 cycles. (Used for `lag_5` features).
* **Minimum Data Requirement:** An engine must have at least **10 cycles** of recorded data before a valid prediction can be generated.



## 3. Sensor Cleaning & Removal
The following sensors were found to have zero variance (constant values) and **must be excluded** from the input vector to avoid model noise:
* **Excluded Sensors:** S1, S5, S6, S10, S16, S18, S19.
* **Logic:** These sensors do not provide any "signal" regarding engine wear.

## 4. Normalization & Scaling
* **Method:** Min-Max Scaling (or Standard Scaling if applied during your specific training run).
* **Scope:** Scaling parameters were calculated on the training set and must be applied to the test set using the same `min` and `max` constants to prevent "Data Leakage."

---
**Najeeb P.A** | *Senior Industrial AI Consultant*
Singapore (Remote Freelance covering UAE & SEA)
