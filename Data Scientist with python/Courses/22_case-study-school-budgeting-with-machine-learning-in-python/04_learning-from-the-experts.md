## [Learning from the experts](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/learning-from-the-experts)

In this chapter, you will learn the tricks used by the competition winner, and implement them yourself using scikit-learn. Enjoy!

<br>

### [How many tokens?](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/learning-from-the-experts?ex=2)

```Python
Q: Assuming we tokenize on punctuation, accepting only alpha-numeric sequences as tokens, how many tokens are in the following string from the main dataset
A: 4, because , and & are not tokens
```

### [Deciding what's a word](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/learning-from-the-experts?ex=3)

```Python
# Import the CountVectorizer
from sklearn.feature_extraction.text import CountVectorizer

# Create the text vector
text_vector = combine_text_columns(X_train)

# Create the token pattern: TOKENS_ALPHANUMERIC
TOKENS_ALPHANUMERIC = '[A-Za-z0-9]+(?=\\s+)'

# Instantiate the CountVectorizer: text_features
text_features = CountVectorizer(token_pattern=TOKENS_ALPHANUMERIC)

# Fit text_features to the text vector
text_features.fit(text_vector)

# Print the first 10 tokens
print(text_features.get_feature_names()[:10])
```

### [N-gram range in scikit-learn](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/learning-from-the-experts?ex=4)

```Python
# Import pipeline
from sklearn.pipeline import Pipeline

# Import classifiers
from sklearn.linear_model import LogisticRegression
from sklearn.multiclass import OneVsRestClassifier

# Import CountVectorizer
from sklearn.feature_extraction.text import CountVectorizer

# Import other preprocessing modules
from sklearn.preprocessing import Imputer
from sklearn.feature_selection import chi2, SelectKBest

# Select 300 best features
chi_k = 300

# Import functional utilities
from sklearn.preprocessing import FunctionTransformer, MaxAbsScaler
from sklearn.pipeline import FeatureUnion

# Perform preprocessing
get_text_data = FunctionTransformer(combine_text_columns, validate=False)
get_numeric_data = FunctionTransformer(lambda x: x[NUMERIC_COLUMNS], validate=False)

# Create the token pattern: TOKENS_ALPHANUMERIC
TOKENS_ALPHANUMERIC = '[A-Za-z0-9]+(?=\\s+)'

# Instantiate pipeline: pl
pl = Pipeline([
        ('union', FeatureUnion(
            transformer_list = [
                ('numeric_features', Pipeline([
                    ('selector', get_numeric_data),
                    ('imputer', Imputer())
                ])),
                ('text_features', Pipeline([
                    ('selector', get_text_data),
                    ('vectorizer', CountVectorizer(token_pattern=TOKENS_ALPHANUMERIC,
                                                   ngram_range=(1, 2))),
                    ('dim_red', SelectKBest(chi2, chi_k))
                ]))
             ]
        )),
        ('scale', MaxAbsScaler()),
        ('clf', OneVsRestClassifier(LogisticRegression()))
    ])
```

### [Which models of the data include interaction terms?](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/learning-from-the-experts?ex=6)

```Python
Q: Which expression(s) include interaction terms?
A: The second expression.
```

### [Implement interaction modeling in scikit-learn](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/learning-from-the-experts?ex=7)

```Python
# Instantiate pipeline: pl
pl = Pipeline([
        ('union', FeatureUnion(
            transformer_list = [
                ('numeric_features', Pipeline([
                    ('selector', get_numeric_data),
                    ('imputer', Imputer())
                ])),
                ('text_features', Pipeline([
                    ('selector', get_text_data),
                    ('vectorizer', CountVectorizer(token_pattern=TOKENS_ALPHANUMERIC, 
                                                   ngram_range=(1, 2))),
                    ('dim_red', SelectKBest(chi2, chi_k))
                ]))
             ]
        )),
        ('int', SparseInteractions(degree=2)),
        ('scale', MaxAbsScaler()),
        ('clf', OneVsRestClassifier(LogisticRegression()))
    ])
```

### [Why is hashing a useful trick?](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/learning-from-the-experts?ex=9)

```Python
Q: Why is hashing a useful trick?
A: Some problems are memory-bound and not easily parallelizable, and hashing enforces a fixed length computation instead of using a mutable datatype (like a dictionary).
```

### [Implementing the hashing trick in scikit-learn](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/learning-from-the-experts?ex=10)

```Python
# Import HashingVectorizer
from sklearn.feature_extraction.text import HashingVectorizer

# Get text data: text_data
text_data = combine_text_columns(X_train)

# Create the token pattern: TOKENS_ALPHANUMERIC
TOKENS_ALPHANUMERIC = '[A-Za-z0-9]+(?=\\s+)' 

# Instantiate the HashingVectorizer: hashing_vec
hashing_vec = HashingVectorizer(token_pattern=TOKENS_ALPHANUMERIC)

# Fit and transform the Hashing Vectorizer
hashed_text = hashing_vec.fit_transform(text_data)

# Create DataFrame and print the head
hashed_df = pd.DataFrame(hashed_text.data)
print(hashed_df.head())
```

### [Build the winning model](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/learning-from-the-experts?ex=11)

```Python
# Import the hashing vectorizer
from sklearn.feature_extraction.text import HashingVectorizer

# Instantiate the winning model pipeline: pl
pl = Pipeline([
        ('union', FeatureUnion(
            transformer_list = [
                ('numeric_features', Pipeline([
                    ('selector', get_numeric_data),
                    ('imputer', Imputer())
                ])),
                ('text_features', Pipeline([
                    ('selector', get_text_data),
                    ('vectorizer', HashingVectorizer(token_pattern=TOKENS_ALPHANUMERIC,
                                                     non_negative=True, norm=None, binary=False,
                                                     ngram_range=(1, 2))),
                    ('dim_red', SelectKBest(chi2, chi_k))
                ]))
             ]
        )),
        ('int', SparseInteractions(degree=2)),
        ('scale', MaxAbsScaler()),
        ('clf', OneVsRestClassifier(LogisticRegression()))
    ])
```

### [What tactics got the winner the best score?](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/learning-from-the-experts?ex=12)

```Python
Q: What tactics got the winner the best score?
A: The winner used skillful NLP, efficient computation, and simple but powerful stats tricks to master the budget data.
```