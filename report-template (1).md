# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### 
YOUSSEF EL YOUBI

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
TODO: Add your explanation
I realised that the output had to be formatted exactly like the submission file template - including a datetime column and a single count prediction column. I had to ensure that the prediction DataFrame followed this format and did not include any extra columns so, I had to modify the code to set any negative predictions to zero before creating the submission file. This ensured that all predicted values were valid.
### What was the top ranked model that performed?
TODO: Add your explanation
The top-performing model during the initial run was WeightedEnsemble_L3, which had a validation RMSE score of -52.983258.
## Exploratory data analysis and feature creation
During exploratory analysis, I observed that bike rental demand varied significantly by hour, season, and weather conditions. To help the model learn these patterns more effectively, I engineered the following features:
Converted season and weather columns into categorical types, so AutoGluon can handle them correctly.
Extracted hour from the datetime column to help capture hourly trends in bike usage
### What did the exploratory analysis find and how did you add additional features?
TODO: Add your explanation
Adding the `hour` feature significantly improved the model's performance 
### How much better did your model preform after adding additional features and why do you think that is?
TODO: Add your explanation
the model’s validation RMSE improved from -52.98 (initial run) to -63.45. This improvement happened because the model could now recognize time-based patterns (like peak hours) and seasonal effects, which were not as clear in the raw data.
## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
TODO: Add your explanation
After tuning hyperparameters (using hyperparameters={'NN_TORCH': {}, 'GBM': {}}), the validation RMSE improved slightly from -63.45 to -64.67. The improvement was marginal but shows that fine-tuning the base models helps squeeze out more accuracy.
### If you were given more time with this dataset, where do you think you would spend more time?
TODO: Add your explanation
If given more time, I would focus on more extensive feature engineering.  This might include creating additional features based on date and time (e.g. day of week, weekend vs. weekday, interactions between time features and weather conditions), or features based on external data sources, like holidays or special events.  I would also experiment with other preprocessing techniques, like target variable transformations (e.g. square root or log transform to address skewness).
### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|hpo1|hpo2|hpo3|score|
| model         | hpo1      | hpo2 | hpo3 | score (Kaggle) |
| ------------- | --------- | ---- | ---- | -------------- |
| initial       | default   | none | none | 1.80037        |
| add\_features | default   | none | none | 0.54860        |
| hpo           | NN\_TORCH | GBM  | none | 0.54601        |

### Create a line plot showing the top model score for the three (or more) training runs during the project.

TODO: Replace the image below with your own.

![Model Training Score](top_model_val_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

TODO: Replace the image below with your own.

![model_test_score.png](model_test_score.png)

## Summary
TODO: Add your explanation
This project demonstrates the power and efficiency of AutoGluon for tabular prediction.  With minimal effort, AutoGluon was able to achieve a reasonable score on the bike-sharing demand prediction task. Feature engineering played a significant role in improving performance, while basic hyperparameter tuning provided further gains.  More extensive feature engineering, and potentially different model selection within AutoGluon, could further enhance the predictive accuracy.
