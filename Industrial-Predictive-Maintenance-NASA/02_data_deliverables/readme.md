# 02 Data Deliverables: Model & Inference Assets

This folder contains the production-ready assets required to deploy the Predictive Maintenance model and process incoming sensor data for real-time RUL estimation.

## 📦 Deliverable Checklist

### 1. The Trained Model (`xgboost_predictive_model.pkl`)
* **Format:** Serialized Python Pickle file.
* **Description:** The final XGBoost Regressor trained on the NASA FD001 dataset. It includes the optimized hyperparameters and the learned weights for all engineered features.
* **Usage:** Can be reloaded using `joblib` or `pickle` for immediate inference.

### 2. Feature Metadata (`feature_list.json` or `.txt`)
* **Description:** A definitive list of the **60 input features** the model expects, in the exact order they were trained.
* **Purpose:** Ensures the inference script re-creates the identical feature vector (including rolling means, lags, and standard deviations) before passing data to the model.
* **Key Features Included:**
    * Raw Sensor Readings (S2, S3, S4, etc.)
    * 10-Cycle Rolling Means
    * 10-Cycle Rolling Standard Deviations
    * 5-Cycle Lag Features

### 3. Scaling & Preprocessing Parameters
* **Description:** Documentation of the constants used for data cleaning (e.g., the 125-cycle RUL cap).
* **Significance:** Any live data must be clipped or normalized using these exact parameters to prevent "Feature Drift" and maintain the **13.76 MAE** accuracy.


---

## 🛠️ Quick Start: Loading the Deliverables

```python
import joblib
import pandas as pd

# Load the brain
model = joblib.load('xgboost_predictive_model.pkl')

# Load your processed snapshot
X_live = pd.read_csv('sample_test_snapshot.csv')

# Execute Prediction
predictions = model.predict(X_live)
print(f"Predicted RUL for Unit 82: {predictions[0]}")
