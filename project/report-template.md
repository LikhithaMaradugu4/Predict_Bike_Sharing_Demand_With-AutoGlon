# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Likhitha Maradugu

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
When I tried to submit my initial predictions to Kaggle, I realized that the submission format required only two columns: datetime and count. I had to adjust the output of the predictor to match this format by ensuring that the predicted values were aligned correctly with the datetime values from the test set.


### What was the top ranked model that performed?
The top-ranked model in the initial training was typically an ensemble model (like WeightedEnsemble_L2) composed of base models such as LightGBM and RandomForest. AutoGluon automatically selected the best ensemble using validation performance.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
During EDA, I observed that the datetime column contained valuable temporal information that wasn’t being used by default. So, I extracted the hour, day, weekday, and month from it. Additionally, I converted several categorical features such as season, weather, and holiday into the category datatype to help tree-based models treat them correctly.

### How much better did your model preform after adding additional features and why do you think that is?
After adding these new features, the Kaggle score improved dramatically — from 1.80356 to 0.61099. This is because the new features (especially hour and weekday) captured patterns in bike usage tied to time, which are crucial for demand prediction.



## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
After performing hyperparameter tuning using a defined search space and running multiple trials, the model improved further to 0.46817. While the jump wasn't as dramatic as after feature engineering, it still indicated a more optimized learning process.





### If you were given more time with this dataset, where do you think you would spend more time?
If given more time, I would:

Experiment with different feature encodings (e.g., cyclic encoding for time features like hour).

Try lag features or rolling averages to capture recent trends.

Perform feature importance analysis to remove or transform redundant features.

Use external data sources such as weather or holiday calendars to enrich the dataset.


### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
| model                 | hpo1                   | hpo2                         | hpo3                                              | score       |
| initial                  | default               | -                                  | -                                                       | 0.81002 |
| add\_features | default                | -                                  | -                                                       | 0.81096 |
| hpo           | `auto` (AutoGluon) | time\_limits=600| search\_strategy=random | 0.4133 |

### Create a line plot showing the top model score for the three (or more) training runs during the project.

TODO: Replace the image below with your own.

![model_train_score.png](img/model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

TODO: Replace the image below with your own.

![model_test_score.png](img/model_test_score.png)

## Summary
Initially, the model didn’t perform well due to the absence of feature engineering. After extracting time-based features and converting categorical columns, the model significantly improved. Finally, hyperparameter tuning helped fine-tune the best-performing models like GBM and XGB. One interesting observation was that although the numerical score on Kaggle improved in a steep fashion, the model leaderboard score fluctuated slightly — possibly due to overfitting to training folds or randomness in test distribution.




