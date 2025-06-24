# Churn Prediction using Machine Learning 

# Objective

Develop a model capable of predicting whether a customer of the telecommunications company "Interconnect" plans to cancel their service. This will enable the company to implement retention strategies, such as personalized offers or special promotions.

## Exploratory Data Analysis (EDA)

During the exploratory analysis, the following insights were identified:

Users with shorter tenure are more likely to cancel the service.

Missing values were detected in columns related to contracted services; these were replaced with "0", assuming the customer did not sign up for those services.

Categorical variables were transformed into numerical and mostly binary format, since many of them represented yes/no responses or the presence/absence of a feature.


## Data Cleaning and Preparation

Once the data was merged and cleaned into a single DataFrame, the correlation between predictor variables and the target variable Churn was analyzed. A strong negative correlation was found with the 'TenureMonths' variable, which led to its exclusion from the model features. Additionally, the columns 'customerID', 'BeginDate', 'EndDate', and 'TenureSegment' were removed since they offered no predictive value.

Correlation matrix:
![Correlation matrix](https://raw.githubusercontent.com/D-Acho/Final_project/main/pictures/correlation_matrix.png)

## Modeling

The initial plan was to test models such as Logistic Regression, Random Forest, XGBoost, and LightGBM. However, since it was difficult to improve the AUC-ROC score, GradientBoosting and CatBoost were also considered.

Model Comparison:

![Correlation matrix](https://raw.githubusercontent.com/D-Acho/Final_project/main/pictures/model_comparison.png)

## Selected Model and Hyperparameter Tuning

The techniques chosen for this project are well suited for the following reasons:

Logistic Regression This is an interpretable statistical technique and useful baseline model. While it has limited capacity for modeling non-linear relationships, it is fast, simple, and helps assess the influence of individual variables.

Random Forest An ensemble model based on decision trees, ideal for capturing non-linear relationships and handling both categorical and numerical data. It is also robust to outliers and overfitting, thanks to the averaging of many trees.

Gradient Boosting, XGBoost, LightGBM, CatBoost These models use boosting techniques, in which trees are built sequentially to correct errors from previous ones. They are powerful at capturing complex interactions between variables and adapting to moderately imbalanced datasets—such as in this case.

The best performance was achieved with the GradientBoosting model, which proved both efficient and fast. After tuning its hyperparameters, the results improved even further:

Best parameters: {'learning_rate': 0.05, 'max_depth': 3, 'min_samples_split': 5, 'n_estimators': 100}

Best ROC-AUC score on validation: 0.8527

Test accuracy: 0.7989

AUC-ROC: 0.8399


## Conclusions and Recommendations

The GradientBoosting model is the most suitable for this use case due to its balance of accuracy, AUC-ROC, and execution time.

It is recommended to integrate the model into customer retention workflows, especially for users with low tenure.

Periodic monitoring of the model's performance is suggested, along with exploring new external variables that could enhance predictive power.
