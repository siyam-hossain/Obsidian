# Why Sample Variance is Divided by (n-1)

The reason we divide by **(n-1)** instead of **(n)** is called **Bessel's Correction**. It gives a more accurate estimate of the **population variance** when we only have a **sample**.

---

## Intuition

Suppose a teacher wants to know the average height of **1,000 students**.

- Measuring all 1,000 students is expensive, so the teacher measures only **5 students**.

- Those 5 students are a **sample**.

Since the sample is only part of the population, the sample mean is usually **closer to the sample values** than the true population mean.

As a result, the squared deviations

$$
(x_i-\bar{x})^2
$$

tend to be **too small**.

If we divide by **(n)**, the variance will usually **underestimate** the true population variance.

---

## Example

Suppose the sample is

$$
2,4,6
$$

### Step 1: Compute the Sample Mean

$$
\bar{x} = \frac{2+4+6}{3} = 4
$$

### Step 2: Squared Deviations

|   $x_i$   | $x_i-\bar{x}$ | $(x_i-\bar{x})^2$ |
| :-------: | :-----------: | :---------------: |
|     2     |      -2       |         4         |
|     4     |       0       |         0         |
|     6     |       2       |         4         |
| **Total** |               |       **8**       |

---

### If we divide by (n=3)

# $$

\frac{8}{3}

=2.67

$$

---

### If we divide by (n-1=2)

#
$$

\frac{8}{2}

=4

$$

The value **4** is a better estimate of the population variance.

---

## Why "n − 1"?

When calculating the sample mean,

#
$$

\bar{x}

\frac{x_1+x_2+\cdots+x_n}{n},

$$

one piece of information is "used up."

For example, suppose


$$

n=5

$$

and the sample mean is


$$

\bar{x}=10.

$$

If you already know the first four values,


$$

8,;9,;10,;11,

$$

the fifth value is **forced**.

Because


$$

\frac{8+9+10+11+x_5}{5}=10,

$$

we have


$$

38+x_5=50

$$

so


$$

x_5=12.

$$

The fifth value is no longer free to vary.

Therefore:

- Total observations = **5**
- Independent observations = **4**

This is why we say the sample has


$$

n-1

$$

**degrees of freedom**.

---

## Why Population Variance Uses (N)

For a population, we know **every value** and the **true mean** (\mu).
Nothing has to be estimated.
Therefore, we divide by


$$

N.

$$

---

## Summary

|Population Variance|Sample Variance|
|---|---|
|Uses the true mean ((\mu))|Uses the estimated mean ((\bar{x}))|
|Divide by (N)|Divide by (n-1)|
|Exact variance|Estimate of population variance|
|No correction needed|Uses **Bessel's correction** to avoid underestimating variance|

### Easy way to remember

> **Population = Divide by (N)** (you know everyone).
> **Sample = Divide by (n-1)** (you estimated the mean, so one degree of freedom is lost).
$$
