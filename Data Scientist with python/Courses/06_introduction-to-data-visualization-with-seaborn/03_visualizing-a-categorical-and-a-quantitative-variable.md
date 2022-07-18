## [Visualizing a Categorical and a Quantitative Variable](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-a-categorical-and-a-quantitative-variable)

Categorical variables are present in nearly every dataset, but they are especially prominent in survey data. In this chapter, you will learn how to create and customize categorical plots such as box plots, bar plots, count plots, and point plots. Along the way, you will explore survey data from young people about their interests, students about their study habits, and adult men about their feelings about masculinity.

<br>

### [Count plots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-a-categorical-and-a-quantitative-variable?ex=2)

```Python
# Create count plot of internet usage
sns.catplot(x="Internet usage",
            data=survey_data,
            kind="count")

# Show plot
plt.show()

#####################################################

# Change the orientation of the plot
sns.catplot(y="Internet usage", data=survey_data,
            kind="count")

# Show plot
plt.show()

#####################################################

# Separate into column subplots based on age category
sns.catplot(y="Internet usage", data=survey_data,
            kind="count",
            col="Age Category")
# Show plot
plt.show()
```

### [Bar plots with percentages](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-a-categorical-and-a-quantitative-variable?ex=3)

```Python
# Create a bar plot of interest in math, separated by gender

sns.catplot(x="Gender", y="Interested in Math",
            data=survey_data,
            kind="bar")
# Show plot
plt.show()
```

### [Customizing bar plots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-a-categorical-and-a-quantitative-variable?ex=4)

```Python
# Create bar plot of average final grade in each study category
sns.catplot(x="study_time", y="G3",
            data=student_data,
            kind="bar")
# Show plot
plt.show()

#####################################################

# List of categories from lowest to highest
category_order = ["<2 hours", 
                  "2 to 5 hours", 
                  "5 to 10 hours", 
                  ">10 hours"]

# Rearrange the categories
sns.catplot(x="study_time", y="G3",
            data=student_data,
            kind="bar",
            order=["<2 hours", 
                    "2 to 5 hours", 
                    "5 to 10 hours", 
                    ">10 hours"])

# Show plot
plt.show()

#####################################################

# List of categories from lowest to highest
category_order = ["<2 hours", 
                  "2 to 5 hours", 
                  "5 to 10 hours", 
                  ">10 hours"]

# Turn off the confidence intervals
sns.catplot(x="study_time", y="G3",
            data=student_data,
            kind="bar",
            order=category_order,
            ci=None)
# Show plot
plt.show()
```

### [Create and interpret a box plot](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-a-categorical-and-a-quantitative-variable?ex=6)

```Python
# Specify the category ordering
study_time_order = ["<2 hours", "2 to 5 hours", 
                    "5 to 10 hours", ">10 hours"]

# Create a box plot and set the order of the categories

sns.catplot(x="study_time", y="G3", 
            data=student_data,
            kind='box',
            order=study_time_order)

# Show plot
plt.show()

#####################################################

Q: Which of the following is a correct interpretation of this box plot?
A: The median grade among students studying less than 2 hours is 10.0.

```

### [Omitting outliers](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-a-categorical-and-a-quantitative-variable?ex=7)

```Python
# Create a box plot with subgroups and omit the outliers
sns.catplot(x="internet",y="G3",
            data=student_data,
            kind='box',
            hue="location",
            sym='') # Omitting outliers

# Show plot
plt.show()
```

### [Adjusting the whiskers](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-a-categorical-and-a-quantitative-variable?ex=8)

```Python
# Set the whiskers to 0.5 * IQR
sns.catplot(x="romantic", y="G3",
            data=student_data,
            kind="box",
            whis=0.5)

# Show plot
plt.show()

#####################################################

# Extend the whiskers to the 5th and 95th percentile
sns.catplot(x="romantic", y="G3",
            data=student_data,
            kind="box",
            whis=[5,95])

# Show plot
plt.show()

#####################################################

# Set the whiskers at the min and max values
sns.catplot(x="romantic", y="G3",
            data=student_data,
            kind="box",
            whis=[0, 100])

# Show plot
plt.show()
```

### [Customizing point plots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-a-categorical-and-a-quantitative-variable?ex=10)

```Python
# Create a point plot of family relationship vs. absences
sns.catplot(x="famrel", y="absences",
			data=student_data,
            kind="point")
                 
# Show plot
plt.show()

#####################################################

# Add caps to the confidence interval
sns.catplot(x="famrel", y="absences",
			data=student_data,
            kind="point",
            capsize=0.2)
             
# Show plot
plt.show()

#####################################################

# Remove the lines joining the points
sns.catplot(x="famrel", y="absences",
			data=student_data,
            kind="point",
            capsize=0.2,
            join=False)
            
# Show plot
plt.show()
```

### [Point plots with subgroups](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/visualizing-a-categorical-and-a-quantitative-variable?ex=11)

```Python
# Create a point plot that uses color to create subgroups
sns.catplot(x="romantic", y="absences",
			data=student_data,
            kind="point",
            hue="school")
            
# Show plot
plt.show()

#####################################################

# Turn off the confidence intervals for this plot
sns.catplot(x="romantic", y="absences",
			data=student_data,
            kind="point",
            hue="school",
            ci=None)
# Show plot
plt.show()

#####################################################

# Import median function from numpy
from numpy import median

# Plot the median number of absences instead of the mean
sns.catplot(x="romantic", y="absences",
			data=student_data,
            kind="point",
            hue="school",
            ci=None,
            estimator=median)
            
# Show plot
plt.show()
```