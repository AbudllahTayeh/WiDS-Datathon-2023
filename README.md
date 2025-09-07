# Some-Work-On-WiDS-Datathon-2023
This project will be in two phases: - Exploratory and Explanatory analysis - Modelling and prediction
# WiDS Datathon 2023: Sub-seasonal Weather Forecasting

## Project Overview

This project is an entry for the [WiDS (Women in Data Science) Datathon 2023](https://www.widsconference.org/datathon/). The primary objective is to improve sub-seasonal weather forecasts by blending physics-based models with machine learning. Accurate forecasts for weather conditions 15-45 days out are crucial for helping communities and industries adapt to the challenges posed by extreme weather events and climate change.

The specific task is to predict the arithmetic mean of the maximum and minimum temperature over a 14-day period for various locations across the United States.

## Methodology

The solution is developed in a single Jupyter Notebook (`main.ipynb`) and follows a standard data science workflow:

1.  **Data Loading:** The training (`train_data.csv`) and testing (`test_data.csv`) datasets are loaded using `pandas`.

2.  **Data Cleaning & Preprocessing:**
    * **Missing Value Imputation:** A systematic approach is taken to handle missing values. Numerical features are imputed with their **median**, while categorical features are filled with their **mode**. This ensures that the model receives a complete dataset for training.
    * **Data Type Conversion:** The `startdate` column is converted to a proper `datetime` object to enable time-based feature extraction.

3.  **Feature Engineering:**
    * New features are created from the `startdate` to help the model better understand seasonality (e.g., `month`, `day_of_year`).
    * Cyclical features (`sin_day_of_year`, `cos_day_of_year`) are generated from the day of the year to effectively represent its cyclical nature to the tree-based model.
    * The categorical feature `climateregions__climateregion` is one-hot encoded to be used in the model.

4.  **Modeling:**
    * **Model Selection:** A **LightGBM (Light Gradient Boosting Machine)** regressor is chosen for this task. It is a powerful, efficient, and highly effective algorithm for tabular data and is a frequent choice in top-performing competition solutions.
    * **Training & Validation:** The data is split into training and validation sets. The model is trained on the training set and uses the validation set for early stopping, which prevents overfitting and helps find the optimal number of boosting rounds.

5.  **Prediction & Submission:**
    * The trained model is used to make predictions on the preprocessed test dataset.
    * The final predictions are formatted into a `submission.csv` file with two columns (`index` and `contest-tmp2m-14d__tmp2m`), as required by the competition rules.

## Getting Started

### Prerequisites

Ensure you have Python 3 installed. The required libraries for this project can be installed via pip:

```bash
pip install pandas numpy scikit-learn lightgbm matplotlib seaborn jupyter
```
Usage
Launch Jupyter Notebook or JupyterLab.

Open main.ipynb.

Run the cells sequentially from top to bottom.

Upon successful execution, a submission.csv file will be generated in the project directory.

Results
The primary output of this project is the submission.csv file, which contains the predicted mean temperatures for each entry in the test set. The model's performance is evaluated against a hidden test set on the competition platform using the Root Mean Squared Error (RMSE) metric.

Future Work
To further improve the model's performance, the following steps could be explored:

Hyperparameter Tuning: Use techniques like Grid Search, Random Search, or Bayesian Optimization to find the optimal set of parameters for the LightGBM model.

Advanced Feature Engineering: Explore interactions between features (e.g., temperature and location) or incorporate more complex climate data.

Cross-Validation: Implement a more robust cross-validation strategy (e.g., K-Fold or Time-Series Split) for a better estimate of the model's generalization performance.

Ensemble Modeling: Combine predictions from multiple different models (e.g., XGBoost, CatBoost, or Neural Networks) to potentially achieve a more accurate and robust final prediction.
