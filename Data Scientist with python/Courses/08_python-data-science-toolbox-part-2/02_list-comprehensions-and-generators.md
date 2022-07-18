## [Write a basic list comprehension](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators)

In this chapter, you'll build on your knowledge of iterators and be introduced to list comprehensions, which allow you to create complicated lists—and lists of lists—in one line of code! List comprehensions can dramatically simplify your code and make it more efficient, and will become a vital part of your Python data science toolbox. You'll then learn about generators, which are extremely helpful when working with large sequences of data that you may not want to store in memory, but instead generate on the fly.

<br>


### [Write a basic list comprehension](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=2)

```Python
Q: How would a list comprehension that produces a list of the first character of each string in doctor look like? Note that the list comprehension uses doc as the iterator variable. What will the output be?
A: The list comprehension is [doc[0] for doc in doctor] and produces the list ['h', 'c', 'c', 't', 'w']
```

### [List comprehension over iterables](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=3)

```Python
Q: Given the following objects below, which of these can we build list comprehensions over?
A: You can build list comprehensions over all the objects except the integer object valjean.
```

### [Writing list comprehensions](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=4)

```Python
# Create list comprehension: squares
squares = [i*i for i in range(10)]
```

### [Nested list comprehensions](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=5)

```Python
# Create a 5 x 5 matrix using a list of lists: matrix
matrix = [[col for col in range(5)] for row in range(5)]

# Print the matrix
for row in matrix:
    print(row)
```

### [Using conditionals in comprehensions (1)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=7)

```Python
# Create a list of strings: fellowship
fellowship = ['frodo', 'samwise', 'merry', 'aragorn', 'legolas', 'boromir', 'gimli']

# Create list comprehension: new_fellowship
new_fellowship = [member for member in fellowship if len(member) >= 7]

# Print the new list
print(new_fellowship)
```

### [Using conditionals in comprehensions (2)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=8)

```Python
# Create a list of strings: fellowship
fellowship = ['frodo', 'samwise', 'merry', 'aragorn', 'legolas', 'boromir', 'gimli']

# Create list comprehension: new_fellowship
new_fellowship = [member if len(member)>=7 else '' for member in fellowship]

# Print the new list
print(new_fellowship)
```

### [Dict comprehensions](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=9)

```Python
# Create a list of strings: fellowship
fellowship = ['frodo', 'samwise', 'merry', 'aragorn', 'legolas', 'boromir', 'gimli']

# Create dict comprehension: new_fellowship
new_fellowship = { member:len(member) for member in fellowship }

# Print the new dictionary
print(new_fellowship)
```

### [List comprehensions vs. generators](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=11)

```Python
Q: Based on your observations and what you can recall from the video, select from the options below the best description for the difference between list comprehensions and generators.
A: A list comprehension produces a list as output, a generator produces a generator object.
```

### [Write your own generator expressions](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=12)

```Python
# Create generator object: result
result = (num for num in range(31))

# Print the first 5 values
print(next(result))
print(next(result))
print(next(result))
print(next(result))
print(next(result))

# Print the rest of the values
for value in result:
    print(value)
```

### [Changing the output in generator expressions](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=13)

```Python
# Create a list of strings: lannister
lannister = ['cersei', 'jaime', 'tywin', 'tyrion', 'joffrey']

# Create a generator object: lengths
lengths = (len(person) for person in lannister)

# Iterate over and print the values in lengths
for value in lengths:
    print(value)
```

### [Build a generator](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=14)

```Python
# Create a list of strings
lannister = ['cersei', 'jaime', 'tywin', 'tyrion', 'joffrey']

# Define generator function get_lengths
def get_lengths(input_list):
    """Generator function that yields the
    length of the strings in input_list."""

    # Yield the length of a string
    for person in input_list:
        yield len(person);

# Print the values generated by get_lengths()
for value in get_lengths(lannister):
    print(value)
```

### [List comprehensions for time-stamped data](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=16)

```Python
# Extract the created_at column from df: tweet_time
tweet_time = df.created_at

# Extract the clock time: tweet_clock_time
tweet_clock_time = [entry[11:19] for entry in tweet_time]

# Print the extracted times
print(tweet_clock_time)
```

### [Conditional list comprehensions for time-stamped data](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/list-comprehensions-and-generators?ex=17)

```Python
# Extract the created_at column from df: tweet_time
tweet_time = df['created_at']

# Extract the clock time: tweet_clock_time
tweet_clock_time = [entry[11:19] for entry in tweet_time if entry[17:19] == '19']

# Print the extracted times
print(tweet_clock_time)
```