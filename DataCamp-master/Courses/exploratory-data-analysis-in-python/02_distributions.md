## [Distributions](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/distributions)

In the first chapter, having cleaned and validated your data, you began exploring it by using histograms to visualize distributions. In this chapter, you'll learn how to represent distributions using Probability Mass Functions (PMFs) and Cumulative Distribution Functions (CDFs). You'll learn when to use each of them, and why, while working with a new dataset obtained from the General Social Survey.

<br>

### [Make a PMF](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/distributions?ex=2)

```
# Compute the PMF for year
pmf_year = Pmf(gss['year'], normalize=False)

# Print the result
print(pmf_year)

#####################################################

Q: How many respondents were interviewed in 2016?
A: 2867
```

### [Plot a PMF](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/distributions?ex=3)

```
# Select the age column
age = gss['age']

#####################################################

# Select the age column
age = gss['age']

# Make a PMF of age
pmf_age = Pmf(age)

#####################################################

# Select the age column
age = gss['age']

# Make a PMF of age
pmf_age = Pmf(age)

# Plot the PMF
pmf_age.bar()

# Label the axes
plt.xlabel('Age')
plt.ylabel('PMF')
plt.show()
```

### [Make a CDF](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/distributions?ex=5)

```
# Select the age column
age = gss['age']

#####################################################

# Select the age column
age = gss['age']

# Compute the CDF of age
cdf_age = Cdf(age)

#####################################################

# Select the age column
age = gss['age']

# Compute the CDF of age
cdf_age = Cdf(age)

# Calculate the CDF of 30
print(cdf_age(30))

#####################################################

Q: What fraction of the respondents in the GSS dataset are OLDER than 30?
A: Approximately 75%
```

### [Compute IQR](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/distributions?ex=6)

```
# Calculate the 75th percentile 
percentile_75th = cdf_income.inverse(0.75)

#####################################################

# Calculate the 75th percentile 
percentile_75th = cdf_income.inverse(0.75)

# Calculate the 25th percentile
percentile_25th = cdf_income.inverse(0.25)

#####################################################

# Calculate the 75th percentile 
percentile_75th = cdf_income.inverse(0.75)

# Calculate the 25th percentile
percentile_25th = cdf_income.inverse(0.25)

# Calculate the interquartile range
iqr = percentile_75th - percentile_25th

# Print the interquartile range
print(iqr)

#####################################################

Q: What is the interquartile range (IQR) of income in the GSS dataset?
A: Approximately 29676
```

### [Plot a CDF](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/distributions?ex=7)

```
# Select realinc
income = gss['realinc']

# Make the CDF
cdf_income = Cdf(income)

# Plot it
cdf_income.plot()

# Label the axes
plt.xlabel('Income (1986 USD)')
plt.ylabel('CDF')
plt.show()
```

### [Distribution of education](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/distributions?ex=9)

```
Q: What fraction of respondents report that they have 12 years of education or fewer?
A: Approximately 53%
```

### [Extract education levels](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/distributions?ex=10)

```
# Select educ
educ = gss['educ']

# Bachelor's degree
bach = (educ >= 16)

# Associate degree
assc = (educ >= 14) & (educ < 16)

# High school (12 or fewer years of education)
high = (educ <= 12)
print(high.mean())
```

### [Plot income CDFs](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/distributions?ex=11)

```
income = gss['realinc']

# Plot the CDFs
Cdf(income[high]).plot(label='High school')
Cdf(income[assc]).plot(label='Associate')
Cdf(income[bach]).plot(label='Bachelor')

# Label the axes
plt.xlabel('Income (1986 USD)')
plt.ylabel('CDF')
plt.legend()
plt.show()
```

### [Distribution of income](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/distributions?ex=13)

```
# Extract realinc and compute its log
income = gss['realinc']
log_income = np.log10(income)

# Compute mean and standard deviation
mean = log_income.mean()
std = log_income.std()
print(mean, std)

# Make a norm object
from scipy.stats import norm
dist = norm(mean,std)
```

### [Comparing CDFs](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/distributions?ex=14)

```
# Evaluate the model CDF
xs = np.linspace(2, 5.5)
ys = dist.cdf(xs)

# Plot the model CDF
plt.clf()
plt.plot(xs, ys, color='gray')

# Create and plot the Cdf of log_income
Cdf(log_income).plot()
    
# Label the axes
plt.xlabel('log10 of realinc')
plt.ylabel('CDF')
plt.show()
```

### [Comparing PDFs](https://campus.datacamp.com/courses/exploratory-data-analysis-in-python/distributions?ex=15)

```
# Evaluate the normal PDF
xs = np.linspace(2, 5.5)
ys = dist.pdf(xs)

# Plot the model PDF
plt.clf()
plt.plot(xs, ys, color='gray')

# Plot the data KDE
sns.kdeplot(log_income)

# Label the axes
plt.xlabel('log10 of realinc')
plt.ylabel('PDF')
plt.show()
```