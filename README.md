
# Custom Pseudorandom Number Generator (PRNG)

This project implements a custom Pseudorandom Number Generator (`PRNG`) and evaluates its quality through:
-  Histogram analysis for uniformity
-  Lag plot analysis for dependency

All plots are saved as ".png" files.

## Uniformity Plot

```python
def custom_prng(seed, a=1103515245, c=12345, m=2**31, size=1000):
    numbers = []
    x = seed
    for _ in range(size):
        x = (a * x + c) % m
        numbers.append(x / m)  # Normalize to [0, 1)
    return numbers
```

Interpretation:
If the PRNG is good, the histogram will be relatively flat — indicating a uniform distribution.


## Lag Plot (Dependency Check)

```python
import matplotlib.pyplot as plt
import seaborn as sns
from pandas.plotting import lag_plot

# Generate data
random_nums = custom_prng(seed=42, size=1000)

# Plot histogram
plt.figure(figsize=(10, 4))
sns.histplot(random_nums, bins=20, kde=True, color='skyblue')
plt.title("Uniformity Test: Histogram of PRNG Output")
plt.xlabel("Value")
plt.ylabel("Frequency")
plt.show()

# Dependency plot
plt.figure(figsize=(6, 6))
plt.scatter(random_nums[:-1], random_nums[1:], alpha=0.5)
plt.title("Dependency Test: x[i] vs x[i+1]")
plt.xlabel("x[i]")
plt.ylabel("x[i+1]")
plt.grid(True)
plt.show()
```

Interpretation:
A truly random PRNG will show no clear pattern or clustering.
If points form lines or shapes, the generator may be too predictable.

## Output Files

 "uniformity.png" → Shows distribution histogram, 
 "dependency.png" → Shows correlation between successive numbers

### How to Run:
1. Open a file in google colab
2. Copy paste the python code to the file
3. Run all cells
4. See the plots saved in the same directory
