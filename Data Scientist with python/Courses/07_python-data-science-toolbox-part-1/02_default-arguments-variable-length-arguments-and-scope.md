## [Default arguments, variable-length arguments and scope](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope)

In this chapter, you'll learn to write functions with default arguments so that the user doesn't always need to specify them, and variable-length arguments so they can pass an arbitrary number of arguments on to your functions. You'll also learn about the essential concept of scope.

<br>

### [Pop quiz on understanding scope](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope)

```Python
Q: What are the values printed out when you call func1() and func2()?
What is the value of num in the global scope after calling func1() and func2()?
A: func1() prints out 3, func2() prints out 10, and the value of num in the global scope is 6.
```

### [The keyword global](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope?ex=3)

```Python
# Create a string: team
team = "teen titans"

# Define change_team()
def change_team():
    """Change the value of the global variable team."""

    # Use team in global scope
    global team

    # Change the value of team in global: team
    team = "justice league"
    
# Print team
print(team)

# Call change_team()
change_team()

# Print team
print(team)
```

### [Python's built-in scope](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope?ex=4)

```Python
Q: Which of the following names is NOT in the module builtins?
A: 'array'
```

### [Nested Functions I](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope?ex=6)

```Python
# Define three_shouts
def three_shouts(word1, word2, word3):
    """Returns a tuple of strings
    concatenated with '!!!'."""

    # Define inner
    def inner(word):
        """Returns a string concatenated with '!!!'."""
        return word + '!!!'

    # Return a tuple of strings
    return (inner(word1), inner(word2), inner(word3))

# Call three_shouts() and print
print(three_shouts('a', 'b', 'c'))
```

### [Nested Functions II](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope?ex=7)

```Python
# Define echo
def echo(n):
    """Return the inner_echo function."""

    # Define inner_echo
    def inner_echo(word1):
        """Concatenate n copies of word1."""
        echo_word = word1 * n
        return echo_word

    # Return inner_echo
    return inner_echo
    

# Call echo: twice
twice = echo(2)

# Call echo: thrice
thrice = echo(3)

# Call twice() and thrice() then print
print(twice('hello'), thrice('hello'))
```

### [The keyword nonlocal and nested functions](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope?ex=8)

```Python
# Define echo_shout()
def echo_shout(word):
    """Change the value of a nonlocal variable"""
    
    # Concatenate word with itself: echo_word
    echo_word = word*2
    
    # Print echo_word
    print(echo_word)
    
    # Define inner function shout()
    def shout():
        """Alter a variable in the enclosing scope"""    
        # Use echo_word in nonlocal scope
        nonlocal echo_word
        
        # Change echo_word to echo_word concatenated with '!!!'
        echo_word += "!!!"
    
    # Call function shout()
    shout()
    
    # Print echo_word
    print(echo_word)

# Call function echo_shout() with argument 'hello'
echo_shout("hello")
```

### [Functions with one default argument](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope?ex=10)

```Python
# Define shout_echo
def shout_echo(word1, echo=1):
    """Concatenate echo copies of word1 and three
     exclamation marks at the end of the string."""

    # Concatenate echo copies of word1 using *: echo_word
    echo_word = word1*echo

    # Concatenate '!!!' to echo_word: shout_word
    shout_word = echo_word + '!!!'

    # Return shout_word
    return shout_word

# Call shout_echo() with "Hey": no_echo
no_echo = shout_echo("Hey")

# Call shout_echo() with "Hey" and echo=5: with_echo
with_echo = shout_echo("Hey", echo=5)

# Print no_echo and with_echo
print(no_echo)
print(with_echo)
```

### [Functions with multiple default arguments](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope?ex=11)

```Python
# Define shout_echo
def shout_echo(word1, echo=1, intense=False):
    """Concatenate echo copies of word1 and three
    exclamation marks at the end of the string."""

    # Concatenate echo copies of word1 using *: echo_word
    echo_word = word1 * echo

    # Make echo_word uppercase if intense is True
    if intense is True:
        # Make uppercase and concatenate '!!!': echo_word_new
        echo_word_new = echo_word.upper() + '!!!'
    else:
        # Concatenate '!!!' to echo_word: echo_word_new
        echo_word_new = echo_word + '!!!'

    # Return echo_word_new
    return echo_word_new

# Call shout_echo() with "Hey", echo=5 and intense=True: with_big_echo
with_big_echo = shout_echo("Hey", echo=5, intense=True)

# Call shout_echo() with "Hey" and intense=True: big_no_echo
big_no_echo = shout_echo("Hey", intense=True)

# Print values
print(with_big_echo)
print(big_no_echo)
```

### [Functions with variable-length arguments (*args)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope?ex=12)

```Python
# Define gibberish
def gibberish(*args):
    """Concatenate strings in *args together."""

    # Initialize an empty string: hodgepodge
    hodgepodge = ""

    # Concatenate the strings in args
    for word in args:
        hodgepodge += word

    # Return hodgepodge
    return hodgepodge

# Call gibberish() with one string: one_word
one_word = gibberish("luke")

# Call gibberish() with five strings: many_words
many_words = gibberish("luke", "leia", "han", "obi", "darth")

# Print one_word and many_words
print(one_word)
print(many_words)
```

### [Functions with variable-length keyword arguments (**kwargs)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope?ex=13)

```Python
# Define report_status
def report_status(**kwargs):
    """Print out the status of a movie character."""

    print("\nBEGIN: REPORT\n")

    # Iterate over the key-value pairs of kwargs
    for keys, values in kwargs.items():
        # Print out the keys and values, separated by a colon ':'
        print(keys + ": " + values)

    print("\nEND REPORT")

# First call to report_status()
report_status(name="luke", affiliation="jedi", status="missing")

# Second call to report_status()
report_status(name="anakin", affiliation="sith lord", status="deceased")
```

### [Bringing it all together (1)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope?ex=15)

```Python
# Define count_entries()
def count_entries(df, col_name="lang"):
    """Return a dictionary with counts of
    occurrences as value for each key."""

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
result1 = count_entries(tweets_df, "lang")

# Call count_entries(): result2
result2 = count_entries(tweets_df, "source")

# Print result1 and result2
print(result1)
print(result2)
```

### [Bringing it all together (2)](https://campus.datacamp.com/courses/python-data-science-toolbox-part-1/default-arguments-variable-length-arguments-and-scope?ex=16)

```Python
# Define count_entries()
def count_entries(df, *args):
    """Return a dictionary with counts of
    occurrences as value for each key."""
    
    #Initialize an empty dictionary: cols_count
    cols_count = {}
    
    # Iterate over column names in args
    for col_name in args:
    
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
result1 = count_entries(tweets_df, "lang")

# Call count_entries(): result2
result2 =  count_entries(tweets_df, "lang", "source")

# Print result1 and result2
print(result1)
print(result2)
```