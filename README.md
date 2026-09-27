# Heart Disease Risk Prediction — Web App (v2)

A Streamlit-based clinical decision-support tool predicting heart disease risk
using a class-balanced Logistic Regression model trained on the Framingham
Heart Study dataset (4,238 records). 10-fold CV performance: ROC-AUC ≈ 0.72,
Recall ≈ 0.67.

## What's new in this version

- **Look up existing patient by ID** — select any of the 4,238 patients from
  the underlying dataset by ID; their details auto-fill and you can generate
  a prediction with one click. Useful for demos, testing, and validating the
  model against known outcomes (the actual recorded outcome is shown for
  reference, though the model never sees it).
- **New patient entry** — the original manual-entry form, for a patient not
  in the dataset.
- **Lifestyle factor callouts** — every prediction now highlights smoking
  intensity and BMI specifically, with contextual warnings tied to this
  study's own dose-response findings (e.g. heavy smoking ≈ double the heart
  disease rate of light smoking), since lifestyle factors are this study's
  core contribution.

## Project files

```
webapp_v2/
├── app.py                              # Streamlit application
├── framingham_final_lr_model.joblib    # Trained model + preprocessing pipeline
├── patient_records.csv                 # 4,238 patient records for ID lookup
├── requirements.txt
└── README.md
```

## Run locally

```bash
python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
streamlit run app.py
```

## Deploy on Streamlit Community Cloud

1. Push this folder to a GitHub repo.
2. Go to [share.streamlit.io](https://share.streamlit.io), sign in with GitHub.
3. New app → select repo → main file `app.py` → Deploy.

## Note on patient_records.csv

This file contains the de-identified Framingham dataset records (no personally
identifying information — this is the same public research dataset used
throughout the study), relabeled with synthetic Patient IDs (P00001–P04238)
purely for lookup convenience in the demo. It is not real patient data.

## Disclaimer

Research prototype. Supports, does not replace, clinical judgement.
