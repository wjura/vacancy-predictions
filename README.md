# Time Series Vacancy Prediction for UBC Student Housing

## Project Goals
The goal of my project is to predict vacancies in student housing to optimize occupancy, improve resource planning, and maximize revenue. 
I chose this project because I work in student housing management, and this is a challenge I often face. I wanted to apply the skills I’ve gained during my data science program to address this real-world problem.

## Process

### Data Preparation ()

Data Collection: Gathered data on vacancies by concatenating multiple reports into a single combined file.
Missing Values Check: Inspected for and handled missing values in the dataset.

### Data Cleaning ()

Error Record Removal: Identified and removed erroneous records (e.g., buildings marked as fully vacant before their actual existence).
Datetime Conversion: Converted date column to a consistent datetime format.
Room Type Aggregation: Simplified and aggregated room types into more general categories for analysis.
Exploratory Data Analysis: Visualized data to uncover trends, seasonal patterns, and anomalies.

### Data Aggreggation ()

By Area: Aggregated data by date for each area individually.
Daily Vacancies: Summed up all areas and calculate total vacancies per day.

### Model Development

General Prophet Model: Created a single Prophet model to analyze all areas combined.
Separate Area Models: Developed individual models for each area to capture localized trends.

Column Renaming: Renamed columns to fit Prophet's required format: ds for the timestamp; y for the target variable (vacancies).
Holidays Definition: Marked contract turnover dates as holidays to account for their impact.
Additional Regressor: Incorporated the end-of-month indicator as a regressor to improve model accuracy.

Model Training and Evaluation
Baseline Model: Created an initial baseline model for comparison.
Future Predictions: Generated predictions for future vacancies using the baseline model.
Clipping Negative Values: Ensured predictions did not go below zero by applying clipping.
Cross-Validation: Validated the model's accuracy and performance over different time windows.
Hyperparameter Tuning: Iteratively optimized key parameters:
    changepoint_prior_scale
    seasonality_prior_scale
    yearly_seasonality

Model Evaluation:
Evaluated the performance of the tuned model using selected metrics, such as RMSE, to ensure improvements over the baseline.

## Results

Evaluation metric used for the model:  

The Root Mean Square Error (RMSE) was chosen as the evaluation metric because it is highly sensitive to large errors, making it an excellent choice for this context. Large prediction errors in vacancy forecasting can lead to significant operational challenges, such as over- or underestimating the need for housing staff or resources. RMSE emphasizes larger errors more than smaller ones, ensuring the model prioritizes avoiding costly mistakes.

Baseline model:  
Initially, the baseline model seemed to perform well. However, evaluation revealed significant discrepancies between its predictions and actual vacancy numbers, with an average RMSE error of approximately 245 vacancies. While the model performed fairly well on the training data, it struggled to forecast future vacancies accurately, especially during the high turnover peak around May.

The uncertainty interval, visualized as the shaded region around the prediction line, was significantly wider for the forecast compared to the training data. This indicated the model was less confident in its future predictions, reflecting its limitations in generalizing beyond the training set.

Model after hyperparameter tuning: 
Best Parameters Identified:

changepoint_prior_scale: 0.001 - Adjusts the model's flexibility in detecting changepoints, allowing it to capture subtle trend changes.
seasonality_prior_scale: 1 - Controls the strength of the seasonality component in the model, balancing its influence.
yearly_seasonality: 20 - Specifies the complexity of the yearly seasonal pattern by determining the number of Fourier terms.

After tuning, the model's future predictions improved significantly. The uncertainty interval became narrower, indicating increased confidence in the forecasts. While the model is not yet perfect, the improvements are notable. The average RMSE error decreased by 60%, dropping to approximately 79 vacancies. This demonstrates the value of fine tuning in enhancing the model's accuracy and reliability.


## Future Goals

- Predicting vacancies using more features, such as room type;
- Exploring the actual impact on revenue and including that in the forecast;
- Comparing with other models, like SARIMA;
- Predicting how long it takes for a specific room in student housing to become vacant, which could be particularly useful for students, as many have preferences for specific areas, floors, or sides of the building. 
- Deploying the best model in a user-friendly environment where users can easily input their preferences and get predictions