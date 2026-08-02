# Covariance and Correlation

## Covariance

### Definition

**Covariance** measures the **direction** of the relationship between two variables.

It tells us whether two variables tend to increase or decrease together.
- Positive covariance → Variables move in the same direction.
- Negative covariance → Variables move in opposite directions.
- Zero covariance → No linear relationship.

---

## Population Covariance

$$
\operatorname{Cov}(X,Y)=
\frac{\sum_{i=1}^{N}(x_i-\mu_x)(y_i-\mu_y)}{N}
$$

---

## Sample Covariance

$$
\operatorname{Cov}(X,Y)=
\frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}{n-1}
$$

---

## Symbols

| Symbol | Meaning |
|--------|---------|
| $x_i,\;y_i$ | Observations of X and Y |
| $\mu_x,\;\mu_y$ | Population means |
| $\bar{x},\;\bar{y}$ | Sample means |
| $N$ | Population size |
| $n$ | Sample size |

---

## Interpretation

| Covariance | Meaning |
|------------|---------|
| Cov(X,Y) > 0 | Positive relationship |
| Cov(X,Y) < 0 | Negative relationship |
| Cov(X,Y) = 0 | No linear relationship |

---

## Example

| Hours Studied ($X$) | Exam Score ($Y$) |
|:-------------------:|:----------------:|
| 2 | 60 |
| 4 | 70 |
| 6 | 80 |
| 8 | 90 |

As study hours increase, exam scores also increase.

Therefore,

$$
\boxed{\operatorname{Cov}(X,Y) > 0}
$$

---

# Correlation

## Definition

**Correlation** measures both the **strength** and the **direction** of the linear relationship between two variables.

Unlike covariance, correlation is **unit-free** and always lies between **−1** and **+1**.

---
# Pearson Correlation Coefficient and Spearman Rank Correlation

## Pearson Correlation Coefficient

### Definition

The **Pearson Correlation Coefficient** measures the **strength** and **direction** of the **linear relationship** between two numerical variables.

It is denoted by **\(r\)**.

---

## Formula

$$
r=
\frac{\operatorname{Cov}(X,Y)}
{s_xs_y}
$$

or equivalently,

$$
r=
\frac{\sum (x_i-\bar{x})(y_i-\bar{y})}
{\sqrt{\sum (x_i-\bar{x})^2
\sum (y_i-\bar{y})^2}}
$$

---
where

| Symbol | Meaning |
|--------|---------|
| $r$ | Pearson correlation coefficient |
| $\operatorname{Cov}(X,Y)$ | Covariance |
| $s_x$ | Standard deviation of X |
| $s_y$ | Standard deviation of Y |

---

## Range of Correlation

$$
-1 \le r \le 1
$$

---

## Interpretation

| Correlation ($r$) | Relationship                  |
| ----------------: | ----------------------------- |
|              $+1$ | Perfect positive correlation  |
|    $0.7$ to $0.9$ | Strong positive correlation   |
|    $0.3$ to $0.7$ | Moderate positive correlation |
|               $0$ | No linear correlation         |
|  $-0.3$ to $-0.7$ | Moderate negative correlation |
|  $-0.7$ to $-0.9$ | Strong negative correlation   |
|              $-1$ | Perfect negative correlation  |

---

## Example

| Hours Studied | Exam Score |
|:-------------:|:----------:|
| 2 | 60 |
| 4 | 70 |
| 6 | 80 |
| 8 | 90 |

As study hours increase, exam scores also increase.

$$
r=1
$$

This indicates a **perfect positive linear relationship**.

---

# Spearman Rank Correlation

## Definition

The **Spearman Rank Correlation** measures the **strength** and **direction** of a **monotonic relationship** between two variables using their **ranks** instead of their actual values.

It is denoted by **\(\rho\)** (rho) or **\(r_s\)**.

---

## Formula

$$
r_s
=
1-
\frac{6\sum d_i^2}
{n(n^2-1)}
$$

where

| Symbol | Meaning |
|--------|---------|
| $d_i$ | Difference between the ranks |
| $n$ | Number of observations |

---

## Example

| Student | Math Rank | Physics Rank | $d$ | $d^2$ |
|:------:|:---------:|:------------:|:---:|:-----:|
| A | 1 | 2 | -1 | 1 |
| B | 2 | 1 | 1 | 1 |
| C | 3 | 3 | 0 | 0 |
| D | 4 | 4 | 0 | 0 |
| **Total** | | | | **2** |

### Step 1: Apply the Formula

$$
\begin{aligned}
r_s
    &=1-\frac{6(2)}{4(4^2-1)}\\
    &=1-\frac{12}{60}\\
    &=1-0.2\\
    &=0.8
\end{aligned}
$$

---

## Interpretation

$$
r_s=0.8
$$

This indicates a **strong positive monotonic relationship** between the two rankings.

---

# Pearson vs Spearman

| Pearson Correlation | Spearman Rank Correlation |
|----------------------|---------------------------|
| Uses actual values | Uses ranks |
| Measures linear relationship | Measures monotonic relationship |
| Sensitive to outliers | Less sensitive to outliers |
| Requires numerical data | Works with ranked or ordinal data |
| Formula uses covariance | Formula uses rank differences |

---

# When to Use

### Use Pearson Correlation when:

- Data is numerical.
- The relationship is approximately linear.
- There are no extreme outliers.

### Use Spearman Correlation when:

- Data is ranked or ordinal.
- The relationship is monotonic but not necessarily linear.
- The data contains outliers or is not normally distributed.

---

- **Pearson Correlation** measures the strength and direction of a **linear** relationship.
- **Spearman Rank Correlation** measures the strength and direction of a **monotonic** relationship using **ranks**.
- Both coefficients range from **−1 to +1**:
  - **+1** → Perfect positive relationship.
  - **0** → No relationship.
  - **−1** → Perfect negative relationship.

---

## Examples

### Positive Correlation

```text
Y
↑
│          •
│       •
│    •
│  •
│•
└────────────────→ X
```

As X increases, Y increases.

---

### Negative Correlation

```text
Y
↑
│•
│  •
│    •
│      •
│         •
└────────────────→ X
```

As X increases, Y decreases.

---

### No Correlation

```text
Y
↑
│   •     •
│      •
│ •      •
│    •
│       •
└────────────────→ X
```

No clear linear relationship.

---

# Covariance vs Correlation

| Covariance | Correlation |
|------------|-------------|
| Measures direction only | Measures both direction and strength |
| Depends on units | Unit-free |
| Range is unbounded | Always between −1 and +1 |
| Difficult to compare | Easy to compare |

---
- **Covariance** indicates whether two variables move together or in opposite directions.
- **Correlation** indicates both the direction and the strength of the linear relationship.
- Correlation is a standardized version of covariance, making it easier to interpret and compare.

---
# Mathematical Example

Given the data:

| $X$ | $Y$ |
|:---:|:---:|
| 2 | 4 |
| 4 | 6 |
| 6 | 8 |
| 8 | 10 |

---

## Step 1: Find the Means

$$
\begin{aligned}
\bar{x}
    &= \frac{2+4+6+8}{4} \\
    &= \frac{20}{4} \\
    &= 5
\end{aligned}
$$

$$
\begin{aligned}
\bar{y}
    &= \frac{4+6+8+10}{4} \\
    &= \frac{28}{4} \\
    &= 7
\end{aligned}
$$

---

## Step 2: Compute the Deviations

| $x_i$ | $y_i$ | $x_i-\bar{x}$ | $y_i-\bar{y}$ | $(x_i-\bar{x})(y_i-\bar{y})$ |
|:-----:|:-----:|:-------------:|:-------------:|:----------------------------:|
| 2 | 4 | -3 | -3 | 9 |
| 4 | 6 | -1 | -1 | 1 |
| 6 | 8 | 1 | 1 | 1 |
| 8 | 10 | 3 | 3 | 9 |
| **Total** | | | | **20** |

---

## Step 3: Calculate Sample Covariance

$$
\begin{aligned}
\operatorname{Cov}(X,Y)
    &= \frac{\sum (x_i-\bar{x})(y_i-\bar{y})}{n-1} \\
    &= \frac{20}{4-1} \\
    &= \frac{20}{3} \\
    &\approx 6.67
\end{aligned}
$$

---

## Step 4: Calculate Standard Deviations

For X:

$$
\begin{aligned}
s_x
    &= \sqrt{\frac{(-3)^2+(-1)^2+1^2+3^2}{3}} \\
    &= \sqrt{\frac{20}{3}} \\
    &\approx 2.58
\end{aligned}
$$

For Y:

$$
\begin{aligned}
s_y
    &= \sqrt{\frac{(-3)^2+(-1)^2+1^2+3^2}{3}} \\
    &= \sqrt{\frac{20}{3}} \\
    &\approx 2.58
\end{aligned}
$$

---

## Step 5: Calculate Correlation

$$
\begin{aligned}
r
    &= \frac{\operatorname{Cov}(X,Y)}{s_x s_y} \\
    &= \frac{6.67}{2.58 \times 2.58} \\
    &= \frac{6.67}{6.67} \\
    &= 1
\end{aligned}
$$

---

## Final Results

| Measure | Value |
|---------|------:|
| Sample Covariance | 6.67 |
| Sample Correlation | 1.00 |

---

## Interpretation

- **Covariance = 6.67** → Positive relationship (both variables increase together).
- **Correlation = 1** → Perfect positive linear relationship.