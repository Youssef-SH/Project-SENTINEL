# **Fire Prediction Model Prototype**

### Project SENTINEL - Wildfire Prediction

## Overview

This prototype model is part of **Project SENTINEL** and is designed to predict wildfire occurrences and severity (in terms of area burned) in California using historical fire records and climate data. The primary goals are:
1. **Classification**: Predict whether a wildfire will occur in a given location and time.
2. **Regression**: Predict the area affected by wildfires if a fire occurs (still under construction and not yet integrated).

The model uses both historical wildfire data and climate information from nearby weather stations to build accurate predictions that can aid disaster preparedness.

## Project Structure

- `fire_model.py`: Main code for data preprocessing, model training, and evaluation.
- `data/`: Contains the wildfire and weather datasets (`California_Wildfire_Records_23.csv` and `CA_Multistation_ClimaticData.csv`).
- `fire_occurrence_classifier.pkl`: Saved classification model to predict fire occurrence.
- `README.md`: Detailed explanation of the model's purpose, methodology, and usage.

## Dataset Description

### 1. California Wildfire Records
This dataset includes historical records of wildfires in California. Key columns used include:
- **DATE**: Start date of the wildfire.
- **LOCATION**: Location of the wildfire.
- **AREA_SQUARE_KM**: Area affected by the wildfire in square kilometers.
  
### 2. Multistation Climate Data
This dataset provides historical climate data from various weather stations. Key features include:
- **Avg Max Air Temp (C)**: Average maximum air temperature.
- **Total Precip (mm)**: Total precipitation.
- **Avg Wind Speed (m/s)**: Average wind speed.

## Data Preprocessing

The model undergoes several preprocessing steps:

1. **Data Cleaning**:
   - Dropped irrelevant columns.
   - Converted dates to datetime formats and estimated missing dates based on historical averages.
   - Mapped wildfire locations to nearby weather stations for climate data association.

2. **Outlier Handling and Imputation**:
   - Identified and retained extreme wildfire cases as they provide important insights for severe conditions.
   - Interpolated missing climate values using linear interpolation.
   - Removed outliers based on domain knowledge (e.g., unrealistic precipitation or temperature values).

3. **Feature Engineering**:
   - One-hot encoding for locations.
   - Cyclical encoding for months to capture seasonality.
   - Aggregated fire events by month-year to align with climate data granularity.

## Model Training

### Classification Model

A **Gradient Boosting Classifier** is trained to predict fire occurrence. This model uses features such as air temperature, precipitation, wind speed, and month-seasonality indicators. The data was balanced using **SMOTE** to handle class imbalance between fire and non-fire events.

- **Cross-Validation Accuracy**: Average accuracy achieved using time series cross-validation.
- **Test Set Accuracy**: Final accuracy on the test set.

### Regression Model (Under Construction)

A **Gradient Boosting Regressor** is being developed to predict the fire area if a wildfire occurs. This model is still under construction and not yet integrated into the prototype.

## Evaluation

### Classification Metrics
- **Confusion Matrix**: Visualizes true positives, true negatives, false positives, and false negatives.
- **Classification Report**: Provides precision, recall, F1-score, and support for each class.
  
### Model Interpretability
- **SHAP (SHapley Additive exPlanations)**: Used to interpret feature importance in the classifier, helping to understand which climate and time-based features contribute most to fire predictions.

## Installation and Usage

1. **Requirements**:
   - Install the required libraries using:
     ```bash
     pip install pandas numpy scikit-learn matplotlib seaborn joblib shap geopy imbalanced-learn
     ```

2. **Run the Model**:
   - To train or test the model, load `fire_model.py` and follow the functions as structured in the code.

3. **Using the Saved Model**:
   - Load `fire_occurrence_classifier.pkl` to make predictions on new data:
     ```python
     import joblib
     classifier = joblib.load('fire_occurrence_classifier.pkl')
     ```

## Results and Visualizations

- **Distribution Plots**: Visualized the distributions of key features and target variables.
- **Scatter Plots**: Explored relationships between weather features and fire occurrence/severity.
- **Box Plots**: Identified and confirmed the importance of severe cases in the dataset.

