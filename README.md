# Concrete Strength Prediction

A machine learning project for predicting **concrete compressive strength** from material composition and curing age using **multilinear regression implemented with TensorFlow**.

## Project Overview

This notebook builds a regression model to estimate the compressive strength of concrete based on 8 input features:

- Cement
- Blast furnace slag
- Fly ash
- Water
- Superplasticizer
- Coarse aggregate
- Fine aggregate
- Age

The workflow covers the full modeling process, including:

- data loading and exploration
- data cleaning
- correlation analysis and visualization
- feature scaling
- train-test split
- TensorFlow-based regression model implementation
- model training with gradient descent
- evaluation on training and test data
- prediction uncertainty analysis

## Objective

The goal of this project is to predict the compressive strength of concrete and understand which material components have the greatest influence on strength.

## Dataset

The dataset contains **1030 rows** and **9 columns** originally:

- 8 input variables
- 1 target variable: `csMPA` (compressive strength in MPa)

### Data Quality Findings

After checking the dataset:

- all columns were numeric (`float64`)
- no missing values were found
- **25 duplicate rows** were identified and removed
- final cleaned dataset size: **1005 rows**

## Methods Used

### 1. Exploratory Data Analysis

The notebook first inspects the dataset structure, summary statistics, and feature meanings.

### 2. Data Cleaning

Duplicate rows are removed to improve data quality before modeling.

### 3. Correlation Analysis

A correlation matrix and pairplot are used to study relationships between features and concrete strength.

The strongest correlations with compressive strength were:

- **cement**: `0.488`
- **superplasticizer**: `0.344`
- **age**: `0.337`

Negative correlations included:

- **water**: `-0.270`
- **fine_agg**: `-0.186`
- **coarse_agg**: `-0.145`

These results suggest that higher cement content, superplasticizer content, and curing age tend to increase compressive strength, while higher water content tends to reduce it.

### 4. Feature Scaling

`MinMaxScaler` is used to normalize all input features before training.

### 5. Model Building

The regression model is implemented manually in TensorFlow using:

- trainable weights and bias
- a linear regression function: `z = xw + b`
- mean squared error (MSE) loss
- stochastic gradient descent (SGD) optimizer
- `tf.GradientTape` for automatic differentiation

### 6. Model Training

The model is trained for **5000 epochs**.

Training loss decreased from a very large initial value to:

- **Final training loss: 106.7453**

### 7. Evaluation

Model performance was measured using **RMSE (Root Mean Squared Error)**.

- **Training RMSE:** `10.3317 MPa`
- **Test RMSE:** `11.1697 MPa`

The training and test errors are close, which suggests that the model generalizes reasonably well and does not show severe overfitting.

### 8. Prediction Uncertainty Analysis

The notebook also analyzes prediction deviations on the test set.

- **RMSE on test set:** `11.1697 MPa`
- **Predictions with |error| > RMSE:** `29`
- **Total test samples:** `101`
- **Percentage of deviations larger than RMSE:** `28.71%`
- **Mean absolute deviation:** `8.8588 MPa`
- **Max deviation:** `30.7034 MPa`
- **Min deviation:** `0.1340 MPa`

## Learned Model Parameters

After training, the learned coefficients were:

- Cement: `38.8158`
- Slag: `22.7041`
- Ash: `7.4397`
- Water: `-18.4171`
- Superplasticizer: `20.5772`
- Coarse Aggregate: `0.3972`
- Fine Aggregate: `-4.0529`
- Age: `36.0091`
- Bias: `15.0046`

These values indicate the relative influence of each normalized feature on the predicted concrete strength.

## Visualizations Included

The notebook includes several visual outputs:

- correlation heatmap
- pairplot of all variables
- training loss curve
- predicted vs actual values on training data
- predicted vs actual values on test data
- histogram of prediction deviations

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- TensorFlow
- Jupyter Notebook

## File Structure

```bash
Concrete_Strength_Prediction.ipynb
README.md
```

## How to Run

1. Clone this repository:

```bash
git clone <your-repository-url>
cd <your-repository-folder>
```

2. Install dependencies:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn tensorflow openpyxl jupyter
```

3. Open Jupyter Notebook:

```bash
jupyter notebook
```

4. Run `Concrete_Strength_Prediction.ipynb` cell by cell.

## Results Summary

This project shows that a simple multilinear regression model can learn meaningful relationships between concrete ingredients and compressive strength. The model achieved a **test RMSE of about 11.17 MPa**, which indicates moderate predictive performance. Important variables such as cement, superplasticizer, and age contributed positively to strength, while water had a negative effect.

## Possible Improvements

Future improvements could include:

- trying more advanced regression models such as Random Forest, XGBoost, or Neural Networks
- using feature engineering to capture nonlinear relationships
- tuning hyperparameters such as learning rate and epoch count
- adding evaluation metrics such as MAE and R²
- using cross-validation for more robust performance estimation

## Author

Created as part of a machine learning / deep learning practice project on concrete compressive strength prediction.
