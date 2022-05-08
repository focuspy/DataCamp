## [Discovering interpretable features](https://campus.datacamp.com/courses/unsupervised-learning-in-python/discovering-interpretable-features)

In this chapter, you'll learn about a dimension reduction technique called "Non-negative matrix factorization" ("NMF") that expresses samples as combinations of interpretable parts. For example, it expresses documents as combinations of topics, and images in terms of commonly occurring visual patterns. You'll also learn to use NMF to build recommender systems that can find you similar articles to read, or musical artists that match your listening history!

<br>

### [Non-negative data](https://campus.datacamp.com/courses/unsupervised-learning-in-python/discovering-interpretable-features?ex=2)

```
Q: Which of the following 2-dimensional arrays are examples of non-negative data?
A: 1 and 3
```

### [NMF applied to Wikipedia articles](https://campus.datacamp.com/courses/unsupervised-learning-in-python/discovering-interpretable-features?ex=3)

```
# Import NMF
from sklearn.decomposition import NMF

# Create an NMF instance: model
model = NMF(n_components=6)

# Fit the model to articles
model.fit(articles)

# Transform the articles: nmf_features
nmf_features = model.transform(articles)

# Print the NMF features
print(nmf_features.round(2))
```

### [NMF features of the Wikipedia articles](https://campus.datacamp.com/courses/unsupervised-learning-in-python/discovering-interpretable-features?ex=4)

```
# Import pandas
import pandas as pd

# Create a pandas DataFrame: df
df = pd.DataFrame(nmf_features,index=titles)

# Print the row for 'Anne Hathaway'
print(df.loc['Anne Hathaway'])

# Print the row for 'Denzel Washington'
print(df.loc['Denzel Washington'])
```

### [NMF reconstructs samples](https://campus.datacamp.com/courses/unsupervised-learning-in-python/discovering-interpretable-features?ex=5)

```
Q: If the NMF feature values of a sample are [2, 1], then which of the following is most likely to represent the original sample?
A: [2.2, 1.1, 2.1].
```

### [NMF learns topics of documents](https://campus.datacamp.com/courses/unsupervised-learning-in-python/discovering-interpretable-features?ex=7)

```
# Import pandas
import pandas as pd

# Create a DataFrame: components_df
components_df = pd.DataFrame(model.components_, columns=words)

# Print the shape of the DataFrame
print(components_df.shape)

# Select row 3: component
component = components_df.iloc[3]

# Print result of nlargest
print(component.nlargest())
```

### [Explore the LED digits dataset](https://campus.datacamp.com/courses/unsupervised-learning-in-python/discovering-interpretable-features?ex=8)

```
# Import pyplot
from matplotlib import pyplot as plt

# Select the 0th row: digit
digit = samples[0,:]

# Print digit
print(digit)

# Reshape digit to a 13x8 array: bitmap
bitmap = digit.reshape(13, 8)

# Print bitmap
print(bitmap)

# Use plt.imshow to display bitmap
plt.imshow(bitmap, cmap='gray', interpolation='nearest')
plt.colorbar()
plt.show()
```

### [NMF learns the parts of images](https://campus.datacamp.com/courses/unsupervised-learning-in-python/discovering-interpretable-features?ex=9)

```
# Import NMF
from sklearn.decomposition import NMF

# Create an NMF model: model
model = NMF(n_components=7)

# Apply fit_transform to samples: features
features = model.fit_transform(samples)

# Call show_as_image on each component
for component in model.components_:
    show_as_image(component)

# Assign the 0th row of features: digit_features
digit_features = features[0,:]

# Print digit_features
print(digit_features)
```

### [PCA doesn't learn parts](https://campus.datacamp.com/courses/unsupervised-learning-in-python/discovering-interpretable-features?ex=10)

```
# Import PCA
from sklearn.decomposition import PCA

# Create a PCA instance: model
model = PCA(n_components=7)

# Apply fit_transform to samples: features
features = model.fit_transform(samples)

# Call show_as_image on each component
for component in model.components_:
    show_as_image(component)
```

### [Which articles are similar to 'Cristiano Ronaldo'?](https://campus.datacamp.com/courses/unsupervised-learning-in-python/discovering-interpretable-features?ex=12)

```
# Perform the necessary imports
import pandas as pd
from sklearn.preprocessing import normalize

# Normalize the NMF features: norm_features
norm_features = normalize(nmf_features)

# Create a DataFrame: df
df = pd.DataFrame(norm_features, index=titles)

# Select the row corresponding to 'Cristiano Ronaldo': article
article = df.loc['Cristiano Ronaldo']

# Compute the dot products: similarities
similarities = df.dot(article)

# Display those with the largest cosine similarity
print(similarities.nlargest())
```

### [Recommend musical artists part I](https://campus.datacamp.com/courses/unsupervised-learning-in-python/discovering-interpretable-features?ex=13)

```
# Perform the necessary imports
from sklearn.decomposition import NMF
from sklearn.preprocessing import Normalizer, MaxAbsScaler
from sklearn.pipeline import make_pipeline

# Create a MaxAbsScaler: scaler
scaler = MaxAbsScaler()

# Create an NMF model: nmf
nmf = NMF(n_components=20)

# Create a Normalizer: normalizer
normalizer = Normalizer()

# Create a pipeline: pipeline
pipeline = make_pipeline(scaler, nmf,normalizer)

# Apply fit_transform to artists: norm_features
norm_features = pipeline.fit_transform(artists)
```

### [Recommend musical artists part II](https://campus.datacamp.com/courses/unsupervised-learning-in-python/discovering-interpretable-features?ex=14)

```
# Import pandas
import pandas as pd

# Create a DataFrame: df
df = pd.DataFrame(norm_features,index=artist_names)

# Select row of 'Bruce Springsteen': artist
artist = df.loc['Bruce Springsteen',:]

# Compute cosine similarities: similarities
similarities = df.dot(artist)

# Display those with highest cosine similarity
print(similarities.nlargest())
```