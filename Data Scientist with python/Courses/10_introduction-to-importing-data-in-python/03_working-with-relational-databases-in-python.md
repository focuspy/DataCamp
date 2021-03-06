## Working with relational databases in Python

In this chapter, you'll learn how to extract meaningful data from relational databases, an essential skill for any data scientist. You will learn about relational models, how to create SQL queries, how to filter and order your SQL records, and how to perform advanced queries by joining database tables.

<br>

### [Pop quiz: The relational model](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/working-with-relational-databases-in-python-3?ex=2)

```Python
Q: Which of the following is not part of the relational model?
A: Each row or record in a table represents an instance of an entity type.
```

### [Creating a database engine](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/working-with-relational-databases-in-python-3?ex=4)

```Python
# Import necessary module
from sqlalchemy import create_engine

# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')
```

### [What are the tables in the database?](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/working-with-relational-databases-in-python-3?ex=5)

```Python
# Import necessary module
from sqlalchemy import create_engine

# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Save the table names to a list: table_names
table_names = engine.table_names()

# Print the table names to the shell
print(table_names)
```

### [The Hello World of SQL Queries!](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/working-with-relational-databases-in-python-3?ex=7)

```Python
# Import packages
from sqlalchemy import create_engine
import pandas as pd

# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Open engine connection: con
con = engine.connect()

# Perform query: rs
rs = con.execute('SELECT * FROM Album')

# Save results of the query to DataFrame: df
df = pd.DataFrame(rs)

# Close connection
con.close()

# Print head of DataFrame df
print(df.head())
```

### [Customizing the Hello World of SQL Queries](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/working-with-relational-databases-in-python-3?ex=8)

```Python
# Open engine in context manager
# Perform query and save results to DataFrame: df
with engine.connect() as con:
    rs = con.execute('SELECT lastname, title FROM employee')
    df = pd.DataFrame(rs.fetchmany(3))
    df.columns = rs.keys()

# Print the length of the DataFrame df
print(len(df))

# Print the head of the DataFrame df
print(df.head())
```

### [Filtering your database records using SQL's WHERE](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/working-with-relational-databases-in-python-3?ex=9)

```Python
# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Open engine in context manager
# Perform query and save results to DataFrame: df
with engine.connect() as con:
    rs = con.execute('SELECT * FROM employee WHERE employeeid >= 6')
    df = pd.DataFrame(rs.fetchall())
    df.columns = rs.keys()

# Print the head of the DataFrame df
print(df.head())
```

### [Ordering your SQL records with ORDER BY](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/working-with-relational-databases-in-python-3?ex=10)

```Python
# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Open engine in context manager
with engine.connect() as con:
    rs = con.execute('SELECT * FROM employee ORDER BY birthdate')
    df = pd.DataFrame(rs.fetchall())

    # Set the DataFrame's column names
    df.columns = rs.keys()

# Print head of DataFrame
print(df.head())

```

### [Pandas and The Hello World of SQL Queries!](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/working-with-relational-databases-in-python-3?ex=12)

```Python
# Import packages
from sqlalchemy import create_engine
import pandas as pd

# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Execute query and store records in DataFrame: df
df = pd.read_sql_query('SELECT * FROM album', engine)

# Print head of DataFrame
print(df.head())

# Open engine in context manager and store query result in df1
with engine.connect() as con:
    rs = con.execute("SELECT * FROM Album")
    df1 = pd.DataFrame(rs.fetchall())
    df1.columns = rs.keys()

# Confirm that both methods yield the same result
print(df.equals(df1))
```

### [Pandas for more complex querying](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/working-with-relational-databases-in-python-3?ex=13)

```Python
# Import packages
from sqlalchemy import create_engine
import pandas as pd

# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Execute query and store records in DataFrame: df
df = pd.read_sql_query('SELECT * FROM employee WHERE employeeid >= 6 ORDER BY birthdate', engine)

# Print head of DataFrame
print(df.head())
```

### [The power of SQL lies in relationships between tables: INNER JOIN](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/working-with-relational-databases-in-python-3?ex=15)

```Python
# Open engine in context manager
# Perform query and save results to DataFrame: df
with engine.connect() as con:
    rs = con.execute('SELECT title, name FROM album INNER JOIN artist WHERE album.artistid = artist.artistid')
    df = pd.DataFrame(rs.fetchall())
    df.columns = rs.keys()

# Print head of DataFrame df
print(df.head())
```

### [Filtering your INNER JOIN](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/working-with-relational-databases-in-python-3?ex=16)

```Python
# Execute query and store records in DataFrame: df
df = pd.read_sql_query('SELECT * FROM PlaylistTrack INNER JOIN Track on PlaylistTrack.TrackId = Track.TrackId WHERE Milliseconds < 250000', engine)

# Print head of DataFrame
print(df.head())
```