# Standard Deviation

## 2. Standard Deviation

Standard deviation measures how much the data values deviate (spread) from the mean. It is simply the **square root of the variance**.

### Population vs Sample Formula

| Measure                | Population Formula                                    | Sample Formula                                         |
| ---------------------- | ----------------------------------------------------- | ------------------------------------------------------ |
| **Standard Deviation** | $\sigma = \sqrt{\frac{\sum_{i=1}^{N}(x_i-\mu)^2}{N}}$ | $s = \sqrt{\frac{\sum_{i=1}^{n}(x_i-\bar{x})^2}{n-1}}$ |

### Symbols

| Symbol    | Meaning                       |
| --------- | ----------------------------- |
| $\sigma$  | Population standard deviation |
| $s$       | Sample standard deviation     |
| $\mu$     | Population mean               |
| $\bar{x}$ | Sample mean                   |
| $x_i$     | Individual observation        |
| $N$       | Population size               |
| $n$       | Sample size                   |

---

## Example

Given data:

$$
2,\;4,\;6,\;8,\;10
$$

### Step 1: Find the Mean

$$
\begin{aligned}
\mu
    &= \frac{2+4+6+8+10}{5} \\
    &= \frac{30}{5} \\
    &= 6
\end{aligned}
$$

### Step 2: Calculate the Variance

|   $x_i$   | $x_i-\mu$ | $(x_i-\mu)^2$ |
| :-------: | :-------: | :-----------: |
|     2     |    -4     |      16       |
|     4     |    -2     |       4       |
|     6     |     0     |       0       |
|     8     |     2     |       4       |
|    10     |     4     |      16       |
| **Total** |           |    **40**     |

$$
\begin{aligned}
\sigma^2
    &= \frac{40}{5} \\
    &= 8
\end{aligned}
$$

### Step 3: Find the Standard Deviation

$$
\begin{aligned}
\sigma
    &= \sqrt{\sigma^2} \\
    &= \sqrt{8} \\
    &\approx 2.83
\end{aligned}
$$

> **Population Standard Deviation:** $\boxed{\sigma \approx 2.83}$

---

## Sample Standard Deviation

Using the same data as a sample:

$$
\begin{aligned}
s^2
    &= \frac{40}{5-1} \\
    &= \frac{40}{4} \\
    &= 10
\end{aligned}
$$

$$
\begin{aligned}
s
    &= \sqrt{10} \\
    &\approx 3.16
\end{aligned}
$$

> **Sample Standard Deviation:** $\boxed{s \approx 3.16}$

### Easy way to remember

- **Variance** = Average **squared** distance from the mean.
- **Standard Deviation** = **Square root of the variance**.

$$
\boxed{\text{Standard Deviation} = \sqrt{\text{Variance}}}
$$

The advantage of standard deviation is that it is expressed in the **same units as the original data**, making it much easier to interpret than variance.
