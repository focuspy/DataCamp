## [Lambda functions and error-handling](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling)

Learn about lambda functions, which allow you to write functions quickly and on the fly. You'll also practice handling errors in your functions, which is an essential skill. Then, apply your new skills to answer data science questions.

<br>

### [Pop quiz on lambda functions](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling?ex=2)

```Python
Q: How would you write a lambda function add_bangs that adds three exclamation points '!!!' to the end of a string a?
How would you call add_bangs with the argument 'hello'?
A: The lambda function definition is: add_bangs = (lambda a: a + '!!!'), and the function call is: add_bangs('hello').
```

### [Writing a lambda function you already know](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling?ex=3)

```Python
# Define echo_word as a lambda function: echo_word
echo_word = (lambda word1,echo:word1*echo)

# Call echo_word: result
result = echo_word("hey",5)

# Print result
print(result)
```

### [Map() and lambda functions](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling?ex=4)

```Python
# Create a list of strings: spells
spells = ["protego", "accio", "expecto patronum", "legilimens"]

# Use map() to apply a lambda function over spells: shout_spells
shout_spells = map(lambda spell: spell+"!!!", spells)

# Convert shout_spells to a list: shout_spells_list
shout_spells_list = list(shout_spells)

# Print the result
print(shout_spells_list)
```

### [Filter() and lambda functions](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling?ex=5)

```Python
# Create a list of strings: fellowship
fellowship = ['frodo', 'samwise', 'merry', 'pippin', 'aragorn', 'boromir', 'legolas', 'gimli', 'gandalf']

# Use filter() to apply a lambda function over fellowship: result
result = filter(lambda a: len(a)>6, fellowship)

# Convert result to a list: result_list
result_list = list(result)

# Print result_list
print(result_list)
```

### [Reduce() and lambda functions](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling?ex=6)

```Python
# Import reduce from functools
from functools import reduce

# Create a list of strings: stark
stark = ['robb', 'sansa', 'arya', 'brandon', 'rickon']

# Use reduce() to apply a lambda function over stark: result
result = reduce(lambda item1,item2: item1+item2, stark)

# Print the result
print(result)
```

### [Pop quiz about errors](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling?ex=8)

```Python
Q: Which of the function calls raises an error and what type of error is raised?
A: The call len(525600) raises a TypeError.
```

### [Error handling with try-except](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling?ex=9)

```Python
# Define shout_echo
def shout_echo(word1, echo=1):
    """Concatenate echo copies of word1 and three
    exclamation marks at the end of the string."""

    # Initialize empty strings: echo_word, shout_words
    echo_word = shout_words = ""

    # Add exception handling with try-except
    try:
        # Concatenate echo copies of word1 using *: echo_word
        echo_word = word1*echo

        # Concatenate '!!!' to echo_word: shout_words
        shout_words = echo_word + "!!!"
    except:
        # Print error message
        print("word1 must be a string and echo must be an integer.")

    # Return shout_words
    return shout_words

# Call shout_echo
shout_echo("particle", echo="accelerator")
```

### [Error handling by raising an error](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling?ex=10)

```Python
# Define shout_echo
def shout_echo(word1, echo=1):
    """Concatenate echo copies of word1 and three
    exclamation marks at the end of the string."""

    # Raise an error with raise
    if echo < 0:
        raise ValueError("echo must be greater than or equal to 0")

    # Concatenate echo copies of word1 using *: echo_word
    echo_word = word1 * echo

    # Concatenate '!!!' to echo_word: shout_word
    shout_word = echo_word + '!!!'

    # Return shout_word
    return shout_word

# Call shout_echo
shout_echo("particle", echo=5)
```

### [Bringing it all together (1)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling?ex=12)

```Python
# Select retweets from the Twitter DataFrame: result
result = filter(lambda x:x[0:2]=="RT", tweets_df["text"])

# Create list from filter object result: res_list
res_list = list(result)

# Print all retweets in res_list
for tweet in res_list:
    print(tweet)
```

### [Bringing it all together (2)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling?ex=13)

```Python
# Define count_entries()
def count_entries(df, col_name='lang'):
    """Return a dictionary with counts of
    occurrences as value for each key."""

    # Initialize an empty dictionary: cols_count
    cols_count = {}

    # Add try block
    try:
        # Extract column from DataFrame: col
        col = df[col_name]
        
        # Iterate over the column in dataframe
        for entry in col:
    
            # If entry is in cols_count, add 1
            if entry in cols_count.keys():
                cols_count[entry] += 1
            # Else add the entry to cols_count, set the value to 1
            else:
                cols_count[entry] = 1
    
        # Return the cols_count dictionary
        return cols_count

    # Add except block
    except:
        print("The DataFrame does not have a " + col_name + " column")

# Call count_entries(): result1
result1 = count_entries(tweets_df, 'lang')

# Print result1
print(result1)
```

### [Bringing it all together (3)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling?ex=14)

```Python
# Define count_entries()
def count_entries(df, col_name='lang'):
    """Return a dictionary with counts of
    occurrences as value for each key."""
    
    # Raise a ValueError if col_name is NOT in DataFrame
    if col_name not in df.columns:
        raise ValueError('The DataFrame does not have a ' + col_name + ' column.')

    # Initialize an empty dictionary: cols_count
    cols_count = {}
    
    # Extract column from DataFrame: col
    col = df[col_name]
    
    # Iterate over the column in DataFrame
    for entry in col:

        # If entry is in cols_count, add 1
        if entry in cols_count.keys():
            cols_count[entry] += 1
            # Else add the entry to cols_count, set the value to 1
        else:
            cols_count[entry] = 1
        
        # Return the cols_count dictionary
    return cols_count

# Call count_entries(): result1
result1 = count_entries(tweets_df, 'lang')

# Print result1
print(result1)
```

### [Bringing it all together: testing your error handling skills](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/lambda-functions-and-error-handling?ex=15)

```
Q: What is the last line of the output?
A: 'ValueError: The DataFrame does not have a lang1 column.'
```