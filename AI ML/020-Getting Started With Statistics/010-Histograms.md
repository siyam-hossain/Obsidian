# Histograms (Descriptive Statistics)

## Definition

A **histogram** is a graphical representation of the distribution of **numerical data**. It groups data into continuous intervals called **bins** and displays the frequency of observations in each interval.

> A histogram helps us understand the **shape**, **center**, **spread**, and **outliers** of a dataset.

---

## Example Dataset

Student Exam Scores:

$$
45,\;52,\;58,\;61,\;64,\;67,\;72,\;75,\;78,\;81,\;85,\;89,\;92,\;95
$$

Group the scores into intervals (bins):

| Score Range | Frequency |
|-------------|----------:|
| 40–49 | 1 |
| 50–59 | 2 |
| 60–69 | 3 |
| 70–79 | 3 |
| 80–89 | 3 |
| 90–99 | 2 |

---

## Histogram (ASCII)

```text
Frequency
3 |        ███ ███ ███
2 |    ██  ███ ███ ███ ██
1 | ██ ██  ███ ███ ███ ██
  +-------------------------
    40 50  60   70  80 90
```

---

# Characteristics of a Histogram

- Bars touch each other because the data is continuous.
- X-axis represents intervals (bins).
- Y-axis represents frequency.
- Taller bars indicate more observations in that interval.

---

# What Can a Histogram Tell Us?

A histogram helps us identify:

- Data distribution
- Center of the data
- Spread (variability)
- Outliers
- Skewness
- Number of peaks (modality)

---

# Types of Histogram Shapes

## 1. Symmetric Distribution

```text
        █
      ███
    ███████
      ███
        █
```

Characteristics:

- Left and right sides are approximately equal.
- Mean ≈ Median ≈ Mode.

---

## 2. Right-Skewed (Positive Skew)

```text
████████
██████
████
██
█
```

Characteristics:

- Long tail extends to the right.
- Mean > Median > Mode.

Examples:

- Income
- House prices

---

## 3. Left-Skewed (Negative Skew)

```text
        █
      ██
    ████
██████
████████
```

Characteristics:

- Long tail extends to the left.
- Mean < Median < Mode.

Examples:

- Easy exam scores
- Retirement age

---

## 4. Uniform Distribution

```text
████
████
████
████
████
```

Characteristics:

- All intervals have approximately equal frequencies.

---

## 5. Bimodal Distribution

```text
███     ███
████   ████
█████ █████
```

Characteristics:

- Two distinct peaks.
- May indicate two different groups in the data.

Example:
- Heights of males and females combined.

---

# Histogram vs Bar Chart

| Histogram | Bar Chart |
|------------|-----------|
| Used for numerical data | Used for categorical data |
| Bars touch each other | Bars are separated |
| X-axis shows intervals | X-axis shows categories |
| Displays distribution | Compares categories |

---

# Advantages

- Easy to understand data distribution.
- Identifies skewness and outliers.
- Useful for large datasets.
- Helps compare different distributions.

---

# Limitations

- Bin size affects the appearance.
- Exact values cannot be identified.
- Not suitable for categorical data.

---

# Summary

- A histogram displays the frequency distribution of **continuous numerical data**.
- Bars are adjacent because the data is continuous.
- Histograms help visualize the shape, spread, center, and outliers of a dataset.