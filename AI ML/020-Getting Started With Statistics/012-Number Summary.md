# Number Summary (Descriptive Statistics)

## Definition

A **Number Summary**, also called the **Five-Number Summary**, is a concise way to describe the distribution of a dataset.

It consists of five important values:

1. Minimum
2. First Quartile ($Q_1$)
3. Median ($Q_2$)
4. Third Quartile ($Q_3$)
5. Maximum

> The five-number summary provides information about the **center**, **spread**, and **distribution** of the data.

---

# Five-Number Summary

| Statistic      | Description                      |
| -------------- | -------------------------------- |
| Minimum        | Smallest observation             |
| $Q_1$          | First Quartile (25th percentile) |
| Median ($Q_2$) | Middle value (50th percentile)   |
| $Q_3$          | Third Quartile (75th percentile) |
| Maximum        | Largest observation              |

---

# Example

Given the ordered dataset:

$$
2,\;4,\;6,\;8,\;10,\;12,\;14,\;16,\;18,\;20
$$

## Step 1: Minimum

$$
\boxed{2}
$$

---

## Step 2: First Quartile ($Q_1$)

### Find the Position

$$
\begin{aligned}
L
    &= \frac{1(n+1)}{4} \\
    &= \frac{1(10+1)}{4} \\
    &= 2.75
\end{aligned}
$$

The position **2.75** lies between the **2nd** and **3rd** observations.

| Position | Value |
| -------: | ----: |
|        2 |     4 |
|        3 |     6 |

### Interpolation

$$
\begin{aligned}
Q_1
    &= 4 + 0.75(6-4) \\
    &= 4 + 1.5 \\
    &= 5.5
\end{aligned}
$$

---

## Step 3: Median

Since there are 10 observations,

$$
Q_2
=
\frac{10+12}{2}
=
11
$$

---

## Step 4: Third Quartile ($Q_3$)

### Find the Position

$$
\begin{aligned}
L
    &= \frac{3(n+1)}{4} \\
    &= \frac{3(10+1)}{4} \\
    &= 8.25
\end{aligned}
$$

The position **8.25** lies between the **8th** and **9th** observations.

| Position | Value |
| -------: | ----: |
|        8 |    16 |
|        9 |    18 |

### Interpolation

$$
\begin{aligned}
Q_3
    &= 16 + 0.25(18-16) \\
    &= 16 + 0.5 \\
    &= 16.5
\end{aligned}
$$

---

## Step 5: Maximum

$$
\boxed{20}
$$

---

# Five-Number Summary

| Statistic | Value |
| --------- | ----: |
| Minimum   |     2 |
| $Q_1$     |   5.5 |
| Median    |    11 |
| $Q_3$     |  16.5 |
| Maximum   |    20 |

---

# Visualization

```text
Minimum      Q1      Median      Q3      Maximum
   |----------|----------|----------|----------|
   2         5.5         11        16.5       20
```

---

# Why Is the Five-Number Summary Important?

It helps us:

- Understand the center of the data.
- Measure the spread of the data.
- Detect possible outliers.
- Construct a box plot.
- Compare different datasets.

---

# Interquartile Range (IQR)

The **Interquartile Range (IQR)** measures the spread of the middle 50% of the data.

$$
IQR = Q_3 - Q_1
$$

### Example

$$
\begin{aligned}
IQR
    &= 16.5 - 5.5 \\
    &= 11
\end{aligned}
$$

---

# Detecting Outliers

The lower and upper fences are:

$$
\text{Lower Fence}=Q_1-1.5(IQR)
$$

$$
\text{Upper Fence}=Q_3+1.5(IQR)
$$

For the example:

$$
\begin{aligned}
\text{Lower Fence}
    &=5.5-1.5(11)\\
    &=-11
\end{aligned}
$$

$$
\begin{aligned}
\text{Upper Fence}
    &=16.5+1.5(11)\\
    &=33
\end{aligned}
$$

Any observation

- less than **−11**, or
- greater than **33**

is considered a potential outlier.

---

# Relationship Between Measures

| Measure | Description       |
| ------- | ----------------- |
| Minimum | Smallest value    |
| Maximum | Largest value     |
| Range   | Maximum − Minimum |
| Median  | Middle value      |
| $Q_1$   | 25% of data below |
| $Q_3$   | 75% of data below |
| IQR     | Middle 50% spread |

---

# Summary

- The **Five-Number Summary** consists of:
    - Minimum
    - First Quartile ($Q_1$)
    - Median ($Q_2$)
    - Third Quartile ($Q_3$)
    - Maximum
- It summarizes the distribution of a dataset.
- It is the foundation for creating **box plots** and identifying **outliers**.

---
