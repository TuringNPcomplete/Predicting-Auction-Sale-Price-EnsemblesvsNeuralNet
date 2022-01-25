# Predicting Auction Sale Price using the kaggle bulldozer auction sales data: Modeling with Ensembles vs NeuralNet
The performances of tree ensembles and neural networks on structured data are evaluated. In addition, the effectiveness of combining neural network and decision trees (such as random trees, histogram based gradient boosting, and xgboost) is investigated.
Covariant shift, Random forest's inability to extrapolate, and data leakage are investigated.

A simple 2-layer Neural network outperformed xgboost, followed by random forests. The worst performance based on RMSE was obtained from the histogram based gradient boosting regressor.

Overall, the best rmse **(0.220194)**--about **4.04%** improvement over the kaggle's leaderboard first place score -- was obtained by taking the average of the predictions by the neural network and xgboost regressor.

**Key takeaways**: 
1. Random forests are generally bad at extrapolating, hence, if there is a shift in the domain between the training input and the validation (or test) inputs, then the random forest model will perform rather poorly on the validation set(or test set).

![rf_failure](https://user-images.githubusercontent.com/50182879/150931611-fc849e6e-3cff-4e75-9bff-6c16b1d749e5.png)
The red portion of the plot above shows the extrapolation problem. The random forest was trained on the first 70% of the data and used to make predictions on thr full data including the last 30%. It fails because there is an obvious linear trend it was unable to properly capture. Moreover, the predictions by random forests are confined within the range of the training input labels, since random forests make predictions by taking the average of previously observed data. Hence, when the input for prediction is 

2. To improve the performance of random forests, you could attempt to find the columns or features on which the training and validation sets differ the most. You may drop the ones that least impacts the accuracy of the model. To achieve this, I trained a random forest that can tell if a given input is from a training set or validation set. This helped me determine if a validation set has the same or similar distribution as the training set. Lastly, I computed the feature importances. The feature importances for this model revealed the degree of dissimilarity of the features between the training and validation sets. The features with high feature importances are the most dissimilar between the sets. `salesID` and `machineID` were significantly different between the sets but impacts RMSE the least, hence they were dropped.

3. For forecasting tasks (time dependent targets), the validation set should not be arbitrarily chosen i.e `train_test_split` may not be your best option for splitting the data. Since you are looking to make predictions on future sales, your validation set should contain more recent data, so that if your model is able to do well on the validation set, then, you can be more confident about its predictions in the future.

4. Data leakage should be investigated. Signs of data leakage include:
   * Unrealistically high level of performance on the test set
   * Apparently meaningless feature(s) scoring very high feature importance
   * Partial dependence plots that do not make sense.
  
  ![popularity](https://user-images.githubusercontent.com/50182879/150969313-721a0836-ae6d-410c-9fda-18f2e8461d95.png)![partial_dependence](https://user-images.githubusercontent.com/50182879/150969324-ce23809b-6d18-4f7a-8237-7322bab2a411.png)




5. An histogram based gradient boosting regressor may not be the best for forecasting or time dependent data

3. A simple Neural network can show superior performance on structured data. A 2-layer neural network showed a 1.93% improvement in RMSE compared to the best random forest model.

4. There is a likely benefit to be derived by using an ensemble of models. In this project, the 
