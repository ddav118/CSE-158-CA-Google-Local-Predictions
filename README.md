# CSE-158---CA-Google-Local-Predictions
In this project we built a Machine Learning Model to predict the ratings of businesses using California Google Local Data (https://cseweb.ucsd.edu/~jmcauley/datasets.html#google_local)

This project was completed in a group of 3 students for the CSE 158 course at UC San Diego during Fall 2021 quarter.

Data description:
each review contains: 
- "user_id"
- "business_id"
- temporal data regarding when the review was submitted
- categories of the reviewed business
- full text of the review
- overall rating of the business on 0-5 inclusive scale (only integers)

Data subset criteria:
1) each user has reviewed a minimum of 5 businesses
2) each business has a minimum of 5 reviews
3) businesses are located in California

Description of Major Files
1. "CA_5.json.gz": file contains all user ratings of businesses with the subset criteria mentioned above
2. "places_CA.json.gz": file contains all business description metadata
3. "David/Assignment2-David.ipynb": all exploratory data analysis, feature extraction methods, and machine learning models were created and tested in this file
4. "Final Report.pdf": file contains detailed report containing the model selection steps, baseline models for comparison, and results for the best performing model. This file is the MOST IMPORTANT for comprehending the methods used during this project!

Features considered:
- sentiment analysis using 1000 most popular n-grams upto length 5
- one-hot-encoded price
- item2vec
- user rating from cosine similarity
- and temporal analysis

Results:
1) Ridge Regression Model: We were most pleased with the overall performance of the Ridge Regression model in comparison to the 3 Baseline models and alternative regression models in terms of MSE: 0.607 for this model compared to 0.764, 0.727, and 0.718 for the respective baselines.

2) Ablation Experiment: However, the large discrepancy in MSE between the train and validation sets led us to believe that this model was overfitting the training data. As such, we conducted an ablation experiment in which we removed each feature from the model one-by-one. For our final model, we ended up completely removing both the user rating from cosine similarity and temporal regression features due to the decreases in validation MSE when these features were removed during the ablation experiment. As such, the train and validation MSE’s for the final model were 0.510 and 0.575, respectively. Since these two MSE values are much closer, this suggests that our model is not overfitting the training data.

3) Feature Importances: From the results of the ablation experiment, the ranking of features from most-least important was: review text sentiment analysis using n-grams upto 5, Item2Vec, One-Hot Encoded Price, Temporal Dynamics, and the User Reviews from Cosine Similarities of Businesses. The Validation MSE’s from each step of the ablation experiment were 0.691, 0.611, 0.609, 0.599, and 0.573 for the respective features above. Clearly, the Sentiment Analysis Feature using the 1000 most popular n-grams of review text data proved to be the most important feature since the Validation MSE increased drastically when it was removed from the model.

4) Hyperparameter Tuning: Once we finalized which parameters to use, we performed hyperparameter tuning of the final Ridge Regression model using the validation set, and determined that the regularization coefficient C=1 gave the lowest MSE values on the validation set. Reported Test MSE: For our final step, we calculated the MSE to be 0.568 from the predictions of this tuned Ridge Regression Model on the untouched test set. This means that on average, this model predicts ratings 0.753 [or sqrt(0.568)] stars away from the true rating for this dataset.

References:
[1] Rajiv Pasricha, Julian McAuley. 2018.
Translation-based factorization machines
for sequential recommendation. In RecSys
[2] Ruining He, Wang-Cheng Kang, Julian
McAuley. 2017. Translation-based
recommendation. In RecSys
[3] Farman Ullah, Ghulam Sarwar, Sung
Chang Lee, Yun Kyung Park, Kyeong
Deok Moon, and Jin Tae Kim. 2012.
Hybrid recommender system with
temporal information. In ICOIN. IEEE.
[4] Yehuda Koren. 2010. Collaborative
Filtering with Temporal Dynamics.
Commun. ACM (2010).
