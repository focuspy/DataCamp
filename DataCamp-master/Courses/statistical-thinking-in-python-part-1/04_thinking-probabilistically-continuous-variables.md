# [Thinking Probabilistically-- Continuous Variables](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-continuous-variables)

It’s time to move onto continuous variables, such as those that can take on any fractional value. Many of the principles are the same, but there are some subtleties. At the end of this final chapter, you will be speaking the probabilistic language you need to launch into the inference techniques covered in the sequel to this course.

<br>

### [Interpreting PDFs](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-continuous-variables?ex=2)

```
Q: Which of the following is true?
A: x is more likely to be less than 10 than to be greater than 10.
```

### [Interpreting CDFs](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-continuous-variables?ex=3)

```
Q: Using the CDF, what is the probability that x is greater than 10?
A: 0.25
```

### [The Normal PDF](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-continuous-variables?ex=5)

```
# Draw 100000 samples from Normal distribution with stds of interest: samples_std1, samples_std3, samples_std10
samples_std1 = np.random.normal(20, 1, size=100000)
samples_std3 = np.random.normal(20, 3, size=100000)
samples_std10 = np.random.normal(20, 10, size=100000)

# Make histograms
_ = plt.hist(samples_std1, bins=100, normed=True, histtype='step')
_ = plt.hist(samples_std3, bins=100,normed=True, histtype='step')
_ = plt.hist(samples_std10, bins=100,normed=True, histtype='step')

# Make a legend, set limits and show plot
_ = plt.legend(('std = 1', 'std = 3', 'std = 10'))
plt.ylim(-0.01, 0.42)
plt.show()
```

### [The Normal CDF](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-continuous-variables?ex=6)

```
# Generate CDFs
x_std1, y_std1 = ecdf(samples_std1)
x_std3, y_std3 = ecdf(samples_std3)
x_std10, y_std10 = ecdf(samples_std10)

# Plot CDFs
_ = plt.plot(x_std1, y_std1, marker='.', linestyle='none')
_ = plt.plot(x_std3, y_std3, marker='.', linestyle='none')
_ = plt.plot(x_std10, y_std10, marker='.', linestyle='none')


# Make a legend and show the plot
_ = plt.legend(('std = 1', 'std = 3', 'std = 10'), loc='lower right')
plt.show()
```

### [Gauss and the 10 Deutschmark banknote](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-continuous-variables?ex=8)

```
Q: What are the mean and standard deviation, respectively, of the Normal distribution that was on the 10 Deutschmark banknote, shown to the right?
A: mean = 3, std = 1
```

### [Are the Belmont Stakes results Normally distributed?](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-continuous-variables?ex=9)

```
# Compute mean and standard deviation: mu, sigma
mu = belmont_no_outliers.mean()
sigma = belmont_no_outliers.std()


# Sample out of a normal distribution with this mu and sigma: samples
samples = np.random.normal(mu, sigma, size = 10000)

# Get the CDF of the samples and of the data
x_theor, y_theor = ecdf(samples)
x, y = ecdf(belmont_no_outliers)

# Plot the CDFs and show the plot
_ = plt.plot(x_theor, y_theor)
_ = plt.plot(x, y, marker='.', linestyle='none')
_ = plt.xlabel('Belmont winning time (sec.)')
_ = plt.ylabel('CDF')
plt.show()
```

### [What are the chances of a horse matching or beating Secretariat's record?](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-continuous-variables?ex=10)

```
# Take a million samples out of the Normal distribution: samples
samples = np.random.normal(mu, sigma, size=1000000)

# Compute the fraction that are faster than 144 seconds: prob
prob = np.sum(samples <= 144)/len(samples)

# Print the result
print('Probability of besting Secretariat:', prob)
```

### [Matching a story and a distribution](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-continuous-variables?ex=12)

```
Q: How might we expect the time between Major League no-hitters to be distributed?
A: Exponential
```

### [Waiting for the next Secretariat](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-continuous-variables?ex=13)

```
Q: How is the waiting time until the next performance as good or better than Secretariat's distributed
A: Exponential: A horse as fast as Secretariat is a rare event, which can be modeled as a Poisson process, and the waiting time between arrivals of a Poisson process is Exponentially distributed.
```

### [If you have a story, you can simulate it!](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-continuous-variables?ex=14)

```
def successive_poisson(tau1, tau2, size=1):
    """Compute time for arrival of 2 successive Poisson processes."""
    # Draw samples out of first exponential distribution: t1
    t1 = np.random.exponential(tau1, size=size)

    # Draw samples out of second exponential distribution: t2
    t2 = np.random.exponential(tau2, size=size)

    return t1 + t2
```

### [Distribution of no-hitters and cycles](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-continuous-variables?ex=15)

```
# Draw samples of waiting times: waiting_times
waiting_times = successive_poisson(764, 715, 100000)

# Make the histogram
_ = plt.hist(waiting_times, bins=100, normed=True, histtype='step')

# Label axes
_ = plt.xlabel('Waiting times')
_ = plt.ylabel('Probability')

# Show the plot
plt.show()
```