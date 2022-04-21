## Hypothesis test examples

As you saw from the last chapter, hypothesis testing can be a bit tricky. You need to define the null hypothesis, figure out how to simulate it, and define clearly what it means to be "more extreme" in order to compute the p-value. Like any skill, practice makes perfect, and this chapter gives you some good practice with hypothesis tests.

<br>

### The vote for the Civil Rights Act in 1964

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


### A time-on-website analog

```

# Compute the observed difference in mean inter-no-hitter times: nht_diff_obs
nht_diff_obs = ____

# Acquire 10,000 permutation replicates of difference in mean no-hitter time: perm_replicates
perm_replicates = ____


# Compute and print the p-value: p
p = ____
print('p-val =', p)
```
