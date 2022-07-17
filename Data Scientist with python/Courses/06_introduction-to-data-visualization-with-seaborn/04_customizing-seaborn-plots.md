## [Customizing Seaborn Plots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/customizing-seaborn-plots-4)

In this final chapter, you will learn how to add informative plot titles and axis labels, which are one of the most important parts of any data visualization! You will also learn how to customize the style of your visualizations in order to more quickly orient your audience to the key takeaways. Then, you will put everything you have learned together for the final exercises of the course!

<br>

### [Changing style and palette](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/customizing-seaborn-plots-4?ex=2)

```
# Set the style to "whitegrid"
sns.set_style("whitegrid")

# Create a count plot of survey responses
category_order = ["Never", "Rarely", "Sometimes", 
                  "Often", "Always"]

sns.catplot(x="Parents Advice", 
            data=survey_data, 
            kind="count", 
            order=category_order)

# Show plot
plt.show()

#####################################################

# Set the color palette to "Purples"
sns.set_style("whitegrid")
sns.set_palette("Purples")

# Create a count plot of survey responses
category_order = ["Never", "Rarely", "Sometimes", 
                  "Often", "Always"]

sns.catplot(x="Parents Advice", 
            data=survey_data, 
            kind="count", 
            order=category_order)

# Show plot
plt.show()

#####################################################

# Change the color palette to "RdBu"
sns.set_style("whitegrid")
sns.set_palette("RdBu")

# Create a count plot of survey responses
category_order = ["Never", "Rarely", "Sometimes", 
                  "Often", "Always"]

sns.catplot(x="Parents Advice", 
            data=survey_data, 
            kind="count", 
            order=category_order)

# Show plot
plt.show()

```

### [Changing the scale](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/customizing-seaborn-plots-4?ex=3)

```
# Set the context to "paper"
sns.set_context("paper")

# Create bar plot
sns.catplot(x="Number of Siblings", y="Feels Lonely",
            data=survey_data, kind="bar")

# Show plot
plt.show()

#####################################################

# Change the context to "notebook"
sns.set_context("notebook")

# Create bar plot
sns.catplot(x="Number of Siblings", y="Feels Lonely",
            data=survey_data, kind="bar")

# Show plot
plt.show()

#####################################################

# Change the context to "talk"
sns.set_context("talk")

# Create bar plot
sns.catplot(x="Number of Siblings", y="Feels Lonely",
            data=survey_data, kind="bar")

# Show plot
plt.show()

#####################################################

# Change the context to "poster"
sns.set_context("poster")

# Create bar plot
sns.catplot(x="Number of Siblings", y="Feels Lonely",
            data=survey_data, kind="bar")

# Show plot
plt.show()
```

### [Using a custom palette](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/customizing-seaborn-plots-4?ex=4)

```
# Set the style to "darkgrid"
sns.set_style("darkgrid")

# Set a custom color palette
sns.set_palette(["#39A7D0", "#36ADA4"])

# Create the box plot of age distribution by gender
sns.catplot(x="Gender",
            y="Age",
            data=survey_data,
            kind="box")

# Show plot
plt.show()
```

### [FacetGrids vs. AxesSubplots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/customizing-seaborn-plots-4?ex=6)

```
# Create scatter plot
g = sns.relplot(x="weight", 
                y="horsepower", 
                data=mpg,
                kind="scatter")

# Identify plot type
type_of_g = type(g)

# Print type
print(type_of_g)

#####################################################

Q: Which other Seaborn function creates a FacetGrid object instead of an AxesSubplot object?
A:sns.catplot()
```

### [Adding a title to a FacetGrid object](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/customizing-seaborn-plots-4?ex=7)

```
# Create scatter plot
g = sns.relplot(x="weight",
                y="horsepower",
                data=mpg,
                kind="scatter")

# Add a title "Car Weight vs. Horsepower"
g.fig.suptitle("Car Weight vs. Horsepower")

# Show plot
plt.show()
```

### [Adding a title and axis labels](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/customizing-seaborn-plots-4?ex=9)

```
# Create line plot
g = sns.lineplot(x="model_year", y="mpg_mean", 
                 data=mpg_mean,
                 hue="origin")

# Add a title "Average MPG Over Time"
g.set_title("Average MPG Over Time")

# Show plot
plt.show()

#####################################################

# Create line plot
g = sns.lineplot(x="model_year", y="mpg_mean", 
                 data=mpg_mean,
                 hue="origin")

# Add a title "Average MPG Over Time"
g.set_title("Average MPG Over Time")

# Add x-axis and y-axis labels
g.set(xlabel="Car Model Year",
      ylabel="Average MPG")


# Show plot
plt.show()
```

### [Rotating x-tick labels](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/customizing-seaborn-plots-4?ex=10)

```
# Create point plot
sns.catplot(x="origin",
            y="acceleration",
            data=mpg,
            kind="point",
            join=False,
            capsize=0.1)

# Rotate x-tick labels
plt.xticks(rotation=90)

# Show plot
plt.show()
```

### [Box plot with subgroups](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/customizing-seaborn-plots-4?ex=12)

```
# Set palette to "Blues"
sns.set_palette("Blues")

# Adjust to add subgroups based on "Interested in Pets"
g = sns.catplot(x="Gender",
                y="Age",
                data=survey_data,
                kind="box",
                hue="Interested in Pets")

# Set title to "Age of Those Interested in Pets vs. Not"
g.fig.suptitle("Age of Those Interested in Pets vs. Not")

# Show plot
plt.show()
```

### [Bar plot with subgroups and subplots](https://campus.datacamp.com/courses/introduction-to-data-visualization-with-seaborn/customizing-seaborn-plots-4?ex=13)

```
# Set the figure style to "dark"
sns.set_style("dark")

# Adjust to add subplots per gender
g = sns.catplot(x="Village - town",
                y="Likes Techno",
                data=survey_data,
                kind="bar",
                col="Gender")

# Add title and axis labels
g.fig.suptitle("Percentage of Young People Who Like Techno", y=1.02)
g.set(xlabel="Location of Residence",
       ylabel="% Who Like Techno")

# Show plot
plt.show()
```