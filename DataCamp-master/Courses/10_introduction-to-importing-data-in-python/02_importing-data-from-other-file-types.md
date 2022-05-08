## Importing data from other file types

You've learned how to import flat files, but there are many other file types you will potentially have to work with as a data scientist. In this chapter, you'll learn how to import data into Python from a wide array of important file types. These include pickled files, Excel spreadsheets, SAS and Stata files, HDF5 files, a file type for storing large quantities of numerical data, and MATLAB files.

<br>

### [Not so flat any more](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=2)

```
Q: Check out the contents of your current directory and answer the following questions: (1) which file is in your directory and NOT an example of a flat file; (2) why is it not a flat file?
A: battledeath.xlsx is not a flat because it is a spreadsheet consisting of many sheets, not a single table.
```


### [Loading a pickled file](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=3)

```
# Import pickle package
import pickle

# Open pickle file and load data: d
with open('data.pkl', 'rb') as file:
    d = pickle.load(file)

# Print d
print(d)

# Print datatype of d
print(type(d))
```

### [Listing sheets in Excel files](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=4)

```
# Import pandas
import pandas as pd

# Assign spreadsheet filename: file
file = 'battledeath.xlsx'

# Load spreadsheet: xls
xls = pd.ExcelFile(file)

# Print sheet names
print(xls.sheet_names)
```

### [Importing sheets from Excel files](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=5)

```
# Load a sheet into a DataFrame by name: df1
df1 = xls.parse('2004')

# Print the head of the DataFrame df1
print(df1.head())

# Load a sheet into a DataFrame by index: df2
df2 = xls.parse(0)

# Print the head of the DataFrame df2
print(df2.head())
```

### [Customizing your spreadsheet import](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=6)

```
# Parse the first sheet and rename the columns: df1
df1 = xls.parse('2002', skiprows=1, names=['Country','AAM due to War (2002)'])

# Print the head of the DataFrame df1
print(df1.head())

# Parse the first column of the second sheet and rename the column: df2
df2 = xls.parse(1, usecols=[0], skiprows=1, names=['Country'])

# Print the head of the DataFrame df2
print(df2.head())
```

### [How to import SAS7BDAT](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=8)

```
Q: How do you correctly import the function SAS7BDAT() from the package sas7bdat?
A: import SAS7BDAT from sas7bdat
```

### [Importing SAS files](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=9)

```
# Import sas7bdat package
from sas7bdat import SAS7BDAT

# Save file to a DataFrame: df_sas
with SAS7BDAT('sales.sas7bdat') as file:
    df_sas = file.to_data_frame()

# Print head of DataFrame
print(df_sas.head())

# Plot histogram of DataFrame features (pandas and pyplot already imported)
pd.DataFrame.hist(df_sas[['P']])
plt.ylabel('count')
plt.show()
```

### [Using read_stata to import Stata files](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=10)

```
Q: What is the correct way of using the read_stata() function to import disarea.dta into the object df?
A: df = pd.read_stata('disarea.dta')
```

### [Importing Stata files](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=11)

```
# Import pandas
import pandas as pd

# Load Stata file into a pandas DataFrame: df
df = pd.read_stata('disarea.dta')

# Print the head of the DataFrame df
print(df.head())

# Plot histogram of one column of the DataFrame
pd.DataFrame.hist(df[['disa10']])
plt.xlabel('Extent of disease')
plt.ylabel('Number of countries')
plt.show()
```

### [Using h5py to import HDF5 files](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=13)

```
# Import packages
import numpy as np
import h5py

# Assign filename: file
file = 'LIGO_data.hdf5'

# Load file: data
data = h5py.File(file, 'r')

# Print the datatype of the loaded file
print(type(data))

# Print the keys of the file
for key in data.keys():
    print(key)
```

### [Extracting data from your HDF5 file](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=15)

```
# Get the HDF5 group: group
group = data['strain']

# Check out keys of group
for key in group.keys():
    print(key)

# Set variable equal to time series data: strain
strain = data['strain']['Strain'].value

# Set number of time points to sample: num_samples
num_samples = 10000

# Set time vector
time = np.arange(0, 1, 1/num_samples)

# Plot data
plt.plot(time, strain[:num_samples])
plt.xlabel('GPS Time (s)')
plt.ylabel('strain')
plt.show()
```

### [Loading .mat files](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=17)

```
# Import package
import scipy.io

# Load MATLAB file: mat
mat = scipy.io.loadmat('albeck_gene_expression.mat')

# Print the datatype type of mat
print(type(mat))
```

### [The structure of .mat in Python](https://campus.datacamp.com/courses/introduction-to-importing-data-in-python/importing-data-from-other-file-types-2?ex=18)

```
# Print the keys of the MATLAB dictionary
print(mat.keys())

# Print the type of the value corresponding to the key 'CYratioCyt'
print(type(mat['CYratioCyt']))

# Print the shape of the value corresponding to the key 'CYratioCyt'
print(np.shape(mat['CYratioCyt']))

# Subset the array and plot it
data = mat['CYratioCyt'][25, 5:]
fig = plt.figure()
plt.plot(data)
plt.xlabel('time (min.)')
plt.ylabel('normalized fluorescence (measure of expression)')
plt.show()
```