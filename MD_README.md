Here’s a rewritten version that keeps everything you need but removes the dependency on creating a *Segment* field, while still making ROI a core dashboard and decision factor.

---

# **Top 50–100 U.S. Metropolitan Areas for Institutional Real Estate Investment — JP Morgan Lens**

---

## **1️⃣ Project Objective**

Build a **data-driven selection and ranking model** for U.S. metros that integrates **housing activity, affordability, income strength, and demographic momentum** — with **return on investment** (ROI) as a key driver in the analysis.

**Key business question:**

> *Which U.S. metropolitan areas in 2025 offer the strongest combination of liquidity, growth, yield, income strength, and long-term demand for large-scale real estate investment?*

**Final deliverable:**
An **interactive Tableau dashboard suite** for institutional real estate decision-making at JP Morgan, using KPI scores and ROI-focused visualizations instead of pre-set market segments.

---

## **2️⃣ Data Sources**

**From Realtor.com**

* **Hotness metrics**: `hot__hotness_rank`, `hot__hotness_score`, `hot__demand_score`, `hot__supply_score`
* **Price trends**: `hot__median_listing_price`, `hot__median_listing_price_mm`, `hot__median_listing_price_yy`
* **Days on Market (DOM)**: `hot__median_days_on_market`, `hot__median_days_on_market_mm`, `hot__median_days_on_market_yy`
* **Listing counts & pending ratios**: `inv__active_listing_count`, `inv__new_listing_count`, `inv__pending_ratio`
* **Price change shares**: `inv__price_increased_share`, `inv__price_reduced_share`

**From Numbeo**

* **Price to Income Ratio**: `numbeo__Price_To_Income_Ratio`
* **Gross Rental Yields**: `numbeo__Gross_Rental_Yield_City_Centre`, `numbeo__Gross_Rental_Yield_Outside_of_Centre`
* **Price to Rent Ratios**: `numbeo__Price_To_Rent_Ratio_City_Centre`, `numbeo__Price_To_Rent_Ratio_Outside_of_Centre`
* **Mortgage as % of Income**: `numbeo__MortgagePctIncome`
* **Affordability Index**: `numbeo__AffordabilityIndex`

**Added Data**

* **Median Household Income**: `Median_Household_Income`
* **Population (2020 & 2024)**: `Population_2020_Estimate`, `Population_2024_Estimate`
* **Population Growth %**: `Population_Percent_Change_2020_2024`

---

## **3️⃣ KPI Engineering**

| **Score**               | **Data Inputs**                                                                                                  | **Purpose**                                                     |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| **Liquidity Score**     | `inv__pending_ratio`, inverse of `hot__median_days_on_market`, `inv__active_listing_count`                       | Measures how quickly properties sell and market activity level. |
| **Growth Score**        | inverse of `hot__hotness_rank`, `hot__median_listing_price_mm`, `hot__median_listing_price_yy`                   | Tracks market appreciation trends.                              |
| **Yield Score**         | `numbeo__Gross_Rental_Yield_City_Centre`, `numbeo__Gross_Rental_Yield_Outside_of_Centre`, inverse of rent ratios | Shows rental return potential relative to property prices.      |
| **Affordability Score** | inverse of `numbeo__Price_To_Income_Ratio`, inverse of `numbeo__MortgagePctIncome`, `numbeo__AffordabilityIndex` | Identifies sustainable housing markets for buyers/renters.      |
| **Income Strength**     | `Median_Household_Income`                                                                                        | Reflects ability of residents to support housing costs.         |
| **Population Momentum** | `Population_Percent_Change_2020_2024`                                                                            | Captures demand growth potential.                               |

---

## **4️⃣ Tableau Dashboard Suite **

### **A. Market Opportunity Map** *(Best for big-picture ranking)*

* US map colored by **Composite Opportunity Score** (weighted mix of KPIs).
* Hover: All KPI values.
* Filters: Region, population tier, ROI score thresholds.

### **B. Liquidity & Risk Monitor** *(Best for timing entry/exit)*

* Line chart: `hot__median_days_on_market` over time.
* Bar chart: `inv__pending_ratio` vs. `inv__price_reduced_share`.
* Color by risk status (e.g., “fast-moving” vs. “slowing”).

### **C. Affordability & Growth Tracker** *(Best for sustainable growth)*

* Scatterplot: `Affordability_Score` vs. `Growth_Score`.
* Color by `Population_Percent_Change_2020_2024`.
* Size by `hot__median_listing_price`.

### **D. Yield & Income Playbook** *(Best for ROI)*

* Bubble chart: `Yield_Score` (x-axis) vs. `Median_Household_Income` (y-axis).
* Color by **ROI Composite Score** = `(Yield_Score + Income_Strength) / 2`.
* Size by `Population_Momentum`.
* Quadrants highlight:

  * High Yield / High Income = prime ROI
  * High Yield / Low Income = higher risk
  * Low Yield / High Income = stability over cash flow
  * Low Yield / Low Income = low priority

---

## **5️⃣ Extra Consultancy Deliverables**

* **Executive Summary PDF** — Top 20 ROI markets and top 20 overall opportunity markets.
* **Scenario Analysis** — How rising/falling interest rates could change scores.
* **Data Dictionary** — Definitions and sources for every KPI.
* **Quarterly Update Process** — Steps for refreshing KPIs and ROI ranking.

---

## **6️⃣ How We Get This Done**

1. **Data Prep:** Merge all Realtor.com, Numbeo, and extra datasets by metro name.
2. **KPI Calculation:** Apply z-score or min-max normalization to produce the 6 KPI scores.
3. **Composite Scores:** Create a Composite Opportunity Score and ROI Composite Score (Yield + Income Strength).
4. **Export:** Save the enriched dataset as a Tableau-ready CSV.
5. **Dashboard Build:**

   * Link KPI fields to visual elements
   * Use KPI-based colors instead of fixed segments
   * Create filters for ROI, liquidity, and growth thresholds
6. **Testing:** Validate tooltips, filters, and score distributions.
7. **Presentation:** Walk JP Morgan through how each dashboard answers a different investment question, with ROI Playbook as the go-to for maximizing returns.

---

If you’d like, I can now prepare **the exact ROI Composite Score code and Tableau calc fields** so you can skip manual formula setup and just focus on building visuals. That way, the ROI dashboard works immediately without any segmentation logic.
