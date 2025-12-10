# Weather Intelligence System — Delhi

**Author:** Shruti Somvanshi
**Registration Number:** 12310394
**Subject:** INT234 : PREDICTIVE ANALYTICS

---

> A human-friendly Weather Intelligence System for Delhi that analyzes historical weather, predicts next-day rainfall and temperature, and translates predictions into actionable recommendations (umbrella, clothes drying, travel suggestions).

<!-- TOC -->

## Table of Contents

1. [Project Overview](#project-overview)
2. [Interactive Demo](#interactive-demo)
3. [What's inside (Files & Structure)](#whats-inside-files--structure)
4. [Models & Performance](#models--performance)
5. [Visualizations & Insights](#visualizations--insights)
6. [Install & Run (Quick Start)](#install--run-quick-start)
7. [Usage Examples](#usage-examples)

   * [Rain Prediction (Classification)](#rain-prediction-classification)
   * [Temperature Prediction (Regression)](#temperature-prediction-regression)
   * [Travel Recommendation System](#travel-recommendation-system)
8. [How it makes decisions (explainability)](#how-it-makes-decisions-explainability)
9. [Extending the Project](#extending-the-project)
10. [Contributing](#contributing)
11. [Citing / Acknowledgements](#citing--acknowledgements)
12. [Contact](#contact)

---

## Project Overview

This repository contains code and documentation for a Weather Intelligence System built using 20+ years of Delhi weather data. The system focuses on three main capabilities:

* **Rainfall Prediction (Classification):** Predicts whether it will rain tomorrow (0 = No | 1 = Yes). Achieved **~80%+ accuracy** on test splits.
* **Temperature Prediction (Regression):** Predicts next-day *Temp Max* using a Random Forest regressor. Example: predicted 23.39°C for 9 Dec 2025 vs actual 24°C.
* **Travel Recommendation System:** Rule-based recommendations that suggest suitable Indian destinations based on temperature, month, and season. (Roadmap: convert to ML-driven recommender.)

The goal is to turn raw forecasts into actionable, everyday recommendations like "carry an umbrella", "clothes will dry today", or "good day for hill-station travel".

---

## Interactive Demo

> NOTE: Replace the placeholder below with your hosted demo (Streamlit/Flask/Gradio) or local demo GIF.

**Demo GIF / Screenshot (placeholder)**

![demo-placeholder](./assets/demo-placeholder.gif)

You can run the demo locally (instructions in Quick Start) or deploy it to Streamlit Cloud / Heroku / Vercel for live interactions.

---

## What's inside (Files & Structure)

```
/ (root)
├─ data/                     # raw & processed CSVs (20+ years of Delhi weather)
├─ notebooks/                # EDA and modeling notebooks
├─ src/                      # modular code: data, features, models, utils
│   ├─ data_loader.py
│   ├─ features.py
│   ├─ train_models.py
│   ├─ predict.py
│   └─ recommender.py
├─ app/                      # Streamlit/Flask demo app
├─ assets/                   # images, demo videos, sample plots
├─ requirements.txt
└─ README.md
```

> **Data privacy:** The dataset used here is historical weather data for Delhi. Make sure any shared datasets comply with source licensing.

---

## Models & Performance

### Model 1 — Rainfall Prediction (Classification)

* **Type:** Binary Classification (Rain / No Rain)
* **Model(s) tried:** Logistic Regression, Random Forest, XGBoost
* **Final model:** [best-performing — specify in `notebooks/`]
* **Performance:** ~**80%+ accuracy** on hold-out test set.
* **Example (10 Dec 2025):** `Rain = 0`, `Probability of rain = 1.66%`

### Model 2 — Temperature Prediction (Regression)

* **Type:** Regression (Next-day Temp Max)
* **Model:** Random Forest Regressor
* **Example (9 Dec 2025):** Predicted 23.39°C, Actual 24°C.

> For reproducible exact metrics (precision, recall, F1, RMSE), check the `notebooks/model_evaluation.ipynb` which contains the test-train split, cross-validation results, and feature importance plots.

---

## Visualizations & Insights

Helpful visuals included in `assets/` and notebooks:

* Temperature trend over 20+ years
* Monthly & seasonal rainfall analysis
* Rainy vs Non-Rainy day counts
* Clothes-drying & umbrella decision graphs (decision thresholds)
* Temperature histograms & heatmaps
* Model comparison charts and feature importances

Tip: Use the notebooks to re-run visualizations after changing filters (year range, season, etc.).

---

## Install & Run (Quick Start)

**Requirements**

* Python 3.8+
* Virtual environment recommended

```bash
# clone the repo
git clone <your-repo-url>
cd Weather-Intelligence-System

# create venv
python -m venv .venv
source .venv/bin/activate    # macOS / Linux
.venv\Scripts\activate     # Windows

# install deps
pip install -r requirements.txt

# run demo (Streamlit example)
streamlit run app/streamlit_app.py
```

If you prefer a Flask API instead of Streamlit, instructions and `app/api.py` are included.

---

## Usage Examples

### Rain Prediction (Classification)

Use `src/predict.py` to load the saved classifier and predict next-day rain probability.

**CLI usage (example):**

```bash
python src/predict.py --model models/rain_classifier.pkl --input data/today_features.csv
# Output: probability, predicted class (0/1), human-readable advice (carry umbrella / no umbrella)
```

**Sample output**

```
Prediction: No Rain (0)
Probability of Rain: 1.66%
Advice: No umbrella needed — low risk of rain.
```

### Temperature Prediction (Regression)

```bash
python src/predict_temp.py --model models/temp_rf.pkl --input data/today_features.csv
# Output: predicted Temp Max (°C)
```

**Sample output**

```
Predicted Temp Max for 2025-12-09: 23.39 °C
Advice: Mild day — ideal for daytime outdoor activities. Clothes likely to dry if wind/sun present.
```

### Travel Recommendation System

A small rule-based recommender suggests destinations based on `temperature`, `month`, and `season`.

**Example rule**: If `temp <= 20` and `month in [11,12,1,2]` → recommend hill stations with winter festivals; if `temp >= 30` and `season == 'Monsoon'` → recommend coastal/sea-facing locations.

**CLI usage**

```bash
python src/recommender.py --temp 24 --month 12 --season winter
# Output: list of recommended places + short reasoning
```

---

## How it makes decisions (explainability)

* **Feature Importance:** For Random Forests, feature importances are logged and visualized so you can see which features drive predictions (e.g., previous-day rainfall, humidity, month, wind speed).
* **Thresholds & Rules:** The travel recommender is rule-based and fully transparent. The umbrella/clothes-drying advice maps from predicted rain probability and predicted temperature to simple thresholds (documented in `src/utils/thresholds.py`).
* **Calibration:** Probability calibration (Platt scaling / isotonic) is used for rain classifier to make probability outputs more trustworthy.

---

## Extending the Project

Ideas for future work:

* Turn the travel recommender into an ML-based ranking model using destination historical weather + user preferences.
* Add short-term nowcasting using satellite / radar feeds.
* Deploy the model behind an API with authentication and usage quotas.
* Add solar-index predictions for optimizing outdoor solar tasks.

---

## Contributing

Contributions, bug reports, and feature requests are welcome. Please open an issue or submit a pull request.

Guidelines:

* Follow the existing code style (PEP8)
* Add tests for new features
* Update notebooks / readme when adding datasets or models

---

## Citing / Acknowledgements

If you use this project in research or a product, please cite the repo and mention the author:

**Shruti Somvanshi — Weather Intelligence System (INT234 : PREDICTIVE ANALYTICS)**

---

## Contact

If you have questions or want to collaborate:

* **Author:** Shruti Somvanshi
* **Registration Number:** 12310394
* **Subject:** INT234 : PREDICTIVE ANALYTICS
* **Email (optional):** add your contact email here

---

## License

This project is released under the MIT License — see `LICENSE` for details.

---

*Generated README — feel free to edit sections (Demo placeholder, contact email, dataset source and license) before publishing.*

