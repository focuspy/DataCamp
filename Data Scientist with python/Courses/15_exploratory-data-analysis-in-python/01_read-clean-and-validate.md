## [Read, clean, and validate](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/read-clean-and-validate)

The first step of almost any data project is to read the data, check for errors and special cases, and prepare data for analysis. This is exactly what you'll do in this chapter, while working with a dataset obtained from the National Survey of Family Growth.

<br>

### [Read the codebook](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/read-clean-and-validate?ex=2)

```Python
Q: How many respondents refused to answer this question?
A: 1.
```

### [Exploring the NSFG data](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/read-clean-and-validate?ex=3)

```Python
# Display the number of rows and columns
nsfg.shape

#####################################################

# Display the number of rows and columns
nsfg.shape

# Display the names of the columns
nsfg.columns

#####################################################

# Display the number of rows and columns
nsfg.shape

# Display the names of the columns
nsfg.columns

# Select column birthwgt_oz1: ounces
ounces = nsfg['birthwgt_oz1']

#####################################################

# Display the number of rows and columns
nsfg.shape

# Display the names of the columns
nsfg.columns

# Select column birthwgt_oz1: ounces
ounces = nsfg['birthwgt_oz1']

# Print the first 5 elements of ounces
print(ounces.head())
```
### [Validate a variable](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/read-clean-and-validate?ex=5)

```Python
Q: How many pregnancies in this dataset ended with a live birth?
A: 6489
```

### [Clean a variable](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/read-clean-and-validate?ex=6)

```Python
# Replace the value 8 with NaN
nsfg['nbrnaliv'].replace(8, np.nan, inplace=True)

# Print the values and their frequencies
print(nsfg['nbrnaliv'].value_counts())
```

### [Compute a variable](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/read-clean-and-validate?ex=7)

```Python
# Select the columns and divide by 100
agecon = nsfg['agecon'] / 100
agepreg = nsfg['agepreg'] / 100

#####################################################

# Select the columns and divide by 100
agecon = nsfg['agecon'] / 100
agepreg = nsfg['agepreg'] / 100

# Compute the difference
preg_length = agepreg - agecon

#####################################################

# Select the columns and divide by 100
agecon = nsfg['agecon'] / 100
agepreg = nsfg['agepreg'] / 100

# Compute the difference
preg_length = agepreg - agecon

# Compute summary statistics
print(preg_length.describe())
```

### [Make a histogram](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/read-clean-and-validate?ex=9)

```Python
# Plot the histogram
plt.hist(agecon, bins=20)

# Label the axes
plt.xlabel('Age at conception')
plt.ylabel('Number of pregnancies')

# Show the figure
plt.show()

#####################################################

# Plot the histogram
plt.hist(agecon, bins=20, histtype='step')

# Label the axes
plt.xlabel('Age at conception')
plt.ylabel('Number of pregnancies')

# Show the figure
plt.show()
```

### [Compute birth weight](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/read-clean-and-validate?ex=10)

```Python
# Create a Boolean Series for full-term babies
full_term = nsfg['prglngth'] >= 37

# Select the weights of full-term babies
full_term_weight = birth_weight[full_term]

# Compute the mean weight of full-term babies
print(full_term_weight.mean())
```

### [Filter](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/read-clean-and-validate?ex=11)

```Python
# Filter full-term babies
full_term = nsfg['prglngth'] >= 37

# Filter single births
single = nsfg['nbrnaliv'] == 1

# Compute birth weight for single full-term babies
single_full_term_weight = birth_weight[full_term & single]
print('Single full-term mean:', single_full_term_weight.mean())

# Compute birth weight for multiple full-term babies
mult_full_term_weight = birth_weight[full_term & ~single]
print('Multiple full-term mean:', mult_full_term_weight.mean())
```