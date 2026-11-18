# Hotel Harmony: Booking Analysis for Elite Hotels International

An exploratory data analysis (EDA) of 119,390 hotel bookings in Python. I cleaned the data, answered 25 business questions (basic, medium and advanced), and turned the results into clear recommendations on cancellations, pricing and marketing.

---

## Business problem

Elite Hotels International runs a **City Hotel** and a **Resort Hotel**. Management wants to understand booking patterns and guest behaviour so they can:

- cut cancellations
- plan staff and supplies for busy months
- price rooms better
- aim marketing at the right guests and channels

---

## Dataset

| Item | Detail |
|---|---|
| Source | [Hotel Booking Demand (Kaggle)](https://www.kaggle.com/jessemostipak/hotel-booking-demand) |
| Background | [Data in Brief article](https://www.sciencedirect.com/science/article/pii/S2352340918315191) |
| Rows | 119,390 bookings (87,228 after cleaning) |
| Columns | 32 |
| Hotels | City Hotel and Resort Hotel |
| Arrival dates | July 2015 to August 2017 |
| Price column | `adr` = average daily rate (price per night, in euro) |

---

## Tools

Python, pandas, NumPy, Matplotlib, Seaborn, statsmodels, Google Colab

---

## Project workflow

```
Load data  ->  Clean data  ->  EDA steps  ->  25 questions  ->  Conclusion
```

---

## Data cleaning

| Step | What I did | Rows affected |
|---|---|---|
| Missing values | `children`, `agent`, `company` filled with 0 (0 = none). `country` filled with "Unknown" | 4 / 16,340 / 112,593 / 488 |
| Dates | Turned text dates into real dates. Joined arrival year, month and day into one date column | all rows |
| Duplicates | Removed exact copies of a row | 31,994 |
| Impossible values | Removed bookings with 0 guests, one negative ADR and one ADR of 5,400 | 166 + 2 |
| Column fixes | `meal` "Undefined" changed to "SC" (same meaning). Decimal columns changed to whole numbers | n/a |
| New columns | `total_nights`, `total_guests`, `revenue` (ADR x nights), `season` | n/a |
| Outliers | Checked with box plots and kept them, because long lead times and long stays are real bookings | n/a |

**Result:** 119,390 rows became 87,228 rows, with no missing values left.

---

## Questions solved

| Level | Questions | Examples |
|---|---|---|
| Basic | 10 | Average lead time, number of cancellations, top country, ADR per hotel, parking demand |
| Medium | 10 | Cancellation rate per hotel, ADR per market segment, lead time vs cancellation, revenue by month, ADR trend |
| Advanced | 5 | Logistic regression for cancellation drivers, regression of ADR on guest numbers, seasonal cancellations, lead time by market segment |

All code and answers are in [`Hotel_Operations_EDA.ipynb`](Hotel_Operations_EDA.ipynb).

---

## Key numbers

| Metric | Value |
|---|---|
| Total bookings (cleaned) | 87,228 |
| Cancellation rate | 27.5% |
| Average lead time | 80 days (median 49) |
| Average stay | 3.63 nights |
| Average ADR | 106.46 euro |
| Revenue from completed stays | about 23.0 million euro |
| Special requests per booking | 0.70 |

---

## Key findings

**1. City Hotel is busier, Online TA brings most bookings, and August is the peak month.**
City Hotel gets 61% of bookings. Online travel agents (Online TA) bring 59% of all bookings. August has the most arrivals and the most revenue.


**2. The earlier a guest books, the more likely they cancel.**
Only 8% of bookings made within a week are canceled, compared with about 40% of bookings made more than 180 days ahead.


**3. City Hotel cancels more but earns more per night.**
Cancellation rate is 30.1% at the City Hotel and 23.5% at the Resort Hotel. Average ADR is 111 euro vs 99 euro.

**4. Resort Hotel prices swing with the season.**
The Resort averages about 49 euro in January and 188 euro in August. The City Hotel stays between about 85 and 128 euro all year. July-August prices were about 33% higher in 2017 than in 2015.


**5. Repeat guests and guests with special requests are more reliable.**
Repeat guests cancel much less. Cancellations fall from 33% (no special requests) to 6-11% (four or five requests).

**6. Cancellation drivers (logistic regression).**
Non-refundable deposits, previous cancellations, long lead time and higher ADR push cancellations up. Repeat guests, special requests and booking changes push them down. The model gets 75.3% of bookings right, against 72.5% for always guessing "not canceled", so it is useful for understanding drivers, not for predicting single bookings.


**7. Other results.**
Portugal is the top country (31% of bookings). Room type A is booked most (65%). 86% of bookings come through a travel agent. 8.4% of bookings need parking. Each child adds about 39 euro per night and each adult about 21 euro. Repeat guests stay about half as long as new guests (1.95 vs 3.70 nights).

---

## Recommendations

1. **Cut cancellations.** Ask for a deposit or send a reconfirmation message for bookings made 90+ days ahead. Keep a small overbooking buffer for July-August, when cancellations peak at about 32%.
2. **Plan for peak season.** Schedule staff and supplies around July-August. Run offers in November-February, when demand and prices are lowest.
3. **Grow direct bookings.** Direct earns almost the same per night as Online TA (117 vs 118 euro), and Online TA is 59% of all bookings, which is a lot to depend on.
4. **Price by season and guest mix.** Keep high summer prices at the Resort Hotel and offer family packages, since children raise ADR the most.
5. **Reward repeat guests** with short-stay and weekend offers.
6. **Focus marketing** on the top 5 countries (Portugal, UK, France, Spain, Germany), about 68% of bookings.

---

## Limits and next steps

- The data has no guest rating, so satisfaction was only estimated from special requests and cancellations. Review scores would answer this properly.
- Non-refundable bookings show a 95% cancellation rate. This looks odd and should be checked with the booking team.
- Duplicate rows were removed on the assumption that they were repeats.
- Only July and August appear in all three years, so yearly trends are limited.
- Next: compare reserved vs assigned room type, and build a Power BI dashboard from the cleaned data.

---
