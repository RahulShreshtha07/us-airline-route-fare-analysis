# US Airline Route & Fare Analysis

**A time-aware machine learning study of pricing dynamics in mature airline markets**

> Understanding structured pricing behavior in U.S. domestic aviation to benchmark emerging market dynamics

---

## 📊 Project Overview

This project builds and evaluates predictive models for U.S. airline route-level fares using rigorous temporal validation. The goal is to understand how competitive forces and market structure shape pricing in aviation, with insights applicable to emerging markets like India.

**Key Challenge:** Most airline pricing is non-stationary and exhibits temporal dependencies. Standard ML validation breaks this assumption. This project enforces strict time-aware validation to ensure realistic performance estimates.

---

## 🎯 Problem Statement

- **Business Context:** Airline pricing is driven by route-specific competition, capacity, and seasonal demand. Understanding these dynamics is crucial for revenue management and market analysis.
- **Analytical Gap:** Public benchmarks for U.S. fare prediction are limited. This project builds a rigorous, reproducible baseline.
- **Approach:** Feature engineering + regularized regression + time-aware validation = realistic performance on unseen future data.

---

## 📁 Dataset

**Source:** U.S. domestic airline route-level aggregated quarterly data (Kaggle)

**Features:**
- **Pricing:** Average fare, price volatility (lagged & rolling statistics)
- **Market Structure:** Passenger volume, route distance, carrier market share
- **Competition:** Largest-carrier indicator, low-fare-carrier presence
- **Temporal:** Year, quarter, seasonal indicators

**Scope:** Market-level aggregated data, NOT individual ticket transactions

---

## 🔧 Methodology

### 1. **Feature Engineering**
- Lagged fare statistics (t-1, t-2 quarters)
- Rolling averages (2-quarter, 4-quarter windows)
- Distance-based route segmentation
- Seasonal and temporal encoding

### 2. **Time-Aware Validation**
Strict temporal split (no future data leaks into training):
- **Train:** Historical periods
- **Validation:** Following period (no overlap)
- **Test:** Final holdout period

### 3. **Modeling Strategy**
| Model | Purpose | Notes |
|-------|---------|-------|
| **Baseline** | Strong reference | Route-level mean fare |
| **Ridge Regression** | Linear with regularization | Handles multicollinearity |
| **Gradient Boosting** | Non-linear comparison | Captures interactions |

### 4. **Evaluation**
- **Metric:** R² (variance explained), RMSE, MAE
- **Granularity:** Overall + segment-wise (by route distance)
- **Residual Analysis:** Error patterns by route type

---

## 🔍 Key Findings

### Model Performance
- **Ridge Regression** substantially outperforms baseline under temporal validation
  - Baseline R²: ~0.33 | Ridge R²: ~0.64 | **+94% improvement**
- **Regularization:** Strong regularization (α=100) favored, indicating multicollinearity in engineered features
- **Gradient Boosting:** Marginal gains (~3-5%), suggesting linear model captures most predictive signal

### Segment-Specific Insights
- **Short-haul routes (< 500 mi):** RMSE ~$15-20, highly predictable
- **Long-haul routes (> 1500 mi):** RMSE ~$40-50, prediction error 2-3× higher
- **Implication:** Segment-specific models could materially improve accuracy on premium routes

### Business Impact
- Long-distance routes exhibit structurally different pricing dynamics (likely hub effects, international connections)
- Competitor presence and market share are strong fare predictors
- Temporal features capture seasonal patterns effectively

---

## 💡 Business Recommendations

1. **Segment-Specific Modeling:** Build separate models for short/medium vs. long/ultra-long-haul routes
2. **Competitive Monitoring:** Integrate real-time competitor pricing data for dynamic model updates
3. **Demand Integration:** Incorporate booking pace and demand elasticity for improved forecasts
4. **Production Pipeline:** Implement automated retraining and drift detection (fares are non-stationary)

---

## ⚠️ Limitations & Future Work

### Current Limitations
- Aggregated market-level data (no individual transaction granularity)
- Missing demand elasticity and booking pace features
- Limited external factors (fuel costs, macroeconomic variables)
- 2-3% of data removed due to data quality issues

### Future Improvements
1. **Demand Features:** Booking curve data, load factors
2. **Macro Features:** Fuel prices, GDP, employment trends
3. **Ensemble Methods:** Stacking/blending to combine model strengths
4. **Causal Analysis:** Understand feature importance and counterfactual scenarios
5. **External Validation:** Test on held-out airlines/routes for generalization

---

## 🚀 How to Run

### Prerequisites
- Python 3.8+
- Jupyter Notebook

### Setup

```bash
# Clone the repository
git clone https://github.com/RahulShreshtha07/us-airline-route-fare-analysis.git
cd us-airline-route-fare-analysis

# Install dependencies
pip install -r requirements.txt
```

### Run the Analysis

```bash
# Open the notebook
jupyter notebook us_airline_route_fare_analysis.ipynb

# Execute all cells to reproduce results
# Runtime: ~5-10 minutes on standard hardware
```

### Output
- Model performance metrics and visualizations
- Feature importance rankings
- Segment-wise error analysis
- Predictions on test set

---

## 📊 Repository Structure

```
.
├── README.md                              # This file
├── requirements.txt                       # Python dependencies
├── us_airline_route_fare_analysis.ipynb   # Main analysis notebook
├── US_Airline_Flight - Dataset.zip        # Raw data (Kaggle source)
└── kaggle_link.txt                        # Dataset source link
```

---

## 📚 Key Libraries

- **Data:** pandas, numpy
- **ML:** scikit-learn, XGBoost
- **Viz:** matplotlib, seaborn
- **Stats:** scipy.stats

---

## 👤 Author

Rahul Shreshtha  
*Data Science Learner | Machine Learning Practitioner*

---

## 📄 License

This project is open source. Use freely for learning and non-commercial purposes.

---

## 🔗 References & Resources

- **Dataset:** [Kaggle - US Airline Flight Data](https://www.kaggle.com)
- **Techniques:** Time series cross-validation, regularized regression, feature engineering
- **Related Work:** Revenue management literature, airline pricing models

---

**Last Updated:** January 2025  
**Status:** Complete & Reproducible
