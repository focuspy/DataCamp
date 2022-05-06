## [Hypothesis test examples](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-2/hypothesis-test-examples?ex=2)

As you saw from the last chapter, hypothesis testing can be a bit tricky. You need to define the null hypothesis, figure out how to simulate it, and define clearly what it means to be "more extreme" in order to compute the p-value. Like any skill, practice makes perfect, and this chapter gives you some good practice with hypothesis tests.

<br>

### [The vote for the Civil Rights Act in 1964](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-2/hypothesis-test-examples?ex=2)

```
# Construct arrays of data: dems, reps
dems = np.array([True] * 153 + [False] * 91)
reps = np.array([True] * 136 + [False] * 35)

def frac_yea_dems(dems, reps):
    """Compute fraction of Democrat yea votes."""
    frac = np.sum(dems) / len(dems)
    return frac

# Acquire permutation samples: perm_replicates
perm_replicates = draw_perm_reps(dems, reps, frac_yea_dems, 10000)

# Compute and print p-value: p
p = np.sum(perm_replicates <= 153/244) / len(perm_replicates)
print('p-value =', p)
```

### [What is equivalent?](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-2/hypothesis-test-examples?ex=3)

```
Q: Which of the following situations involving testing by a web-based company has an equivalent set up for an A/B test as the one you just did with the Civil Rights Act of 1964?
A: You measure the number of people who click on an ad on your company's website before and after changing its color.
```

### [A time-on-website analog](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-2/hypothesis-test-examples?ex=4)

```
# Compute the observed difference in mean inter-no-hitter times: nht_diff_obs
nht_diff_obs = diff_of_means(nht_dead, nht_live)

# Acquire 10,000 permutation replicates of difference in mean no-hitter time: perm_replicates
perm_replicates = draw_perm_reps(nht_dead, nht_live,
                                 diff_of_means, size=10000)

# Compute and print the p-value: p
p = np.sum(perm_replicates <= nht_diff_obs) / len(perm_replicates)
print('p-val =',p)
```

### [What should you have done first?](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-2/hypothesis-test-examples?ex=5)

```
Q: But what should you have done with the data first?
A: Performed EDA, perhaps plotting the ECDFs of inter-no-hitter times in the dead ball and live ball eras.
```

### [Simulating a null hypothesis concerning correlation](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-2/hypothesis-test-examples?ex=7)

```
Q: To do the test, you need to simulate the data assuming the null hypothesis is true. Of the following choices, which is the best way to do it?
A: Do a permutation test: Permute the illiteracy values but leave the fertility values fixed to generate a new set of (illiteracy, fertility) data.
```

### [Hypothesis test on Pearson correlation](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-2/hypothesis-test-examples?ex=8)

```
# Compute observed correlation: r_obs
r_obs = pearson_r(illiteracy, fertility)

# Initialize permutation replicates: perm_replicates
perm_replicates = np.empty(10000)

# Draw replicates
for i in range(10000):
    # Permute illiteracy measurments: illiteracy_permuted
    illiteracy_permuted = np.random.permutation(illiteracy)

    # Compute Pearson correlation
    perm_replicates[i] = pearson_r(illiteracy_permuted, fertility)

# Compute p-value: p
p = np.sum(perm_replicates >= r_obs) / len(perm_replicates)
print('p-val =', p)
```

### [Do neonicotinoid insecticides have unintended consequences?](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-2/hypothesis-test-examples?ex=9)

```
# Compute x,y values for ECDFs
x_control, y_control = ecdf(control)
x_treated, y_treated = ecdf(treated)

# Plot the ECDFs
plt.plot(x_control, y_control, marker='.', linestyle='none')
plt.plot(x_treated, y_treated, marker='.', linestyle='none')

# Set the margins
plt.margins(0.02)

# Add a legend
plt.legend(('control', 'treated'), loc='lower right')

# Label axes and show plot
plt.xlabel('millions of alive sperm per mL')
plt.ylabel('ECDF')
plt.show()
```

### [Bootstrap hypothesis test on bee sperm counts](https://campus.datacamp.com/courses/statistical-thinking-in-python-part-2/hypothesis-test-examples?ex=10)

```
# Compute the difference in mean sperm count: diff_means
diff_means = np.mean(control) - np.mean(treated)

# Compute mean of pooled data: mean_count
mean_count = np.mean(np.concatenate((control, treated)))

# Generate shifted data sets
control_shifted = control - np.mean(control) + mean_count
treated_shifted = treated - np.mean(treated) + mean_count

# Generate bootstrap replicates
bs_reps_control = draw_bs_reps(control_shifted,
                               np.mean, size=10000)
bs_reps_treated = draw_bs_reps(treated_shifted,
                               np.mean, size=10000)

# Get replicates of difference of means: bs_replicates
bs_replicates = bs_reps_control - bs_reps_treated

# Compute and print p-value: p
p = np.sum(bs_replicates >= np.mean(control) - np.mean(treated)) \
            / len(bs_replicates)
print('p-value =', p)
```