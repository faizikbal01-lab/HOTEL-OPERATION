

# 🏨 Hotel Booking Analysis & Cancellation Prediction

Exploratory data analysis and machine learning on hotel booking data to uncover cancellation patterns and predict which bookings are likely to cancel — helping hotels reduce revenue loss.

---

## 📊 Key Results

| Model | Accuracy |
|---|---|
| Logistic Regression | ~80% |
| Multiple Linear Regression (ADR) | statsmodels OLS |

**Top cancellation predictors:** `deposit_type`, `lead_time`, `market_segment`, `total_of_special_requests`

---

## 🔍 What's Inside

- **EDA** — Cancellation rates by hotel type, month, market segment, room type, country
- **Revenue Analysis** — ADR trends over time, monthly revenue patterns
- **Logistic Regression** — Predict booking cancellations with feature significance (p-values)
- **Multiple Regression** — Model ADR based on guest composition (adults, children, babies)
- **Visualizations** — Scatter plots, bar charts, box plots, line graphs

---

## 🗂️ Project Structure

```
Hotel_Booking_Analysis/
│
├── hotel_booking_analysis.ipynb   # Main notebook (all analysis + models)
├── hotel booking.csv              # Dataset (place in same directory)
└── README.md
```

---

## ⚙️ Requirements

- Python 3.8+
- Jupyter Notebook or Google Colab

---

## 🚀 Getting Started

**1. Clone the repository**
```bash
git clone https://github.com/your-username/hotel-booking-analysis.git
cd hotel-booking-analysis
```

**2. Install dependencies**
```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels jupyter
```

**3. Add the dataset**

Place `hotel booking.csv` in the root project folder (same level as the notebook).

> 📥 Dataset source: [Kaggle - Hotel Booking Demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand)

---

## 💡 Key Findings

- **City hotels** have a significantly higher cancellation rate than resort hotels
- **Longer lead times** strongly correlate with higher cancellation probability
- **No-deposit bookings** cancel far less than non-refundable ones
- **August** is the peak arrival month; **January** sees the lowest bookings
- **Guests with more special requests** are less likely to cancel

---

## 📌 Recommendations for Improvement

- [ ] Add Random Forest / XGBoost for better prediction accuracy
- [ ] Build a confusion matrix and ROC-AUC curve for model evaluation
- [ ] Deploy as a simple web app (Streamlit) for real-time prediction
- [ ] Add feature importance plot to replace raw coefficients
- [ ] Include a `requirements.txt` file for one-command installs

---

## Author

**[Mohd Faiz]**

- **Role:** Business and Data Analyst
- **GitHub:** [https://github.com/faizikbal01-lab](https://github.com/your-github-handle)

---

*Disclaimer: This analysis is based on a publicly available hotel bookings dataset and is intended for educational and research purposes only. Business decisions should not be made solely on the basis of this analysis.*

