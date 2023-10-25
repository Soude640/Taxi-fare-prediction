New York City Taxi Fare Prediction
Training an ML model to predict taxi fares using Google BigQueryML and NYC TLC Trips

NYC taxi fare prediction Kaggle Challenge

Experiment Details
This dataset is available on Google Cloud Public Datasets, and it contains New York City's taxi and limousine trips since 2009. in it's tables, it usually contains fields like number of passengers, pickup and dropoff latitude and longitude, trip distance, fare amount, tax amount, tolls amount, payment information, tips , taxes , etc. We use Google BigQuery to dive into the data and train a regression model on it. Google BigQuery is a standard SQL developed by Google. and it allows us to explore and train on terabytes and terabytes of data while dealing with memory limits and operation headaches.

In this project, we first loaded the dataset into BigQuery and decided to filter outliers by limiting the fare amount to 6–200 dollars and limiting the pickup and dropoff locations to New York City itself in order to avoid very long cab trips in our train and evaulation set. These two decreased number of rows from 1 billion to 820 million. For this experiment, we didn't want to use all the 820 million rows for training or evaluation. Instead, we used FARM_FINGERPRINT as a hash function on the pickup_datetime column and picked 1/1000 of the data for training and another 1/1000 of the data for evaluation. For feature engineering, we picked tolls_amount + fare_amount to be the labels for prediction (because tips are considered noise in total_fare). We used day of week, hour of day, Euclidean distance between pickup and dropoff point, and distance between pickup and dropoff point in latitude and longitude and passengers count as our features. Google BigQuery is pretty new; it only supports linear regression models from all types of regression models. Thus, we used linear regression as our model. After that, we calculated RMSE as an evaluation metric, and it was about 5. Thus, the model could predict the fare amount with 5-dollar accuracy, which is not bad for such a small training set and simple model. We can reach better accuracy with training on more data, filtering outliers, using normalization on some features, and picking more complex models.
