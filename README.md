# Predict Bike Sharing Demand with AutoGluon

### Project 1 of the Udacity AWS Machine Learning Fundamentals Nanodegree Program

This project tackles the [Bike Sharing Demand Kaggle competition](https://www.kaggle.com/c/bike-sharing-demand) by leveraging the power of **AutoGluon**, an open-source AutoML library. The primary goal is to train a high-performing model that accurately predicts the hourly demand for rental bikes based on historical usage patterns and environmental factors.

---

## Project Overview

In this project, I utilized the `TabularPrediction` capabilities of AutoGluon to automate the process of model selection, hyperparameter tuning, and ensembling. The objective was to build a robust predictive model with minimal manual intervention and achieve a high-ranking score in the Kaggle competition.

AutoGluon simplifies the end-to-end machine learning workflow by automatically training and evaluating a wide range of models, including LightGBM, CatBoost, XGBoost, and deep neural networks, and then stacking them into a powerful ensemble.

## Dataset

The project uses the dataset provided by the [Bike Sharing Demand](https://www.kaggle.com/c/bike-sharing-demand/data) competition on Kaggle. The dataset contains hourly rental data spanning two years, with features including:

-   `datetime` - hourly date + timestamp
-   `season` - 1 = spring, 2 = summer, 3 = fall, 4 = winter
-   `holiday` - whether the day is considered a holiday
-   `workingday` - whether the day is neither a weekend nor holiday
-   `weather` - 1: Clear, 2: Mist, 3: Light Snow/Rain, 4: Heavy Rain/Snow
-   `temp` - temperature in Celsius
-   `atemp` - "feels like" temperature in Celsius
-   `humidity` - relative humidity
-   `windspeed` - wind speed
-   `count` - the total number of bikes rented (this is the target variable)

## Key Steps and Implementation

1.  **Data Loading & Preprocessing:** The initial `train.csv` and `test.csv` files were loaded into Pandas DataFrames.
2.  **Feature Engineering:** The `datetime` column was parsed into more granular features, such as `hour`, `day`, and `month`, to help the models capture cyclical patterns.
3.  **Model Training with AutoGluon:**
    -   A `TabularPredictor` was instantiated, specifying the `count` column as the label to predict.
    -   The `predictor.fit()` method was called on the training data. This single line of code triggers AutoGluon to:
        -   Automatically infer data types.
        -   Train multiple state-of-the-art models.
        -   Perform hyperparameter optimization.
        -   Create weighted ensembles of the best-performing models.
4.  **Prediction and Submission:**
    -   The trained predictor was used to generate predictions on the `test.csv` dataset.
    -   Since the competition requires non-negative predictions, any negative values were clipped to zero.
    -   The final predictions were formatted into a `submission.csv` file, ready for upload to Kaggle.

## Results

AutoGluon's automated approach proved highly effective. The ensembled model was able to capture complex relationships within the data, leading to a strong performance in the competition. The `predictor.leaderboard()` command provided a clear ranking of all trained models, showcasing the power of stacking and ensembling.

*(Optional: You could add your Kaggle score here, for example: "The final model achieved a Kaggle score of X.XXXX, placing in the top Y% of the competition.")*

## Usage

To run this project and reproduce the results:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/Asma-Nasr/Predict-Bike-Sharing-Demand-with-AutoGluon.git
    ```
2.  **Navigate to the project directory:**
    ```bash
    cd Predict-Bike-Sharing-Demand-with-AutoGluon
    ```
3.  **Install dependencies:** Ensure you have AutoGluon and its dependencies installed.
    ```bash
    pip install autogluon
    ```
4.  **Run the notebook:** Open and run the Jupyter Notebook (`.ipynb` file) included in the repository to execute the entire data processing and model training pipeline.
