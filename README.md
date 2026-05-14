# Detecting Appreciation-Led Pricing in Texas Housing Markets
### Using User-Cost Theory to Evaluate Rent-Implied Valuation (2010–2019)

*By Chinedu Okafor*

---

## Overview

This project investigates whether Texas housing markets were priced consistently with rent-implied fundamentals between 2010 and 2019. Using a user-cost valuation framework, it asks:

> *For a given city and year: what annual home price growth did the market have to assume for buying to make more sense than renting — and was the market operating on rental fundamentals at all, or driven purely by appreciation expectations?*

The analysis covers four major Texas metros — Dallas, Houston, Austin, and San Antonio — and integrates three public data sources to build a cross-market, multi-year valuation dataset.

---

## Key Findings

- **60% of valid metro-year observations** fell into appreciation-led (speculation-dominated) pricing regimes
- **Dallas** exhibited persistent divergence from rent-based valuation across the entire analysis window
- **Houston** remained comparatively fundamentals-aligned in years where the model was applicable
- Rent-based equilibrium explained only a limited subset of pricing behavior — Texas metros were largely not priced on rental fundamentals during this period
- Sensitivity testing showed the core conclusion holds across depreciation assumptions of 2–4%, though the margin is significant enough that `d` should be treated as an assumption rather than a settled constant

---

## Data Sources

| Dataset | Source | Description |
|---|---|---|
| **ZHVI** | [Zillow Research](https://www.zillow.com/research/data/) | Median home values by metro area, monthly |
| **ZORI** | [Zillow Research](https://www.zillow.com/research/data/) | Median observed rents by metro area, monthly |
| **MORTGAGE30US** | [FRED](https://fred.stlouisfed.org/series/MORTGAGE30US) | Weekly 30-year fixed mortgage rates |

> **Note:** Data files are not included in this repository. Download them directly from the links above and place them in your Google Drive as described in the setup instructions.

---

## Methodology

The analysis is built on the **rent-vs-own equilibrium formula** from user-cost theory:

$$g = r + d - \frac{R}{P}$$

| Variable | Definition |
|---|---|
| `g` | Implied annual home price growth (what the market is pricing in) |
| `r` | 30-year mortgage rate |
| `d` | Depreciation + maintenance constant (baseline: 3%) |
| `R` | Annual rent for an equivalent home |
| `P` | Current home price |

From this, we derive the **implied rent** (`u`) — the rent that would make buying and renting financially equivalent given actual future appreciation — and compute the **R/u ratio** to classify each metro-year into a pricing regime.

### Model Assumptions
- Renting and owning provide equivalent housing utility
- Market participants price homes using expected appreciation
- Ownership costs can be approximated by a fixed depreciation constant
- Mortgage rates proxy financing cost

### Limitations
- Ex-post appreciation is used as a validation input rather than a forward-looking expectation
- Non-financial ownership benefits (stability, customization) are excluded
- Local supply constraints are not explicitly modeled

---

## Notebook Structure

| Step | Description |
|---|---|
| 1 | Setup — mount Google Drive, import libraries, define constants |
| 2 | Load datasets (ZHVI, ZORI, FRED) + data validation |
| 3 | Explore Texas home price growth (2010–2019) |
| 4 | Case study: Dallas 2020 single-city deep dive |
| 5 | Multi-city, multi-year analysis (2010–2019) |
| 6 | Calculate R/u ratio and classify pricing regimes |
| 7 | Visualize R/u ratio over time with regime shading |
| 8 | Summary, interpretation, and conclusion |
| 9 | Sensitivity analysis on the depreciation constant `d` |

---

## Setup

This notebook runs in **Google Colab**.

1. Clone or download this repository
2. Download the three datasets from the links above
3. Upload them to Google Drive under:
   ```
   MyDrive/Datasets/Zillow_Research/Metro_zhvi_uc_sfrcondo_tier_0.33_0.67_sm_sa_month.csv
   MyDrive/Datasets/Zillow_Research/Metro_zori_uc_sfrcondomfr_sm_sa_month.csv
   MyDrive/Datasets/Zillow_Research/MORTGAGE30US.csv
   ```
4. Open `housing_market_analysis.ipynb` in Google Colab
5. Run all cells in order

**Dependencies:** `pandas`, `matplotlib` — both are pre-installed in Google Colab.

---

## Results

Of 40 total city/year combinations analyzed:

| Regime | Count |
|---|---|
| Speculation-dominated (`g_actual > r + d`) | 24 |
| No rent data available | 11 |
| Undervalued (valid R/u > 1) | 5 |

The 5 valid R/u observations — Houston 2015–2016, Austin 2015, San Antonio 2015 and 2019 — all showed R/u ratios well above 1 (ranging ~3–7), indicating homes were meaningfully undervalued relative to rents in those windows, consistent with the strong appreciation that followed.

---

## Next Steps

- Acquire or impute Dallas rent data pre-2014 to complete the full analysis window
- Extend analysis post-2019 to capture the COVID-era housing surge and subsequent correction
- Compare Texas metros to the national average using the `United States` row in ZHVI

---

## Tools & Skills Demonstrated

`Python` · `pandas` · `matplotlib` · `Google Colab` · `data wrangling` · `economic modeling` · `sensitivity analysis` · `multi-source data integration`
