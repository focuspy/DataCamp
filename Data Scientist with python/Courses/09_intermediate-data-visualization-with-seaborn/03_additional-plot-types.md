## [Additional Plot Types](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/additional-plot-types)

Overview of more complex plot types included in Seaborn.

<br>

### [stripplot() and swarmplot()](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/additional-plot-types?ex=2)

```Python
# Create the stripplot
sns.stripplot(data=df,
         x='Award_Amount',
         y='Model Selected',
         jitter=True)

plt.show()

#####################################################

# Create and display a swarmplot with hue set to the Region
sns.swarmplot(data=df,
         x='Award_Amount',
         y='Model Selected',
         hue='Region')

plt.show()
```

### [boxplots, violinplots and lvplots](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/additional-plot-types?ex=3)

```Python
# Create a boxplot
sns.boxplot(data=df,
         x='Award_Amount',
         y='Model Selected')

plt.show()
plt.clf()

#####################################################

# Create a violinplot with the husl palette
sns.violinplot(data=df,
         x='Award_Amount',
         y='Model Selected',
         palette='husl')

plt.show()
plt.clf()

#####################################################

# Create a lvplot with the Paired palette and the Region column as the hue
sns.lvplot(data=df,
         x='Award_Amount',
         y='Model Selected',
         palette='Paired',
         hue='Region')

plt.show()
plt.clf()
```

### [barplots, pointplots and countplots](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/additional-plot-types?ex=4)

```Python
# Show a countplot with the number of models used with each region a different color
sns.countplot(data=df,
         y="Model Selected",
         hue="Region")

plt.show()
plt.clf()

#####################################################

# Create a pointplot and include the capsize in order to show caps on the error bars
sns.pointplot(data=df,
         y='Award_Amount',
         x='Model Selected',
         capsize=.1)

plt.show()
plt.clf()

#####################################################

# Create a barplot with each Region shown as a different color
sns.barplot(data=df,
         y='Award_Amount',
         x='Model Selected',
         hue="Region")

plt.show()
plt.clf()
```

### [Regression and residual plots](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/additional-plot-types?ex=6)

```Python
# Display a regression plot for Tuition
sns.regplot(data=df,
         y='Tuition',
         x="SAT_AVG_ALL",
         marker='^',
         color='g')

plt.show()
plt.clf()

#####################################################

# Display the residual plot
sns.residplot(data=df,
          y='Tuition',
          x="SAT_AVG_ALL",
          color='g')

plt.show()
plt.clf()
```

### [Regression plot parameters](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/additional-plot-types?ex=7)

```Python
# Plot a regression plot of Tuition and the Percentage of Pell Grants
sns.regplot(data=df,
            y='Tuition',
            x="PCTPELL")

plt.show()
plt.clf()

#####################################################

# Create another plot that estimates the tuition by PCTPELL
sns.regplot(data=df,
            y='Tuition',
            x="PCTPELL",
            x_bins=5)

plt.show()
plt.clf()

#####################################################

# The final plot should include a line using a 2nd order polynomial
sns.regplot(data=df,
            y='Tuition',
            x="PCTPELL",
            x_bins=5,
            order=2)

plt.show()
plt.clf()
```

### [Binning data](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/additional-plot-types?ex=8)

```Python
# Create a scatter plot by disabling the regression line
sns.regplot(data=df,
            y='Tuition',
            x="UG",
            fit_reg=False)

plt.show()
plt.clf()

#####################################################

# Create a scatter plot and bin the data into 5 bins
sns.regplot(data=df,
            y='Tuition',
            x="UG",
            x_bins=5)

plt.show()
plt.clf()

#####################################################

# Create a regplot and bin the data into 8 bins
sns.regplot(data=df,
         y='Tuition',
         x="UG",
         x_bins=8)

plt.show()
plt.clf()
```

### [Creating heatmaps](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/additional-plot-types?ex=10)

```Python
# Create a crosstab table of the data
pd_crosstab = pd.crosstab(df["Group"], df["YEAR"])
print(pd_crosstab)

# Plot a heatmap of the table
sns.heatmap(pd_crosstab)

# Rotate tick marks for visibility
plt.yticks(rotation=0)
plt.xticks(rotation=90)

plt.show()
```

### [Customizing heatmaps](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/additional-plot-types?ex=11)

```Python
# Create the crosstab DataFrame
pd_crosstab = pd.crosstab(df["Group"], df["YEAR"])

# Plot a heatmap of the table with no color bar and using the BuGn palette
sns.heatmap(pd_crosstab, cbar=False, cmap="BuGn", linewidths=0.3)

# Rotate tick marks for visibility
plt.yticks(rotation=0)
plt.xticks(rotation=90)

#Show the plot
plt.show()
plt.clf()
```