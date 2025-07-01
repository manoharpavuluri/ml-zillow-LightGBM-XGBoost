# Zillow Home Value Prediction Challenge

## Project Overview

This project addresses Zillow's Home Value Prediction Challenge from Kaggle, focusing on predicting the log-error between Zillow's Zestimate and actual sale prices for residential properties in California.

### Problem Statement
- **Target**: Predict the log-error between Zestimate and actual sale price
- **Formula**: `log-error = log(Zestimate) - log(SalePrice)`
- **Scope**: Properties in Los Angeles, Orange, and Ventura counties, California
- **Time Period**: Predictions for Fall 2017 based on 2016 data

## Dataset Information

### Data Sources
- **Properties Data**: ~2.99M properties with 58 features (2016 & 2017)
- **Training Data**: 90,275 transactions before October 15, 2016
- **Test Data**: Transactions between October 15 and December 31, 2016
- **Features**: 57 property characteristics including location, size, amenities, and tax information

### Key Statistics
- **Total Properties**: 2,985,217
- **Training Samples**: 90,275 (2016) / 77,613 (2017)
- **Unique Sales**: 90,150 (125 duplicates in 2016 data)
- **Feature Types**: Continuous and categorical variables

## Methodology

### 1. Data Exploration & Analysis
- Comprehensive feature analysis with missing value assessment
- Statistical summary of all variables
- Identification of data quality issues and patterns

### 2. Feature Engineering
- **Property Age**: `2018 - yearbuilt`
- **Amenity Indicators**: 
  - `has_basement`: Binary indicator for basement presence
  - `has_pool`: Pool availability indicator
  - `has_patio_yard`: Patio/yard building indicator
  - `has_storage_yard`: Storage yard indicator
  - `has_garage`: Garage availability indicator

### 3. Data Preprocessing
- **Missing Value Treatment**: 
  - Features with >90% missing values removed
  - Median imputation for remaining missing values
  - Zero-filling for logical null values (e.g., no pool = 0)
- **Feature Selection**: Removed non-categorical object columns
- **Data Type Optimization**: Converted to appropriate numeric types

### 4. Correlation Analysis
- Feature correlation analysis with target variable
- Identification of most predictive features
- Visualization of feature importance patterns

## Machine Learning Models

### 1. LightGBM Model
**Configuration:**
- **Objective**: Regression with MAE metric
- **Learning Rate**: 0.01
- **Boosting Type**: GBDT
- **Number of Leaves**: 22
- **Subsample**: 0.7
- **Colsample by Tree**: 0.85
- **Iterations**: 430

**Key Features:**
- Handles missing values automatically
- Efficient memory usage
- Fast training and prediction

### 2. XGBoost Model (Version 1)
**Configuration:**
- **Objective**: reg:linear
- **Learning Rate (eta)**: 0.04
- **Max Depth**: 6
- **Subsample**: 0.80
- **Lambda**: 0.8 (L2 regularization)
- **Alpha**: 0.4 (L1 regularization)
- **Iterations**: 150

### 3. XGBoost Model (Version 2)
**Configuration:**
- **Objective**: reg:squarederror
- **Learning Rate (eta)**: 0.05
- **Max Depth**: 8
- **Subsample**: 0.7
- **Colsample by Tree**: 0.7
- **Iterations**: 50

## Key Findings

### Feature Importance
The analysis revealed several highly predictive features:
- **Location-based**: Latitude, longitude, region identifiers
- **Property Characteristics**: Square footage, number of bedrooms/bathrooms
- **Tax Information**: Tax values, assessment data
- **Amenities**: Pool, garage, basement indicators

### Data Quality Insights
- Significant missing data in certain features (>90% in some cases)
- Mixed data types requiring careful preprocessing
- Duplicate transactions requiring deduplication

## Visualizations

The project includes comprehensive visualizations:

### Missing Data Analysis
![Missing Features](https://github.com/manoharpavuluri/zillow-LightGBM-XGBoost/blob/master/photos/missingfeature.png)

### Feature Correlation
![Feature Correlation](https://github.com/manoharpavuluri/zillow-LightGBM-XGBoost/blob/master/photos/feature_core.png)

### Feature Importance
![Feature Importance](https://github.com/manoharpavuluri/zillow-LightGBM-XGBoost/blob/master/photos/feature_imp.png)

### Model Tree Visualization
![Tree Structure](https://github.com/manoharpavuluri/zillow-LightGBM-XGBoost/blob/master/photos/tree.png)

## Technical Stack

- **Python**: Primary programming language
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computations
- **Matplotlib/Seaborn**: Data visualization
- **LightGBM**: Gradient boosting framework
- **XGBoost**: Extreme gradient boosting
- **Scikit-learn**: Machine learning utilities
- **Yellowbrick**: Model visualization

## Future Enhancements

The project is designed for iterative improvement:
- **Ensemble Methods**: Combine predictions from multiple models
- **Advanced Feature Engineering**: Time-based features, market trends
- **Hyperparameter Optimization**: Grid search and Bayesian optimization
- **Cross-Validation**: Robust model evaluation
- **Feature Selection**: Advanced feature selection techniques

## Repository Structure

```
ml-zillow-LightGBM-XGBoost/
├── README.md              # Project documentation
├── requirements.txt       # Python dependencies
├── Zestimate.ipynb        # Main analysis notebook
└── photos/                # Visualization outputs
    ├── missingfeature.png
    ├── feature_core.png
    ├── feature_imp.png
    └── tree.png
```

## Getting Started

1. Clone the repository
2. Install required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Open `Zestimate.ipynb` in Jupyter Notebook
4. Follow the analysis workflow

## License

This project is part of the Zillow Home Value Prediction Challenge and follows the competition's terms and conditions.

---

*This project demonstrates advanced machine learning techniques for real estate valuation, combining data science best practices with domain-specific feature engineering.*

