# Marketing Sales Prediction Model

This repository contains a multiple linear regression analysis to estimate sales for a small business based on historical marketing promotion data. The analysis explores the impact of TV, radio, social media, and influencer promotions on sales, using a synthetic dataset from Kaggle.

## Project Overview

The goal of this project is to help a small business optimize its marketing strategy by identifying which promotional channels (TV, radio, social media, and influencer) most effectively drive sales. A multiple linear regression model was developed to quantify the relationship between these independent variables and sales (in millions of dollars).

### Dataset
- **Source**: [Dummy Marketing and Sales Data](https://www.kaggle.com/datasets/harrimansaragih/dummy-advertising-and-sales-data?select=Dummy+Data+HSS.csv) by harrimansaragih on Kaggle.
- **Description**: A synthetic dataset with approximately 572 observations, including:
  - **TV**: Promotional budget (categories: Low, Medium, High).
  - **Radio**: Promotional budget (in millions of dollars).
  - **Social Media**: Promotional budget (in millions of dollars).
  - **Influencer**: Influencer size (categories: Mega, Macro, Micro, Nano).
  - **Sales**: Total sales generated (in millions of dollars).
- **Reference**: harrimansaragih. (n.d.). *Dummy marketing and sales data* [Data set]. Kaggle. https://www.kaggle.com/datasets/harrimansaragih/dummy-advertising-and-sales-data?select=Dummy+Data+HSS.csv

## Analysis Steps

1. **Data Exploration and Cleaning**:
   - Loaded and cleaned the dataset (`marketing_sales_data.csv`) by removing missing values.
   - Renamed columns for consistency (e.g., `Social Media` to `Social_Media`).

2. **Exploratory Data Analysis (EDA)**:
   - Used `seaborn.pairplot()` to visualize relationships between variables.
   - Calculated mean sales by TV and Influencer categories to assess their predictive potential.
   - Identified linear relationships between Radio, Social Media, and Sales, with TV showing a strong categorical effect.

3. **Model Development**:
   - Built a multiple linear regression model using the formula `Sales ~ C(TV) + Radio` with `statsmodels.ols`.
   - Excluded Social Media (due to correlation with Radio) and Influencer (weak predictive power).

4. **Model Validation**:
   - Checked assumptions:
     - **Linearity**: Confirmed with scatter plots (Radio vs. Sales).
     - **Normality**: Validated with histogram and Q-Q plot of residuals.
     - **Homoscedasticity**: Verified with residuals vs. fitted values plot.
     - **Multicollinearity**: Assessed with VIF (no issues with only one continuous variable, Radio).
   - Model performance: R-squared = 0.904, indicating 90.4% of sales variance is explained.

5. **Results Interpretation**:
   - **Coefficients**:
     - Intercept: 218.5261 million (baseline sales).
     - C(TV)[T.Low]: -154.2971 million (reduction vs. High).
     - C(TV)[T.Medium]: -75.3120 million (reduction vs. High).
     - Radio: 2.9669 million (increase per million spent).
   - **Insights**: High TV budgets significantly boost sales, and each million spent on radio adds ~3 million in sales.

## Recommendations
- Prioritize high TV promotional budgets to maximize sales.
- Invest in radio promotions to incrementally increase sales.
- Consider collecting more granular TV budget data or additional variables (e.g., campaign location, season) to improve model accuracy.

## Files
- `marketing_sales_data.csv`: The cleaned dataset used for analysis.
- `marketing_sales_analysis.py`: Python script containing the full analysis (data loading, EDA, modeling, and visualization).

## Visualization
<img width="542" height="528" alt="image" src="https://github.com/user-attachments/assets/76ab3ab7-e1cf-443c-a082-8fc268218b34" />

The repository includes plots generated with `matplotlib` and `seaborn`:
- Scatter plots of Radio vs. Sales and Social Media vs. Sales.
- Histogram and Q-Q plot of residuals.
- Residuals vs. Fitted Values plot.

## How to Run
1. Clone the repository: `git clone <repository-url>`.
2. Install dependencies: `pip install pandas matplotlib seaborn statsmodels`.
3. Run the analysis script: `python marketing_sales_analysis.py`.
