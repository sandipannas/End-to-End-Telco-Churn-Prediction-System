# Telco Customer Churn

Local machine-learning project for predicting telecom customer churn. It includes
a trained model, a FastAPI prediction API, and a Gradio interface.

## Local setup (Windows)

Use Python 3.11. From the project root, create and activate a virtual environment,
then install the dependencies:

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

If PowerShell blocks activation, run the environment's Python directly instead:

```powershell
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Start the API and web interface:

```powershell
.\.venv\Scripts\python.exe -m uvicorn src.app.main:app --reload --host 127.0.0.1 --port 8000
```

- API documentation: <http://127.0.0.1:8000/docs>
- Gradio interface: <http://127.0.0.1:8000/ui>
- Health check: <http://127.0.0.1:8000/>

The bundled trained model is used for predictions, so the Kaggle dataset is only
needed if you want to prepare data or train a new model.

## Dataset and training

Download the Telco Customer Churn dataset from
<https://www.kaggle.com/datasets/blastchar/telco-customer-churn> using your
Kaggle account. Extract `WA_Fn-UseC_-Telco-Customer-Churn.csv`, create
`data\raw` in the project root, and place or rename the CSV to:

```text
data\raw\Telco-Customer-Churn.csv
```

Run the training pipeline from the project root:

```powershell
.\.venv\Scripts\python.exe scripts\run_pipeline.py --input data\raw\Telco-Customer-Churn.csv --target Churn
```

The pipeline writes processed data to `data\processed`, model artifacts to
`artifacts`, and experiment logs to `mlruns`.

## Tests

```powershell
.\.venv\Scripts\python.exe scripts\test_pipeline_phase1_data_features.py
.\.venv\Scripts\python.exe scripts\test_pipeline_phase2_modeling.py
```

With the API running, test the prediction endpoint in a separate terminal:

```powershell
.\.venv\Scripts\python.exe scripts\test_fastapi.py
```
