## [Sharing visualizations with others](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/sharing-visualizations-with-others)

This chapter shows you how to share your visualizations with others: how to save your figures as files, how to adjust their look and feel, and how to automate their creation based on input data.

<br>

### [Selecting a style for printing](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/sharing-visualizations-with-others?ex=2)

```Python
Q: What style should you choose for your figures?
A: 'grayscale'
```

### [Switching between styles](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/sharing-visualizations-with-others?ex=3)

```Python
# Use the "ggplot" style and create new Figure/Axes
plt.style.use('ggplot')
fig, ax = plt.subplots()
ax.plot(seattle_weather["MONTH"], seattle_weather["MLY-TAVG-NORMAL"])
plt.show()

#####################################################

# Use the "Solarize_Light2" style and create new Figure/Axes
plt.style.use('Solarize_Light2')
fig, ax = plt.subplots()
ax.plot(austin_weather["MONTH"], austin_weather["MLY-TAVG-NORMAL"])
plt.show()
```

### [Saving a file several times](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/sharing-visualizations-with-others?ex=5)

```Python
# Show the figure
plt.show()

#####################################################

# Save as a PNG file
fig.savefig('my_figure.png')

#####################################################

# Save as a PNG file with 300 dpi
fig.savefig('my_figure_300dpi.png', dpi=300)
```

### [Save a figure with different sizes](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/sharing-visualizations-with-others?ex=6)

```Python
# Set figure dimensions and save as a PNG
fig.set_size_inches([3,5])
fig.savefig('figure_3_5.png')

#####################################################

# Set figure dimensions and save as a PNG
fig.set_size_inches([5,3])
fig.savefig('figure_5_3.png')
```

### [Unique values of a column](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/sharing-visualizations-with-others?ex=8)

```Python
# Extract the "Sport" column
sports_column = summer_2016_medals['Sport']

# Find the unique values of the "Sport" column
sports = sports_column.unique()

# Print out the unique sports values
print(sports)
```

### [Automate your visualization](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-matplotlib/sharing-visualizations-with-others?ex=9)

```Python
fig, ax = plt.subplots()

# Loop over the different sports branches
for sport in sports:
  # Extract the rows only for this sport
  sport_df = summer_2016_medals[summer_2016_medals['Sport'] == sport]
  # Add a bar for the "Weight" mean with std y error bar
  ax.bar(sport, sport_df["Weight"].mean(), yerr=sport_df["Weight"].std())

ax.set_ylabel("Weight")
ax.set_xticklabels(sports, rotation=90)

# Save the figure to file
fig.savefig('sports_weights.png')
```