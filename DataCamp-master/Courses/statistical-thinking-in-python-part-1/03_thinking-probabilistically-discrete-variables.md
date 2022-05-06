# Thinking Probabilistically-- Discrete Variables

Statistical inference rests upon probability. Because we can very rarely say anything meaningful with absolute certainty from data, we use probabilistic language to make quantitative statements about data. In this chapter, you will learn how to think probabilistically about discrete quantities: those that can only take certain values, like integers.

<br>

### [What is the goal of statistical inference?](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-discrete-variables?ex=2)

```
Q: Why do we do statistical inference?
A: All of these.
```

### [Why do we use the language of probability?](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-discrete-variables?ex=3)

```
Q: Which of the following is not a reason why we use probabilistic language in statistical inference?
A: Probabilistic language is not very precise.
```

### [Generating random numbers using the np.random module](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-discrete-variables?ex=5)

```
# Seed the random number generator
np.random.seed(42)

# Initialize random numbers: random_numbers
random_numbers = np.empty(100000)
# Generate random numbers by looping over range(100000)
for i in range(100000):
    random_numbers[i] = np.random.random()

# Plot a histogram
_ = plt.hist(random_numbers)

# Show the plot
plt.show()
```

### [The np.random module and Bernoulli trials](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-discrete-variables?ex=6)

```
def perform_bernoulli_trials(n, p):
    """Perform n Bernoulli trials with success probability p
    and return number of successes."""
    # Initialize number of successes: n_success
    n_success = 0

    # Perform trials
    for i in range(n):
        # Choose random number between zero and one: random_number
        random_number = np.random.random()

        # If less than p, it's a success so add one to n_success
        if random_number < p:
            n_success += 1

    return n_success
```

### [How many defaults might we expect?](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-discrete-variables?ex=7)

```
# Seed random number generator
np.random.seed(42)

# Initialize the number of defaults: n_defaults
n_defaults = np.empty(1000)

# Compute the number of defaults
for i in range(1000):
    n_defaults[i] = perform_bernoulli_trials(100, 0.05)


# Plot the histogram with default number of bins; label your axes
_ = plt.hist(n_defaults, normed=True)
_ = plt.xlabel('number of defaults out of 100 loans')
_ = plt.ylabel('probability')

# Show the plot
plt.show()
```

### [Will the bank fail?](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-discrete-variables?ex=8)

```
# Compute ECDF: x, y
x, y = ecdf(n_defaults)

# Plot the ECDF with labeled axes
plt.plot(x, y, marker='.', linestyle='none')
plt.xlabel('Number of Defaults out of 100')
plt.ylabel('CDF')

# Show the plot
plt.show()

# Compute the number of 100-loan simulations with 10 or more defaults: n_lose_money
n_lose_money = sum(n_defaults >= 10)

# Compute and print probability of losing money
print('Probability of losing money =', n_lose_money / len(n_defaults))
```

### [Sampling out of the Binomial distribution](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-discrete-variables?ex=10)

```
# Take 10,000 samples out of the binomial distribution: n_defaults
n_defaults = np.random.binomial(n=100, p=0.05, size=10000)

# Compute CDF: x, y
x, y = ecdf(n_defaults)

# Plot the CDF with axis labels
_ = plt.plot(x,y, marker = '.', linestyle = 'none')
_ = plt.xlabel('x')
_ = plt.ylabel('y')

# Show the plot
plt.show()
```

### [Plotting the Binomial PMF](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-discrete-variables?ex=11)

```
# Compute bin edges: bins
bins = np.arange(0, max(n_defaults) + 1.5) - 0.5

# Generate histogram
_ = plt.hist(n_defaults, normed=True, bins=bins)

# Label axes
_ = plt.xlabel('x')
_ = plt.ylabel('y')

# Show the plot
plt.show()
```

### [Relationship between Binomial and Poisson distributions](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-discrete-variables?ex=13)

```
# Draw 10,000 samples out of Poisson distribution: samples_poisson
samples_poisson = np.random.poisson(10, size=10000)

# Print the mean and standard deviation
print('Poisson:     ', np.mean(samples_poisson),
                       np.std(samples_poisson))

# Specify values of n and p to consider for Binomial: n, p
n = [20, 100, 1000]
p = [0.5, 0.1, 0.01]


# Draw 10,000 samples for each n,p pair: samples_binomial
for i in range(3):
    samples_binomial = np.random.binomial(n[i], p[i], size=10000)

    # Print results
    print('n =', n[i], 'Binom:', np.mean(samples_binomial),
                                 np.std(samples_binomial))
```

### [How many no-hitters in a season?](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-discrete-variables?ex=14)

```
Q: Which probability distribution would be appropriate to describe the number of no-hitters we would expect in a given season?
A: Both Binomial and Poisson, though Poisson is easier to model and compute.
```

### [Was 2015 anomalous?](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-1/thinking-probabilistically-discrete-variables?ex=15)

```
# Draw 10,000 samples out of Poisson distribution: n_nohitters
n_nohitters = np.random.poisson(251/115, size=10000)

# Compute number of samples that are seven or greater: n_large
n_large = np.sum(n_nohitters >= 7)

# Compute probability of getting seven or more: p_large
p_large = n_large / 10000

# Print the result
print('Probability of seven or more no-hitters:', p_large)
```