# Hotel Booking Analysis & Cancellation Prediction

## Project Overview

Revenue optimization and demand forecasting are critical priorities for the hospitality industry. This project presents a comprehensive **Exploratory Data Analysis (EDA)** and **Predictive Modeling** study of hotel booking records (87,396 entries) spanning City Hotels and Resort Hotels. The study examines booking patterns, cancellation drivers, revenue trends, and guest behavior across multiple market segments.

As a **Business and Data Analyst**, the objective was to convert raw reservation data into strategic insights that help hotel operators minimize cancellation losses, optimize pricing, and better understand guest preferences.

---

## Business & Hospitality Objectives

The analysis seeks to provide data-backed answers to the following critical questions:

1. **Cancellation Risk:** What are the strongest predictors of booking cancellations — and how does lead time, deposit type, and special requests affect cancellation probability?
2. **Revenue Analysis:** Which months and hotel types generate the highest Average Daily Rate (ADR) and total revenue?
3. **Market Segmentation:** How do different market segments (Online TA, Corporate, Direct, etc.) differ in lead times and booking volumes?
4. **Guest Behavior:** How do repeated guests differ from new guests in terms of stay duration, and what proportion of bookings require parking or make special requests?
5. **Pricing Drivers:** How do guest composition (adults, children, babies) influence the ADR through multiple regression modeling?

---

## Dataset Description

The analysis is based on a hotel bookings dataset with **87,396 records** and **33 key attributes**, including:

| Feature | Description |
| --- | --- |
| `hotel` | Hotel type: City Hotel or Resort Hotel. |
| `is_canceled` | Booking cancellation status (1: Canceled, 0: Not Canceled). |
| `lead_time` | Number of days between booking date and arrival date. |
| `arrival_date_month` | Month of arrival. |
| `arrival_date_year` | Year of arrival. |
| `stays_in_week_nights` | Number of weeknight stays. |
| `stays_in_weekend_nights` | Number of weekend night stays. |
| `adults` / `children` / `babies` | Composition of the guest party. |
| `market_segment` | Booking channel (e.g., Online TA, Corporate, Direct, Aviation). |
| `adr` | Average Daily Rate — revenue per occupied room per night (EUR). |
| `deposit_type` | Type of deposit made at booking. |
| `customer_type` | Classification of the booking customer. |
| `total_of_special_requests` | Number of special requests made by the guest. |
| `booking_changes` | Number of amendments made to the reservation. |
| `required_car_parking_spaces` | Whether parking was requested. |
| `country` | Country of origin of the guest. |
| `reservation_status_date` | Date of the last reservation status change. |

---

## Methodology & Technical Stack

### Technologies Used

- **Python:** Core language for all data processing and analysis.
- **Pandas:** Data loading, feature engineering (total stays, revenue per booking), aggregation, and cross-tabulation.
- **Matplotlib & Seaborn:** Scatter plots, bar charts, line plots, box plots, and pair plots for visual storytelling.
- **Scikit-learn:** Logistic Regression model training, one-hot encoding, train-test splitting, and classification metrics.
- **Statsmodels:** OLS Multiple Linear Regression for ADR prediction and statistical significance testing (p-values, R²).
- **SciPy:** Statistical correlation and hypothesis testing support.

### Analytical Workflow

1. **Data Loading & Feature Engineering:** Parsed `arrival_date` from year/month/day components. Computed `total_stays` and `revenue_per_booking` as derived features.
2. **Cancellation Analysis:** Profiled cancellation rates by hotel type, lead time (scatter), month, and number of special requests.
3. **Revenue & ADR Trends:** Tracked ADR over time (time series), per year, per hotel type, and by number of special requests.
4. **Market Segment Profiling:** Analyzed lead time distributions across segments and booking volumes by month and channel.
5. **Guest Behavior Analysis:** Compared average stay duration between new and repeated guests, assessed parking demand, and correlated booking changes with special requests.
6. **Logistic Regression (Cancellation Prediction):** Trained and evaluated a model on features including `lead_time`, `booking_changes`, `total_of_special_requests`, `hotel`, `market_segment`, `deposit_type`, and `customer_type`. Extracted feature coefficients using Statsmodels.
7. **Multiple Linear Regression (ADR Prediction):** Modeled ADR as a function of `adults`, `children`, and `babies` using OLS. Reported R², adjusted R², and p-values for each predictor.
8. **Visualization of Relationships:** Scatter plots for ADR vs. each guest composition variable; box plots for lead time by market segment.

---

## Key Insights (Executive Summary)

- **City Hotels Have Higher Cancellation Rates:** City Hotels show a 30.0% cancellation rate versus 23.5% for Resort Hotels, suggesting a difference in booking intent and customer profile.
- **Total Cancellations: 24,025** out of 87,396 bookings — over 27% of all reservations were ultimately canceled.
- **Lead Time Drives Cancellations:** Longer lead times are positively correlated with cancellation likelihood (coefficient: +0.006), meaning bookings made far in advance carry higher cancellation risk.
- **Special Requests Reduce Cancellations:** `total_of_special_requests` has the strongest negative coefficient (−0.65) in the logistic model, indicating that engaged guests with specific needs are far less likely to cancel.
- **August is the Peak Month** for both arrivals and revenue. August generated **€7.24M** in total revenue — more than double July's €5.86M.
- **Average Lead Time is 79.89 days**, giving hotels approximately an 11-week window for demand management and dynamic pricing.
- **ADR is Higher at City Hotels (€111.0 vs. €99.0)** compared to Resort Hotels, though Resort Hotels may compensate through longer average stays.
- **Average Stay Duration is 3.63 nights** overall (2.63 weeknights + 1.01 weekend nights), with repeated guests showing different stay patterns.
- **Portugal (PRT) is the Top Source Market**, accounting for the highest count of bookings in the dataset.
- **86.4% of bookings** were made through travel agents, underscoring the critical role of OTA and agent channels.
- **Only 8.37% of guests** required car parking, while the average number of special requests was 0.70 per booking.
- **Logistic Regression Accuracy: 76.7%**, with strong precision for non-canceled bookings (0.78) but weaker recall for cancellations (0.28) — suggesting a class imbalance challenge.
- **OLS R² = 0.165**, indicating that `adults`, `children`, and `babies` alone explain 16.5% of ADR variance — a meaningful signal but not sufficient as a standalone pricing model.

---

## Recommendations for GitHub Upload

Before publishing this project to GitHub, the following improvements are recommended to maximise usability, reproducibility, and professional quality.

### 1. Data Quality & Cleaning

- **Handle zero-guest bookings:** The dataset is known to contain rows where `adults`, `children`, and `babies` are all zero — logically invalid bookings that skew ADR and revenue calculations. Add a validation step that flags and removes these records, and log how many were dropped.
- **Cap extreme ADR outliers:** Outlier ADR values (e.g. €5,400/night) are present in this dataset and can distort regression models and revenue totals. Apply an IQR-based or percentile cap (e.g. top 1%) and document the threshold chosen, or at minimum visualise the ADR distribution before and after filtering.
- **Fix the `/content/` file path hardcode:** The notebook currently loads the dataset from `/content/hotel booking.csv` — a Google Colab-specific path. Replace this with a relative path (`data/raw/hotel_booking.csv`) so the notebook runs without modification on any machine.
- **Rename the dataset file:** `hotel booking.csv` contains a space, which can cause issues in shell scripts and some tools. Rename to `hotel_booking.csv` and update all references in the notebook.
- **Validate `arrival_date` reconstruction:** The date is parsed from three separate columns (`arrival_date_year`, `arrival_date_month`, `arrival_date_day_of_month`). Add a sanity check that the resulting `arrival_date` column contains no `NaT` values and that the date range (2015–2017) matches expectations before proceeding with time-series analysis.
- **Address missing values explicitly:** The dataset has known null entries in `children`, `country`, and `agent` columns. Add a dedicated cleaning cell that prints null counts per column, fills or drops them with documented rationale, and confirms the final row count.

### 2. Repository Structure

- **Move away from `/content/` (Colab) to a portable layout:** Structure the project so it runs identically locally, in Colab, and in CI. Use relative paths and a `data/` folder:

  ```
  ├── data/
  │   ├── raw/                    # hotel_booking.csv (or download instructions)
  │   └── processed/              # Cleaned dataset after pipeline runs
  ├── notebooks/
  │   └── hotel_booking_eda.ipynb
  ├── src/
  │   └── features.py             # total_stays, revenue_per_booking helpers
  ├── outputs/
  │   └── figures/                # Saved charts (ADR trend, cancellation rates, etc.)
  └── README.md
  ```

- **Rename the notebook:** `hotelbookingEDA.ipynb` lacks separators and has inconsistent casing. Rename to `hotel_booking_eda.ipynb` for readability and cross-platform compatibility.
- **Do not commit the raw CSV if it is large:** The hotel bookings dataset is ~7 MB. Add a download note in `data/raw/README.md` pointing to the Kaggle source, and add `data/raw/*.csv` to `.gitignore` to keep the repo lightweight.
- **Add a `.gitignore`:** Exclude `__pycache__/`, `.ipynb_checkpoints/`, `*.pyc`, `data/raw/*.csv`, and any virtual environment folders.

### 3. Documentation

- **Add a `requirements.txt`:** Pin the exact versions of all dependencies so the notebook is reproducible:

  ```
  pandas==2.x.x
  matplotlib==3.x.x
  seaborn==0.x.x
  scikit-learn==1.x.x
  statsmodels==0.x.x
  scipy==1.x.x
  ```

- **Add docstrings to feature engineering functions:** The `total_stays` and `revenue_per_booking` derivations should be documented with formulas — e.g. `total_stays = stays_in_week_nights + stays_in_weekend_nights`, `revenue_per_booking = adr × total_stays`. This makes the derived columns auditable.
- **Save all visualisations as image files:** Add `plt.savefig('outputs/figures/<chart_name>.png', dpi=150, bbox_inches='tight')` before each `plt.show()` call. This allows charts to be embedded in the README and reused in reports without re-running the notebook.
- **Embed key charts in the README:** Reference saved figures directly — for example, the ADR time-series and monthly revenue bar chart are strong visual hooks:

  ```markdown
  ![Monthly Revenue by Hotel Type](outputs/figures/monthly_revenue.png)
  ![Cancellation Rate by Lead Time](outputs/figures/cancellation_lead_time.png)
  ```

- **Add a model summary table to the README:** Include the logistic regression and OLS results in a compact table so readers can assess model quality at a glance without running the notebook:

  | Model | Target | Key Features | Accuracy / R² |
  |---|---|---|---|
  | Logistic Regression | `is_canceled` | Lead time, deposit type, special requests | 76.7% |
  | OLS Regression | `adr` | Adults, children, babies | R² = 0.165 |

### 4. Ethics, Privacy & Attribution

- **Cite the original dataset source:** The dataset is publicly available on Kaggle. Add the full attribution:
  > Antonio, N., de Almeida, A., & Nunes, L. (2019). *Hotel booking demand datasets.* Data in Brief, 22, 41–49. DOI: 10.1016/j.dib.2018.11.126. Available on Kaggle: https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand
- **Note the dataset's temporal scope:** The data covers 2015–2017. Hotel market dynamics, OTA dominance, and pricing norms have shifted since then — add a visible note in the README that findings reflect a historical window and are not representative of current hospitality conditions.
- **Flag country-level data sensitivity:** The `country` column contains guest country of origin. While anonymised at the individual level, aggregated country-of-origin statistics could be commercially sensitive. Note this in the disclaimer.
- **Add a `LICENSE` file:** Use **MIT License** for the analysis code and notebooks. Clarify that the license covers only your work, not the underlying dataset, which is governed by its own terms on Kaggle.

### 5. Model & Analysis Quality Improvements

- **Address the class imbalance in the logistic model:** The recall for cancellations is only 0.28 — the model is heavily biased toward predicting non-cancellation. Apply SMOTE oversampling or `class_weight='balanced'` in scikit-learn and report the updated classification report. This is the most impactful single improvement to the predictive model.
- **Add a confusion matrix visualisation:** A heatmap of the confusion matrix (`ConfusionMatrixDisplay` from scikit-learn) makes the 76.7% accuracy figure much more interpretable — readers can immediately see where the model fails.
- **Expand the ADR regression model:** An R² of 0.165 means guest composition alone explains very little of ADR variance. Add `hotel`, `arrival_date_month`, `market_segment`, and `lead_time` as additional predictors and report the improvement. This would make the regression section significantly more valuable.
- **Add feature importance or coefficient plot for the logistic model:** A horizontal bar chart of Statsmodels coefficients (with confidence intervals) visually communicates the relative importance of each cancellation predictor and is a standard inclusion in EDA-to-ML projects.
- **Report precision and recall separately for both classes:** The current metrics note strong precision for non-canceled bookings but weak cancellation recall. Include the full `classification_report` output (or a formatted table) in both the notebook and README so readers can assess business trade-offs (false negatives = undetected cancellations = lost revenue protection).
- **Add a lead time distribution plot by cancellation status:** A side-by-side histogram of lead times for canceled vs. non-canceled bookings would visually reinforce the `+0.006` lead-time coefficient finding and is a compelling chart for the README.

## Author

**[Mohd Faiz]**

- **Role:** Business and Data Analyst
- **GitHub:** [https://github.com/faizikbal01-lab](https://github.com/your-github-handle)

---

*Disclaimer: This analysis is based on a publicly available hotel bookings dataset and is intended for educational and research purposes only. Business decisions should not be made solely on the basis of this analysis.*

