## [Introduction to Clustering](https://campus.datacamp.com/courses/cluster-analysis-in-python/introduction-to-clustering)

Before you are ready to classify news articles, you need to be introduced to the basics of clustering. This chapter familiarizes you with a class of machine learning algorithms called unsupervised learning and then introduces you to clustering, one of the popular unsupervised learning algorithms. You will know about two popular clustering techniques - hierarchical clustering and k-means clustering. The chapter concludes with basic pre-processing steps before you start clustering data.

<br>

### [Unsupervised learning in real world](https://campus.datacamp.com/courses/cluster-analysis-in-python/introduction-to-clustering?ex=2)

```
Q: Which of the following examples can be solved with unsupervised learning?
A: Segmentation of learners at DataCamp based on courses they complete. The training data has no labels.
```

### [Pokémon sightings](https://campus.datacamp.com/courses/cluster-analysis-in-python/introduction-to-clustering?ex=3)

```
# Import plotting class from matplotlib library
from matplotlib import pyplot as plt

# Create a scatter plot
plt.scatter(x, y)

# Display the scatter plot
plt.show()
```

### [Pokémon sightings: hierarchical clustering](https://campus.datacamp.com/courses/cluster-analysis-in-python/introduction-to-clustering?ex=5)

```
# Import kmeans and vq functions
from scipy.cluster.vq import kmeans, vq

# Compute cluster centers
centroids,_ = kmeans(df, 2)

# Assign cluster labels
df['cluster_labels'], _ = vq(df, centroids)

# Plot the points with seaborn
sns.scatterplot(x='x', y='y', hue='cluster_labels', data=df)
plt.show()
```

### [Normalize basic list data](https://campus.datacamp.com/courses/cluster-analysis-in-python/introduction-to-clustering?ex=8)

```
# Import the whiten function
from scipy.cluster.vq import whiten

goals_for = [4,3,2,3,1,1,2,0,1,4]

# Use the whiten() function to standardize the data
scaled_data = whiten(data)
print(scaled_data)
```

### [](https://campus.datacamp.com/courses/cluster-analysis-in-python/introduction-to-clustering?ex=8)

```
# Import the whiten function
from scipy.cluster.vq import whiten

goals_for = [4,3,2,3,1,1,2,0,1,4]

# Use the whiten() function to standardize the data
scaled_data = whiten(goals_for)
print(scaled_data)
```

### [Visualize normalized data](https://campus.datacamp.com/courses/cluster-analysis-in-python/introduction-to-clustering?ex=9)

```
# Plot original data
plt.plot(goals_for, label='original')

# Plot scaled data
plt.plot(scaled_data, label='scaled')

# Show the legend in the plot
plt.legend()

# Display the plot
plt.show()
```

### [Normalization of small numbers](https://campus.datacamp.com/courses/cluster-analysis-in-python/introduction-to-clustering?ex=10)

```
# Prepare data
rate_cuts = [0.0025, 0.001, -0.0005, -0.001, -0.0005, 0.0025, -0.001, -0.0015, -0.001, 0.0005]

# Use the whiten() function to standardize the data
scaled_data = whiten(rate_cuts)

# Plot original data
plt.plot(rate_cuts, label='original')

# Plot scaled data
plt.plot(scaled_data, label='scaled')

plt.legend()
plt.show()
```

### [FIFA 18: Normalize data](https://campus.datacamp.com/courses/cluster-analysis-in-python/introduction-to-clustering?ex=11)

```
# Scale wage and value
fifa['scaled_wage'] = whiten(fifa['eur_wage'])
fifa['scaled_value'] = whiten(fifa['eur_value'])

#####################################################

# Scale wage and value
fifa['scaled_wage'] = whiten(fifa['eur_wage'])
fifa['scaled_value'] = whiten(fifa['eur_value'])

# Plot the two columns in a scatter plot
fifa.plot(x='scaled_wage', y='scaled_value', kind='scatter')
plt.show()

#####################################################

# Scale wage and value
fifa['scaled_wage'] = whiten(fifa['eur_wage'])
fifa['scaled_value'] = whiten(fifa['eur_value'])

# Plot the two columns in a scatter plot
fifa.plot(x='scaled_wage', y='scaled_value', kind = 'scatter')
plt.show()

# Check mean and standard deviation of scaled values
print(fifa[['scaled_wage', 'scaled_value']].describe())
```