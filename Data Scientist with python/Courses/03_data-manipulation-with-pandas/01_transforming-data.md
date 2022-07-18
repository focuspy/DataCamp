## [Transforming Data](https://campus.datacamp.com/courses/data-manipulation-with-pandas/transforming-dataframes)

Let’s master the pandas basics. Learn how to inspect DataFrames and perform fundamental manipulations, including sorting rows, subsetting, and adding new columns.

<br>

### [Inspecting a DataFrame](https://campus.datacamp.com/courses/data-manipulation-with-pandas/transforming-dataframes?ex=2)

```Python
# Print the head of the homelessness data
print(homelessness.head())

# Print information about homelessness
print(homelessness.info())

# Print the shape of homelessness
print(homelessness.shape)

# Print a description of homelessness
print(homelessness.describe())
```

### [Parts of a DataFrame](https://campus.datacamp.com/courses/data-manipulation-with-pandas/transforming-dataframes?ex=3)

```Python
# Import pandas using the alias pd
import pandas as pd

# Print the values of homelessness
print(homelessness.values)

# Print the column index of homelessness
print(homelessness.columns)

# Print the row index of homelessness
print(homelessness.index)
```

### [Sorting rows](https://campus.datacamp.com/courses/data-manipulation-with-pandas/transforming-dataframes?ex=5)

```Python
# Sort homelessness by individual
homelessness_ind = homelessness.sort_values("individuals")

# Print the top few rows
print(homelessness_ind.head())

#####################################################

# Sort homelessness by descending family members
homelessness_fam = homelessness.sort_values("family_members", ascending=False)

# Print the top few rows
print (homelessness_fam.head())

#####################################################

# Sort homelessness by region, then descending family members
homelessness_reg_fam = homelessness.sort_values(["region", "family_members"], ascending=[True, False])

# Print the top few rows
print(homelessness_reg_fam.head())
```

### [Subsetting columns](https://campus.datacamp.com/courses/data-manipulation-with-pandas/transforming-dataframes?ex=6)

```Python
# Select the individuals column
individuals = homelessness["individuals"]

# Print the head of the result
print (individuals.head())

#####################################################

# Select the state and family_members columns
state_fam = homelessness[["state", "family_members"]]

# Print the head of the result
print (state_fam.head())

#####################################################

# Select only the individuals and state columns, in that order
ind_state = homelessness[["individuals", "state"]]

# Print the head of the result
print (ind_state.head())
```

### [Subsetting rows](https://campus.datacamp.com/courses/data-manipulation-with-pandas/transforming-dataframes?ex=7)

```Python
# Filter for rows where individuals is greater than 10000
ind_gt_10k = homelessness[homelessness["individuals"] > 10000]

# See the result
print(ind_gt_10k)

#####################################################

# Filter for rows where region is Mountain
mountain_reg = homelessness[homelessness["region"] == "Mountain"]

# See the result
print (mountain_reg)

#####################################################

# Filter for rows where family_members is less than 1000 
# and region is Pacific
fam_lt_1k_pac = homelessness[(homelessness["family_members"] < 1000) & (homelessness["region"]=="Pacific")]

# See the result
print(fam_lt_1k_pac)
```

### [Subsetting rows by categorical variables](https://campus.datacamp.com/courses/data-manipulation-with-pandas/transforming-dataframes?ex=8)

```Python
# Subset for rows in South Atlantic or Mid-Atlantic regions
south_mid_atlantic = homelessness[homelessness["region"].isin(["South Atlantic", "Mid-Atlantic"])]

# See the result
print(south_mid_atlantic)

#####################################################

# The Mojave Desert states
canu = ["California", "Arizona", "Nevada", "Utah"]

# Filter for rows in the Mojave Desert states
mojave_homelessness = homelessness[homelessness["state"].isin(canu)]

# See the result
print(mojave_homelessness)
```

### [Adding new columns](https://campus.datacamp.com/courses/data-manipulation-with-pandas/transforming-dataframes?ex=10)

```Python
# Add total col as sum of individuals and family_members
homelessness["total"] = homelessness["individuals"] + homelessness["family_members"]

# Add p_individuals col as proportion of individuals
homelessness["p_individuals"] = homelessness["individuals"] / homelessness["total"]

# See the result
print(homelessness)
```

### [Combo-attack!](https://campus.datacamp.com/courses/data-manipulation-with-pandas/transforming-dataframes?ex=11)

```Python
# Create indiv_per_10k col as homeless individuals per 10k state pop
homelessness["indiv_per_10k"] = 10000 * homelessness["individuals"] / homelessness["state_pop"] 

# Subset rows for indiv_per_10k greater than 20
high_homelessness = homelessness[homelessness["indiv_per_10k"] > 20]

# Sort high_homelessness by descending indiv_per_10k
high_homelessness_srt = high_homelessness.sort_values("indiv_per_10k", ascending=False)

# From high_homelessness_srt, select the state and indiv_per_10k cols
result = high_homelessness_srt[["state","indiv_per_10k"]]

# See the result
print(result)
```