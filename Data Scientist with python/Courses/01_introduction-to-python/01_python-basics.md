## [Python Basics](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics)

An introduction to the basic concepts of Python. Learn how to use Python interactively and by using a script. Create your first variables and acquaint yourself with Python's basic data types.

<br>

### [The Python Interface](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics?ex=2)

```Python
# Example, do not modify!
print(5 / 8)

# Print the sum of 7 and 10
print(7 + 10)
```

### [When to use Python?](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics?ex=3)

```Python
Q: Python is a pretty versatile language. For which applications can you use Python?
A: All of the above.
```

### [Any comments?](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics?ex=4)

```Python
# Division
print(5 / 8)

# Addition
print(7 + 10)
```

### [Python as a calculator](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics?ex=5)

```Python
# Addition, subtraction
print(5 + 5)
print(5 - 5)

# Multiplication, division, modulo, and exponentiation
print(3 * 5)
print(10 / 2)
print(18 % 7)
print(4 ** 2)

# How much is your $100 worth after 7 years?
print(100 * (1.1**7))
```

### [Variable Assignment](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics?ex=7)

```Python
# Create a variable savings
savings = 100

# Print out savings
print(savings)
```

### [Calculations with variables](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics?ex=8)

```Python
# Create a variable savings
savings = 100

# Create a variable growth_multiplier
growth_multiplier = 1.1

# Calculate result
result = savings * (growth_multiplier **7)

# Print out result
print(result)
```

### [Other variable types](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics?ex=9)

```Python
# Create a variable desc
desc = "compound interest"

# Create a variable profitable
profitable = True
```

### [Guess the type](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics?ex=10)

```Python
Q: Which of the following options is correct?
A: a is of type float, b is of type str, c is of type bool
```

### [Operations with other types](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics?ex=11)

```Python
savings = 100
growth_multiplier = 1.1
desc = "compound interest"

# Assign product of growth_multiplier and savings to year1
year1 = savings * growth_multiplier

# Print the type of year1
print(type(year1))

# Assign sum of desc and desc to doubledesc
doubledesc= desc + desc

# Print out doubledesc
print (doubledesc)
```

### [Type conversion](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics?ex=12)

```Python
# Definition of savings and result
savings = 100
result = 100 * 1.10 ** 7

# Fix the printout
print("I started with $" + str(savings) + " and now have $" + str(result) + ". Awesome!")

# Definition of pi_string
pi_string = "3.1415926"

# Convert pi_string into float: pi_float
pi_float = float(pi_string)
print (pi_float)
```

### [Can Python handle everything?](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics?ex=13)

```Python
Q: Now that you know something more about combining different sources of information, have a look at the four Python expressions below. Which one of these will throw an error?
A: "The correct answer to this multiple choice exercise is answer number " + 2 .
```