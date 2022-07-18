## [Python Lists](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists)

Learn to store, access, and manipulate data in lists: the first step toward efficiently working with huge amounts of data.

<br>

### [Create a list](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=2)

```Python
# area variables (in square meters)
hall = 11.25
kit = 18.0
liv = 20.0
bed = 10.75
bath = 9.50

# Create list areas
areas= [hall , kit , liv , bed, bath]

# Print areas
print(areas)
```

### [Create list with different types](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=3)

```Python
# area variables (in square meters)
hall = 11.25
kit = 18.0
liv = 20.0
bed = 10.75
bath = 9.50

# Adapt list areas
areas = ["hallway", hall, "kitchen" , kit, "living room", liv, "bedroom" ,bed, "bathroom", bath]

# Print areas
print(areas)
```

### [Select the valid list](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=4)

```Python
Q: Can you tell which ones of the following lines of Python code are valid ways to build a list?
A: A, B and C
```

### [List of lists](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=5)

```Python
# area variables (in square meters)
hall = 11.25
kit = 18.0
liv = 20.0
bed = 10.75
bath = 9.50

# house information as list of lists
house = [["hallway", hall],
         ["kitchen", kit],
         ["living room", liv],
         ["bedroom",bed],
         ["bathroom", bath]]
# Print out house
print(house)

# Print out the type of house
print(type(house))
```

### [Subset and conquer](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=7)

```Python
# Create the areas list
areas = ["hallway", 11.25, "kitchen", 18.0, "living room", 20.0, "bedroom", 10.75, "bathroom", 9.50]

# Print out second element from areas
print(areas[1])

# Print out last element from areas
print(areas[-1:])

# Print out the area of the living room
print(areas[5])
```

### [Subset and calculate](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=8)

```Python
# Create the areas list
areas = ["hallway", 11.25, "kitchen", 18.0, "living room", 20.0, "bedroom", 10.75, "bathroom", 9.50]

# Sum of kitchen and bedroom area: eat_sleep_area
eat_sleep_area = areas[3]+areas[7]

# Print the variable eat_sleep_area
print(eat_sleep_area)
```

### [Slicing and dicing](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=9)

```Python
# Create the areas list
areas = ["hallway", 11.25, "kitchen", 18.0, "living room", 20.0, "bedroom", 10.75, "bathroom", 9.50]

# Use slicing to create downstairs
downstairs = areas[0:6]

# Use slicing to create upstairs
upstairs = areas[6:10]

# Print out downstairs and upstairs
print(downstairs)
print(upstairs)
```

### [Slicing and dicing (2)](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=10)

```Python
# Create the areas list
areas = ["hallway", 11.25, "kitchen", 18.0, "living room", 20.0, "bedroom", 10.75, "bathroom", 9.50]

# Alternative slicing to create downstairs
downstairs = areas[ :6]
print(downstairs)
# Alternative slicing to create upstairs
upstairs= areas [6:]
print(upstairs)
```

### [Subsetting lists of lists](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=11)

```Python
Q: What will house[-1][1] return?
A: A float: the bathroom area
```

### [Replace list elements](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=13)

```Python
# Create the areas list
areas = ["hallway", 11.25, "kitchen", 18.0, "living room", 20.0, "bedroom", 10.75, "bathroom", 9.50]

# Correct the bathroom area
areas [9] = 10.50
print(areas)
# Change "living room" to "chill zone"
areas [4] = "chill zone"
print (areas)
```

### [Extend a list](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=14)

```Python
# Create the areas list and make some changes
areas = ["hallway", 11.25, "kitchen", 18.0, "chill zone", 20.0,
         "bedroom", 10.75, "bathroom", 10.50]

# Add poolhouse data to areas, new list is areas_1
areas_1 = areas + ["poolhouse", 24.5]
print(areas_1)
# Add garage data to areas_1, new list is areas_2
areas_2 = areas_1 + ["garage", 15.45]
print(areas_2)
```

### [Delete list elements](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=15)

```Python
Q: Which of the code chunks will do the job for us?
A: del(areas[-4:-2])
```

### [Inner workings of lists](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-2-python-lists?ex=16)

```Python
# Create list areas
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Create areas_copy
areas_copy = list(areas)

# Change areas_copy
areas_copy[0] = 5.0

# Print areas
print(areas)
print(areas_copy)
```