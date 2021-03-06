## [Classification](https://app.datacamp.com/learn/courses/supervised-learning-with-scikit-learn)

In this chapter, you will be introduced to classification problems and learn how to solve them using supervised learning techniques. And you’ll apply what you learn to a political dataset, where you classify the party affiliation of United States congressmen based on their voting records.

<br>

### [Which of these is a classification problem?](https://campus.datacamp.com/courses/supervised-learning-with-scikit-learn/classification?ex=2)

```Python
Q: Which of these is a classification problem?
A: Using labeled financial data to predict whether the value of a stock will go up or go down next week.
```

### [Numerical EDA](https://campus.datacamp.com/courses/supervised-learning-with-scikit-learn/classification?ex=4)

```Python
Q: Get started with your EDA now by exploring this voting records dataset numerically. It has been pre-loaded for you into a DataFrame called df. Use pandas' .head(), .info(), and .describe() methods in the IPython Shell to explore the DataFrame, and select the statement below that is not true.
A: There are 17 predictor variables, or features, in this DataFrame.
```

### [Visual EDA](https://campus.datacamp.com/courses/supervised-learning-with-scikit-learn/classification?ex=5)

```Python
Q: Of these two bills, for which ones do Democrats vote resoundingly in favor of, compared to Republicans? 
A: Both 'satellite' and 'missile'.
```

### [k-Nearest Neighbors: Fit](https://campus.datacamp.com/courses/supervised-learning-with-scikit-learn/classification?ex=7)

```Python
# Import KNeighborsClassifier from sklearn.neighbors
from sklearn.neighbors import KNeighborsClassifier 

# Create arrays for the features and the response variable
y = df['party'].values
X = df.drop('party', axis=1).values

# Create a k-NN classifier with 6 neighbors
knn = KNeighborsClassifier(n_neighbors=6)

# Fit the classifier to the data
knn.fit(X, y)
```

### [k-Nearest Neighbors: Fit](https://campus.datacamp.com/courses/supervised-learning-with-scikit-learn/classification?ex=8)

```Python
# Import KNeighborsClassifier from sklearn.neighbors
from sklearn.neighbors import KNeighborsClassifier 

# Create arrays for the features and the response variable
y = df['party'].values
X = df.drop('party', axis=1).values

# Create a k-NN classifier with 6 neighbors: knn
knn = KNeighborsClassifier(n_neighbors=6)

# Fit the classifier to the data
knn.fit(X, y)

# Predict the labels for the training data X: y_pred
y_pred = knn.predict(X)

# Predict and print the label for the new data point X_new
new_prediction = knn.predict(X_new)
print("Prediction: {}".format(new_prediction)) 
```

### [The digits recognition dataset](https://campus.datacamp.com/courses/supervised-learning-with-scikit-learn/classification?ex=10)

```Python
# Import necessary modules
from sklearn import datasets
import matplotlib.pyplot as plt

# Load the digits dataset: digits
digits = datasets.load_digits()

# Print the keys and DESCR of the dataset
print(digits.keys())
print(digits.DESCR)

# Print the shape of the images and data keys
print(digits.images.shape)
print(digits.data.shape)

# Display digit 1010
plt.imshow(digits.images[1010], cmap=plt.cm.gray_r, interpolation='nearest')
plt.show()
```

### [Train/Test Split + Fit/Predict/Accuracy](https://campus.datacamp.com/courses/supervised-learning-with-scikit-learn/classification?ex=11)

```Python
# Import necessary modules
from sklearn.neighbors import KNeighborsClassifier 
from sklearn.model_selection import train_test_split

# Create feature and target arrays
X = digits.data
y = digits.target

# Split into training and test set
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state=42, stratify=y)

# Create a k-NN classifier with 7 neighbors: knn
knn = KNeighborsClassifier(n_neighbors=7)

# Fit the classifier to the training data
knn.fit(X_train, y_train)

# Print the accuracy
print(knn.score(X_test, y_test))
```

### [Overfitting and underfitting](https://campus.datacamp.com/courses/supervised-learning-with-scikit-learn/classification?ex=12)

```Python
# Setup arrays to store train and test accuracies
neighbors = np.arange(1, 9)
train_accuracy = np.empty(len(neighbors))
test_accuracy = np.empty(len(neighbors))

# Loop over different values of k
for i, k in enumerate(neighbors):
    # Setup a k-NN Classifier with k neighbors: knn
    knn = KNeighborsClassifier(n_neighbors=k)

    # Fit the classifier to the training data
    knn.fit(X_train, y_train)
    
    #Compute accuracy on the training set
    train_accuracy[i] = knn.score(X_train, y_train)

    #Compute accuracy on the testing set
    test_accuracy[i] = knn.score(X_test, y_test)

# Generate plot
plt.title('k-NN: Varying Number of Neighbors')
plt.plot(neighbors, test_accuracy, label = 'Testing Accuracy')
plt.plot(neighbors, train_accuracy, label = 'Training Accuracy')
plt.legend()
plt.xlabel('Number of Neighbors')
plt.ylabel('Accuracy')
plt.show()
```