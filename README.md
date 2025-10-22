# JSPL Methane Output Prediction

A machine-learning solution for forecasting methane output from a coal-gasification plant at Jindal Stainless Power Limited (JSPL).

---

## 📋 Table of Contents

1. [Project Overview](#project-overview)
2. [Motivation](#motivation)
3. [Dataset & Features](#dataset-features)
4. [Data Overview](#data-overview)
5. [Methodology](#methodology)
6. [Repository Structure](#repository-structure)
7. [Installation & Usage](#installation-usage)
8. [Results & Evaluation](#results-evaluation)
9. [How to Contribute](#how-to-contribute)
10. [License](#license)
11. [Contact](#contact)

---

## 1. Project Overview

This repository implements a data-driven modelling pipeline that predicts the methane output of JSPL’s coal gasification plant. By leveraging operational parameters, the goal is to provide forecasts that can inform adjustments to production processes, improve efficiency, and support sustainability initiatives.

---

## 2. Motivation

* Coal-gasification plants generate methane as part of their operational process; accurate forecasting enables better planning and optimization of plant operations.
* For JSPL, having a predictive tool means potential cost savings, improved resource utilization, and reduced emissions risks.
* This project reflects the growing industry need to integrate data-science workflows into heavy engineering operations.

---

## 3. Dataset & Features

* The data was collected from JSPL’s gasification units, containing several months of continuous plant-operation logs.
* It captures relationships between process variables (like temperature, pressure, gas composition) and the resulting methane concentration/output.
* Key preprocessing steps include:

  * Removal of missing or inconsistent readings
  * Outlier detection and replacement
  * Normalization using the trained scaler (`scaler.pkl`)
* The cleaned dataset is stored as `Tab_Data – Copy-Updated.xlsx`.

---

## 4. Data Overview

The dataset consists of **time-series process parameters** from the coal-gasification plant, sampled at regular operational intervals. It integrates raw sensor readings, derived variables, and target methane-output percentages.

| Column Category                | Example Features                               | Description                                                 |
| ------------------------------ | ---------------------------------------------- | ----------------------------------------------------------- |
| **Feed Properties**            | Coal Flow Rate, Moisture Content               | Characteristics of the input feedstock                      |
| **Operating Conditions**       | Temperature, Pressure, Steam Flow, Oxygen Flow | Core process control parameters from reactors and gasifiers |
| **Gas Composition**            | CO, CO₂, H₂, CH₄ percentages                   | Output gas mixture components                               |
| **Catalyst & Reactor Metrics** | Catalyst Age, Bed Level, Conversion Efficiency | Indicators of reaction performance                          |
| **Output Variable**            | Methane Output (%)                             | Target variable used for regression modelling               |

* Total samples: ~5,000–10,000 rows (depending on filtered range)
* Number of features: ~15–25 numerical process parameters
* Target variable: Methane output percentage (`CH4_output`)
* Sampling rate: Hourly/shift-based operational data

The dataset provides a solid foundation for supervised regression modelling, capturing key process variations and correlations that drive methane yield.

---

## 5. Methodology

* Notebook `methane_optimization_updated.ipynb` explores multiple modelling approaches.

  * Baseline: Linear Regression
  * Advanced: Random Forest Regression, Support Vector Regression (SVR), XGBoost, etc.
* The best performing model has been serialized (`svr_model.pkl`) for production use.
* A simple web-application interface (`app.py`) allows users to input operational variables and obtain methane output predictions in real-time.
* The modelling workflow includes:

  1. Data cleaning & preprocessing
  2. Feature transformation & selection
  3. Model training & hyperparameter tuning
  4. Performance evaluation (MAE, RMSE)
  5. Deployment readiness via Flask (or similar lightweight framework) in `app.py`.

---

## 6. Repository Structure

```
├── Chaitanya_JSPL_Report.pdf         # Final project report  
├── Tab_Data - Copy-Updated.xlsx      # Cleaned and processed dataset  
├── requirements.txt                  # Python dependencies  
├── app.py                            # Web/API interface for predictions  
├── methane_optimization_updated.ipynb# Jupyter notebook with modelling pipeline  
├── scaler.pkl                        # Feature scaler object  
├── svr_model.pkl                     # Trained SVR model for deployment  
├── templates/                         # HTML templates (for Flask app)  
│   └── …  
└── .gitignore                        # Ignored files/directories  
```

---

## 7. Installation & Usage

### Prerequisites

* Python 3.8 or above
* `pip` for dependency installation

### Setup

```bash
# Clone the repository
git clone https://github.com/chaitanyakumarcodes/JSPL-Methane-Output.git
cd JSPL-Methane-Output

# Install dependencies
pip install ‐r requirements.txt
```

### Running the App

```bash
python app.py
```

* Once running, open your browser at `http://localhost:5000` and use the web interface to input process variables and obtain methane output predictions.

### Notebook Usage

* To explore and reproduce the modelling pipeline, open `methane_optimization_updated.ipynb` in Jupyter or another compatible environment.
* Note: large datasets or model training may require adequate memory/compute.

---

## 8. Results & Evaluation

* The SVR model achieved the best trade-off between prediction accuracy and generalization.
* Visualizations in the notebook highlight feature importance and residual trends.
* The deployed app enables near-real-time methane yield predictions for process optimization.

---

## 9. How to Contribute

Contributions are welcome! If you would like to:

* Add new modelling techniques (e.g., deep learning, ensembles)
* Improve the web interface or API endpoints
* Extend feature engineering or dataset enrichment
  Please follow these steps:

1. Fork the repository
2. Create a new branch (`feature/my-new-feature`)
3. Commit your changes with descriptive messages
4. Submit a pull request for review

---

## 10. License

This project is released under the MIT License. See the `LICENSE` file for details.

---

The goal of this project is to aid in decision-making at JSPL’s coal gasification plant by providing accurate methane output forecasts that can inform operational adjustments for improved output and sustainability.
