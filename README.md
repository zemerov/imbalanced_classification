# 1C application assignment 

## Task 2: Machine Learning

\*Note: to see all plots correctly use html version.

### Data description
The original dataset is given [here](https://www.kaggle.com/shivamb/real-or-fake-fake-jobposting-prediction) 

This dataset contains 18K job descriptions out of which about 800 are fake. The data consists of both textual information and meta-information about the jobs.


### Target 

Predict job ad is fake or real.


### Results

| Model            | Accuracy      | F1    | Precision | Recall |
| ---------------- |:-------------:| -----:|-----------|--------|
| LogReg (baseline)| 0.78          | 0.22  | 0.13      | 0.76   |
| CatBoost clf     | 0.96          | 0.66  | 0.55      | 0.83   |
| XGBoost clf      | 0.98          | 0.80  | 0.91      | 0.71   |


Get different scores. Catboost and XGB both perform good results, if better recall is preffered choose CatBoost, otherwise XGB is a good 
option


Additionaly, I found out that fake ads ussually have poor company description and unspecify required experience.

#### There is different features impact
![Feature importance](/img/importance.png)