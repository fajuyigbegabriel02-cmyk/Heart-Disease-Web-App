# Heart Disease Risk Prediction — Web App (Framingham Model)

A Streamlit-based clinical decision-support tool that predicts heart disease
risk from patient clinical data, using a class-balanced Logistic Regression
model trained on the Framingham Heart Study dataset (4,238 records).

10-fold cross-validated performance: ROC-AUC ≈ 0.72, PR-AUC ≈ 0.35, Recall ≈ 0.67.
The model was deliberately tuned (`class_weight='balanced'`) to prioritize
catching at-risk patients given the dataset's 85/15 class imbalance — expect
more false positives than a standard-threshold model, which is the right
trade-off for a screening tool.

## Project files

```
webapp/
├── app.py                              # Streamlit application
├── framingham_final_lr_model.joblib    # Trained model + preprocessing pipeline
├── requirements.txt                    # Python dependencies
└── README.md
```

## 1. Run locally

```bash
python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

pip install -r requirements.txt

streamlit run app.py
```

The app opens at `http://localhost:8501`.

## 2. Push to GitHub

```bash
git init
git add .
git commit -m "Framingham heart disease prediction app"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo-name>.git
git push -u origin main
```

## 3. Deploy for free on Streamlit Community Cloud

1. Go to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub.
2. Click **"New app"**, select your repo, branch `main`, main file `app.py`.
3. Click **Deploy**. You'll get a public URL to share for evaluation.

## Inputs the app collects

Demographics: age, gender, education level
Lifestyle: current smoker (yes/no), cigarettes per day
Medical history: BP medication, prior stroke, hypertension, diabetes
Vitals/labs: total cholesterol, systolic BP, diastolic BP, BMI, resting heart rate, glucose

## Model notes

- Preprocessing (median/mode imputation, scaling, one-hot encoding) is bundled
  inside `framingham_final_lr_model.joblib` alongside the fitted model, so
  `app.py` only calls `.transform()` and `.predict_proba()`.
- The model was trained with `class_weight='balanced'` to counter the dataset's
  85/15 imbalance, favoring recall over raw accuracy — appropriate for a
  screening context where missing a true positive is costlier than a false alarm.

## Disclaimer

This tool is a research prototype intended to support, not replace, clinical
judgment. Predictions should not be used as a sole basis for diagnosis or
treatment decisions.
