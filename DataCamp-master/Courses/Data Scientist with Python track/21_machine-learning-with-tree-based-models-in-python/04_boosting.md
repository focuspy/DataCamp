## [Boosting](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/boosting)

Boosting refers to an ensemble method in which several models are trained sequentially with each model learning from the errors of its predecessors. In this chapter, you'll be introduced to the two boosting methods of AdaBoost and Gradient Boosting.

<br>

### [Define the AdaBoost classifier](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/boosting?ex=2)

```
# Import DecisionTreeClassifier
from sklearn.tree import DecisionTreeClassifier

# Import AdaBoostClassifier
from sklearn.ensemble import AdaBoostClassifier

# Instantiate dt
dt = DecisionTreeClassifier(max_depth = 2, random_state=1)

# Instantiate ada
ada = AdaBoostClassifier(base_estimator=dt, n_estimators=180, random_state=1)
```

### [Train the AdaBoost classifier](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/boosting?ex=3)

```
# Fit ada to the training set
ada.fit(X_train, y_train)

# Compute the probabilities of obtaining the positive class
y_pred_proba = ada.predict_proba(X_test)[:, 1]
```

### [Evaluate the AdaBoost classifier](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/boosting?ex=4)

```
# Import roc_auc_score
from sklearn.metrics import roc_auc_score

# Evaluate test-set roc_auc_score
ada_roc_auc = roc_auc_score(y_test, y_pred_proba)

# Print roc_auc_score
print('ROC AUC score: {:.2f}'.format(ada_roc_auc))
```

### [Define the GB regressor](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/boosting?ex=6)

```
# Import GradientBoostingRegressor
from sklearn.ensemble import GradientBoostingRegressor 

# Instantiate gb
gb = GradientBoostingRegressor(max_depth = 4, 
            n_estimators = 200,
            random_state=2)
```

### [Train the GB regressor](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/boosting?ex=7)

```
# Fit gb to the training set
gb.fit(X_train, y_train)

# Predict test set labels
y_pred = gb.predict(X_test)
```

### [Evaluate the GB regressor](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/boosting?ex=8)

```
# Import mean_squared_error as MSE
from sklearn.metrics import mean_squared_error as MSE

# Compute MSE
mse_test = MSE(y_test, y_pred)

# Compute RMSE
rmse_test = mse_test ** 0.5

# Print RMSE
print('Test set RMSE of gb: {:.3f}'.format(rmse_test))
```

### [Regression with SGB](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/boosting?ex=10)

```
# Import GradientBoostingRegressor
from sklearn.ensemble import GradientBoostingRegressor

# Instantiate sgbr
sgbr = GradientBoostingRegressor(max_depth=4, 
            subsample=0.9,
            max_features=0.75,
            n_estimators=200,
            random_state=2)
```

### [Train the SGB regressor](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/boosting?ex=11)

```
# Fit sgbr to the training set
sgbr.fit(X_train, y_train)

# Predict test set labels
y_pred = sgbr.predict(X_test)
```

### [Evaluate the SGB regressor](https://campus.datacamp.com/courses/machine-learning-with-tree-based-models-in-python/boosting?ex=12)

```
# Import mean_squared_error as MSE
from sklearn.metrics import mean_squared_error as MSE

# Compute test set MSE
mse_test = MSE(y_test, y_pred)

# Compute test set RMSE
rmse_test = mse_test ** 0.5

# Print rmse_test
print('Test set RMSE of sgbr: {:.3f}'.format(rmse_test))
```