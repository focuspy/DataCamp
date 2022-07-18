## [Record linkage](https://campus.datacamp.com/courses/cleaning-data-in-python/record-linkage-4)

Record linkage is a powerful technique used to merge multiple datasets together, used when values have typos or different spellings. In this chapter, you'll learn how to link records by calculating the similarity between strings—you’ll then use your new skills to join two restaurant review datasets into one clean master dataset.

<br>

### [Minimum edit distance](https://campus.datacamp.com/courses/cleaning-data-in-python/record-linkage-4?ex=2)

```Python
Q: What is the minimum edit distance from 'sign' to 'sing', and which operation(s) gets you there?
A: 1 by transposing 'g' with 'n'.
```

### [The cutoff point](https://campus.datacamp.com/courses/cleaning-data-in-python/record-linkage-4?ex=3)

```Python
# Import process from fuzzywuzzy
from fuzzywuzzy import process

# Store the unique values of cuisine_type in unique_types
unique_types = restaurants['cuisine_type'].unique()

# Calculate similarity of 'asian' to all values of unique_types
print(process.extract('asian', unique_types, limit = len(unique_types)))

# Calculate similarity of 'american' to all values of unique_types
print(process.extract('american', unique_types, limit = len(unique_types)))

# Calculate similarity of 'italian' to all values of unique_types
print(process.extract('italian', unique_types, limit = len(unique_types)))
```

### [Remapping categories II](https://campus.datacamp.com/courses/cleaning-data-in-python/record-linkage-4?ex=4)

```Python
# Print unique values to confirm mapping
print(restaurants['cuisine_type'].unique())

#####################################################

# Create a list of matches, comparing 'italian' with the cuisine_type column
matches = process.extract('italian', restaurants['cuisine_type'], limit=len(restaurants.cuisine_type))

# Inspect the first 5 matches
print(matches[0:5])

#####################################################

c# Create a list of matches, comparing 'italian' with the cuisine_type column
matches = process.extract('italian', restaurants['cuisine_type'], limit=len(restaurants.cuisine_type))

# Iterate through the list of matches to italian
for match in matches:
  # Check whether the similarity score is greater than or equal to 80
  if match[1] >= 80:
    # Select all rows where the cuisine_type is spelled this way, and set them to the correct cuisine
    restaurants.loc[restaurants['cuisine_type'] == match[0]] = 'italian'

#####################################################

# Iterate through categories
for cuisine in categories:  
  # Create a list of matches, comparing cuisine with the cuisine_type column
  matches = process.extract(cuisine, restaurants['cuisine_type'], limit=len(restaurants.cuisine_type))

  # Iterate through the list of matches
  for match in matches:
     # Check whether the similarity score is greater than or equal to 80
    if match[1] >= 80:
      # If it is, select all rows where the cuisine_type is spelled this way, and set them to the correct cuisine
      restaurants.loc[restaurants['cuisine_type'] == match[0]] = cuisine
      
# Inspect the final result
print(restaurants['cuisine_type'].unique())

```

### [Pairs of restaurants](https://campus.datacamp.com/courses/cleaning-data-in-python/record-linkage-4?ex=7)

```Python
# Create an indexer and object and find possible pairs
indexer = recordlinkage.Index()

# Block pairing on cuisine_type
indexer.block('cuisine_type')

# Generate pairs
pairs = indexer.index(restaurants, restaurants_new)

#####################################################

Q:What are the steps remaining to link both restaurants DataFrames, and in what order?
A:Compare between columns, score the comparison, then link the DataFrames.
```

### [Similar restaurants](https://campus.datacamp.com/courses/cleaning-data-in-python/record-linkage-4?ex=8)

```Python
# Create a comparison object
comp_cl = recordlinkage.Compare()

#####################################################

# Create a comparison object
comp_cl = recordlinkage.Compare()

# Find exact matches on city, cuisine_types 
comp_cl.exact('city', 'city', label='city')
comp_cl.exact('cuisine_type', 'cuisine_type', label = 'cuisine_type')

# Find similar matches of rest_name
comp_cl.string('rest_name', 'rest_name', label='name', threshold = 0.8)

#####################################################

# Create a comparison object
comp_cl = recordlinkage.Compare()

# Find exact matches on city, cuisine_types - 
comp_cl.exact('city', 'city', label='city')
comp_cl.exact('cuisine_type', 'cuisine_type', label='cuisine_type')

# Find similar matches of rest_name
comp_cl.string('rest_name', 'rest_name', label='name', threshold = 0.8) 

# Get potential matches and print
potential_matches = comp_cl.compute(pairs, restaurants, restaurants_new)
print(potential_matches)

#####################################################

Q: Where n is the minimum number of columns you want matching to ensure a proper duplicate find, what do you think should the value of n be?
A: 3 because I need to have matches in all my columns.
```

### [Getting the right index](https://campus.datacamp.com/courses/cleaning-data-in-python/record-linkage-4?ex=10)

```Python
Q:How do you extract all values of the uid_1 index column?
A: Both 1 and 3 are correct.
```

### [Linking them together!](https://campus.datacamp.com/courses/cleaning-data-in-python/record-linkage-4?ex=11)

```Python
# Isolate potential matches with row sum >=3
matches = potential_matches[potential_matches.sum(axis=1) >= 3]

# Get values of second column index of matches
matching_indices = matches.index.get_level_values(1)

# Subset restaurants_new based on non-duplicate values
non_dup = restaurants_new[~restaurants_new.index.isin(matching_indices)]

# Append non_dup to restaurants
full_restaurants = restaurants.append(non_dup)
print(full_restaurants)
```