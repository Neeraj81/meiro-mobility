# meiro-mobility

This assignment evaluates different models for predicting demand based on various features such as year, month, day, hour, hourly_sub, peek traffic hours, and high traffic zone. The goal is to understand the features and also understand which models/model will be suitable for which situations.

## Table of Contents
- [Introduction](#introduction)
- [EDA/Feature engineering](#EDAFeature)
- [Models](#models)
- [Considerations](#considerations)
- [Approach](#approch)
- [Assumptions](#assumptions)
- [Hurdles](#hurdles)
- [Solution](#solution)



# Introduction
- We have the raw data (may be this data is generated not original/real)
- We use this data and try to understand and explore it and understand the demand relation
- Then we try to train models and understa


# EDA/Feature
- **Features:**
  - spacial : Made all the spacial points into groups/cluster using KMeans (long, lat)
    - here, i took 35 cluster which is approx of 2.5-3.5 km *2.5-3.5 km area
    - This cluster no. is used as main features
    ![download](https://github.com/Neeraj81/meiro-mobility/assets/53859942/6f9110d3-d82b-4c35-a6ee-6d6331c219dd)

  - time : time based featured like 15 min sub hour, hour, data, month, year.
  - weather : i tried to use wether details
    - this may have correlation like temperature, perception 
  - Other features are not that corelated to others.
 
    



## Models

- Two models:
 - classical statistical- Continuous data
 - Ml/ensemble models- Need variable and learn complex relation

### Linear Regression

- **Advantages:**
  - Simple and interpretable.
  - Fast training and prediction.
  - Less prone to overfitting on small datasets.
- **Disadvantages:**
  - Assumes a linear relationship between features and target may not true for large/realtime data.

### Random Forest

- **Advantages:**
  - Robust to overfitting and noise.
  - Handles non-linearity and interactions between features.
  - Provides feature importance.
- **Disadvantages:**
  - May require more trees for better performance.
  - Slower than linear models but faster than some other ensemble methods.

### XGBoost

- **Advantages:**
  - Powerful and widely used.
  - Can capture complex non-linear relationships.
  - Handles missing values well.
- **Disadvantages:**
  - Requires careful hyperparameter tuning.
  - Longer training time compared to simpler models.

### LightGBM

- **Advantages:**
  - Efficient and scalable for large datasets.
  - Handles categorical features well without one-hot encoding.
  - Reduces memory usage and training time.
- **Disadvantages:**
  - Requires parameter tuning.
  - Less interpretability compared to simpler models.

### Deep Neural Network (DNN)

- **Advantages:**
  - Can capture intricate patterns in the data.
  - Automatically learns hierarchical features.
  - Suitable for large and complex datasets.
- **Disadvantages:**
  - Requires a large amount of data to avoid overfitting.
  - Sensitive to hyperparameter choices and architecture design.
  - Longer training times, especially on larger networks.


## Considerations:
- **Interpretability**:
  - If it's crucial to easily understand and explain the model, simple ones like Linear Regression are a good choice.
- **Speed**:
  - If we need quick predictions or want to try out different things fast, Linear Regression and LightGBM might be faster.
- **Complexity of Patterns**:
  - If the relationship between things is really complicated, ensemble methods like XGBoost and Random Forest, as well as DNNs, might do well.
- **Data Size**:
  - For small amounts of data, simple models like Linear Regression might be better, while more complex methods like ensemble models and DNNs work better with a lot of data.


## Approach 
- Firstly i thought to do by grouping the each 15 min time intervel with the cluster but the data with demand is less , 40% which is not labled, or trip not booked for the 15 min time interval.
- this is the reason i cannot take the trend into consideration (as some 15 time interval have zero bookings)
- approach was simple, finding the best features more corelation and then building model and tune accordingly
  
## Assumptions:
- If this data is realtime then it may have more correlated features
- even with the weather data (extra)

## Hurdles:
- feature engineering, featuring weather took time
- as some features are not correlated like past demand (very short trend)
  
## Solution
- Correlation is missing in the dataset (major part)
- all models performed till 80-88%




#### Best model at learning this data are DNN and XBoost, but the cost and time of DNN is more than the Xboost



## Bonus
1. For making the model that take request from users we need to deploy them in the web/cloud
   - choosing a development infra like cloud which can handle and scale or inhouse cloud (which is costly)
   - serve the model in framework like Tensorflow serving , fastapi to deply
   - containerize for easy development and reproducibility of models in the environment.
2. We can make the model available for different regions/areas by making replica and hosting them in the cloud (different regions)
   - for better accuracy we also need to localize the model
3. model can be deployed locally or using frameworks or in cloud (custom models)
   - for any extranal apis we need to establish secure connection with keys, authentications
   - api design can be done using RESTful API integrating with app and endpoints need to be correct.
   - monitoring can be done by releasing versions, checking the connection, alerts if any thing stops and feedback from the users for improvement
