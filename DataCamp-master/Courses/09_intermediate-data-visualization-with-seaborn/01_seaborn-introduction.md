## [Seaborn Introduction](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/seaborn-introduction)

Introduction to the Seaborn library and where it fits in the Python visualization landscape.

<br>

### [Seaborn foundation](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/seaborn-introduction?ex=2)

```
Q: What library provides the foundation for pandas and Seaborn plotting?
A: matplotlib
```

### [Reading a csv file](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/seaborn-introduction?ex=3)

```
# import all modules
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Read in the DataFrame
df = pd.read_csv(grant_file)
```

### [Comparing a histogram and distplot](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/seaborn-introduction?ex=4)

```
# Display pandas histogram
df['Award_Amount'].plot.hist()
plt.show()

# Clear out the pandas histogram
plt.clf()

#####################################################

# Display a Seaborn distplot
sns.distplot(df['Award_Amount'])
plt.show()

# Clear the distplot
plt.clf()
```

### [Plot a histogram](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/seaborn-introduction?ex=6)

```
# Create a distplot
sns.distplot(df['Award_Amount'],
             kde=False,
             bins=20)

# Display the plot
plt.show()
```

### [Rug plot and kde shading](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/seaborn-introduction?ex=7)

```
# Create a distplot of the Award Amount
sns.distplot(df['Award_Amount'],
             hist=False,
             rug=True,
             kde_kws={'shade':True})

# Plot the results
plt.show()
```

### [Interpreting the results](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/seaborn-introduction?ex=8)

```
Q: Looking at this distplot, which of these choices can you infer based on the visualization?
A: There are a large group of award amounts < $400K.
```

### [Create a regression plot](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/seaborn-introduction?ex=10)

```
# Create a regression plot of premiums vs. insurance_losses
sns.regplot(x="insurance_losses", y="premiums", data=df)

# Display the plot
plt.show()

#####################################################

# Create an lmplot of premiums vs. insurance_losses
sns.lmplot(data=df,
           x="insurance_losses",
           y="premiums")

# Display the second plot
plt.show()
```

### [Plotting multiple variables](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/seaborn-introduction?ex=11)

```
# Create a regression plot using hue
sns.lmplot(data=df,
           x="insurance_losses",
           y="premiums",
           hue="Region")

# Show the results
plt.show()
```

### [Facetting multiple regressions](https://campus.datacamp.com/courses/intermediate-data-visualization-with-seaborn/seaborn-introduction?ex=12)

```
# Create a regression plot with multiple rows
sns.lmplot(data=df,
           x="insurance_losses",
           y="premiums",
           row="Region")

# Show the plot
plt.show()
```