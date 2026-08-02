# Percentiles and Quartiles

## Percentiles

### Definition

A **percentile** is a measure that divides a dataset into **100 equal parts**.

The **k-th percentile** is the value below which **k% of the observations** fall.

> Percentiles are used to compare an individual's value with the rest of the dataset.

---

## Examples

- **25th Percentile (P25)** → 25% of observations are below this value.
- **50th Percentile (P50)** → Median.
- **75th Percentile (P75)** → 75% of observations are below this value.
- **90th Percentile (P90)** → 90% of observations are below this value.

---

## Formula

The position of the **k-th percentile** is

$$
L=\frac{k}{100}(n+1)
$$

where

| Symbol | Meaning                    |
| ------ | -------------------------- |
| $L$    | Position of the percentile |
| $k$    | Desired percentile (1–99)  |
| $n$    | Number of observations     |

If the position is not a whole number, use **interpolation** between the two nearest observations.

---

## Example

Given the ordered data:

$$
2,\;4,\;6,\;8,\;10,\;12,\;14,\;16,\;18,\;20
$$

Find the **25th percentile**.

### Step 1: Number of observations

$$
n=10
$$

### Step 2: Find the position

$$
\begin{aligned}
L
    &=\frac{25}{100}(10+1)\\
    &=2.75
\end{aligned}
$$

The 25th percentile lies between the **2nd** and **3rd** observations.

- 2nd value = 4
- 3rd value = 6

Using interpolation:

$$
\begin{aligned}
P_{25}
    &=4+0.75(6-4)\\
    &=5.5
\end{aligned}
$$

---

# Quartiles

## Definition

Quartiles divide a dataset into **four equal parts**.

There are three quartiles:

| Quartile | Percentile | Meaning        |
| -------- | ---------: | -------------- |
| $Q_1$    |       25th | Lower Quartile |
| $Q_2$    |       50th | Median         |
| $Q_3$    |       75th | Upper Quartile |

---

## Formula

The position of the **k-th quartile** is

$$
L=\frac{k(n+1)}{4}
$$

where

- $k=1$ for $Q_1$
- $k=2$ for $Q_2$
- $k=3$ for $Q_3$

---

## Example

Given the ordered data:

$$
2,\;4,\;6,\;8,\;10,\;12,\;14,\;16,\;18,\;20
$$

### First Quartile ($Q_1$)

$$
\begin{aligned}
L
    &=\frac{1(10+1)}{4}\\
    &=2.75
\end{aligned}
$$

$$
Q_1=5.5
$$

---

### Second Quartile ($Q_2$)

$$
\begin{aligned}
L
    &=\frac{2(10+1)}{4}\\
    &=5.5
\end{aligned}
$$

The value lies halfway between

10 and 12.

$$
Q_2=11
$$

---

### Third Quartile ($Q_3$)

$$
\begin{aligned}
L
    &=\frac{3(10+1)}{4}\\
    &=8.25
\end{aligned}
$$

The value lies between

16 and 18.

$$
\begin{aligned}
Q_3
    &=16+0.25(18-16)\\
    &=16.5
\end{aligned}
$$

---

# Relationship Between Quartiles and Percentiles

| Quartile | Equivalent Percentile |
| -------- | --------------------: |
| $Q_1$    |              $P_{25}$ |
| $Q_2$    |     $P_{50}$ (Median) |
| $Q_3$    |              $P_{75}$ |

---

# Visualization

```text
Minimum    Q1        Q2        Q3      Maximum
|----------|---------|---------|----------|
0%        25%       50%       75%      100%
```

---

The quartile formula is:

$$
L=\frac{k(n+1)}{4}
$$

where:

- (L) = Position of the quartile
- (k) = Quartile number (1, 2, or 3)
- (n) = Number of observations

---

## Example: Finding (Q_1)

Given the ordered data:

$$
2,;4,;6,;8,;10,;12,;14,;16,;18,;20
$$

There are

$$
n=10
$$

Using the formula:

$$
\begin{aligned}
L
&= \frac{1(10+1)}{4} \
&= \frac{11}{4} \
&= 2.75
\end{aligned}
$$

The position is **2.75**.

This means:

- The whole number **2** tells you to start at the **2nd observation**.
- The decimal part **0.75** tells you to move **75% of the way** toward the **3rd observation**.

The observations are:

| Position | Value |
| -------: | ----: |
|        2 |     4 |
|        3 |     6 |

So,

# $$

Q_1 =

4

- 0.75(6-4)  
  $$

Why?

- Difference between the values:

$$
6-4=2
$$

- Take **75%** of that difference:

$$
0.75\times2=1.5
$$

- Add it to the lower value:

$$
4+1.5=5.5
$$

Therefore,

$$
\boxed{Q_1=5.5}
$$

---

## Where did **0.75** come from?

It comes **directly from the position**:

$$
L=2.75
$$

Split it into:

- Integer part = **2**
- Fractional part = **0.75**

The **fractional part** is always the interpolation factor.

For example:

| Position (L) | Interpolation Factor |
| -----------: | -------------------: |
|         2.25 |                 0.25 |
|         2.50 |                 0.50 |
|         2.75 |                 0.75 |
|         8.10 |                 0.10 |
|         8.90 |                 0.90 |

**General interpolation formula:**

If

$$
L=i+f,
$$

where:

- (i) = integer part of the position
- (f) = fractional part ((0 <= f < 1)),

then

$$
\boxed{\text{Quartile} = x_i + f(x_{i+1}-x_i)}
$$

Here:

- (L=2.75)
- (i=2)
- (f=0.75)

so

$$
Q_1=4+0.75(6-4)=5.5.
$$

So, **0.75 is not part of the quartile formula**—it is the **fractional part of the calculated position (2.75)**, which tells you how far to interpolate between two adjacent observations.

---

# Applications

Percentiles and quartiles are commonly used to:

- Compare student exam scores.
- Measure growth in children.
- Analyze salaries and income.
- Identify outliers using the Interquartile Range (IQR).
- Summarize data distributions.

---

# Summary

- **Percentiles** divide data into **100 equal parts**.
- **Quartiles** divide data into **4 equal parts**.
- **Median** is the **50th percentile** and the **second quartile ($Q_2$)**.
- Quartiles help summarize the spread of a dataset and are the basis for the **Interquartile Range (IQR)**.
