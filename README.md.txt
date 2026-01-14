# US Airline Route & Fare Analysis

## Overview
This project analyzes U.S. domestic airline route-level pricing to understand fare behavior in a mature, competitive aviation market.  
The motivation is to study structured pricing dynamics in the U.S. as a reference framework for reasoning about fare volatility and competition-related challenges observed in emerging airline markets such as India.

The analysis combines exploratory data analysis with supervised machine learning under strict temporal validation to ensure realistic and trustworthy results.

---

## Dataset
- U.S. domestic airline route-level data aggregated at quarterly frequency
- Key features include:
  - Average fare
  - Passenger volumes
  - Route distance (miles)
  - Largest-carrier and low-fare-carrier indicators
  - Carrier market share metrics
  - Temporal attributes
- The data reflects **market-level pricing behavior**, not individual ticket transactions.

---

## Methodology
- Feature engineering using lagged and rolling fare statistics
- Strict time-aware train/validation split to prevent data leakage
- Baseline benchmarking using mean fare per route
- Ridge Regression with time-aware cross-validation for regularization selection
- Controlled Gradient Boosting for non-linear comparison
- Residual diagnostics and segment-wise error analysis by route distance

---

## Key Findings
- Ridge Regression substantially outperformed a strong route-level baseline under temporal validation (R² ~0.33 → ~0.64).
- Time-aware cross-validation favored strong regularization (α = 100), indicating significant multicollinearity among engineered features.
- Prediction error increases systematically for long-haul and ultra-long-haul routes, reflecting structurally different pricing dynamics.
- Non-linear models provided marginal additional gains, suggesting limited but present non-linear effects.

---

## Business Insights
- Long-haul and ultra-long-haul routes exhibit approximately 2× higher pricing error than short-haul routes.
- Segment-specific pricing models (short/medium vs long/ultra-long haul) could materially improve forecast accuracy for premium routes.
- These findings provide a useful benchmark for understanding how structured competition and segmentation may improve fare predictability in airline markets.

---

## Limitations & Next Steps
- Competitive intensity and demand elasticity features were not available and represent opportunities for future improvement.
- Segment-specific models could further reduce error on long-haul routes.
- In production, models would require periodic retraining and monitoring for pricing drift.

---

## How to Run
1. Clone the repository  
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
