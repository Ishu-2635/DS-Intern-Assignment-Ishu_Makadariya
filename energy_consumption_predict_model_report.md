Energy Consumption Modeling Report
----------------------------------
 Dataset Summary
- 16,857 rows
- Target variable: `equipment_energy_consumption`
- Time-based patterns observed


Exploratory Data Analysis (EDA)

- Data recorded at 10-minute intervals
- Target variable (equipment_energy_consumption) was highly skewed
- Outliers present in energy and some environmental readings
- Missing values found across various features
- Median imputation used due to skewness

Feature Engineering

- Extracted timestamp components: year, month, day, hour, minute
- Created lag features: lag_1 to lag_3
- Added rolling statistics: rolling_mean_3, rolling_std_3
- Data sorted in chronological order

Model Evaluation

Model                           | R² Score | RMSE   | MAE
------------------------------- |----------|--------|------
XGBoost                         | 0.9775   | 21.78  | 6.77
Random Forest (no random vars)  | 0.9727   | 24.04  | 6.90
Random Forest (with random vars)| 0.9725   | 24.06  | 6.98
Linear Regression               | 1.0000   | 3.12   | 2.27

Note: Linear Regression is likely overfitting 

Feature Importance Insights

- rolling_mean_3, lag_1, and lag_2 account for over 90% of feature importance
- rolling_std_3 also contributes meaningfully
- External and random variables have very low importance
- Time-based features like hour and day contribute marginally

Key Takeaways

- Energy consumption shows strong temporal repetition
- Lag and rolling features derived from the target drive most model performance
- Environmental features (e.g., humidity, zone temperatures) add little value
- Perfect scores in linear regression suggest overfitting

Recommendations

Keep:
- Top 15-20 important features, especially lag and rolling stats
- Useful time indicators like hour and day

Drop:
- Low-importance columns like random variables and many zone sensor readings