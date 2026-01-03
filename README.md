# What drives the price of a car?

## Project Overview

This project analyzes a large used car dataset to identify the key factors that influence used car prices. The objective is to provide actionable insights to used car dealership to support better inventory selection and pricing. 

**Full analysis and code:**  
👉 [Jupyter Notebook – Used Car Price Analysis](ml-used-car-analysis.ipynb)


## Business Objective

The business objective of this task is to help car dealerships to understand which vehicle features/characteristics strongly influence the price of used cars so that they can work out on better inventory and pricing. Using provided dataset, we aim to identify the impact of features such as vehicle age, manufacturer, transmission type, odometer reading and other features on the car's sale price. This problem can be framed as supervised regression task where the goal is to develop and train a predictive model to identify the relationship between car's features and its price. The outcome of this task is to provide actionable insights and recommendations to dealerships so that it can help dealers in selecting the inventory with higher resale value and price the cars competitively.

## Data Understanding

* In this application, Kaggle used car dataset is used. The original dataset contained information on 3 million used cars. The provided dataset contains information on 426K cars to ensure speed of processing.
* Analyzed data to check quality issues such as missing information, invalid or unrealistic values.
* Analyzed the relation between features and target variable (price) using plots to visualize the relationshp and to identify significance of the feature in influencing the car price.
* Missing Values: There are significant number of missing values for certain features especially size, VIN, condition, cylinders, drive type, paint color indicating data quality issues.
* Anomolies/Outliers: The min value of the price column is 0 and max is ~3B which indicates data errors and unrealistic price values. There seems to be significant number of entries with price as zero, which are certainly not useful for the model, requiring the data cleanup during preparation phase. The maximum value of odomoter is 10M and max age of the vehicle is 126 which indicate errors and unrealistic data.

## Data Preparation

* Applied cut-off for both price and odometer at 99.5th percentile to exclude the extreme outliers and unrealistic data.
* Exclulded features such as ID, VIN, size, paint color that did not exhibit significant influence on the price.
* Removed samples with invalid values and handled missing values with appropriate replacements (using median for numeric features and a special category 'unknown' for categorial features)
* Fixed data types
* Engineered new feature "vehicle_age" which is more generalized than 'year' and applied cut-off at 99.5th percentile to eliminate unrealistic and incorrect values.
* Split the prepared dataset into training and test subsets in 80/20 ratio.
* Applied One Hot Encoding for categorial features and Standard Scalar for numeric features

## Modeling

* Three models were trained and evaluated on the same test dataset:
   * Linear Regression (baseline model)
   * Ridge Regression
   * Lasso Regression
 * To compare the performance of the regression models, the following evaluation metrics were used:
   * Mean Squared Error (MSE)
   * Root Mean Squared Error (RMSE)
   * R2 (R square)
 * The results indicate that all three models perform very similarly, with nearly identical MSE, RMSE, and R2 values. This suggests that the relationship between features and price is largely linear.

## Evaluation

* After training and evaluating multiple regression models: Linear, Ridge, and Lasso regressions, the Ridge regression model was selected as the final model due to its slightly better performance in terms of MSE, RMSE, and R2, and its ability to reduce potentioal overfitting.
* Interpreted the coefficients to provide business insights after unscaling the numeric features.
* Numeric features such as vehicle age and odometer have negative coefficients, indicating that older cars and higher mileage reduce the prices.
* Categorical features reveal key drivers: premium brands like Tesla (+15,955), Porsche (+9,530), and Datsun (+8,652) strongly increase the price, while brands like fiat (-8,113), mitsubishi (-6,662.73), hyundai (-4,009) decrease it.
* Other important categories include title status (Parts Only reduces price and Clean titles increase it) and fuel type (diesel increases price).

## Deployment

### Key Drivers
* **Vehicle Age**: New vehicles retain better value. For each additional year of a vehicle's age, the price decreases by ~$450, holding all other features constant.
* **Mileage**: For each additional mile on the odometer, the price decreases by ~$0.092 (i.e., $92 for every 1,000 miles).
* Top Categories having positive impact on the price
  * Premium brands like Tesla (+15,955), Porsche (+9,530), and Datsun (+8,652) strongly increase the price.
  * The diesel fueled cars have higher price (+11,453) compared to other fuel types.
  * Clean title status increases the price by (+3,360).
  * Pickup trucks provide better sale price compared to other types like SUV, min-van, Sedan etc...
  * 4WD vehicles increase the price (+2,622) compared to other types (FWD)
* Top Categories with negative impact on the price
  * Mass brands like fiat (-8,113), mitsubishi (-6,662.73), hyundai (-4,009) decrease the price.
  * Title status 'parts_only' has higher negative impact on the price (-4,999)
  * Used electric vehicles do not increase the prices (unless premium brand like Tesla) when compared to their gas counter parts (-5,659)
    
### Recommendations
* Focus on adding more low-mileage 4WD vehicles (especially Pickup trucks) to the inventory.
* Acquire premium brands like Tesla, Porsche to maximize margins.
* Add diesel pickup trucks for high value sales.

### Next Steps
* Update the model periodically with new used car data to reflect changing demand.
* Provide dealer sales data to work on a predictive model that can provide recommendations to maximize the profit based on the margins and volume.
 

