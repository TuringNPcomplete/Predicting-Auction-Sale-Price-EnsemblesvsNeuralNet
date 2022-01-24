# Predicting Auction Sale Price using the kaggle bulldozer auction sales data: Modeling with Ensembles vs NeuralNet
The performances of tree ensembles and neural networks on structured data are evaluated. In addition, the effectiveness of combining \
neural network and decision trees (such as random trees, histogram based gradient boosting, and neural networks) is investigated.
Covariant shift, Random forest's inability to extrapolate, and data leakage are investigated.
A simple 2-layer Neural network outperformed xgboost, followed by random forests. The worst performance based on RMSE was obtained from the histogram based gradient boosting regressor.

Overall, the best rmse (0.220194)--about 4.04% improvement over the kaggle's leaderboard first place score -- was obtained by taking the average of the predictions \
...by the neural network and xgboost regressor.
