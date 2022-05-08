## [Model Tuning](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/model-tuning)

The hyperparameters of a machine learning model are parameters that are not learned from data. They should be set prior to fitting the model to the training set. In this chapter, you'll learn how to tune the hyperparameters of a tree-based model using grid search cross validation.

<br>

### [Tree hyperparameters](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/model-tuning?ex=2)

```
Q: Which of the following is not a hyperparameter of dt?
A: min_features
```

### [Set the tree's hyperparameter grid](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/model-tuning?ex=3)

```
# Define params_dt
params_dt = {'max_depth': [2, 3, 4], 'min_samples_leaf': [0.12, 0.14, 0.16, 0.18]}
```

### [Search for the optimal tree](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/model-tuning?ex=4)

```
# Import GridSearchCV
from sklearn.model_selection import GridSearchCV

# Instantiate grid_dt
grid_dt = GridSearchCV(estimator=dt,
                       param_grid=params_dt,
                       scoring='roc_auc',
                       cv=5,
                       n_jobs=-1)
```

### [Evaluate the optimal tree](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/model-tuning?ex=5)

```
# Import roc_auc_score from sklearn.metrics 
from sklearn.metrics import roc_auc_score

# Extract the best estimator
best_model = grid_dt.best_estimator_

# Predict the test set probabilities of the positive class
y_pred_proba = best_model.predict_proba(X_test)[:,1]

# Compute test_roc_auc
test_roc_auc = roc_auc_score(y_test, y_pred_proba)

# Print test_roc_auc
print('Test set ROC AUC score: {:.3f}'.format(test_roc_auc))
```

### [Random forests hyperparameters](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/model-tuning?ex=7)

```
Q: Which of the following is not a hyperparameter of rf?
A: learning_rate
```

### [Set the hyperparameter grid of RF](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/model-tuning?ex=8)

```
# Define the dictionary 'params_rf'
params_rf = {'n_estimators': [100, 350, 500], 'max_features': ['log2', 'auto', 'sqrt'], 'min_samples_leaf': [2, 10, 30]}
```

### [Search for the optimal forest](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/model-tuning?ex=9)

```
# Import GridSearchCV
from sklearn.model_selection import  GridSearchCV

# Instantiate grid_rf
grid_rf = GridSearchCV(estimator=rf,
                       param_grid=params_rf,
                       scoring='neg_mean_squared_error',
                       cv=3,
                       verbose=1,
                       n_jobs=-1)
```

### [Evaluate the optimal forest](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/model-tuning?ex=10)

```
# Import mean_squared_error from sklearn.metrics as MSE 
from sklearn.metrics import mean_squared_error as MSE

# Extract the best estimator
best_model = grid_rf.best_estimator_

# Predict test set labels
y_pred = best_model.predict(X_test)

# Compute rmse_test
rmse_test = MSE(y_test, y_pred)**0.5

# Print rmse_test
print('Test RMSE of best model: {:.3f}'.format(rmse_test))
```