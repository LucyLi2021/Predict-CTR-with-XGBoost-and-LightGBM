# Predict CTR with XGBoost and LightGBM

My undergraduate thesis: Predicting CTR about recommended ads with XGBoost and LightGBM

Because Internet companies have a natural user pool and generate innumerable data every day, how to make full use of these data to actively recommend advertisements to users and obtain more revenue has become the top priority of the company's development. Taking JD.com as an example, the company has developed the platforms of Shufang and Jingshutong, focusing on the precise placement of advertisements by people. In Shufang, users are affixed with various labels to facilitate targeted crowd selection to place advertisements; in Jingshutong, advertisements placed are tracked to facilitate the detection of placement effects. An indispensable indicator for evaluating effects is the click-through rate of advertisements. The more users click on the advertisement, the higher the advertiser's profit may be.

This article selects the data of question A in the "2020 DIGIX GLOBAL AI CHALLENGE" of Huawei's 2020 competition. The topic of the question is "Advertisement CTR Prediction". The data has 41,907,133 rows, including 36 variables, which can be downloaded directly from websites such as Kaggle. It should be noted that, based on user privacy considerations, the data has been anonymized. Because the XGBoost and LightGBM models have frequently won awards in competitions in recent years, this article selects these two models to train and predict data. Based on the models, this article chooses the AUC and Log Loss functions to evaluate the performance of the model training, and chooses the accuracy, precision, recall and F1 to evaluate the performance of the model prediction.

During the data preprocessing, because the clicked data is significantly less than the unclicked data, the data is unbalanced. This article first performs a down sampling operation on the data to obtain 500,000 samples while eliminating the unbalance. Then, this article deletes the useless columns, and combines the one-hot encoding to determine the processing method of the text format data. Finally, the importance of variables is ranked by training the XGBoost and LightGBM models with default parameters, and then the variables with the lowest importance are deleted in turn to determine the optimal set of variables.

During model training, the parameters are tuned through grid search and cross-validation to try to obtain a relatively optimal model. Because in reality, the magnitude of the data is very large, the training speed of the model is also an important reference factor. After the model is tuned, the best model evaluated in terms of accuracy and efficiency is the LightGBM model with Log Loss as the evaluation function, and the Log Loss value is 0.6108. The main reason is that the training speed of LightGBM is significantly faster than that of XGBoost, which is about three times of XGBoost, and the difference in accuracy between the two is not obvious. The final model predicts that the accuracy is 66.96%, the precision is 68.43%, the recall is 62.96%, the F1 is 65.58%, and the recommended ad click-through rate is 31.48%.

In addition to tuning parameters through grid search, we can also optimize the data acquisition process. This article originally used pure random sampling to obtain sample data, but the existence of randomness may cause some data containing important information to be deleted. Therefore, this paper combines random sampling and k-means clustering, and collects sample data in each category. In this way, not only the imbalance of the sample is eliminated, but the original information is retained. After re-tuning the parameters, the Log Loss value of LightGBM is 0.5977. Because the Log Loss should be as small as possible, the performance of the model is improved. The prediction results are also improved, the accuracy is 67.99%, the precision is 69.17%, the recall rate is 64.91%, the F1 is 66.97%, and the recommended ad click-through rate is 32.46%.

In general, this paper optimizes the model through cluster sampling and parameter grid search, and compares the performance of XGBoost and LightGBM in a multi-dimensional manner. Finally, an optimal click-through rate prediction model is established, which predicts user behavior from disorganized data and makes decisions about advertising recommendations.
