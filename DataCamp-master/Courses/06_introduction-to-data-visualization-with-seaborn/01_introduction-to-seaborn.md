## [Introduction to Seaborn](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/introduction-to-seaborn)

What is Seaborn, and when should you use it? In this chapter, you will find out! Plus, you will learn how to create scatter plots and count plots with both lists of data and pandas DataFrames. You will also be introduced to one of the big advantages of using Seaborn - the ability to easily add a third variable to your plots by using color to represent different subgroups.

<br>

### [Making a scatter plot with lists](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/introduction-to-seaborn?ex=2)

```
# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

#####################################################

# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Create scatter plot with GDP on the x-axis and number of phones on the y-axis
sns.scatterplot(x=gdp, y=phones);

#####################################################

# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Create scatter plot with GDP on the x-axis and number of phones on the y-axis
sns.scatterplot(x=gdp, y=phones)

# Show plot
plt.show()

#####################################################

# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Change this scatter plot to have percent literate on the y-axis
sns.scatterplot(x=gdp, y=percent_literate)

# Show plot
plt.show()
```

### [Making a count plot with a list](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/introduction-to-seaborn?ex=3)

```
# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Change this scatter plot to have percent literate on the y-axis
sns.scatterplot(x=gdp, y=percent_literate)

# Show plot
plt.show()
```

### ["Tidy" vs. "untidy" data](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/introduction-to-seaborn?ex=5)

```
# Import Pandas
import pandas as pd

# Create a DataFrame from csv file
df = pd.read_csv(csv_filepath)

# Print the head of df
print(df.head())

#####################################################

Q: View the first five rows of the DataFrame df. Is it tidy? Why or why not?
A: No, because a single column contains different types of information.
```

### [Making a count plot with a DataFrame](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/introduction-to-seaborn?ex=6)

```
# Import Matplotlib, Pandas, and Seaborn
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns

# Create a DataFrame from csv file
df = pd.read_csv(csv_filepath)

# Create a count plot with "Spiders" on the x-axis
sns.countplot(x='Spiders', data=df)

# Display the plot
plt.show()
```

### [Hue and scatter plots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/introduction-to-seaborn?ex=8)

```
# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Create a scatter plot of absences vs. final grade
sns.scatterplot(x='absences', y='G3', data=student_data, hue='location')

# Show plot
plt.show()

#####################################################

# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Change the legend order in the scatter plot
sns.scatterplot(x="absences", y="G3", 
                data=student_data, 
                hue="location",
                hue_order=["Rural","Urban"])

# Show plot
plt.show()

```

### [Hue and count plots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/introduction-to-seaborn?ex=9)

```
# Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

# Create a dictionary mapping subgroup values to colors
palette_colors = {'Rural': "green", 'Urban': "blue"}

# Create a count plot of school with location subgroups
sns.countplot(x='school',
                data=student_data,
                hue='location',
                palette=palette_colors)

# Display plot
plt.show()
```