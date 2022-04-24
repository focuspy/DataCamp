## [Merging Ordered and Time-Series Data ](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-ordered-and-time-series-data)

In this final chapter, you’ll step up a gear and learn to apply pandas' specialized methods for merging time-series and ordered data together with real-world financial and economic data from the city of Chicago. You’ll also learn how to query resulting tables using a SQL-style format, and unpivot data using the melt method. 

<br>

### [Correlation between GDP and S&P500](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-ordered-and-time-series-data?ex=2)

```
# Use merge_ordered() to merge gdp and sp500 on year and date
gdp_sp500 = pd.merge_ordered(gdp, sp500, left_on='year', right_on='date', 
                             how='left')

# Print gdp_sp500
print(gdp_sp500)

#####################################################

# Use merge_ordered() to merge gdp and sp500, interpolate missing value
gdp_sp500 = pd.merge_ordered(gdp, sp500, left_on='year', right_on='date', 
                             how='left',  fill_method='ffill')

# Print gdp_sp500
print (gdp_sp500)

#####################################################

# Use merge_ordered() to merge gdp and sp500, interpolate missing value
gdp_sp500 = pd.merge_ordered(gdp, sp500, left_on='year', right_on='date', 
                             how='left',  fill_method='ffill')

# Subset the gdp and returns columns
gdp_returns = gdp_sp500[['gdp', 'returns']]

# Print gdp_returns correlation
print (gdp_returns.corr())
```

### [Phillips curve using merge_ordered()](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-ordered-and-time-series-data?ex=3)

```
# Use merge_ordered() to merge inflation, unemployment with inner join
inflation_unemploy = pd.merge_ordered(inflation, unemployment, on='date', how='inner')

# Print inflation_unemploy 
print(inflation_unemploy)

# Plot a scatter plot of unemployment_rate vs cpi of inflation_unemploy
inflation_unemploy.plot(x='unemployment_rate', y='cpi' , kind='scatter')
plt.show()
```

### [merge_ordered() caution, multiple columns](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-ordered-and-time-series-data?ex=4)

```
# Merge gdp and pop on date and country with fill and notice rows 2 and 3
ctry_date = pd.merge_ordered(gdp, pop, on=['date', 'country', ], 
                             fill_method='ffill')

# Print ctry_date
print(ctry_date)

#####################################################

# Merge gdp and pop on country and date with fill
date_ctry = pd.merge_ordered(gdp, pop, on=['country', 'date', ], fill_method='ffill')

# Print date_ctry
print(date_ctry)
```

### [Using merge_asof() to study stocks](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-ordered-and-time-series-data?ex=6)

```
# Use merge_asof() to merge jpm and wells
jpm_wells = pd.merge_asof(jpm, wells, on='date_time', suffixes=('', '_wells'), direction='nearest')


# Use merge_asof() to merge jpm_wells and bac
jpm_wells_bac = pd.merge_asof(jpm_wells, bac, on=['date_time'], suffixes=('_jpm', '_bac'), direction='nearest')


# Compute price diff
price_diffs = jpm_wells_bac.diff()

# Plot the price diff of the close of jpm, wells and bac only
price_diffs.plot(y=['close_jpm', 'close_wells', 'close_bac'])
plt.show()
```

### [Using merge_asof() to create dataset](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-ordered-and-time-series-data?ex=7)

```
# Merge gdp and recession on date using merge_asof()
gdp_recession = pd.merge_asof(gdp, recession, on='date')

# Create a list based on the row value of gdp_recession['econ_status']
is_recession = ['r' if s=='recession' else 'g' for s in gdp_recession['econ_status']]

# Plot a bar chart of gdp_recession
gdp_recession.plot(kind='bar', y='gdp', x='date', color=is_recession, rot=90)
plt.show()
```

### [Explore financials with .query()](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-ordered-and-time-series-data?ex=10)

```
Q: Use the .query() method and the IPython shell to explore social_fin and select the True statement.
A: There are 6 rows where the net income has a negative value.
```

### [Subsetting rows with .query()](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-ordered-and-time-series-data?ex=11)

```
# Merge gdp and pop on date and country with fill
gdp_pop = pd.merge_ordered(gdp, pop, on=['country','date'], fill_method='ffill')

#####################################################

# Merge gdp and pop on date and country with fill
gdp_pop = pd.merge_ordered(gdp, pop, on=['country','date'], fill_method='ffill')

# Add a column named gdp_per_capita to gdp_pop that divides the gdp by pop
gdp_pop['gdp_per_capita'] = gdp_pop['gdp'] / gdp_pop['pop']

#####################################################

# Merge gdp and pop on date and country with fill
gdp_pop = pd.merge_ordered(gdp, pop, on=['country','date'], fill_method='ffill')

# Add a column named gdp_per_capita to gdp_pop that divides the gdp by pop
gdp_pop['gdp_per_capita'] = gdp_pop['gdp'] / gdp_pop['pop']

# Pivot data so gdp_per_capita, where index is date and columns is country
gdp_pivot = gdp_pop.pivot_table('gdp_per_capita', 'date', 'country')

#####################################################

# Merge gdp and pop on date and country with fill
gdp_pop = pd.merge_ordered(gdp, pop, on=['country','date'], fill_method='ffill')

# Add a column named gdp_per_capita to gdp_pop that divides the gdp by pop
gdp_pop['gdp_per_capita'] = gdp_pop['gdp'] / gdp_pop['pop']

# Pivot data so gdp_per_capita, where index is date and columns is country
gdp_pivot = gdp_pop.pivot_table('gdp_per_capita', 'date', 'country')

# Select dates equal to or greater than 1991-01-01
recent_gdp_pop = gdp_pivot.query('date>="1991-01-01"')

# Plot recent_gdp_pop
recent_gdp_pop.plot(rot=90)
plt.show()
```

### [Select the right .melt() arguments](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-ordered-and-time-series-data?ex=13)

```
Q: You are given a table named inflation. Chose the option to get the same output as the table below.
A: inflation.melt(id_vars=['country','indicator'], var_name='year', value_name='annual')
```

### [Using .melt() to reshape government data](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-ordered-and-time-series-data?ex=14)

```
# unpivot everything besides the year column
ur_tall = ur_wide.melt(id_vars=['year'], var_name='month', value_name='unempl_rate')

# Create a date column using the month and year columns of ur_tall
ur_tall['date'] = pd.to_datetime(ur_tall['year'] + '-' + ur_tall['month'])

# Sort ur_tall by date in ascending order
ur_sorted = ur_tall.sort_values(by='date')

# Plot the unempl_rate by date
ur_sorted.plot(x='date', y='unempl_rate')
plt.show()
```

### [Using .melt() for stocks vs bond performance](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-ordered-and-time-series-data?ex=15)

```
# Use melt on ten_yr, unpivot everything besides the metric column
bond_perc = ten_yr.melt(id_vars=['metric'], var_name='date', value_name='close')

# Use query on bond_perc to select only the rows where metric=close
bond_perc_close = bond_perc.query('metric=="close"')

# Merge (ordered) dji and bond_perc_close on date with an inner join
dow_bond = pd.merge_ordered(dji, bond_perc_close, on='date', how='inner', suffixes=['_dow', '_bond'])


# Plot only the close_dow and close_bond columns
dow_bond.plot(y=['close_dow', 'close_bond'], x='date', rot=90)
plt.show()
```