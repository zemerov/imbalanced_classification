# Fake Job Prediction

\*Note: There is a pdf version for your convenience.

Repo structure:
* main.ipynb contains data processing and model training. 
* model_explanation.ipynb contains some beautiful visualizations
with [SHAP](https://github.com/slundberg/shap) library   

## Data description
The original dataset is given [here](https://www.kaggle.com/shivamb/real-or-fake-fake-jobposting-prediction) 

This dataset contains 18K job descriptions out of which about 800 are fake. The data consists of both textual information and meta-information about the jobs.
The dataset is highly imbalanced with only 4.84% positive values.


## Choose metric
Due to imbalanced classes possible metrics were AUC-ROC or AUC-PR. I prefer AUC-PR because finding positive class is more 
important for the task. AUC-ROC treats each class equally, however AUC-PR is more sensitive for the positive label. 

## Exploratory analysis

### Initial data
Initially dataframe consists of 16 features. Majority of them are strings.
There are some categorical features. 

### Feature engineering and feature importance
For text data I simply add symbol-length feature. 

Furthermore, I wanted to know the importance of each feature for the prediction.
For this reason I simply trained several gradient boosting models on each single feature. 

![Feature importance](/img/single_feature.jpg)

len_company_profile has the biggest importance for the target value.
Due to this fact I supposed to add some features with company_profile description. 
It is a text feature so that tf-idf representation could help to increase performance. 


## Results
There were trained various model.

| Model                              | AUC-PR      | 
| -----------------------------------|:-----------:| 
| LogReg (baseline)                  | 0.183       | 
| CatBoost                           | 0.773       | 
| CatBoost (with tf-idf)             | 0.858       | 
| CatBoost (with tf-idf and parameters gridsearch)| 0.877       | 

Comments:

1. LogReg was used as a simple baseline. 
It has really poor quality. It means data has a lot of nonlinear dependencies.

2. There were trained three gradient boosting models.

The best model gets 0.87 AUC-PR on test dataset which is quite good final score.

## Model Explanation

After training the model I used SHAP library for interpretation. 
More examples can be found in model_explanation.ipynb file.

The main interest is feature importance for model prediction.

![Feature importance](/img/importance.jpg)

Obviously len_company_profile and has_company_logo has the biggest impact on predictions. 

So empirically we can predict that post with poor company description and without logo is a fake.  

![Dependency](/img/dependency.jpg)

In this plot it is clearly visible that shorter company description leads to higher impact. 
Furthermore there is a correlation between the len_company_profile and has_company_logo. Companies with short description 
usually do not have logo.