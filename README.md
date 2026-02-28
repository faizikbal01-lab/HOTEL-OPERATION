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

## How to Run

1. **Clone the Repository:**
   ```bash
   git clone <your-repo-url>
   ```

2. **Install Dependencies:**
   ```bash
   pip install pandas seaborn matplotlib scikit-learn statsmodels scipy
   ```

3. **Add the Dataset:** Place `hotel booking.csv` in the `/content/` directory (or update the file path in the notebook accordingly).

4. **Open the Notebook:** Run `hotelbookingEDA.ipynb` cell by cell to reproduce the full analysis, visualizations, and model outputs.

---

## Author

**[Mohd Faiz]**

- **Role:** Business and Data Analyst
- **GitHub:** [https://github.com/faizikbal01-lab](https://github.com/your-github-handle)

---

*Disclaimer: This analysis is based on a publicly available hotel bookings dataset and is intended for educational and research purposes only. Business decisions should not be made solely on the basis of this analysis.*

