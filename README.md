# OlaRideRequestDemandForecast

Ola Ride Request Demand Forecasting
This project aims to predict the number of Ola ride requests in a given location at a specific time interval, helping optimize driver allocation and improve operational efficiency. By forecasting demand accurately, this system can help reduce customer wait times and ensure better utilization of fleet resources.

🧠 Objective
To forecast the number of ride requests for specific pickup clusters (geographical latitude-longitude groupings) in 30-minute intervals across a year. The goal is to build a predictive model that minimizes the RMSE (Root Mean Squared Error) between actual and predicted demand.

📊 Dataset and Features
Data: Cleaned Ola ride request data over 366 days

Granularity: 30-minute time intervals

Spatial Clustering: KMeans used to cluster latitude-longitude into ~50 pickup clusters

Total Data Points: ~878,400 rows (366 days × 48 intervals × 50 clusters)

🔧 Feature Engineering
Three main iterations were used in the model development, each improving on the previous:

Iteration 1: Baseline Model

Features: pickup_cluster, mins, hour, month, quarter, dayofweek

Model: Linear regression followed by Random Forest

Observation: High bias and underfitting, random forest showed overfitting

Iteration 2: Lag Features

Added lag features (lag_1, lag_2, lag_3) to capture short-term temporal dependencies

Explored partial autocorrelation and autocorrelation plots (PACF & ACF) to justify lag selection

Switched to boosting techniques for better generalization

Iteration 3: Rolling Features

Final set of features:

bash
Copy
Edit
['pickup_cluster','mins','hour','month','dayofweek','quarter',
 'lag_1','lag_2','lag_3','rolling_mean']
rolling_mean: Rolling average of past 3 intervals

Model: XGBoost Regressor

Result: Best performance with RMSE significantly improved; model score ≈ 0.91

⚙️ Tools & Libraries Used
Python, Pandas, NumPy

Scikit-learn, XGBoost

Statsmodels (for ACF, PACF plots)

Matplotlib (for visualizations)

Joblib (for model serialization)

✅ Final Outcome
The model achieved a strong predictive accuracy with a score of 0.91, efficiently capturing demand trends.

It is capable of forecasting demand based on both temporal and spatial patterns, making it scalable for real-time driver allocation systems.

