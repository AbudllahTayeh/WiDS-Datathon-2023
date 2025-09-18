# WiDS Datathon 2023: Sub-seasonal Weather Forecasting

## Project Overview

This is an entry for the [WiDS (Women in Data Science) Datathon 2023](https://www.widsconference.org/datathon/). The key objective is to improve sub-seasonal forecasting of weather through the combination of physics-based models and machine learning. Accurate predictions of weather 15-45 days ahead are exceedingly valuable for allowing communities and businesses to manage the effects of extreme climate and weather.

The specific task is to predict the arithmetic mean of the high and low temperature for 14 days over various geographies in the United States.

## Methodology

The code is all in one Jupyter Notebook (`main.ipynb`) and follows a standard data science workflow:

1.  **Data Loading:** The training (`train_data.csv`) and test (`test_data.csv`) datasets are loaded using `pandas`.

2.  **Data Cleaning & Preprocessing:**
* **Missing Value Imputation:** Missing values are handled systematically. Numerical features are imputed with their **median**, and categorical features are replaced with their **mode**. This provides the model with a complete dataset to train on.
* **Data Type Conversion:** The `startdate` column is converted to a correct `datetime` object to enable time-based feature extraction.

3.  **Feature Engineering:**
* New features are obtained from the `startdate` to allow the model to learn seasonality more effectively (e.g., `month`, `day_of_year`).
    * Cyclical features (`sin_day_of_year`, `cos_day_of_year`) are derived from the day of the year so that it can accurately present its cyclical nature to the tree-based model.
    * Categorical feature `climateregions__climateregion` is one-hot encoded for use in the model.

4.  **Modeling:**
* **Model Selection:** A **LightGBM (Light Gradient Boosting Machine)** regressor is chosen here. It is a fast, effective, and strong algorithm for tabular data and one of the top-performing competition solution options.
* **Training & Validation:** The data is split into training and validation sets. The model is trained using the training set and the validation set is utilized for early stopping, which prevents overfitting and decides on the optimal number of boosting rounds.

5.  **Prediction & Submission:**
    * The trained model is used to make predictions on the preprocessed test dataset.
* The final predictions are organized into a `submission.csv` file with two columns (`index` and `contest-tmp2m-14d__tmp2m`) as competition rules demand.

## Getting Started

### Prerequisites

Ensure you have Python 3 installed. The used libraries in this project can be installed via pip:

```bash
pip install pandas numpy scikit-learn lightgbm matplotlib seaborn jupyter
```
Usage
Open Jupyter Notebook or JupyterLab.

Open main.ipynb.

Run the cells from top to bottom.

After successful execution, a submission.csv file will be generated in the project root directory.

Results
The primary result of this project is the submission.csv file containing the predicted mean temperatures for all records in the test set. Model performance is verified against a hidden test set on the competition website using the Root Mean Squared Error (RMSE) metric.

Future Work
To further enhance the performance of the model, the following can be attempted:

Hyperparameter Tuning: Use techniques like Grid Search, Random Search, or Bayesian Optimization to find the optimal parameters for the LightGBM model.

Feature Engineering: Explore feature interactions (e.g., location and temperature) or incorporate additional advanced climate data.

Cross-Validation: Employ a more sophisticated cross-validation technique (e.g., Time-Series Split or K-Fold) to have a better estimate of the model generalization performance.

Ensemble Modeling: Make predictions from many different models (such as XGBoost, CatBoost, or Neural Networks) and potentially end up with a more precise and robust final prediction.
