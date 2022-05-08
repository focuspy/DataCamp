## [NumPy](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy)

NumPy is a fundamental Python package to efficiently practice data science. Learn to work with powerful tools in the NumPy array, and get started with data exploration.

<br>

### [Your First NumPy Array](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=2)

```
# Create list baseball
baseball = [180, 215, 210, 210, 188, 176, 209, 200]

# Import the numpy package as np
import numpy as np

# Create a numpy array from baseball: np_baseball
np_baseball= np.array(baseball)

# Print out type of np_baseball
print (type(np_baseball))
```

### [Baseball players' height](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=3)

```
# height is available as a regular list

# Import numpy
import numpy as np

# Create a numpy array from height_in: np_height_in
np_height_in = np.array(height_in)

# Print out np_height_in
print(np_height_in)

# Convert np_height_in to m: np_height_m
np_height_m = np_height_in * 0.0254

# Print np_height_m
print(np_height_m)
```

### [Baseball player's BMI](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=4)

```
# height and weight are available as regular lists

# Import numpy
import numpy as np

# Create array from height_in with metric units: np_height_m
np_height_m = np.array(height_in) * 0.0254

# Create array from weight_lb with metric units: np_weight_kg
np_weight_kg = np.array(weight_lb) * 0.453592

# Calculate the BMI: bmi
bmi = np_weight_kg / np_height_m ** 2

# Print out bmi
print(bmi)
```

### [Lightweight baseball players](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=5)

```
# height and weight are available as a regular lists

# Import numpy
import numpy as np

# Calculate the BMI: bmi
np_height_m = np.array(height_in) * 0.0254
np_weight_kg = np.array(weight_lb) * 0.453592
bmi = np_weight_kg / np_height_m ** 2

# Create the light array
light = bmi < 21

# Print out light
print(light)

# Print out BMIs of all baseball players whose BMI is below 21
print(bmi[light])
```

### [NumPy Side Effects](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=6)

```
Q: Can you tell which code chunk builds the exact same Python object?
A: np.array([4, 3, 0]) + np.array([0, 2, 2])
```

### [Subsetting NumPy Arrays](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=7)

```
# height and weight are available as a regular lists

# Import numpy
import numpy as np

# Store weight and height lists as numpy arrays
np_weight_lb = np.array(weight_lb)
np_height_in = np.array(height_in)

# Print out the weight at index 50
print(np.array(np_weight_lb[50]))

# Print out sub-array of np_height_in: index 100 up to and including index 110
print(np.array(np_height_in[100:111]))
```

### [Your First 2D NumPy Array](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=9)

```
# Create baseball, a list of lists
baseball = [[180, 78.4],
            [215, 102.7],
            [210, 98.5],
            [188, 75.2]]

# Import numpy
import numpy as np

# Create a 2D numpy array from baseball: np_baseball
np_baseball = np.array(baseball)

# Print out the type of np_baseball
print(type(np_baseball))

# Print out the shape of np_baseball
print(np_baseball.shape)
```

### [Baseball data in 2D form](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=10)

```
# baseball is available as a regular list of lists

# Import numpy package
import numpy as np

# Create a 2D numpy array from baseball: np_baseball
np_baseball = np.array(baseball)

# Print out the shape of np_baseball
print(np_baseball.shape)
```

### [Subsetting 2D NumPy Arrays](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=11)

```
# baseball is available as a regular list of lists

# Import numpy package
import numpy as np

# Create np_baseball (2 cols)
np_baseball = np.array(baseball)

# Print out the 50th row of np_baseball

print(np_baseball[49,:])

# Select the entire second column of np_baseball: np_weight_lb
np_weight_lb = np_baseball[:,1]

# Print out height of 124th player
print(np_baseball[123, 0])
```

### [2D Arithmetic](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=12)

```
# baseball is available as a regular list of lists
# updated is available as 2D numpy array

# Import numpy package
import numpy as np

# Create np_baseball (3 cols)
np_baseball = np.array(baseball)

# Print out addition of np_baseball and updated
print(np_baseball + updated)

# Create numpy array: conversion
conversion = np.array([0.0254, 0.453592, 1])

# Print out product of np_baseball and conversion
print(np_baseball*conversion)
```

### [Average versus median](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=14)

```
# np_baseball is available

# Import numpy
import numpy as np

# Create np_height_in from np_baseball
np_height_in = np.array(np_baseball[:,0])

# Print out the mean of np_height_in
print(np.mean(np_height_in))

# Print out the median of np_height_in
print(np.median(np_height_in))
```

### [Explore the baseball data](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=15)

```
# np_baseball is available

# Import numpy
import numpy as np

# Print mean height (first column)
avg = np.mean(np_baseball[:,0])
print("Average: " + str(avg))

# Print median height. Replace 'None'
med = None
print("Median: " + str(med))

# Print out the standard deviation on height. Replace 'None'
stddev = None
print("Standard Deviation: " + str(stddev))

# Print out correlation between first and second column. Replace 'None'
corr = None
print("Correlation: " + str(corr))
```

### [Blend it all together](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-4-numpy?ex=16)

```
# heights and positions are available as lists

# Import numpy
import numpy as np

# Convert positions and heights to numpy arrays: np_positions, np_heights
np_positions = np.array(positions)
np_heights = np.array(heights)

# Heights of the goalkeepers: gk_heights
gk_heights = np_heights[np_positions == 'GK']

# Heights of the other players: other_heights
other_heights = np_heights[np_positions != 'GK']

# Print out the median height of goalkeepers. Replace 'None'
print("Median height of goalkeepers: " + str(np.median(gk_heights)))

# Print out the median height of other players. Replace 'None'
print("Median height of other players: " + str(np.median(other_heights)))
```