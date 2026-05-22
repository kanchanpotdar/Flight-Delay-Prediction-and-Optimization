# Flight Delay Prediction & Intelligent Rescheduling System

A complete end-to-end Data Analytics and Machine Learning project focused on predicting airline delays and optimizing flight rescheduling using ensemble learning, statistical preprocessing, and operational constraints. This project was developed as part of Open IIT Data Analytics 2024 by Team D-33.

---

# Overview

Airline delays create operational inefficiencies, passenger dissatisfaction, airport congestion, and financial losses for airlines. This project aims to address these challenges through two major components:

- Flight Delay Prediction
- Optimized Flight Rescheduling

The system analyzes historical airline operational data, weather conditions, airport traffic, staffing availability, and flight-level attributes to forecast delays and intelligently reschedule flights under real-world operational constraints.

---

# Features

## Predictive Analytics
- Flight delay forecasting using ensemble machine learning
- Stacked regression architecture
- Hyperparameter optimization using RandomizedSearchCV
- Feature engineering and preprocessing pipeline
- Outlier detection and handling

## Operational Optimization
- Intelligent flight rescheduling
- Delay reduction strategies
- Weather-aware scheduling
- Staff availability constraints
- Aircraft conflict avoidance
- Distance-based threshold optimization

## Data Analytics & Visualization
- Exploratory Data Analysis (EDA)
- Geographic delay visualization
- Weather impact analysis
- Air traffic correlation analysis
- Delay distribution analysis
- Scaled data visualization

---

# Problem Statement

With the increasing popularity of air travel, flight delays have become a major operational issue. Delays affect:

- Airline operational costs
- Passenger experience
- Airport efficiency
- Crew scheduling
- Aircraft utilization

This project focuses on building a predictive system capable of:
1. Forecasting future delays
2. Minimizing disruptions through optimized rescheduling

The final goal is to improve operational resilience and reduce overall delay propagation across airline networks.

---

# Dataset

The dataset contains operational airline data along with environmental and logistical factors affecting departure delays.

## Important Feature Categories

### Temporal Features
- Month
- Day of Month
- Day of Week

### Flight & Carrier Features
- Airline carrier
- Tail number
- Connecting flights

### Airport Operations
- Air traffic
- Ground staff availability
- Fuel availability
- Late arrivals from previous airports

### Passenger Features
- Passenger footfall
- Percentage of late passengers

### Weather Features
- Temperature
- Humidity
- Wind speed
- Wind gust
- Weather condition
- Dew point

### Flight Stage Features
- Departure delay
- Taxi-out time
- Scheduled departure time
- Flight duration

---

# Exploratory Data Analysis (EDA)

The project includes extensive exploratory analysis to understand the major contributors to flight delays.

## Key Insights

### Weather vs Delay
Severe weather conditions such as:
- Heavy rain
- Fog
- Strong wind

show significantly higher departure delays compared to clear weather conditions.

### Daily Delay Variability
Departure delays fluctuate heavily across days, indicating the influence of:
- Operational issues
- Weather conditions
- Demand surges
- Traffic congestion

### Geographic Delay Analysis
Choropleth visualizations revealed certain cities and airports consistently experiencing higher delays due to:
- Congestion
- Air traffic load
- Airport operational inefficiencies

### Air Traffic Correlation
Air traffic volume alone does not strongly determine delays, suggesting multiple interacting factors influence departure punctuality.

### Distance & Wind Impact
Longer flight distances combined with higher wind speeds correlate with increased delays.

---

# Data Preprocessing

A robust preprocessing pipeline was implemented to prepare the dataset for machine learning.

## Missing Value Handling

### Median Imputation
Used for numerical features where outliers could distort the mean.

### Zero Imputation
Applied where missing values represented the absence of a condition or event.

---

## Categorical Encoding

Label Encoding was applied to categorical columns such as:
- Airline carrier
- Wind condition
- Weather condition

This enabled machine learning models to interpret categorical information effectively.

---

## Normalization Techniques

Different normalization techniques were selected based on feature skewness:

| Method | Usage |
|---|---|
| Z-Score Normalization | Normally distributed data |
| Yeo-Johnson Transformation | Moderately skewed data |
| Log Transformation | Highly positively skewed data |

---

# Outlier Detection

Outliers were handled using the Interquartile Range (IQR) method.

## IQR Formula

```math
IQR = Q_3 - Q_1
```

Outliers were identified using:

```math
x < Q_1 - 1.5(IQR)
```

or

```math
x > Q_3 + 1.5(IQR)
```

---

## Outlier Handling Strategy

Instead of removing extreme values entirely, the project used:
- Lower-bound capping
- Upper-bound capping

This preserved dataset size while reducing skewness and preventing instability during training.

---

# Machine Learning Models

The project uses an ensemble learning approach combining multiple gradient boosting models.

## Models Used

### XGBoost
- Strong performance on structured data
- Handles complex nonlinear relationships
- Robust to noise

### LightGBM
- Fast training
- Efficient memory usage
- Optimized for large datasets

### CatBoost
- Excellent handling of categorical features
- Reduces overfitting
- Stable on heterogeneous data

---

# Stacked Ensemble Architecture

The final prediction system uses a Stacking Regressor.

## Base Models
- XGBoost
- LightGBM
- CatBoost

## Meta Learner
- Linear Regression

The stacking approach improves:
- Generalization
- Stability
- Predictive accuracy
- Robustness across operational scenarios

---

# Model Performance

| Metric | Value |
|---|---|
| MAE | 3.04 |
| RMSE | 12.29 |
| R² Score | 0.896 |

The model explains approximately 89.6% of delay variability.

---

# Hyperparameter Tuning

Hyperparameter optimization was performed using:
- RandomizedSearchCV
- 3-Fold Cross Validation
- Negative Mean Squared Error scoring

## Tuned Parameters

### XGBoost
```python
{
    "subsample": 1,
    "n_estimators": 200,
    "max_depth": 10,
    "learning_rate": 0.1
}
```

### LightGBM
```python
{
    "num_leaves": 50,
    "n_estimators": 50,
    "min_child_samples": 10,
    "max_depth": 10,
    "learning_rate": 0.2
}
```

### CatBoost
```python
{
    "n_estimators": 150,
    "learning_rate": 0.1,
    "depth": 10
}
```

---

# Flight Rescheduling System

Beyond prediction, the project includes a rescheduling optimization engine.

## Objective

Reduce total departure delays by dynamically adjusting schedules based on:
- Weather conditions
- Distance thresholds
- Staff availability
- Aircraft scheduling conflicts

---

# Delay Multiplier Logic

Delay multipliers are computed using grouped historical delay patterns.

## Delay Multiplier Formula

```math
Delay\ Multiplier = \frac{Mean\ Group\ Delay}{Overall\ Mean\ Delay}
```

The multiplier is calculated using:
- Weather condition
- Air staff availability
- Ground staff availability
- Flight distance

Missing combinations are assigned a default multiplier of `0.5`.

---

# Operational Constraints

The rescheduling engine considers:

## Weather Constraints
Ensures safe departure and landing conditions.

## Distance Thresholds
Avoids impractical rerouting.

## Staff Constraints
Checks sufficient:
- Air staff
- Ground staff

## Aircraft Conflict Avoidance
Ensures aircraft availability and avoids overlapping schedules.

---

# Threshold Optimization

Quantiles were used to generate adaptive thresholds.

## Optimal Thresholds

| Parameter | Value |
|---|---|
| Distance Threshold | 2248 |
| Air Staff Threshold | 6 |
| Ground Staff Threshold | 22 |

## Maximum Delay Reduction Achieved

```math
8800.5
```

---

# Tech Stack

## Languages
- Python

## Libraries
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- LightGBM
- CatBoost
- Matplotlib
- Seaborn
- Plotly

## ML Techniques
- Ensemble Learning
- Stacking Regression
- Hyperparameter Tuning
- Outlier Detection
- Feature Engineering

---

# Project Workflow

```text
Data Collection
      ↓
Data Cleaning
      ↓
EDA & Visualization
      ↓
Feature Engineering
      ↓
Normalization & Encoding
      ↓
Outlier Handling
      ↓
Model Training
      ↓
Hyperparameter Tuning
      ↓
Stacked Ensemble
      ↓
Delay Prediction
      ↓
Flight Rescheduling Optimization
```

---

# Results

The project successfully:
- Predicted flight delays with high accuracy
- Reduced operational uncertainty
- Built an adaptive rescheduling framework
- Demonstrated practical airline optimization strategies

The ensemble model significantly outperformed standalone models in robustness and generalization.

---

# Future Improvements

- Real-time flight tracking integration
- Live weather API integration
- Deep learning sequence models (LSTM/Transformer)
- Reinforcement learning for scheduling optimization
- Multi-airport network optimization
- Passenger disruption minimization

---

# Team

Team D-33  
Open IIT Data Analytics 2024

---

# References

- XGBoost Documentation
- LightGBM Documentation
- CatBoost Documentation
- Scikit-learn Documentation
- FAA Flight Delay Data
- Airline Operational Research Papers

---

# License

This project is intended for educational and research purposes.
