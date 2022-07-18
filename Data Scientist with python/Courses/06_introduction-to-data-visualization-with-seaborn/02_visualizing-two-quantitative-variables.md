## [Visualizing Two Quantitative Variables](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-two-quantitative-variables)

In this chapter, you will create and customize plots that visualize the relationship between two quantitative variables. To do this, you will use scatter plots and line plots to explore how the level of air pollution in a city changes over the course of a day and how horsepower relates to fuel efficiency in cars. You will also see another big advantage of using Seaborn - the ability to easily create subplots in a single figure!

<br>

### [Creating subplots with col and row](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-two-quantitative-variables?ex=2)

```Python
# Change to use relplot() instead of scatterplot()
sns.relplot(x="absences",
            y="G3",
            data=student_data,
            kind='scatter')

# Show plot
plt.show()

#####################################################

# Change to make subplots based on study time
sns.relplot(x="absences", y="G3", 
            data=student_data,
            kind="scatter",
            col="study_time")

# Show plot
plt.show()

#####################################################

# Change this scatter plot to arrange the plots in rows instead of columns
sns.relplot(x="absences", y="G3", 
            data=student_data,
            kind="scatter", 
            row="study_time")

# Show plot
plt.show()

```

### [Creating two-factor subplots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-two-quantitative-variables?ex=3)

```Python
# Create a scatter plot of G1 vs. G3
sns.relplot(x="G1", y="G3", 
            data=student_data,
            kind="scatter")

# Show plot
plt.show()

#####################################################

# Adjust to add subplots based on school support
sns.relplot(x="G1", y="G3", 
            data=student_data,
            kind="scatter", 
            col="schoolsup",
            col_order=['yes','no'])

# Show plot
plt.show()

#####################################################
# Adjust further to add subplots based on family support
sns.relplot(x="G1", y="G3", 
            data=student_data,
            kind="scatter", 
            col="schoolsup",
            col_order=['yes','no'],
            row="famsup",
            row_order=["yes", "no"])

# Show plot
plt.show()
```

### [Changing the size of scatter plot points](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-two-quantitative-variables?ex=5)

```Python
# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Create scatter plot of horsepower vs. mpg
sns.relplot(x="horsepower", y="mpg", 
            data=mpg, kind="scatter", 
            size="cylinders",
            hue="cylinders")

# Show plot
plt.show()

#####################################################

# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Create scatter plot of horsepower vs. mpg
sns.relplot(x="horsepower", y="mpg", 
            data=mpg, kind="scatter", 
            size="cylinders",
            hue="cylinders")

# Show plot
plt.show()
```

### [Changing the style of scatter plot points](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-two-quantitative-variables?ex=6)

```Python
# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Create a scatter plot of acceleration vs. mpg
sns.relplot(x='acceleration', y='mpg', data=mpg, kind='scatter', style='origin', hue='origin')

# Show plot
plt.show()
```

### [Interpreting line plots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-two-quantitative-variables?ex=8)

```Python
# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Create line plot
sns.relplot(x="model_year",y="mpg",
            data=mpg,
            kind='line')

# Show plot
plt.show()

#####################################################

Q: Which of the following is NOT a correct interpretation of this line plot?
A: The distribution of miles per gallon is smaller in 1973 compared to 1977.

```

### [Visualizing standard deviation with line plots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-two-quantitative-variables?ex=9)

```Python
# Make the shaded area show the standard deviation
sns.relplot(x="model_year", y="mpg",
            data=mpg, kind="line", ci='sd')

# Show plot
plt.show()
```

### [Plotting subgroups in line plots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-two-quantitative-variables?ex=10)

```Python
#####################################################

# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Create line plot of model year vs. horsepower
sns.relplot(x="model_year", y="horsepower", 
            data=mpg, kind="line", 
            ci=None, style="origin", 
            hue="origin", 
            markers=True, 
            dashes=False)

# Show plot
plt.show()

#####################################################

# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Change to create subgroups for country of origin
sns.relplot(x="model_year", y="horsepower", 
            data=mpg, kind="line", 
            ci=None,
            style="origin", 
            hue="origin", )

# Show plot
plt.show()

#####################################################

# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Add markers and make each line have the same style
sns.relplot(x="model_year", y="horsepower", 
            data=mpg, kind="line", 
            ci=None, style="origin", 
            hue="origin", 
            markers=True, 
            dashes=False)

# Show plot
plt.show()
```