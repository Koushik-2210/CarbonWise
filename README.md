# CarbonWise: Machine Learning for Sustainable Business Travel

## Overview

**CarbonWise** is a machine learning project that predicts whether a business trip is likely to be **High Carbon** before the trip is booked.

The goal is to use historical business travel and process data to identify patterns associated with high-carbon travel and support more sustainable travel decisions.

This project was developed as part of a sustainability capstone focused on reducing **Scope 3 business travel emissions** and supporting an organization's **Net Zero 2030** goals.

## Problem Statement

Business travel can contribute significantly to an organization's Scope 3 emissions. However, emission-related information is often available only after travel has occurred.

CarbonWise addresses this problem by predicting the likelihood of a trip being **High Carbon (1)** or **Low Carbon (0)** using information available before or during the travel process.

## Dataset

The project uses business travel data containing features such as:

* Departure and arrival countries and cities
* Transportation type
* Transportation description
* Travel purpose
* Business unit
* Out-of-policy status
* Hotel nights
* Travel costs
* Process/event information

### Target

`HighCarbon`

* `0` → Low Carbon
* `1` → High Carbon

CO₂-related columns that directly reveal the target were excluded from model training to prevent data leakage.

## Approach

The project follows the following workflow:

1. **Data Exploration**

   * Examined feature distributions and class balance.
   * Identified important patterns associated with High Carbon trips.

2. **Feature Engineering**

   * Processed travel and categorical features.
   * Added trip-level features derived from event logs.

3. **Model Development**

   * Used **CatBoost Classifier** for binary classification.
   * CatBoost was selected because of its strong performance with categorical features.

4. **Model Evaluation**

   * Used **Stratified 5-Fold Cross-Validation**.
   * Primary evaluation metric: **ROC-AUC**.

5. **Prediction**

   * Trained the final model using the complete training dataset.
   * Generated probability predictions for the private test dataset.

## Results

The final CatBoost model achieved:

| Metric              |      Result |
| ------------------- | ----------: |
| 5-Fold Mean ROC-AUC | **0.99939** |
| Standard Deviation  | **0.00007** |

The extremely low standard deviation indicates that the model produced highly consistent performance across the five validation folds.

### Important Features

The most influential features identified by the model included:

1. `ShippingType`
2. `ArrivalLocationCountry`
3. `DepartureLocationCity`
4. `HotelNights`
5. `ShippingTypeDescription`
6. `ArrivalLocationCity`
7. `DepartureLocationCountry`

## Submission

The final predictions are probability scores between **0 and 1**.

The submission contains:

```text
TripID,HighCarbon
```

where `HighCarbon` represents the predicted probability that a trip belongs to the High Carbon class.

## Project Structure

```text
CarbonWise/
│
├── EDA_and_Model.ipynb
├── README.md
├── requirements.txt
└── submission.csv
```

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* CatBoost
* Matplotlib
* Seaborn
* Jupyter Notebook

## Key Takeaway

CarbonWise demonstrates how machine learning can move sustainability analysis from **post-trip measurement** toward **proactive decision-making**, allowing organizations to identify potentially high-carbon business travel before it occurs.

---

### Author

**Koushik**
