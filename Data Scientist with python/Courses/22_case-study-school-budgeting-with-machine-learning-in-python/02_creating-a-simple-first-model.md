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

### [Training a model](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/creating-a-simple-first-model?ex=3)

```
# Import classifiers
from sklearn.linear_model import LogisticRegression
from sklearn.multiclass import OneVsRestClassifier

# Create the DataFrame: numeric_data_only
numeric_data_only = df[NUMERIC_COLUMNS].fillna(-1000)

# Get labels and convert to dummy variables: label_dummies
label_dummies = pd.get_dummies(df[LABELS])

# Create training and test sets
X_train, X_test, y_train, y_test = multilabel_train_test_split(numeric_data_only,
                                                               label_dummies,
                                                               size=0.2, 
                                                               seed=123)

# Instantiate the classifier: clf
clf = OneVsRestClassifier(LogisticRegression())

# Fit the classifier to the training data
clf.fit(X_train, y_train)

# Print the accuracy
print("Accuracy: {}".format(clf.score(X_test, y_test)))
```

### [Use your model to predict values on holdout data](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/creating-a-simple-first-model?ex=5)

```
# Instantiate the classifier: clf
clf = OneVsRestClassifier(LogisticRegression())

# Fit it to the training data
clf.fit(X_train, y_train)

# Load the holdout data: holdout
holdout = pd.read_csv('HoldoutData.csv', index_col=0)

# Generate predictions: predictions
predictions = clf.predict_proba(holdout[NUMERIC_COLUMNS].fillna(-1000))
```

### [Writing out your results to a csv for submission](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/creating-a-simple-first-model?ex=6)

```
# Generate predictions: predictions
predictions = clf.predict_proba(holdout[NUMERIC_COLUMNS].fillna(-1000))

# Format predictions in DataFrame: prediction_df
prediction_df = pd.DataFrame(columns=pd.get_dummies(df[LABELS]).columns,
                             index=holdout.index,
                             data=predictions)

# Save prediction_df to csv
prediction_df.to_csv('predictions.csv')

# Submit the predictions for scoring: score
score = score_submission(pred_path='predictions.csv')

# Print score
print('Your model, trained with numeric data only, yields logloss score: {}'.format(score))
```

### [Tokenizing text](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/creating-a-simple-first-model?ex=8)

```
Q: How many tokens (1-grams) are in the string "Title I - Disadvantaged Children/Targeted Assistance" if we tokenize on whitespace and punctuation?
A:6.
```

### [Testing your NLP credentials with n-grams](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/creating-a-simple-first-model?ex=9)

```
Q: In this exercise, your job is to determine the sum of the sizes of 1-grams, 2-grams and 3-grams generated by the string petro-vend fuel and fluids, tokenized on punctuation.
A: 12.
```

### [Creating a bag-of-words in scikit-learn](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/creating-a-simple-first-model?ex=11)

```
# Import CountVectorizer
from sklearn.feature_extraction.text import CountVectorizer

# Create the token pattern: TOKENS_ALPHANUMERIC
TOKENS_ALPHANUMERIC = '[A-Za-z0-9]+(?=\\s+)'

# Fill missing values in df.Position_Extra
df.Position_Extra.fillna('', inplace=True)

# Instantiate the CountVectorizer: vec_alphanumeric
vec_alphanumeric = CountVectorizer(token_pattern=TOKENS_ALPHANUMERIC)

# Fit to the data
vec_alphanumeric.fit(df.Position_Extra)

# Print the number of tokens and first 15 tokens
msg = "There are {} tokens in Position_Extra if we split on non-alpha numeric"
print(msg.format(len(vec_alphanumeric.get_feature_names())))
print(vec_alphanumeric.get_feature_names()[:15])
```

### [Combining text columns for tokenization](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/creating-a-simple-first-model?ex=12)

```
# Define combine_text_columns()
def combine_text_columns(data_frame, to_drop=NUMERIC_COLUMNS + LABELS):
    """ converts all text in each row of data_frame to single vector """
    
    # Drop non-text columns that are in the df
    to_drop = set(to_drop) & set(data_frame.columns.tolist())
    text_data = data_frame.drop(to_drop, axis=1)
    
    # Replace nans with blanks
    text_data.fillna("", inplace=True)
    
    # Join all text items in a row that have a space in between
    return text_data.apply(lambda x: " ".join(x), axis=1)
```

### [What's in a token?](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/creating-a-simple-first-model?ex=13)

```
# Import the CountVectorizer
from sklearn.feature_extraction.text import CountVectorizer

# Create the basic token pattern
TOKENS_BASIC = '\\S+(?=\\s+)'

# Create the alphanumeric token pattern
TOKENS_ALPHANUMERIC = '[A-Za-z0-9]+(?=\\s+)'

# Instantiate basic CountVectorizer: vec_basic
vec_basic = CountVectorizer(token_pattern=TOKENS_BASIC)

# Instantiate alphanumeric CountVectorizer: vec_alphanumeric
vec_alphanumeric = CountVectorizer(token_pattern=TOKENS_ALPHANUMERIC)

# Create the text vector
text_vector = combine_text_columns(df)

# Fit and transform vec_basic
vec_basic.fit_transform(text_vector)

# Print number of tokens of vec_basic
print("There are {} tokens in the dataset".format(len(vec_basic.get_feature_names())))

# Fit and transform vec_alphanumeric
vec_alphanumeric.fit_transform(text_vector)

# Print number of tokens of vec_alphanumeric
print("There are {} alpha-numeric tokens in the dataset".format(len(vec_alphanumeric.get_feature_names())))
```