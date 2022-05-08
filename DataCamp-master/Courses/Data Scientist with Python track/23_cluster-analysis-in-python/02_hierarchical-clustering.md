## [Hierarchical Clustering](https://campus.datacamp.com/courses/cluster-analysis-in-python/hierarchical-clustering-877595ec-58cd-4cf5-837c-704a42eb8776)

This chapter focuses on a popular clustering algorithm - hierarchical clustering - and its implementation in SciPy. In addition to the procedure to perform hierarchical clustering, it attempts to help you answer an important question - how many clusters are present in your data? The chapter concludes with a discussion on the limitations of hierarchical clustering and discusses considerations while using hierarchical clustering.

<br>

### [Hierarchical clustering: ward method](https://campus.datacamp.com/courses/cluster-analysis-in-python/hierarchical-clustering-877595ec-58cd-4cf5-837c-704a42eb8776?ex=2)

```
# Import the fcluster and linkage functions
from scipy.cluster.hierarchy import fcluster, linkage

# Use the linkage() function
distance_matrix = linkage(comic_con[['x_scaled', 'y_scaled']], method = 'ward', metric = 'euclidean')

# Assign cluster labels
comic_con['cluster_labels'] = fcluster(distance_matrix, 2, criterion='maxclust')

# Plot clusters
sns.scatterplot(x='x_scaled', y='y_scaled', 
                hue='cluster_labels', data = comic_con)
plt.show()
```

### [Hierarchical clustering: single method]()

```
# Import the fcluster and linkage functions
from scipy.cluster.hierarchy import fcluster, linkage

# Use the linkage() function
distance_matrix = linkage(comic_con[['x_scaled', 'y_scaled']], method = 'single', metric = 'euclidean')

# Assign cluster labels
comic_con['cluster_labels'] = fcluster(distance_matrix, 2, criterion='maxclust')

# Plot clusters
sns.scatterplot(x='x_scaled', y='y_scaled', 
                hue='cluster_labels', data = comic_con)
plt.show()
```

### [Hierarchical clustering: complete method](https://campus.datacamp.com/courses/cluster-analysis-in-python/hierarchical-clustering-877595ec-58cd-4cf5-837c-704a42eb8776?ex=4)

```
# Import the fcluster and linkage functions
from scipy.cluster.hierarchy import linkage, fcluster

# Use the linkage() function
distance_matrix = linkage(comic_con[['x_scaled', 'y_scaled']], method = 'complete', metric = 'euclidean')

# Assign cluster labels
comic_con['cluster_labels'] = fcluster(distance_matrix, 2, criterion='maxclust')

# Plot clusters
sns.scatterplot(x='x_scaled', y='y_scaled', 
                hue='cluster_labels', data = comic_con)
plt.show()
```

### [Visualize clusters with matplotlib](https://campus.datacamp.com/courses/cluster-analysis-in-python/hierarchical-clustering-877595ec-58cd-4cf5-837c-704a42eb8776?ex=6)

```
# Import the pyplot class
from matplotlib import pyplot as plt

# Define a colors dictionary for clusters
colors = {1:'red', 2:'blue'}

# Plot a scatter plot
comic_con.plot.scatter(x = 'x_scaled', 
                	   y = 'y_scaled',
                	   c = comic_con['cluster_labels'].map(colors))
plt.show()
```

### [Visualize clusters with seaborn](https://campus.datacamp.com/courses/cluster-analysis-in-python/hierarchical-clustering-877595ec-58cd-4cf5-837c-704a42eb8776?ex=7)

```
# Import the seaborn module
import seaborn as sns

# Plot a scatter plot using seaborn
sns.scatterplot(x = 'x_scaled', 
                y = 'y_scaled', 
                hue = 'cluster_labels', 
                data = comic_con)
plt.show()
```

### [Create a dendrogram](https://campus.datacamp.com/courses/cluster-analysis-in-python/hierarchical-clustering-877595ec-58cd-4cf5-837c-704a42eb8776?ex=9)

```
# Import the dendrogram function
from scipy.cluster.hierarchy import dendrogram

# Create a dendrogram
dn = dendrogram(distance_matrix)

# Display the dendogram
plt.show()
```

### [How many clusters in comic con data?](https://campus.datacamp.com/courses/cluster-analysis-in-python/hierarchical-clustering-877595ec-58cd-4cf5-837c-704a42eb8776?ex=10)

```
Q: Given the dendrogram from the last exercise, how many clusters can you see in the data?
A: 2 clusters
```

### [Timing run of hierarchical clustering](https://campus.datacamp.com/courses/cluster-analysis-in-python/hierarchical-clustering-877595ec-58cd-4cf5-837c-704a42eb8776?ex=12)

```
Q: How long does it take to the run the linkage function on the comic con data?
A: 1-5 milliseconds
```

### [FIFA 18: exploring defenders](https://campus.datacamp.com/courses/cluster-analysis-in-python/hierarchical-clustering-877595ec-58cd-4cf5-837c-704a42eb8776?ex=13)

```
# Fit the data into a hierarchical clustering algorithm
distance_matrix = linkage(fifa[['scaled_sliding_tackle', 'scaled_aggression']], 'ward')

#####################################################

# Fit the data into a hierarchical clustering algorithm
distance_matrix = linkage(fifa[['scaled_sliding_tackle', 'scaled_aggression']], 'ward')

# Assign cluster labels to each row of data
fifa['cluster_labels'] = fcluster(distance_matrix, 3, criterion='maxclust')

#####################################################

# Fit the data into a hierarchical clustering algorithm
distance_matrix = linkage(fifa[['scaled_sliding_tackle', 'scaled_aggression']], 'ward')

# Assign cluster labels to each row of data
fifa['cluster_labels'] = fcluster(distance_matrix, 3, criterion='maxclust')

# Display cluster centers of each cluster
print(fifa[['scaled_sliding_tackle', 'scaled_aggression', 'cluster_labels']].groupby('cluster_labels').mean())

#####################################################

# Fit the data into a hierarchical clustering algorithm
distance_matrix = linkage(fifa[['scaled_sliding_tackle', 'scaled_aggression']], 'ward')

# Assign cluster labels to each row of data
fifa['cluster_labels'] = fcluster(distance_matrix, 3, criterion='maxclust')

# Display cluster centers of each cluster
print(fifa[['scaled_sliding_tackle', 'scaled_aggression', 'cluster_labels']].groupby('cluster_labels').mean())

# Create a scatter plot through seaborn
sns.scatterplot(x='scaled_sliding_tackle', y='scaled_aggression', hue='cluster_labels', data=fifa)
plt.show()
```