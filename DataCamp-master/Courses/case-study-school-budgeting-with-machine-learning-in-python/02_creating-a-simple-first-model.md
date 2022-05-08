## [Creating a simple first model](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/creating-a-simple-first-model)

In this chapter, you'll build a first-pass model. You'll use numeric data only to train the model. Spoiler alert - throwing out all of the text data is bad for performance! But you'll learn how to format your predictions. Then, you'll be introduced to natural language processing (NLP) in order to start working with the large amounts of text in the data.

<br>

### [Setting up a train-test split in scikit-learn](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/creating-a-simple-first-model?ex=2)

```
# Setting up a train-test split in scikit-learn
# Create the new DataFrame: numeric_data_only
numeric_data_only = df[NUMERIC_COLUMNS].fillna(-1000)

# Get labels and convert to dummy variables: label_dummies
label_dummies = pd.get_dummies(df[LABELS])

# Create training and test sets
# size of your test set to be 0.2
X_train, X_test, y_train, y_test = multilabel_train_test_split(numeric_data_only,
                                                               label_dummies,
                                                               size=0.2, 
                                                               seed=123)

# Print the info
print("X_train info:")
print(X_train.info())
print("\nX_test info:")  
print(X_test.info())
print("\ny_train info:")  
print(y_train.info())
print("\ny_test info:")  
print(y_test.info())
```