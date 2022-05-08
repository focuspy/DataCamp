## [Introduction to Matplotlib](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/introduction-to-matplotlib)

This chapter introduces the Matplotlib visualization library and demonstrates how to use it with data.

<br>

### [Using the matplotlib.pyplot interface](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/introduction-to-matplotlib?ex=2)

```
# Import the matplotlib.pyplot submodule and name it plt
import matplotlib.pyplot as plt

# Create a Figure and an Axes with plt.subplots
fig, ax = plt.subplots()

# Call the show function to show the result
plt.show()
```

### [Adding data to an Axes object](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/introduction-to-matplotlib?ex=3)

```
# Import the matplotlib.pyplot submodule and name it plt
import matplotlib.pyplot as plt

# Create a Figure and an Axes with plt.subplots
fig, ax = plt.subplots()

# Plot MLY-PRCP-NORMAL from seattle_weather against the MONTH
ax.plot(seattle_weather["MONTH"], seattle_weather["MLY-PRCP-NORMAL"])

# Plot MLY-PRCP-NORMAL from austin_weather against MONTH
ax.plot(austin_weather["MONTH"], austin_weather["MLY-PRCP-NORMAL"])

# Call the show function
plt.show()
```

### [Customizing data appearance](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/introduction-to-matplotlib?ex=5)

```
# Plot Seattle data, setting data appearance
ax.plot(seattle_weather["MONTH"], seattle_weather["MLY-PRCP-NORMAL"], color='b', marker='o', linestyle='--')

# Plot Austin data, setting data appearance
ax.plot(austin_weather["MONTH"], austin_weather["MLY-PRCP-NORMAL"], color='r', marker='v', linestyle='--')

# Call show to display the resulting plot
plt.show()
```

### [Customizing axis labels and adding titles](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/introduction-to-matplotlib?ex=6)

```
ax.plot(seattle_weather["MONTH"], seattle_weather["MLY-PRCP-NORMAL"])
ax.plot(austin_weather["MONTH"], austin_weather["MLY-PRCP-NORMAL"])

# Customize the x-axis label
ax.set_xlabel('Time (months)')

# Customize the y-axis label
ax.set_ylabel('Precipitation (inches)')

# Add the title
ax.set_title('Weather patterns in Austin and Seattle')

# Display the figure
plt.show()
```

### [Creating a grid of subplots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/introduction-to-matplotlib?ex=8)

```
Q: How would you create a Figure with 6 Axes objects organized in 3 rows and 2 columns?
A: fig, ax = plt.subplots(3, 2)
```

### [Creating small multiples with plt.subplots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/introduction-to-matplotlib?ex=9)

```
# Create a Figure and an array of subplots with 2 rows and 2 columns
fig, ax = plt.subplots(2, 2)

# Addressing the top left Axes as index 0, 0, plot month and Seattle precipitation
ax[0, 0].plot(seattle_weather['MONTH'], seattle_weather['MLY-PRCP-NORMAL'])

# In the top right (index 0,1), plot month and Seattle temperatures
ax[0, 1].plot(seattle_weather['MONTH'], seattle_weather['MLY-TAVG-NORMAL'])

# In the bottom left (1, 0) plot month and Austin precipitations
ax[1, 0].plot(austin_weather['MONTH'], austin_weather['MLY-PRCP-NORMAL'])

# In the bottom right (1, 1) plot month and Austin temperatures
ax[1, 1].plot(austin_weather['MONTH'], austin_weather['MLY-TAVG-NORMAL'])

plt.show()
```

### [Small multiples with shared y axis](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/introduction-to-matplotlib?ex=10)

```
# Create a figure and an array of axes: 2 rows, 1 column with shared y axis
fig, ax = plt.subplots(2, 1, sharey=True)

# Plot Seattle precipitation data in the top axes
ax[0].plot(seattle_weather['MONTH'], seattle_weather['MLY-PRCP-NORMAL'], color = 'b')
ax[0].plot(seattle_weather['MONTH'], seattle_weather['MLY-PRCP-25PCTL'], color = 'b', linestyle = '--')
ax[0].plot(seattle_weather['MONTH'], seattle_weather['MLY-PRCP-75PCTL'], color = 'b', linestyle = '--')

# Plot Austin precipitation data in the bottom axes
ax[1].plot(austin_weather['MONTH'], austin_weather['MLY-PRCP-NORMAL'], color = 'r')
ax[1].plot(austin_weather['MONTH'], austin_weather['MLY-PRCP-25PCTL'], color = 'r', linestyle = '--')
ax[1].plot(austin_weather['MONTH'], austin_weather['MLY-PRCP-75PCTL'], color = 'r', linestyle = '--')

plt.show()
```