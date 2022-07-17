## [Diving deep into the Twitter API](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/diving-deep-into-the-twitter-api)

In this chapter, you will consolidate your knowledge of interacting with APIs in a deep dive into the Twitter streaming API. You'll learn how to stream real-time Twitter data, and how to analyze and visualize it.

<br>

### [Streaming tweets](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/diving-deep-into-the-twitter-api?ex=2)

```
# Initialize Stream listener
l = MyStreamListener()

# Create your Stream object with authentication
stream = tweepy.Stream(auth, l)

# Filter Twitter Streams to capture data by the keywords:
stream.filter(['clinton','trump','sanders','cruz'])
```

### [Load and explore your Twitter data](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/diving-deep-into-the-twitter-api?ex=3)

```
# Import package
import json

# String of path to file: tweets_data_path
tweets_data_path = 'tweets.txt'

# Initialize empty list to store tweets: tweets_data
tweets_data = []

# Open connection to file
tweets_file = open(tweets_data_path, "r")

# Read in tweets and store in list: tweets_data
for line in tweets_file:
    tweet = json.loads(line)
    tweets_data.append(tweet)

# Close connection to file
tweets_file.close()

# Print the keys of the first tweet dict
print(tweets_data[0].keys())

```

### [Twitter data to DataFrame](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/diving-deep-into-the-twitter-api?ex=4)

```
# Import package
import pandas as pd

# Build DataFrame of tweet texts and languages
df = pd.DataFrame(tweets_data, columns=['text', 'lang'])

# Print head of DataFrame
print(df.head())
```

### [A little bit of Twitter text analysis](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/diving-deep-into-the-twitter-api?ex=5)

```
# Initialize list to store tweet counts
[clinton, trump, sanders, cruz] = [0, 0, 0, 0]

# Iterate through df, counting the number of tweets in which
# each candidate is mentioned
for index, row in df.iterrows():
    clinton += word_in_text('clinton', row['text'])
    trump += word_in_text('trump', row['text'])
    sanders += word_in_text('sanders', row['text'])
    cruz += word_in_text('cruz', row['text'])

```

### [Plotting your Twitter data](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/diving-deep-into-the-twitter-api?ex=6)

```
# Import packages
import matplotlib.pyplot as plt
import seaborn as sns

# Set seaborn style
sns.set(color_codes=True)

# Create a list of labels:cd
cd = ['clinton', 'trump', 'sanders', 'cruz']

# Plot the bar chart
ax = sns.barplot(cd, [clinton, trump, sanders, cruz])
ax.set(ylabel="count")
plt.show()
```