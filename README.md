# Data-Reconciliation-Modelling-Results-vs-Actual-Outcomes

# 🦠 COVID-19 Forecast Reconciliation — Recalculated Modelling Results vs Actual Outcomes

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)
![SQL](https://img.shields.io/badge/SQL-PostgreSQL%20Compatible-336791?style=flat-square&logo=postgresql)
![PowerBI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?style=flat-square&logo=powerbi)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)
![Records](https://img.shields.io/badge/Records-520%20Weekly%20Observations-orange?style=flat-square)

---

## 📋 Executive Summary

This project performs a full **data reconciliation analysis** comparing COVID-19 epidemiological forecast models against actual reported case outcomes across 5 countries from 2021 to 2022.

The core objective is to independently **recalculate and stress-test model outputs**, quantify forecast error, identify systematic bias, and flag exception records — simulating the kind of model validation work done in healthcare analytics, risk management, and financial forecasting roles.

> **Key Finding:** The model exhibited a systematic **over-forecasting bias of 85%** across all countries, with Germany recording the worst accuracy at **20.9% MAPE** and Brazil the best at **10.4% MAPE**. Only **18.7%** of weekly forecasts fell within the acceptable ≤5% variance threshold.

---

## 🚨 Business Problem

Health authorities and policy-makers rely on epidemiological forecast models to allocate resources, plan hospital capacity, and enforce public health interventions. When those models are inaccurate or systematically biased, the consequences are:

- **Resource misallocation** — over-forecasting leads to unnecessary stockpiling; under-forecasting causes shortages
- **Policy missteps** — lockdown decisions made on inflated projections lose public trust
- **Compounding errors** — unchecked model drift means accuracy degrades silently over time with no alert mechanism

**This project answers three critical business questions:**
1. How accurate was the forecasting model across different countries and time periods?
2. Is the model bias random or systematic — and in which direction?
3. Which specific weeks and countries require urgent exception review and root cause investigation?

---

## 🔧 Methodology

The project follows a structured 5-stage reconciliation pipeline:

```
Stage 1: Data Generation     →   Simulate realistic COVID wave patterns + model bias
Stage 2: Reconciliation       →   Calculate variance, MAE, MAPE, RMSE per country/period
Stage 3: Classification       →   Bucket each forecast into accuracy tiers
Stage 4: Exception Flagging   →   Identify and prioritise high-variance records
Stage 5: Visualisation        →   Deliver insights via Python charts + interactive dashboard
```

### Reconciliation Metrics Used

| Metric | Formula | Purpose |
|--------|---------|---------|
| **Variance** | Forecast − Actual | Raw directional gap |
| **Variance %** | (Forecast − Actual) / Actual × 100 | Normalised gap |
| **MAE** | Mean of \|Forecast − Actual\| | Average absolute error |
| **MAPE** | Mean of (\|Error\| / Actual) × 100 | Scale-independent accuracy |
| **RMSE** | √Mean(Variance²) | Penalises large outliers |

### Accuracy Tiers

| Tier | Threshold | Interpretation |
|------|-----------|----------------|
| ✅ Highly Accurate | ≤ 5% variance | Model performing well |
| 🟡 Acceptable | 5–15% variance | Minor calibration needed |
| 🟠 Poor | 15–30% variance | Significant model drift |
| 🔴 Unacceptable | > 30% variance | Immediate review required |

---

## 🛠️ Skills & Tools

### Languages & Libraries
| Tool | Usage |
|------|-------|
| **Python** | Data generation, reconciliation logic, statistical analysis |
| **Pandas** | Data wrangling, aggregations, pivot tables |
| **NumPy** | Wave simulation, random error modelling |
| **Matplotlib** | 5 production-grade dark-themed static charts |
| **Seaborn** | Diverging variance heatmap |
| **SQL** | 8 reconciliation queries — completeness, exceptions, bias analysis |
| **Power BI** | Interactive dashboard via HTML Viewer visual + DAX measures |
| **HTML / JS / Chart.js** | Standalone interactive dashboard |

### Analytical Skills Demonstrated
- ✅ Data reconciliation & completeness testing
- ✅ Statistical error measurement (MAE, MAPE, RMSE)
- ✅ Model bias detection and directional analysis
- ✅ Exception prioritisation and audit-ready reporting
- ✅ Time series analysis and rolling window calculations
- ✅ Multi-country comparative analysis
- ✅ DAX measure development for Power BI
- ✅ End-to-end pipeline from raw data to executive dashboard

---

## 📊 Results & Business Recommendations

### Reconciliation Summary

| Country | Total Actual | Total Forecast | Variance % | MAPE | Model Bias |
|---------|-------------|----------------|------------|------|------------|
| 🇩🇪 Germany | 6.71M | 8.09M | +20.6% | 20.9% | 94% over-forecast |
| 🇮🇳 India | 52.87M | 63.51M | +20.1% | 20.6% | 95% over-forecast |
| 🇺🇸 USA | 36.61M | 42.54M | +16.2% | 17.0% | 92% over-forecast |
| 🇬🇧 UK | 9.26M | 10.37M | +12.0% | 14.7% | 80% over-forecast |
| 🇧🇷 Brazil | 15.17M | 16.08M | +6.0% | 10.4% | 63% over-forecast |

### Accuracy Distribution (All 520 Observations)

| Tier | Count | % of Total |
|------|-------|------------|
| 🔴 Unacceptable (>30%) | 74 | 14.2% |
| 🟠 Poor (15–30%) | 181 | 34.8% |
| 🟡 Acceptable (5–15%) | 168 | 32.3% |
| ✅ Highly Accurate (≤5%) | 97 | 18.7% |

### Business Recommendations

**1. Recalibrate the model's upward bias immediately**
85% of all forecasts were over-estimates. This is not random noise — it is a structural flaw in the model's assumptions. The input parameters (transmission rate, recovery assumptions) need downward adjustment.

**2. Prioritise Germany and India for root cause review**
Both countries show consistent MAPE above 20% across all 8 quarters with no improvement trend. A separate model variant should be considered for high-density populations.

**3. Implement a rolling accuracy monitoring system**
The rolling MAE analysis shows no improvement over the 2-year period. A real-time alert should trigger when 4-week rolling MAPE exceeds 15% — currently there is no such mechanism.

**4. Flag and investigate the 74 unacceptable exception records**
14.2% of observations exceeded 30% variance. Each represents a week where resource allocation decisions were made on significantly wrong data. These require individual root cause documentation.

**5. Brazil's model should be studied as a reference case**
At 10.4% MAPE with more balanced over/under forecasting (63%/37%), Brazil's model configuration is the closest to best practice among the five countries.

---

## 🚀 Next Steps

- [ ] **Replace simulated data with real WHO/ECDC data** — connect to live COVID datasets for production-grade validation
- [ ] **Build automated exception alert pipeline** — trigger email/Slack alert when weekly MAPE exceeds 15%
- [ ] **Extend to 10+ countries** — scale the reconciliation framework to a global dataset
- [ ] **Add SARIMA/Prophet model comparison** — compare multiple forecasting models against actuals side-by-side
- [ ] **Deploy interactive dashboard to the web** — host on Streamlit or Netlify for public portfolio access
- [ ] **Integrate with Power BI Service** — schedule automatic weekly refresh when connected to live data source
- [ ] **Add confidence interval analysis** — assess whether actuals fall within model-predicted confidence bands

---

## 📁 Project Structure

```
covid-forecast-reconciliation/
│
├── 📂 data/
│   └── covid_forecast_actuals_powerbi.csv     # Clean dataset (520 rows, 14 columns)
│
├── 📂 python/
│   ├── generate_data.py                        # Dataset generation script
│   └── analysis.py                             # Reconciliation analysis + 5 charts
│
├── 📂 sql/
│   └── reconciliation_queries.sql              # 8 production SQL queries
│
├── 📂 dashboard/
│   ├── covid_reconciliation_dashboard.html     # Standalone interactive dashboard
│   ├── powerbi_html_measure.txt                # Power BI HTML Viewer DAX measure
│   └── covid_dax_measures.txt                  # 35 DAX measures for Power BI
│
├── 📂 outputs/
│   ├── 01_forecast_vs_actual.png
│   ├── 02_variance_heatmap.png
│   ├── 03_mape_accuracy.png
│   ├── 04_rolling_mae.png
│   └── 05_scatter_forecast_actual.png
│
└── README.md
```

---

## ⚡ Quick Start

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/covid-forecast-reconciliation.git
cd covid-forecast-reconciliation

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn

# 3. Generate the dataset
python python/generate_data.py

# 4. Run the full analysis and generate charts
python python/analysis.py

# 5. Open the interactive dashboard
open dashboard/covid_reconciliation_dashboard.html
```

---

## 📬 Connect

Built as part of a data analytics portfolio demonstrating reconciliation, model validation, and business intelligence skills.

> ⭐ If this project was useful or interesting, consider giving it a star!
