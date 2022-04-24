## [Writing your own functions](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/customizing-seaborn-plots-4?ex=13)

In this chapter, you'll learn how to write simple functions, as well as functions that accept multiple arguments and return multiple values. You'll also have the opportunity to apply these new skills to questions commonly encountered by data scientists.

<br>


### [Strings in Python](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/customizing-seaborn-plots-4?ex=13)

```
Q: What are the values in object1, object2, and object3, respectively?
A: object1 contains "dataanalysisvisualization", object2 contains 3, object3 contains "111".
```

### [Recapping built-in functions](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/writing-your-own-functions?ex=3)

```
Q: What are the types of x, y1, and y2?
A: x is a float, y1 is a str, and y2 is a NoneType.
```

### [Write a simple function](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/writing-your-own-functions?ex=4)

```
# Define the function shout
def shout():
    """Print a string with three exclamation marks"""
    # Concatenate the strings: shout_word
    shout_word = "congratulations" + "!!!"
    
    # Print shout_word
    print(shout_word)

# Call shout
shout()
```

### [Single-parameter functions](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/writing-your-own-functions?ex=5)

```
# Define shout with the parameter, word
def shout(word):
    """Print a string with three exclamation marks"""
    # Concatenate the strings: shout_word
    shout_word = word + '!!!'

    # Print shout_word
    print(shout_word)

# Call shout with the string 'congratulations'
print(shout("congratulations"))
```

### [Functions that return single values](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/writing-your-own-functions?ex=6)

```
# Define shout with the parameter, word
def shout(word):
    """Return a string with three exclamation marks"""
    # Concatenate the strings: shout_word
    shout_word = word + "!!!"

    # Replace print with return
    return shout_word

# Pass 'congratulations' to shout: yell
yell = shout("congratulations")

# Print yell
print(yell)
```

### [Functions with multiple parameters](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/writing-your-own-functions?ex=8)

```
# Define shout with parameters word1 and word2
def shout(word1, word2):
    """Concatenate strings with three exclamation marks"""
    # Concatenate word1 with '!!!': shout1
    shout1 = word1 + "!!!"
    
    # Concatenate word2 with '!!!': shout2
    shout2 = word2 + "!!!"
    
    # Concatenate shout1 with shout2: new_shout
    new_shout = shout1 + shout2

    # Return new_shout
    return new_shout

# Pass 'congratulations' and 'you' to shout(): yell
yell = shout("congratulations", "you")

# Print yell
print(yell)
```

### [A brief introduction to tuples](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/writing-your-own-functions?ex=9)

```
# Unpack nums into num1, num2, and num3
num1, num2, num3 = nums

# Construct even_nums
nums = list(nums)
nums[0] = 2
even_nums = (nums)
```

### [Functions that return multiple values](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/writing-your-own-functions?ex=10)

```
# Define shout_all with parameters word1 and word2
def shout_all(word1, word2):
    
    # Concatenate word1 with '!!!': shout1
    shout1 = word1 + "!!!"
    
    # Concatenate word2 with '!!!': shout2
    shout2 = word2 + "!!!"
    
    # Construct a tuple with shout1 and shout2: shout_words
    shout_words = (shout1, shout2)

    # Return shout_words
    return shout_words

# Pass 'congratulations' and 'you' to shout_all(): yell1, yell2
yell1, yell2 = shout_all("congratulations", "you")

# Print yell1 and yell2
print(yell1)
print(yell2)
```

### [Bringing it all together (1)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/writing-your-own-functions?ex=12)

```
# Import pandas
import pandas as pd

# Import Twitter data as DataFrame: df
df = pd.read_csv("tweets.csv")

# Initialize an empty dictionary: langs_count
langs_count = {}

# Extract column from DataFrame: col
col = df['lang']

# Iterate over lang column in DataFrame
for entry in col:

    # If the language is in langs_count, add 1 
    if entry in langs_count.keys():
        langs_count[entry] += 1
    # Else add the language to langs_count, set the value to 1
    else:
        langs_count[entry] = 1

# Print the populated dictionary
print(langs_count)
```

### [Bringing it all together (2)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/writing-your-own-functions?ex=13)

```
# Define count_entries()
def count_entries(df, col_name):
    """Return a dictionary with counts of 
    occurrences as value for each key."""

    # Initialize an empty dictionary: langs_count
    langs_count = {}
    
    # Extract column from DataFrame: col
    col = df[col_name]
    
    # Iterate over lang column in DataFrame
    for entry in col:

        # If the language is in langs_count, add 1
        if entry in langs_count.keys():
            langs_count[entry] += 1

        # Else add the language to langs_count, set the value to 1
        else:
            langs_count[entry] = 1

    # Return the langs_count dictionary
    return langs_count

# Call count_entries(): result
result = count_entries(tweets_df, "lang")

# Print the result
print(result)
```