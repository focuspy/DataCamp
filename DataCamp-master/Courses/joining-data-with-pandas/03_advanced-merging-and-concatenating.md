## [Advanced Merging and Concatenating](https://campus.datacamp.com/courses/joining-data-with-pandas/advanced-merging-and-concatenating) 

In this chapter, you’ll leverage powerful filtering techniques, including semi-joins and anti-joins. You’ll also learn how to glue DataFrames by vertically combining and using the pandas.concat function to create new datasets. Finally, because data is rarely clean, you’ll also learn how to validate your newly combined data structures. 

<br>

### [Steps of a semi join](https://campus.datacamp.com/courses/joining-data-with-pandas/advanced-merging-and-concatenating?ex=2)

```
Q: Sort the steps in the correct order of the technique shown to perform a semi join in pandas

A: 1. Merge the left and right tables on key column using a inner join.

2. Search if the key column in the left table is in the merged tables using the .isin() method creating a boolean series.

3. Subset the rows of the left table.
```

### [Performing an anti join](https://campus.datacamp.com/courses/joining-data-with-pandas/advanced-merging-and-concatenating?ex=3)

```
# Merge employees and top_cust
empl_cust = employees.merge(top_cust, on='srid', 
                            how='left', indicator=True)

#####################################################

# Merge employees and top_cust
empl_cust = employees.merge(top_cust, on='srid', 
                            how='left', indicator=True)

# Select the srid column where _merge is left_only
srid_list = empl_cust.loc[empl_cust['_merge']== 'left_only', 'srid']

#####################################################

# Merge employees and top_cust
empl_cust = employees.merge(top_cust, on='srid', 
                                 how='left', indicator=True)

# Select the srid column where _merge is left_only
srid_list = empl_cust.loc[empl_cust['_merge'] == 'left_only', 'srid']

# Get employees not working with top customers
print(employees[employees['srid'].isin(srid_list)])
```

### [Performing a semi join](https://campus.datacamp.com/courses/joining-data-with-pandas/advanced-merging-and-concatenating?ex=4)

```
# Merge the non_mus_tck and top_invoices tables on tid
tracks_invoices = non_mus_tcks.merge(top_invoices, on='tid', how='inner')

# Use .isin() to subset non_mus_tcks to rows with tid in tracks_invoices
top_tracks = non_mus_tcks[non_mus_tcks['tid'].isin(tracks_invoices['tid'])]

# Group the top_tracks by gid and count the tid rows
cnt_by_gid = top_tracks.groupby(['gid'], as_index=False).agg({'tid':'count'})

# Merge the genres table to cnt_by_gid on gid and print
print(cnt_by_gid.merge(genres, on='gid'))
```

### [Concatenation basics](https://campus.datacamp.com/courses/joining-data-with-pandas/advanced-merging-and-concatenating?ex=6)

```
# Concatenate the tracks
tracks_from_albums = pd.concat([tracks_master,tracks_ride,tracks_st],
                               sort=True)
print(tracks_from_albums)

#####################################################

# Concatenate the tracks so the index goes from 0 to n-1
tracks_from_albums = pd.concat([tracks_master,tracks_ride,tracks_st],
                                ignore_index=True,
                               sort=True)
print(tracks_from_albums)

#####################################################

# Concatenate the tracks, show only columns names that are in all tables
tracks_from_albums = pd.concat([tracks_master,tracks_ride,tracks_st],
                               join="inner",
                               sort=True)
print(tracks_from_albums)
```

### [Concatenating with keys](https://campus.datacamp.com/courses/joining-data-with-pandas/advanced-merging-and-concatenating?ex=7)

```
# Concatenate the tables and add keys
inv_jul_thr_sep = pd.concat([inv_jul,inv_aug,inv_sep], 
                            keys=['7Jul','8Aug','9Sep'])

# Group the invoices by the index keys and find avg of the total column
avg_inv_by_month = inv_jul_thr_sep.groupby(level=0).agg({'total':'mean'})

# Bar plot of avg_inv_by_month
avg_inv_by_month.plot(kind="bar")
plt.show()
```

### [Using the append method](https://campus.datacamp.com/courses/joining-data-with-pandas/advanced-merging-and-concatenating?ex=8)

```
# Use the .append() method to combine the tracks tables
metallica_tracks = tracks_ride.append([tracks_master, tracks_st], sort=False)

# Merge metallica_tracks and invoice_items
tracks_invoices = metallica_tracks.merge(invoice_items, on='tid')

# For each tid and name sum the quantity sold
tracks_sold = tracks_invoices.groupby(['tid','name']).agg({'quantity':'sum'})

# Sort in decending order by quantity and print the results
print(tracks_sold.sort_values(['quantity'], ascending=False))

```

### [Validating a merge](https://campus.datacamp.com/courses/joining-data-with-pandas/advanced-merging-and-concatenating?ex=10)

```
Q: Adjust the validate argument to answer which statement is False.
A: You can use 'many_to_one' without an error, since there is a duplicate key in the left table.
```

### [Concatenate and merge to find common songs](https://campus.datacamp.com/courses/joining-data-with-pandas/advanced-merging-and-concatenating?ex=11)

```
# Concatenate the classic tables vertically
classic_18_19 = pd.concat([classic_18, classic_19], ignore_index=True)

# Concatenate the pop tables vertically
pop_18_19 = pd.concat([pop_18, pop_19], ignore_index=True)

#####################################################

# Concatenate the classic tables vertically
classic_18_19 = pd.concat([classic_18, classic_19], ignore_index=True)

# Concatenate the pop tables vertically
pop_18_19 = pd.concat([pop_18, pop_19], ignore_index=True)

# Merge classic_18_19 with pop_18_19
classic_pop = classic_18_19.merge(pop_18_19, on='tid', how='inner')

# Using .isin(), filter classic_18_19 rows where tid is in classic_pop
popular_classic = classic_18_19[classic_18_19['tid'].isin(classic_pop['tid'])]

# Print popular chart
print(popular_classic)
```