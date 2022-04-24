## [Aggregating Data](https://campus.datacamp.com/courses/data-manipulation-with-pandas/aggregating-dataframes)

In this chapter, you’ll calculate summary statistics on DataFrame columns, and master grouped summary statistics and pivot tables.

<br>

### [Mean and median](https://campus.datacamp.com/courses/data-manipulation-with-pandas/aggregating-dataframes?ex=2)

```
# Print the head of the sales DataFrame
print(sales.head())

# Print the info about the sales DataFrame
print(sales.info())

# Print the mean of weekly_sales
print(sales["weekly_sales"].mean())

# Print the median of weekly_sales
print(sales["weekly_sales"].median())
```

### [Summarizing dates](https://campus.datacamp.com/courses/data-manipulation-with-pandas/aggregating-dataframes?ex=3)

```
# Print the maximum of the date column
print(sales["date"].max())

# Print the minimum of the date column
print(sales["date"].min())

```

### [Efficient summaries](https://campus.datacamp.com/courses/data-manipulation-with-pandas/aggregating-dataframes?ex=4)

```
# A custom IQR function
def iqr(column):
    return column.quantile(0.75) - column.quantile(0.25)
    
# Print IQR of the temperature_c column
print(sales["temperature_c"].agg(iqr))

#####################################################

# A custom IQR function
def iqr(column):
    return column.quantile(0.75) - column.quantile(0.25)

# Update to print IQR of temperature_c, fuel_price_usd_per_l, & unemployment
print(sales[["temperature_c", "fuel_price_usd_per_l", "unemployment"]].agg(iqr))

#####################################################

# Import NumPy and create custom IQR function
import numpy as np
def iqr(column):
    return column.quantile(0.75) - column.quantile(0.25)

# Update to print IQR and median of temperature_c, fuel_price_usd_per_l, & unemployment
print(sales[["temperature_c", "fuel_price_usd_per_l", "unemployment"]].agg([iqr,np.median]))
```

### [Cumulative statistics](https://campus.datacamp.com/courses/data-manipulation-with-pandas/aggregating-dataframes?ex=5)

```
# Sort sales_1_1 by date
sales_1_1 = sales_1_1.sort_values("date")

# Get the cumulative sum of weekly_sales, add as cum_weekly_sales col
sales_1_1["cum_weekly_sales"] = sales_1_1["weekly_sales"].cumsum()

# Get the cumulative max of weekly_sales, add as cum_max_sales col
sales_1_1["cum_max_sales"] = sales_1_1["weekly_sales"].cummax()

# See the columns you calculated
print(sales_1_1[["date", "weekly_sales", "cum_weekly_sales", "cum_max_sales"]])
```

### [Dropping duplicates](https://campus.datacamp.com/courses/data-manipulation-with-pandas/aggregating-dataframes?ex=7)

```
# Drop duplicate store/type combinations
store_types = sales.drop_duplicates(subset=["store", "type"])
print(store_types.head())

# Drop duplicate store/department combinations
store_depts = sales.drop_duplicates(subset=["store", "department"])
print(store_depts.head())

# Subset the rows where is_holiday is True and drop duplicate dates
holiday_dates = sales[sales["is_holiday"]].drop_duplicates("date")

# Print date col of holiday_dates
print(holiday_dates.head())
```

### [Counting categorical variables](https://campus.datacamp.com/courses/data-manipulation-with-pandas/aggregating-dataframes?ex=8)

```
# Count the number of stores of each type
store_counts = store_types["type"].value_counts()
print(store_counts)

# Get the proportion of stores of each type
store_props = store_types["type"].value_counts(normalize=True)
print(store_props)

# Count the number of each department number and sort
dept_counts_sorted = store_depts["department"].value_counts(sort="department", ascending=False)
print(dept_counts_sorted)

# Get the proportion of departments of each number and sort
dept_props_sorted = store_depts["department"].value_counts(sort="department", normalize=True)
print(dept_props_sorted)
```

### [What percent of sales occurred at each store type?](https://campus.datacamp.com/courses/data-manipulation-with-pandas/aggregating-dataframes?ex=10)

```
# Calc total weekly sales
sales_all = sales["weekly_sales"].sum()

# Subset for type A stores, calc total weekly sales
sales_A = sales[sales["type"] == "A"]["weekly_sales"].sum()

# Subset for type B stores, calc total weekly sales
sales_B = sales[sales["type"] == "B"]["weekly_sales"].sum()

# Subset for type C stores, calc total weekly sales
sales_C = sales[sales["type"] == "C"]["weekly_sales"].sum()

# Get proportion for each type
sales_propn_by_type = [sales_A, sales_B, sales_C] / sales_all
print(sales_propn_by_type)
```

### [Calculations with .groupby]()(https://campus.datacamp.com/courses/data-manipulation-with-pandas/aggregating-dataframes?ex=11)

```
# Group by type; calc total weekly sales
sales_by_type = sales.groupby("type")["weekly_sales"].sum()

# Get proportion for each type
sales_propn_by_type = sales_by_type/sum(sales.weekly_sales) 
print(sales_propn_by_type)

#####################################################

# From previous step
sales_by_type = sales.groupby("type")["weekly_sales"].sum()

# Group by type and is_holiday; calc total weekly sales
sales_by_type_is_holiday = sales.groupby(["type",'is_holiday'])["weekly_sales"].sum()
print(sales_by_type_is_holiday)
```

### [Multiple grouped summaries](https://campus.datacamp.com/courses/data-manipulation-with-pandas/aggregating-dataframes?ex=12)

```
# Import numpy with the alias np
import numpy as np

# For each store type, aggregate weekly_sales: get min, max, mean, and median
sales_stats = sales.groupby("type")["weekly_sales"].agg([min, max, np.mean, np.median])

# Print sales_stats
print(sales_stats)

# For each store type, aggregate unemployment and fuel_price_usd_per_l: get min, max, mean, and median
unemp_fuel_stats = sales.groupby("type")[["unemployment", "fuel_price_usd_per_l"]].agg([min, max, np.mean, np.median])

# Print unemp_fuel_stats
print(unemp_fuel_stats)
```

### [Pivoting on one variable](https://campus.datacamp.com/courses/data-manipulation-with-pandas/aggregating-dataframes?ex=14)

```
# Pivot for mean weekly_sales for each store type
mean_sales_by_type = sales.pivot_table(values="weekly_sales", index="type")

# Print mean_sales_by_type
print(mean_sales_by_type)

#####################################################

# Import NumPy as np
import numpy as np

# Pivot for mean and median weekly_sales for each store type
mean_med_sales_by_type = sales.pivot_table(values='weekly_sales', index= 'type', aggfunc=[np.mean, np.median])

# Print mean_med_sales_by_type
print(mean_med_sales_by_type)

#####################################################

# Pivot for mean weekly_sales by store type and holiday 
mean_sales_by_type_holiday = sales.pivot_table(values='weekly_sales', index= 'type', columns='is_holiday')

# Print mean_sales_by_type_holiday
print(mean_sales_by_type_holiday)

```

### [Fill in missing values and sum values with pivot tables](https://campus.datacamp.com/courses/data-manipulation-with-pandas/aggregating-dataframes?ex=15)

```
# Print mean weekly_sales by department and type; fill missing values with 0
import numpy as np
print(sales.pivot_table(values="weekly_sales", index="department", columns="type", aggfunc=np.mean, fill_value=0))

# Print the mean weekly_sales by department and type; fill missing values with 0s; sum all rows and cols
print(sales.pivot_table(values="weekly_sales", index="department", columns="type", fill_value=0, margins=True))
```

