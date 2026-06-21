# Coffee Sales AI

Predict coffee sales using a lightweight ML model and a simple Flask web app.

This repository contains a small demo application that trains a model (linear regression by default), serves a web UI for predictions, and exposes a set of JSON endpoints for analytics, model retraining, and dashboard data.

## Features
- Train and save a regression model with enhanced features (polynomial & interaction terms).
- Browser-based UI to enter inputs and get predicted sales.
- Endpoints for recent predictions, insights, model performance, and dashboard data.
- SQLite-backed storage for prediction records and model performance tracking.

## Quick Start (Windows)

Prerequisites:
- Python 3.10+ (recommended)
- Git (optional)

Commands (from project root):

1. Create and activate a virtual environment

```powershell
python -m venv .venv
. .venv\Scripts\Activate.ps1
```

2. Install dependencies

```powershell
python -m pip install -r "Coffee Sales App/requirements.txt"
```

3. Run the app

```powershell
.venv\Scripts\python.exe "Coffee Sales App/app.py"
```

4. Open the app in your browser

http://127.0.0.1:5000/

## Project Structure
- `app.py` — Flask application and routes
- `model.py` — dataset generation, feature engineering, train/save/load model
- `analytics.py` — insights and visualization helpers
- `dashboards.py` — dashboard data and utilities
- `database.py` — SQLite helpers for storing predictions and performance
- `static/` and `templates/` — web UI assets and templates
- `requirements.txt` — Python dependencies

## Important files and endpoints
- Home UI: `GET /` → renders the main form.
- Predict (form): `POST /predict` → form fields: `temperature`, optional `weekend` checkbox, `marketing` (budget). Returns the rendered page with prediction.
- Recent predictions: `GET /recent-predictions` → JSON list of recent records.
- Retrain model (programmatic): `POST /retrain-model` → retrains model on available data (returns JSON).
- Insights: `GET /insights` → returns analytics JSON.
- Performance analysis: `GET /performance-analysis` → JSON with model metrics.
- Dashboard data: `GET /dashboard-data` → combined data for dashboard UI.
- Explain prediction: `POST /explain-prediction` → JSON body with `temperature`, `is_weekend`, `marketing` returns explanation JSON.

Example cURL to retrain model:

```bash
curl -X POST http://127.0.0.1:5000/retrain-model -H "Content-Type: application/json"
```

Example cURL to get recent predictions:

```bash
curl http://127.0.0.1:5000/recent-predictions
```

## Data & Model
- The app stores prediction records and model performance in `coffee_sales.db` (SQLite).
- The trained model is saved to `coffee_sales_model.pkl` in the project root.
- `model.py` will generate synthetic training data if not enough historical data is available.

## Notes and troubleshooting
- If you see missing package errors, install the package into the active venv: `python -m pip install <package>`.
- On first run the app will train a model automatically (takes a few seconds).
- The Flask server runs in debug mode by default — do not use this setting in production.

## Contributing
- Fixes, improvements, and documentation updates are welcome. Create a branch, commit changes and open a pull request to the repository.

## License
This project is provided as-is for demo and learning purposes. Add a LICENSE file if you plan to open-source it.

---
If you'd like, I can also:
- add a `CONTRIBUTING.md` and `LICENSE` file
- create a small GitHub Actions workflow to run a quick lint/test on push
- help push this repo to your GitHub account (I can provide exact commands for HTTPS or SSH)
