## [Customizing Seaborn Plots](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/customizing-seaborn-plots)

Overview of functions for customizing the display of Seaborn plots.

<br>

### [Setting the default style](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/customizing-seaborn-plots?ex=2)

```
# Plot the pandas histogram
df['fmr_2'].plot.hist()
plt.show()
plt.clf()

# Set the default seaborn style
sns.set()

# Plot the pandas histogram again
df['fmr_2'].plot.hist()
plt.show()
plt.clf()
```

### [Comparing styles](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/customizing-seaborn-plots?ex=3)

```
sns.set_style('dark')
sns.distplot(df['fmr_2'])

plt.show()
plt.clf()

#####################################################

sns.set_style('whitegrid')
sns.distplot(df['fmr_2'])

plt.show()
plt.clf()
```

### [Removing spines](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/customizing-seaborn-plots?ex=4)

```
# Set the style to white
sns.set_style('white')

# Create a regression plot
sns.lmplot(data=df,
           x='pop2010',
           y='fmr_2')

# Remove the spines
sns.despine()

# Show the plot and clear the figure
plt.show()
plt.clf()
```

### [Matplotlib color codes](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/customizing-seaborn-plots?ex=6)

```
# Set style, enable color code, and create a magenta distplot
sns.set(color_codes=True)
sns.distplot(df['fmr_3'], color='m')

# Show the plot
plt.show()
```

### [Using default palettes](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/customizing-seaborn-plots?ex=7)

```
# Loop through differences between bright and colorblind palettes
for p in ['bright', 'colorblind']:
    sns.set_palette(p)
    sns.distplot(df['fmr_3'])
    plt.show()
    
    # Clear the plots    
    plt.clf()
```

### [Creating Custom Palettes](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/customizing-seaborn-plots?ex=9)

```
sns.palplot(sns.color_palette( "Purples", 8))
plt.show()

#####################################################

sns.palplot(sns.color_palette( "husl", 10))
plt.show()

#####################################################

sns.palplot(sns.color_palette( "coolwarm", 6))
plt.show()
```

### [Using matplotlib axes](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/customizing-seaborn-plots?ex=11)

```
# Create a figure and axes
fig, ax = plt.subplots()

# Plot the distribution of data
sns.distplot(df['fmr_3'], ax=ax)

# Create a more descriptive x axis label
ax.set(xlabel="3 Bedroom Fair Market Rent")

# Show the plot
plt.show()
```

### [Additional plot customizations](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/customizing-seaborn-plots?ex=12)

```
# Create a figure and axes
fig, ax = plt.subplots()

# Plot the distribution of 1 bedroom rents
sns.distplot(df['fmr_1'], ax=ax)

# Modify the properties of the plot
ax.set(xlabel="1 Bedroom Fair Market Rent",
       xlim=(100,1500),
       title="US Rent")

# Display the plot
plt.show()
```

### [Adding annotations](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/customizing-seaborn-plots?ex=13)

```
# Create a figure and axes. Then plot the data
fig, ax = plt.subplots()
sns.distplot(df['fmr_1'], ax=ax)

# Customize the labels and limits
ax.set(xlabel="1 Bedroom Fair Market Rent", xlim=(100,1500), title="US Rent")

# Add vertical lines for the median and mean
ax.axvline(x=median, color='m', label='Median', linestyle='--', linewidth=2)
ax.axvline(x=mean, color='b', label='Mean', linestyle='-', linewidth=2)

# Show the legend and plot the data
ax.legend()
plt.show()
```

### [Multiple plots](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/customizing-seaborn-plots?ex=14)

```
# Create a plot with 1 row and 2 columns that share the y axis label
fig, (ax0, ax1) = plt.subplots(nrows=1, ncols=2, sharey=True)

# Plot the distribution of 1 bedroom apartments on ax0
sns.distplot(df['fmr_1'], ax=ax0)
ax0.set(xlabel="1 Bedroom Fair Market Rent", xlim=(100,1500))

# Plot the distribution of 2 bedroom apartments on ax1
sns.distplot(df['fmr_2'], ax=ax1)
ax1.set(xlabel="2 Bedroom Fair Market Rent", xlim=(100,1500))

# Display the plot
plt.show()
```