## [Using iterators in PythonLand](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/using-iterators-in-pythonland)

You'll learn all about iterators and iterables, which you have already worked with when writing for loops. You'll learn some handy functions that will allow you to effectively work with iterators. And you’ll finish the chapter with a use case that is pertinent to the world of data science and dealing with large amounts of data—in this case, data from Twitter that you will load in chunks using iterators.

<br>

### [Iterators vs. Iterables](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/using-iterators-in-pythonland?ex=2)

```Python
Q: Try printing out their values with print() and next() to figure out which is an iterable and which is an iterator.
A: flash1 is an iterable and flash2 is an iterator.
```

### [Iterating over iterables (1)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/using-iterators-in-pythonland?ex=3)

```Python
# Create a list of strings: flash
flash = ['jay garrick', 'barry allen', 'wally west', 'bart allen']

# Print each list item in flash using a for loop
for a in flash:
    print(a)

# Create an iterator for flash: superhero
superhero=iter(flash)

# Print each item from the iterator
print(next(superhero))
print(next(superhero))
print(next(superhero))
print(next(superhero))
```

### [Iterating over iterables (2)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/using-iterators-in-pythonland?ex=4)

```Python
# Create an iterator for range(3): small_value
small_value = iter(range(3))

# Print the values in small_value
print(next(small_value))
print(next(small_value))
print(next(small_value))

# Loop over range(3) and print the values
for num in range(3):
    print(num)

# Create an iterator for range(10 ** 100): googol
googol = iter(range(10**100))

# Print the first 5 values from googol
print(next(googol))
print(next(googol))
print(next(googol))
print(next(googol))
print(next(googol))
```

### [Iterators as function arguments](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/using-iterators-in-pythonland?ex=5)

```Python
# Create a range object: values
values = range(10,21)

# Print the range object
print(values)

# Create a list of integers: values_list
values_list = list(values)

# Print values_list
print(values_list)

# Get the sum of values: values_sum
values_sum = sum(values)

# Print values_sum
print(values_sum)
```

### [Using enumerate](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/using-iterators-in-pythonland?ex=7)

```Python
# Create a list of strings: mutants
mutants = ['charles xavier', 
            'bobby drake', 
            'kurt wagner', 
            'max eisenhardt', 
            'kitty pryde']

# Create a list of tuples: mutant_list
mutant_list = list(enumerate(mutants))

# Print the list of tuples
print(mutant_list)

# Unpack and print the tuple pairs
for index1,value1 in enumerate(mutants):
    print(index1, value1)

# Change the start index
for index2,value2 in enumerate(mutants,start=1):
    print(index2, value2)
```

### [Using zip](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/using-iterators-in-pythonland?ex=8)

```Python
# Create a list of tuples: mutant_data
mutant_data = list(zip(mutants,aliases,powers))

# Print the list of tuples
print(mutant_data)

# Create a zip object using the three lists: mutant_zip
mutant_zip = zip(mutants,aliases,powers)

# Print the zip object
print(mutant_zip)

# Unpack the zip object and print the tuple values
for value1,value2,value3 in mutant_zip:
    print(value1, value2, value3)
```

### [Using * and zip to 'unzip'](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/using-iterators-in-pythonland?ex=9)

```Python
# Create a zip object from mutants and powers: z1
z1 = zip(mutants, powers)

# Print the tuples in z1 by unpacking with *
print(*z1)

# Re-create a zip object from mutants and powers: z1
z1 = zip(mutants, powers)

# 'Unzip' the tuples in z1 by unpacking with * and zip(): result1, result2
result1, result2 = zip(*z1)

# Check if unpacked tuples are equivalent to original tuples
print(result1 == mutants)
print(result2 == powers)
```

### [Processing large amounts of Twitter data](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/using-iterators-in-pythonland?ex=11)

```Python
# Initialize an empty dictionary: counts_dict
counts_dict={}

# Iterate over the file chunk by chunk
for chunk in pd.read_csv('tweets.csv',chunksize=10):

    # Iterate over the column in DataFrame
    for entry in chunk['lang']:
        if entry in counts_dict.keys():
            counts_dict[entry] += 1
        else:
            counts_dict[entry] = 1

# Print the populated dictionary
print(counts_dict)
```

### [Extracting information for large amounts of Twitter data](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/using-iterators-in-pythonland?ex=12)

```Python
# Define count_entries()
def count_entries(csv_file, c_size, colname):
    """Return a dictionary with counts of
    occurrences as value for each key."""
    
    # Initialize an empty dictionary: counts_dict
    counts_dict = {}

    # Iterate over the file chunk by chunk
    for chunk in pd.read_csv(csv_file, chunksize=c_size):

        # Iterate over the column in DataFrame
        for entry in chunk[colname]:
            if entry in counts_dict.keys():
                counts_dict[entry] += 1
            else:
                counts_dict[entry] = 1

    # Return counts_dict
    return counts_dict

# Call count_entries(): result_counts
result_counts = count_entries('tweets.csv', 10, 'lang')

# Print result_counts
print(result_counts)
```