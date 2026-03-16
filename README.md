# 🌡️ Land Temperature Trends (1850–2015)

Exploratory data analysis and regression modelling of global land surface temperatures using the Berkeley Earth dataset.

---

## Overview

This project analyses how land surface temperatures have changed over 165 years, using monthly records from 1850 to 2015. The focus is on **land-only data** — ocean temperatures were deliberately excluded to isolate terrestrial warming trends, which are known to be stronger than global averages.

The analysis covers:
- Data cleaning and quality assessment
- Exploratory visualisation of average, maximum, and minimum temperature trends
- Linear and polynomial regression modelling
- Interpretation of warming rates and asymmetric warming patterns

---

## Key Findings

- **Average land temperature increased at +0.085 °C per decade** over the 165-year period
- **Minimum temperatures are warming faster (+0.114 °C/decade) than maximum temperatures (+0.075 °C/decade)** — nights are warming more rapidly than days
- This asymmetric pattern is a well-documented signature of the greenhouse effect: greenhouse gases trap outgoing longwave radiation, which is particularly relevant at night when there is no incoming solar radiation
- A 2nd-degree polynomial regression consistently outperforms linear regression (R² up to 0.86 vs 0.80), suggesting that warming has been accelerating in recent decades

---

## Dataset

**Source:** [Berkeley Earth Global Land and Ocean Temperature Dataset](https://www.kaggle.com/datasets/berkeleyearth/climate-change-earth-surface-temperature-data) via Kaggle

**File used:** `GlobalTemperatures.csv`

**Columns used:**
| Column | Description |
|--------|-------------|
| `dt` | Date (monthly, YYYY-MM-DD) |
| `LandAverageTemperature` | Global average land temperature (°C) |
| `LandMaxTemperature` | Monthly land maximum temperature (°C) |
| `LandMinTemperature` | Monthly land minimum temperature (°C) |

> Ocean temperature columns were dropped from the analysis.

---

## Methodology

### Why was pre-1850 data excluded?

Records before 1850 show significantly higher noise and irregular fluctuations, likely reflecting sparse observational coverage and non-standardised instrumentation. From 1850 onward, records become more consistent and systematic, coinciding with the beginning of modern instrumental climatology.

### Smoothing

A 12-month rolling mean was applied to all temperature series before regression, in order to remove seasonal oscillations and highlight the long-term trend.

### Regression models

Two models were compared:
- **Linear regression** (degree 1): useful for estimating a single long-term trend rate in °C/decade
- **Polynomial regression** (degree 2): better captures the non-linear acceleration of warming in recent decades

R² values were calculated manually using residual sum of squares to avoid external dependencies.

---

## Results Summary

| Variable | Linear R² | Poly R² | Trend (°C/decade) |
|----------|-----------|---------|-------------------|
| Average  | 0.75      | 0.82    | +0.085            |
| Maximum  | 0.64      | 0.67    | +0.075            |
| Minimum  | 0.80      | 0.86    | +0.114            |

---

## Repository Structure

```
land-temperature-trends-1850-2015/
│
├── data/
│   └── GlobalTemperatures.csv        # Source data (not tracked in git — see note below)
│
├── land-temperature-trends.ipynb     # Main analysis notebook
└── README.md
```

> ⚠️ The dataset file is not included in this repository due to size. Download it from [Kaggle](https://www.kaggle.com/datasets/berkeleyearth/climate-change-earth-surface-temperature-data) and place it in the `data/` folder.

---

## Requirements

```
pandas
numpy
matplotlib
seaborn
```

Install with:
```bash
pip install pandas numpy matplotlib seaborn
```

---

## About

This is a self-directed project — I chose this dataset because I actually care about climate change, not because it was assigned. As a PhD chemist pivoting into data science, I wanted to work on something real and build intuition with time-series data along the way.

More of my work on [LinkedIn](https://www.linkedin.com/in/giuliabalducci).
