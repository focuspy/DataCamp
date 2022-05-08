## Advanced data problems

In this chapter, you’ll dive into more advanced data cleaning problems, such as ensuring that weights are all written in kilograms instead of pounds. You’ll also gain invaluable skills that will help you verify that values have been added correctly and that missing values don’t negatively impact your analyses.

<br>

### [Ambiguous dates](https://campus.datacamp.com/courses/cleaning-data-in-python/advanced-data-problems-3?ex=2)

```
Q: What is the best way to unify the formats for ambiguous values such as 2019-04-07?
A: All of the above are possible, as long as we investigate where our data comes from, and understand the dynamics affecting it before cleaning it.
```

### [Uniform currencies](https://campus.datacamp.com/courses/cleaning-data-in-python/advanced-data-problems-3?ex=3)

```
# Find values of acct_cur that are equal to 'euro'
acct_eu = banking['acct_cur'] == 'euro'

# Convert acct_amount where it is in euro to dollars
banking.loc[acct_eu, 'acct_amount'] = banking.loc[acct_eu, 'acct_amount'] * 1.1 

# Unify acct_cur column by changing 'euro' values to 'dollar'
banking.loc[acct_eu, 'acct_cur'] = 'dollar'

# Assert that only dollar currency remains
assert banking['acct_cur'].unique() == 'dollar'
```

### [Uniform dates](https://campus.datacamp.com/courses/cleaning-data-in-python/advanced-data-problems-3?ex=4)

```
# Print the header of account_opend
print(banking['account_opened'].head())

#####################################################

Q: Why do you think that is?
A: The 21-14-17 entry is erroneous and leads to an error.

#####################################################

# Print the header of account_opened
print(banking['account_opened'].head())

# Convert account_opened to datetime
banking['account_opened'] = pd.to_datetime(banking['account_opened'],
                                           # Infer datetime format
                                           infer_datetime_format = True,
                                           # Return missing value for error
                                           errors = 'coerce') 

#####################################################

# Print the header of account_opend
print(banking['account_opened'].head())

# Convert account_opened to datetime
banking['account_opened'] = pd.to_datetime(banking['account_opened'],
                                           # Infer datetime format
                                           infer_datetime_format = True,
                                           # Return missing value for error
                                           errors = 'coerce') 

# Get year of account opened
banking['acct_year'] = banking['account_opened'].dt.strftime('%Y')

# Print acct_year
print(banking['acct_year'])
```

### [How's our data integrity?](https://campus.datacamp.com/courses/cleaning-data-in-python/advanced-data-problems-3?ex=7)

```
# Store fund columns to sum against
fund_columns = ['fund_A', 'fund_B', 'fund_C', 'fund_D']

# Find rows where fund_columns row sum == inv_amount
inv_equ = banking[fund_columns].sum(axis=1) == banking['inv_amount']

# Store consistent and inconsistent data
consistent_inv = banking[inv_equ]
inconsistent_inv = banking[~inv_equ]

# Store consistent and inconsistent data
print("Number of inconsistent investments: ", inconsistent_inv.shape[0])

#####################################################

# Store today's date and find ages
today = dt.date.today()
ages_manual = today.year - banking['birth_date'].dt.year

# Find rows where age column == ages_manual
age_equ = ages_manual == banking['age']

# Store consistent and inconsistent data
consistent_ages = banking[age_equ]
inconsistent_ages = banking[~age_equ]

# Store consistent and inconsistent data
print("Number of inconsistent ages: ", inconsistent_ages.shape[0])

```
### [Is this missing at random?](https://campus.datacamp.com/courses/cleaning-data-in-python/advanced-data-problems-3?ex=9)

```
Q: You have a DataFrame containing customer satisfaction scores for a service. What type of missingness is the following? 
A: Missing not at random.
```

### [Missing investors](https://campus.datacamp.com/courses/cleaning-data-in-python/advanced-data-problems-3?ex=10)

```
# Print number of missing values in banking
print(banking.isna().sum())

# Visualize missingness matrix
msno.matrix(banking)
plt.show()

#####################################################

# Print number of missing values in banking
print(banking.isna().sum())

# Visualize missingness matrix
msno.matrix(banking)
plt.show()

# Isolate missing and non missing values of inv_amount
missing_investors = banking[banking['inv_amount'].isna()]
investors = banking[~banking['inv_amount'].isna()]

#####################################################

Q: What do you think is going on?
A: The inv_amount is missing only for young customers, since the average age in missing_investors is 22 and the maximum age is 25.

#####################################################

# Print number of missing values in banking
print(banking.isna().sum())

# Visualize missingness matrix
msno.matrix(banking)
plt.show()

# Isolate missing and non missing values of inv_amount
missing_investors = banking[banking['inv_amount'].isna()]
investors = banking[~banking['inv_amount'].isna()]

# Sort banking by age and visualize
banking_sorted = banking.sort_values('age')
msno.matrix(banking_sorted)
plt.show()
```

### [Follow the money](https://campus.datacamp.com/courses/cleaning-data-in-python/advanced-data-problems-3?ex=11)

```
# Drop missing values of cust_id
banking_fullid = banking.dropna(subset = ['cust_id'])

# Compute estimated acct_amount
acct_imp = banking_fullid['inv_amount'] * 5

# Impute missing acct_amount with corresponding acct_imp
banking_imputed = banking_fullid.fillna({'acct_amount':acct_imp})

# Print number of missing values
print(banking_imputed.isna().sum())

```