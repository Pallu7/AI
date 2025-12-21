Power Outage Duration Prediction

Pallabi Lama

Power outages disrupt households, businesses, and critical infrastructure. Predicting
how long an outage will last can help utilities prioritize response and allocate crews
more effectively.
This project builds a machine learning regression model to predict outage duration (minutes)
using a real U.S. outage dataset (Event-correlated Outage Dataset in America, v1). The notebook
follows the full workflow required in AIT620: problem statement, data understanding, data
preparation, modeling, and evaluation.

Table of Content

- Problem  
- Data Understanding  
- Data Preparation  
- Modeling  
- Evaluation  
- References
  
Problem

Outages vary widely in duration depending on the type of event, severity, and response
conditions. Long outages cause major disruption and financial loss. The goal of this
project is to answer the question:
Can we predict the duration of a power outage (in minutes) using historical outage data?
This is a supervised learning regression problem where outage duration is the target variable.

Data Understanding

This project uses a real dataset: Event-correlated Outage Dataset in America (Outage Dataset v1.zip).
It contains aggregated and event-correlated outage information synthesized from multiple sources

The dataset is provided as a ZIP file containing multiple CSV files. The notebook downloads the ZIP,
selects a relevant CSV automatically, and then creates a machine learning dataset by:
- identifying duration (either an existing duration column or computed from start/end timestamps)
- selecting numeric features + low-cardinality categorical features
- cleaning missing/invalid duration values
  
Data Preparation

The dataset is prepared in a structured way to ensure it can be used for machine learning.
The following steps are performed:
1. Download the real dataset ZIP 
   The outage dataset is downloaded directly from the official hosting source to ensure the
   notebook uses real data and remains reproducible.
2. Extract and select a CSV file
   The ZIP file contains multiple CSV files. The notebook lists the files and automatically
   selects a relevant event/correlated outage CSV for analysis.
3. Create the target variable (outage duration in minutes)
   The target variable is defined as outage duration in minutes.  
   - If a duration column already exists, it is converted to numeric and used directly.  
   - If no duration column exists, duration is computed using start and end timestamps:
     \[
     \text{Duration (minutes)} = \frac{\text{End time} - \text{Start time}}{60}
     \]
4. Clean the target variable
   Records with missing duration values are removed. Any negative durations (invalid values)
   are also removed to keep the target variable reliable.
5. Build the feature set (input variables)
   Features are selected automatically to create a useful model input:
   - Numeric columns are kept as primary predictors.
   - Categorical columns are included only if they have low cardinality (limited unique values),
     so one-hot encoding does not create an extremely large number of features.
6. Create modeling datasets (X and y)
   Finally:
   - X is created as the feature matrix (predictor variables).
   - y is created as the target vector (outage duration in minutes).
This preparation ensures the dataset is clean, model-ready, and suitable for training and
evaluating a regression model.

Modeling

This project uses a Random Forest regression model. Random Forest works well for structured
tabular data, can model nonlinear relationships, and is robust to noisy real-world data.
A preprocessing pipeline is used to handle mixed feature types:
- Numeric features are scaled
- Categorical features are one-hot encoded (with unknown categories handled safely)
The model is trained on 80% of the data and tested on 20%.

Evaluation

The model is evaluated using common regression metrics:
- MAE (Mean Absolute Error)
- RMSE (Root Mean Squared Error)
- R² (explained variance)
A scatter plot of actual vs predicted duration is also included to visually check model performance.

References

Open Energy Information (OpenEI). (n.d.). Event-correlated outage dataset in the United States (Outage Dataset v1) [Data set]. U.S. Department of Energy. https://data.openei.org/submissions/6458
Géron, A. (2019). Hands-on machine learning with Scikit-Learn, Keras, and TensorFlow (2nd ed.). O’Reilly Media.
Scikit-learn developers. (n.d.). Scikit-learn documentation. https://scikit-learn.org

