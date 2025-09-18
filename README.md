# WiDS Datathon 2023: Sub-seasonal Weather Forecasting

## Project Overview
This is an entry for the [WiDS (Women in Data Science) Datathon 2023](https://www.widsconference.org/datathon/). The primary goal is to improve sub-seasonal weather forecasting through the integration of physics-based models and machine learning. Consistent 15-45 day forecasts of weather are extremely valuable for empowering communities and businesses to prepare for the effect of extreme weather and climate.

The work here is to predict the arithmetic mean of the high and low temperature for 14 days over various geographies in the United States.

## Methodology

The code is single, combined Jupyter Notebook (`main.ipynb`) and follows a standard data science pipeline:

1.  **Data Loading:** The training (`train_data.csv`) and testing (`test_data.csv`) data are loaded using `pandas`.

2.  **Data Cleaning & Preprocessing:**
* **Imputation of Missing Values:** Missing values are handled in a structured manner. Numerical features are replaced with their **median**, and categorical features are replaced with their **mode**. This provides the model with a complete dataset to train upon.
* **Conversion of Data Types:** The `startdate` column is changed to a proper `datetime` object to enable time-based feature extraction.

3.  **Feature Engineering:**
* New features are extracted from the `startdate` to allow the model to learn seasonality more effectively (e.g., `month`, `day_of_year`).
* Cyclical features (`sin_day_of_year`, `cos_day_of_year`) are derived from the day of the year so that it can adequately expose its cyclical aspect to the tree-based model.
* Categorical feature `climateregions__climateregion` is one-hot encoded to be utilized in the model.

4.  **Modeling:**
* **Model Selection:** A **LightGBM (Light Gradient Boosting Machine)** regressor is employed here. It's an efficient, fast, and strong algorithm for tabular data and one of the top competition solution candidates.
* **Training & Validation:** Both the training and validation sets are formed by dividing the data. The model is trained using the training set and the validation set for early stopping, which prevents overfitting and selects the optimal number of boosting rounds.

5.  **Prediction & Submission:**
    * Prediction on the preprocessed test dataset is performed by the trained model.
* The final predictions are saved in a `submission.csv` file with two columns (`index` and `contest-tmp2m-14d__tmp2m`) because competition rules demand so.
## Getting Started

### Prerequisites

Ensure you have Python 3. The libraries used in this project are installed with pip:

```bash
pip install pandas numpy scikit-learn lightgbm matplotlib seaborn jupyter
```
Usage
Open Jupyter Notebook or JupyterLab.

Open main.ipynb.

Run cells from top to bottom.

After successful execution, a submission.csv file will be produced in the project's root directory.

Results
The primary output of the project is the submission.csv file containing the estimated mean temperatures for every record in the test set. The performance of the model is tested against a blind test set on the competition platform via the Root Mean Squared Error (RMSE) metric.

Future Work
To further enhance the performance of the model, the following may be attempted:

Hyperparameter Tuning: Employ strategies like Grid Search, Random Search, or Bayesian Optimization to find the optimal parameters for the LightGBM model.

Feature Engineering: Explore feature interactions (like temperature and location) or add other sophisticated climate data.

Cross-Validation: Apply a more sophisticated cross-validation technique (such as Time-Series Split or K-Fold) to get a better estimate of the model generalization performance.

Ensemble Modeling: Combine the predictions of many different models (e.g., XGBoost, CatBoost, or Neural Networks) and perhaps even end up with a more accurate and stable overall prediction.
