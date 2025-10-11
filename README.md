
# Impact of Climate Variables on COVID-19 Transmission in US States  
### Baseline Analysis of Climate Influence on Epidemic Dynamics

**Key takeaway:**  
Climate variables have **statistically detectable but limited effects** on COVID-19 transmission.  
**Policy, mobility, and behavioral changes** remain the dominant determinants of spread.

---

## Research Overview

This project examines whether climate conditions—temperature, humidity, and vapor pressure deficit—significantly influence COVID-19 transmission rates across U.S. states.
The analysis integrates multiple heterogeneous datasets (policy, mobility, vaccination, and climate) and employs both statistical and machine learning approaches to quantify climate’s role relative to human-driven factors.

**Research Question:**
Do climate variables meaningfully improve epidemic prediction once major behavioral and policy confounders are controlled?

**Conclusion:**
Climate signals exist but are weak compared to mobility, vaccination, and policy interventions.

---

## Key Results

| Analysis           | Key Finding                                          |
| ------------------ | ---------------------------------------------------- |
| Panel Regression   | Climate coefficients small and often insignificant   |
| GAM                | Non-linear effects (p < 0.001) but modest R² ≈ 0.20  |
| Ablation Study     | Removing climate increased RMSE by **+1.68 (+6.4%)** |
| Feature Importance | Time (48.6%) > Mobility (27.3%) > Climate (15.8%)    |

**Interpretation:**
Climate variables contribute measurably to prediction but have limited practical impact relative to behavioral and policy dynamics.

---

## Datasets

| Category       | Source                  | Description                                       |
| -------------- | ----------------------- | ------------------------------------------------- |
| COVID-19 Cases | Johns Hopkins CSSE      | Daily state-level confirmed cases                 |
| Climate        | NASA POWER              | Temperature, humidity, and vapor pressure deficit |
| Policy         | Oxford OxCGRT           | Government response indices                       |
| Mobility       | Google Mobility Reports | Mobility by sector and baseline change (%)        |
| Vaccination    | US CDC                  | Vaccination and booster rates                     |
| Population     | US Census               | Population normalization (per 100k)               |

All datasets were merged by date and state, standardized, and aligned for consistent time-series modeling.
Preprocessing steps and code are fully detailed in the notebook.

---

## Methods Overview

* **Panel Regression (Fixed Effects):**
  Controls for state and time effects; estimates climate–transmission associations while accounting for unobserved heterogeneity.
* **Granger Causality:**
  Tests predictive value of climate variables over lagged case data; most effects insignificant.
* **Generalized Additive Model (GAM):**
  Captures non-linear relationships between climate and case rates using spline smoothing.
* **Residual Diagnostics:**

  * **Autocorrelation:** Durbin–Watson test and ACF plots
  * **Heteroskedasticity:** Breusch–Pagan test
  * **Normality:** Q–Q plots
    Residuals showed mild serial correlation consistent with epidemic wave patterns, validating model adequacy but motivating time-dependent extensions.
* **Machine Learning (Random Forest):**
  Quantified variable importance and conducted ablation (with vs. without climate).
* **Ablation Validation:**
  RMSE increased by +6.4% without climate, confirming a modest but measurable contribution.

---

## Visualization

### 1. Feature Importance by Category
![Feature Importance by Category](figures/Feature%20Importance%20by%20Category.png)


### 2. COVID-19 Cases and Key Intervention Points
![COVID-19 Cases and Key Intervention Points](figures/COVID-19%20Cases%20and%20Key%20Intervention%20Points.png)


### 3. Top 6 Features Partial Dependence
![Top 6 Features PDP](figures/Top%206%20Features%20PDP.png)

> Visualizations available in full detail in `yonsei_project.ipynb`.

---

## Limitations

1. **Geographic aggregation:** State-capital weather may not represent entire state conditions
2. **Indoor vs. outdoor exposure:** Climate less relevant indoors
3. **Temporal confounding:** Seasonal overlap with policy and variant changes
4. **Causal inference:** Observational design limits causal conclusions
5. **Non-stationarity:** Variant and behavioral shifts disrupt model stability

---

## Project Structure

```
project/
├── data/                 # Cleaned datasets
├── figures/         # Visualization outputs
├── Impact of Climate Variables on COVID-19 Transmission in US States.ipynb  # Main analysis notebook
└── README.md
```

---

## References

* Johns Hopkins University CSSE COVID-19 Data
* NASA POWER Project
* Oxford COVID-19 Government Response Tracker (OxCGRT)
* Google COVID-19 Mobility Reports
* US CDC Vaccination Data
* US Census Bureau Population Estimates
* **Forecasting Epidemic Spread with Recurrent Graph Gate Fusion Transformers (2023)** – consulted as a recent reference on epidemic forecasting models

---

**Last Updated:** October 2025

