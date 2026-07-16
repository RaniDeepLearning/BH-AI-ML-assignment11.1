# BH-AI-ML-assignment11.1
This project analyzes a dataset of approximately 426,000 used-car listings to identify the vehicle characteristics associated with price. The analysis is designed for a used-car dealership seeking to improve inventory acquisition and pricing decisions. The business problem is framed as a supervised regression task.
Vehicle price is the target variable, while characteristics such as manufacturer, vehicle age, mileage, condition, fuel type, transmission, drive type, body type, engine cylinders, color, and location are evaluated as potential predictors.

Link to notebook :

## Business objective

The project aims to:

- Identify the factors most strongly drives the used-car prices.
- Build and compare regression models for estimating listing price.
- Translate model results into practical recommendations for a dealership.
- Highlight the limitations of using a predictive model for real-world pricing decisions.

## Dataset

The course-provided data is used-vehicle dataset. It initially contains:

- **426,880 listings**
- **18 variables**
- A mixture of numerical, categorical, and identifier fields
- `price` as the target variable

The raw data contains missing values, high-cardinality categories, placeholder prices, extreme price and odometer values, and fields that are unsuitable for modeling.

The vehicles.csv dataset is not included in this repository because it exceeds GitHub’s file-size limit. The dataset file is not included in this repository. Place `vehicles.csv` in a local `data/` directory before running the notebook.

## Analysis workflow

The project follows the CRISP-DM framework:
**Business understanding** – Define the dealership's pricing problem as a regression task.
**Data understanding** – Examine dimensions, data types, missingness, duplicates, distributions, outliers, categorical frequencies, correlations, and relationships with price.
**Data preparation** – Clean invalid observations, remove unsuitable fields, engineer vehicle age, split the data, and prepare numerical and categorical features.
**Modeling** – Compare Linear, Ridge, Lasso, and Polynomial Ridge regression using cross-validation and hyperparameter tuning.
**Evaluation** – Evaluate the selected model on unseen test data and examine prediction errors.
**Deployment recommendations** – Convert the analytical findings into dealership actions and identify next steps.

## Data preparation

The principal preparation steps include:

- Removing `id` and `VIN` because they function as identifiers.
- Removing `size` because approximately 72% of its values are missing.
- Removing `model` because its very high cardinality would produce an unnecessarily complex one-hot-encoded dataset.
- Retaining listings priced from **$500 to $100,000**.
- Retaining model years from **1900 to 2022**.
- Excluding odometer readings above **500,000 miles**.
- Standardizing categorical text by removing extra spaces and converting it to lowercase.
- Creating `vehicle_age` from model year and then removing the redundant `year` field.
- Splitting the data into training and test sets before learning imputation values.
- Using one-hot encoding for categorical variables and standardization for numerical variables.

## Exploratory findings

- Used-car prices are strongly right-skewed in the raw dataset.
- Newer and lower-mileage vehicles generally have higher listing prices.
- Prices vary by manufacturer, vehicle type, fuel type, engine size, condition, and location.
- Pickup trucks and trucks have relatively high median listing prices compared with several other common body types.
- 
## Models evaluated
Four regression approaches are compared:
- Linear Regression
- Ridge Regression
- Lasso Regression
- Polynomial Ridge Regression

Categorical features are one-hot encoded, numerical features are scaled where appropriate, and preprocessing is combined with estimation through scikit-learn pipelines. Grid search and cross-validation are used to tune regularization strength and polynomial degree.

## Model performance

RMSE is the primary evaluation metric because it reports error in dollars and gives greater weight to large pricing mistakes.

| Model | Cross-validation RMSE |
|---|---:|
| Linear Regression | $9,463.94 |
| Ridge Regression | $9,014.94 |
| Lasso Regression | $9,014.15 |
| Polynomial Ridge Regression | **$8,044.34** |

The best Polynomial Ridge model uses polynomial degree 3 and Ridge `alpha=3`.

Final held-out test performance:

- **Test RMSE:** $8,071.75
- **Test MAE:** $5,417.93

The close cross-validation and test RMSE values suggest that the selected model generalizes consistently to unseen listings within the analyzed price range.

## Business recommendations

- Consider newer, lower-mileage vehicles when their expected resale value justifies acquisition and reconditioning costs.
- Price high-mileage vehicles carefully because mileage has a substantial negative relationship with listing price.
- Account for manufacturer, body type, fuel type, engine size, condition, and location rather than pricing from age and mileage alone.
- Evaluate luxury, rare, and classic vehicles separately because they may not follow the pricing patterns of typical inventory.
- Use model predictions as a pricing guide alongside mechanical inspection, vehicle history, local demand, and dealership expertise.
- Evaluate expected profit margin rather than assuming that a higher predicted selling price automatically means a better inventory opportunity.

## Limitations

- Missing and inconsistently reported categorical information may affect model accuracy.
- The model was trained only on vehicles priced from $500 to $100,000 and should not be applied outside this range.
- Prediction errors are larger for unusual, very inexpensive, and very expensive vehicles.
- The analysis identifies statistical associations rather than causal effects or direct measures of consumer preference.


## Author
Rani Kumari  
Professional Program in Artificial Intelligence and Machine Learning
