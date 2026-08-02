# Measure of Dispersion

1. Variance
2. Standard Deviation

---

## 1. Variance

| Measure      | Population Formula                                | Sample Formula                                     |
| ------------ | ------------------------------------------------- | -------------------------------------------------- |
| **Variance** | $\sigma^2 = \dfrac{\sum_{i=1}^{N}(x_i-\mu)^2}{N}$ | $s^2 = \dfrac{\sum_{i=1}^{n}(x_i-\bar{x})^2}{n-1}$ |

### Symbols

| Symbol     | Meaning                 |
| ---------- | ----------------------- |
| $\sigma^2$ | Population variance     |
| $s^2$      | Sample variance         |
| $x_i$      | Individual observation  |
| $\mu$      | Population mean         |
| $\bar{x}$  | Sample mean             |
| $N$        | Population size         |
| $n$        | Sample size             |
| $\sum$     | Sum of all observations |

### Notes

- **Population Variance ($\sigma^2$)** divides by **$N$** because it includes every observation in the population.
- **Sample Variance ($s^2$)** divides by **$n-1$** instead of **$n$**. This is called **Bessel's correction**, which provides an unbiased estimate of the population variance.
- Variance measures how far the data points are spread from the mean. A larger variance indicates greater dispersion.

---

# Example: Variance Calculation

## Population Variance

Given data:

$$
2,\;4,\;6,\;8,\;10
$$

### Step 1: Find the Mean

$$
\begin{aligned}
\mu &= \frac{2+4+6+8+10}{5} \\
    &= \frac{30}{5} \\
    &= 6
\end{aligned}
$$

### Step 2: Find Squared Deviations

|   $x_i$   | $x_i-\mu$ | $(x_i-\mu)^2$ |
| :-------: | :-------: | :-----------: |
|     2     |    -4     |      16       |
|     4     |    -2     |       4       |
|     6     |     0     |       0       |
|     8     |     2     |       4       |
|    10     |     4     |      16       |
| **Total** |           |    **40**     |

### Step 3: Apply the Formula

$$
\begin{aligned}
\sigma^2
    &= \frac{\sum_{i=1}^{N}(x_i-\mu)^2}{N} \\
    &= \frac{40}{5} \\
    &= 8
\end{aligned}
$$

> **Population Variance:** $\boxed{\sigma^2 = 8}$

---

## Sample Variance

Using the same data as a sample.

### Step 1: Find the Mean

$$
\bar{x}=6
$$

### Step 2: Apply the Formula

$$
\begin{aligned}
s^2
    &= \frac{\sum_{i=1}^{n}(x_i-\bar{x})^2}{n-1} \\
    &= \frac{40}{5-1} \\
    &= \frac{40}{4} \\
    &= 10
\end{aligned}
$$

> **Sample Variance:** $\boxed{s^2 = 10}$

---

Variance is needed because **the mean alone does not tell us how the data is spread out**. It measures **dispersion**, i.e., how far the data values are from the mean.

### Example 1: Same Mean, Different Variance

Consider two datasets:

| Dataset A     | Dataset B      |
| ------------- | -------------- |
| 4, 5, 6, 7, 8 | 1, 3, 6, 9, 11 |

Both have the same mean:

$$
\mu = \frac{30}{5}=6
$$

However:

- **Dataset A** is tightly clustered around 6.
- **Dataset B** is spread much farther from 6.

Variance tells us this difference.

---

### Visual Representation

```
Dataset A
4   5   6   7   8
        ↑
      Mean = 6
Small spread → Low Variance

Dataset B
1     3     6     9     11
            ↑
          Mean = 6
Large spread → High Variance
```

---

### Why don't we just use the Mean?

Suppose two classes take an exam.

| Class A            | Class B              |
| ------------------ | -------------------- |
| 78, 79, 80, 81, 82 | 40, 60, 80, 100, 120 |

Both have:

$$
\text{Mean} = 80
$$

But:

- **Class A:** Students performed similarly.
- **Class B:** Scores vary dramatically.

Without variance, both classes appear identical.

---

### Why do we square the deviations?

If we simply added the differences from the mean:

$$
-2 + (-1) + 0 + 1 + 2 = 0
$$

Positive and negative values cancel each other.

So we square them:

$$
(-2)^2 + (-1)^2 + 0^2 + 1^2 + 2^2
=4+1+0+1+4
=10
$$

Squaring ensures:

- Every deviation is positive.
- Larger deviations have a greater impact.
- The result accurately reflects the spread of the data.

---

### Real-World Uses of Variance

- 📊 **Statistics:** Measure how consistent data is.
- 💰 **Finance:** Assess investment risk (higher variance = higher risk).
- 🤖 **Machine Learning:** Evaluate model performance and feature distributions.
- 🏭 **Manufacturing:** Monitor product quality and consistency.
- 🌦️ **Weather:** Analyze variability in temperature or rainfall.

---

### Key Takeaway

> **Mean tells you where the center of the data is.**
> **Variance tells you how far the data is spread around that center.**

A dataset is fully described by both its **center (mean)** and its **spread (variance)**. Without variance, two datasets with the same mean can look completely different.
