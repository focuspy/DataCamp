## [Merging Tables With Different Join Types](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-tables-with-different-join-types?ex=2)

Take your knowledge of joins to the next level. In this chapter, you’ll work with TMDb movie data as you learn about left, right, and outer joins. You’ll also discover how to merge a table to itself and merge on a DataFrame index.

<br>

### [Counting missing rows with left join](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-tables-with-different-join-types?ex=2)

```Python
Q: What column is likely the best column to merge the two tables on?
A: on='id'

#####################################################

# Merge movies and financials with a left join
movies_financials = movies.merge(financials, on = 'id', how= 'left')

#####################################################

# Merge the movies table with the financials table with a left join
movies_financials = movies.merge(financials, on='id', how='left')

# Count the number of rows in the budget column that are missing
number_of_missing_fin = movies_financials['budget'].isnull().sum()

# Print the number of movies missing financials
print(number_of_missing_fin)
```

### [Enriching a dataset](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-tables-with-different-join-types?ex=3)

```Python
# Merge the toy_story and taglines tables with a left join
toystory_tag = toy_story.merge(taglines, on='id', how='left')

# Print the rows and shape of toystory_tag
print(toystory_tag)
print(toystory_tag.shape)

#####################################################

# Merge the toy_story and taglines tables with a inner join
toystory_tag = toy_story.merge(taglines, on='id')

# Print the rows and shape of toystory_tag
print(toystory_tag)
print(toystory_tag.shape)
```

### [How many rows with a left join?](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-tables-with-different-join-types?ex=4)

```Python
Q: Select the true statement about left joins. 
A: The output of a one-to-many merge with a left join will have greater than or equal rows than the left table.
```

### [Right join to find unique movies](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-tables-with-different-join-types?ex=6)

```Python
# Merge action_movies to scifi_movies with right join
action_scifi = action_movies.merge(scifi_movies, how='right', on='movie_id')

#####################################################

# Merge action_movies to scifi_movies with right join
action_scifi = action_movies.merge(scifi_movies, how='right',on='movie_id', suffixes=['_act', '_sci'])

# Print the first few rows of action_scifi to see the structure
print(action_scifi.head())

#####################################################

# Merge action_movies to the scifi_movies with right join
action_scifi = action_movies.merge(scifi_movies, on='movie_id', how='right',
                                   suffixes=('_act','_sci'))

# From action_scifi, select only the rows where the genre_act column is null
scifi_only = action_scifi[action_scifi['genre_act'].isnull()]

#####################################################

# Merge action_movies to the scifi_movies with right join
action_scifi = action_movies.merge(scifi_movies, on='movie_id', how='right',
                                   suffixes=('_act','_sci'))

# From action_scifi, select only the rows where the genre_act column is null
scifi_only = action_scifi[action_scifi['genre_act'].isnull()]

# Merge the movies and scifi_only tables with an inner join
movies_and_scifi_only = movies.merge(scifi_only, how='right', left_on='id', right_on='movie_id')

# Print the first few rows and shape of movies_and_scifi_only
print(movies_and_scifi_only.head())
print(movies_and_scifi_only.shape)
```

### [Popular genres with right join](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-tables-with-different-join-types?ex=7)

```Python
# Use right join to merge the movie_to_genres and pop_movies tables
genres_movies = movie_to_genres.merge(pop_movies, how='right', 
                                      left_on='movie_id', 
                                      right_on='id')

# Count the number of genres
genre_count = genres_movies.groupby('genre').agg({'id':'count'})

# Plot a bar chart of the genre_count
genre_count.plot(kind='bar')
plt.show()
```

### [Using outer join to select actors](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-tables-with-different-join-types?ex=8)

```Python
# Merge iron_1_actors to iron_2_actors on id with outer join using suffixes
iron_1_and_2 = iron_1_actors.merge(iron_2_actors,
on='id',
how='outer',
suffixes=('_1','_2'))

# Create an index that returns true if name_1 or name_2 are null
m = ((iron_1_and_2['name_1'].isnull()) |
(iron_1_and_2['name_2'].isnull()))

# Print the first few rows of iron_1_and_2
print(iron_1_and_2[m].head())
```

### [Self join](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-tables-with-different-join-types?ex=10)

```Python
# Merge the crews table to itself
crews_self_merged = crews.merge(crews, on='id', suffixes=('_dir','_crew'))

#####################################################

# Merge the crews table to itself
crews_self_merged = crews.merge(crews, on='id', how='inner',
                                suffixes=('_dir','_crew'))

# Create a Boolean index to select the appropriate
boolean_filter = ((crews_self_merged['job_dir'] == 'Director') & 
     (crews_self_merged['job_crew'] != 'Director'))
direct_crews = crews_self_merged[boolean_filter]

#####################################################

# Merge the crews table to itself
crews_self_merged = crews.merge(crews, on='id', how='inner',
                                suffixes=('_dir','_crew'))

# Create a boolean index to select the appropriate rows
boolean_filter = ((crews_self_merged['job_dir'] == 'Director') & 
                  (crews_self_merged['job_crew'] != 'Director'))
direct_crews = crews_self_merged[boolean_filter]

# Print the first few rows of direct_crews
print(direct_crews.head())
```

### [How does pandas handle self joins?](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-tables-with-different-join-types?ex=11)

```Python
Q:Select the false statement about merging a table to itself.
A:The pandas module limits you to one merge where you merge a table to itself. You cannot repeat this process over and over.
```

### [Index merge for movie ratings](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-tables-with-different-join-types?ex=13)

```Python
# Merge to the movies table the ratings table on the index
movies_ratings = movies.merge(ratings,on="id", how="left")

# Print the first few rows of movies_ratings
print(movies_ratings.head())
```

### [Do sequels earn more?](https://campus.datacamp.com/courses/joining-data-with-pandas/merging-tables-with-different-join-types?ex=14)

```Python
# Merge sequels and financials on index id
sequels_fin = sequels.merge(financials, on='id', how='left')

#####################################################

# Merge sequels and financials on index id
sequels_fin = sequels.merge(financials, on='id', how='left')

# Self merge with suffixes as inner join with left on sequel and right on id
orig_seq = sequels_fin.merge(sequels_fin, how='inner', left_on='sequel', 
                             right_on='id', right_index=True,
                             suffixes=('_org','_seq'))

# Add calculation to subtract revenue_org from revenue_seq 
orig_seq['diff'] = orig_seq['revenue_seq'] - orig_seq['revenue_org']

#####################################################

# Merge sequels and financials on index id
sequels_fin = sequels.merge(financials, on='id', how='left')

# Self merge with suffixes as inner join with left on sequel and right on id
orig_seq = sequels_fin.merge(sequels_fin, how='inner', left_on='sequel', 
                             right_on='id', right_index=True,
                             suffixes=('_org','_seq'))

# Add calculation to subtract revenue_org from revenue_seq 
orig_seq['diff'] = orig_seq['revenue_seq'] - orig_seq['revenue_org']

# Select the title_org, title_seq, and diff 
titles_diff = orig_seq[['title_org','title_seq','diff']]

#####################################################

# Merge sequels and financials on index id
sequels_fin = sequels.merge(financials, on='id', how='left')

# Self merge with suffixes as inner join with left on sequel and right on id
orig_seq = sequels_fin.merge(sequels_fin, how='inner', left_on='sequel', 
                             right_on='id', right_index=True,
                             suffixes=('_org','_seq'))

# Add calculation to subtract revenue_org from revenue_seq 
orig_seq['diff'] = orig_seq['revenue_seq'] - orig_seq['revenue_org']

# Select the title_org, title_seq, and diff 
titles_diff = orig_seq[['title_org','title_seq','diff']]

# Print the first rows of the sorted titles_diff
print(titles_diff.sort_values('diff', ascending=False).head())