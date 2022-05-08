## [Exploring the raw data](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/exploring-the-raw-data)

In this chapter, you'll be introduced to the problem you'll be solving in this course. How do you accurately classify line-items in a school budget based on what that money is being used for? You will explore the raw text and numeric values in the dataset, both quantitatively and visually. And you'll learn how to measure success when trying to predict class labels for each row of the dataset.

<br>

### [What category of problem is this?](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/exploring-the-raw-data?ex=2)

```
Q: What type of machine learning problem is this?
A: Supervised Learning, because the model will be trained using labeled examples.
```

### [What is the goal of the algorithm?](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/exploring-the-raw-data?ex=3)

```
Q:  In this exercise you will tell us what type of supervised machine learning problem this is, and why you think so.
A: Classification, because predicted probabilities will be used to select a label class.
```

### [Loading the data](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/exploring-the-raw-data?ex=5)

```
Q: Use df.info() in the IPython Shell to answer the following questions
A: 1560 rows, 25 columns, 1131 non-null entries in Job_Title_Description.
```

### [Summarizing the data](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/exploring-the-raw-data?ex=6)

```
# Print the summary statistics
print(df.describe())

# Import matplotlib.pyplot as plt
import matplotlib.pyplot as plt

# Create the histogram
plt.hist(df['FTE'].dropna())


# Add title and labels
plt.title('Distribution of %full-time \n employee works')
plt.xlabel('% of full-time')
plt.ylabel('num employees')

# Display the histogram
plt.show()
```

### [Exploring datatypes in pandas](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/exploring-the-raw-data?ex=8)

```
Q: How many columns with dtype object are in the data?
A: 23.
```

### [Encode the labels as categorical variables](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/exploring-the-raw-data?ex=9)

```
# Define the lambda function: categorize_label
categorize_label = lambda x: x.astype('category')

# Convert df[LABELS] to a categorical type
df[LABELS] = df[LABELS].apply(categorize_label, axis=0)

# Print the converted dtypes
print(df[LABELS].dtypes)
```

### [Counting unique labels](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/exploring-the-raw-data?ex=10)

```
# Import matplotlib.pyplot
import matplotlib.pyplot as plt

# Calculate number of unique values for each label: num_unique_labels
num_unique_labels = df[LABELS].apply(pd.Series.nunique)

# Plot number of unique values for each label
num_unique_labels.plot(kind='bar')

# Label the axes
plt.xlabel('Labels')
plt.ylabel('Number of unique values')

# Display the plot
plt.show()
```

### [Penalizing highly confident wrong answers](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/exploring-the-raw-data?ex=12)

```
Q: Select the ordering of the examples which corresponds to the lowest to highest log loss scores. y is an indicator of whether the example was classified correctly. You shouldn't need to crunch any numbers!
A: Lowest: A, Middle: C, Highest: B.
```

### [Computing log loss with NumPy](https://campus.datacamp.com/courses/case-study-school-budgeting-with-machine-learning-in-python/exploring-the-raw-data?ex=13)

```
# Compute and print log loss for 1st case
correct_confident_loss = compute_log_loss(correct_confident, actual_labels)
print("Log loss, correct and confident: {}".format(correct_confident_loss)) 

# Compute log loss for 2nd case
correct_not_confident_loss = compute_log_loss(correct_not_confident, actual_labels)
print("Log loss, correct and not confident: {}".format(correct_not_confident_loss)) 

# Compute and print log loss for 3rd case
wrong_not_confident_loss = compute_log_loss(wrong_not_confident, actual_labels)
print("Log loss, wrong and not confident: {}".format(wrong_not_confident_loss)) 

# Compute and print log loss for 4th case
wrong_confident_loss = compute_log_loss(wrong_confident, actual_labels)
print("Log loss, wrong and confident: {}".format(wrong_confident_loss)) 

# Compute and print log loss for actual labels
actual_labels_loss = compute_log_loss(actual_labels, actual_labels)
print("Log loss, actual labels: {}".format(actual_labels_loss)) 
```