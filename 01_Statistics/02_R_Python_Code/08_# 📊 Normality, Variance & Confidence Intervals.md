# 📊 Statistical Tests for Normality, Variance, and Confidence Intervals in R

Statistical tests help us determine whether our data satisfy the assumptions required for many statistical analyses, such as the **t-test** and **ANOVA**.

In this chapter, we will cover:

- 📈 Shapiro-Wilk Normality Test
- 📊 Levene's Test (Equality of Variance)
- 📏 Confidence Interval for a Mean
- ⚖️ Confidence Interval for the Difference Between Means

---

# 📈 1. Shapiro-Wilk Normality Test

The **Shapiro-Wilk test** checks whether a dataset follows a **normal distribution**.

Many statistical tests assume that the data are normally distributed.

---

## 🎯 Hypotheses

### Null Hypothesis (H₀)

The data are **normally distributed**.

### Alternative Hypothesis (H₁)

The data are **not normally distributed**.

---

## 💻 R Code

### Test Female Weights

```r
shapiro.test(df$Weight[df$Sex=="F"])
```

### Test Male Weights

```r
shapiro.test(df$Weight[df$Sex=="M"])
```

---

## Example Output

```
Shapiro-Wilk normality test

W = 0.9821

p-value = 0.7667
```

---

## 📖 Interpretation

| p-value | Conclusion |
|----------|------------|
| p > 0.05 | ✅ Data are normally distributed |
| p ≤ 0.05 | ❌ Data are not normally distributed |

---

### Example

```
Female:

p = 0.77
```

Since

```
0.77 > 0.05
```

we **fail to reject the null hypothesis**.

Therefore,

✅ Female weights are normally distributed.

Similarly,

```
Male:

p = 0.91
```

Since

```
0.91 > 0.05
```

Male weights are also normally distributed.

---

# 📚 Summary

| Result | Interpretation |
|---------|----------------|
| p > 0.05 | Normal distribution |
| p < 0.05 | Not normally distributed |

---

# 📊 2. Levene's Test (Equality of Variance)

Many statistical tests assume that different groups have **equal variances**.

Levene's Test checks this assumption.

---

## 🎯 Hypotheses

### Null Hypothesis (H₀)

The variances are equal.

### Alternative Hypothesis (H₁)

The variances are different.

---


## Run Levene's Test

```r
leveneTest(Weight ~ Sex,
           center = mean,
           data = df)
```

---

## Example Output

```
Df   F value   Pr(>F)

1     0.022     0.4806
```

---

## 📖 Interpretation

Since

```
p = 0.48
```

and

```
0.48 > 0.05
```

we **fail to reject the null hypothesis**.

Therefore,

✅ The two groups have equal variances.

---

## 📚 Summary

| p-value | Conclusion |
|----------|------------|
| p > 0.05 | Equal variance |
| p ≤ 0.05 | Unequal variance |

---

# 🎯 Why Are These Tests Important?

Before performing

- Independent t-test
- ANOVA

we should check:

✅ Normality

✅ Equal Variance

If both assumptions are satisfied, we can use the standard parametric tests.

---

# 📏 3. Confidence Interval for the Mean

A **Confidence Interval (CI)** estimates the range within which the **true population mean** is likely to lie.

Usually we calculate a **95% Confidence Interval**.

---

## Read Data

```r
df <- read.table(file.choose(),
                 header=TRUE,
                 sep=";",
                 dec=",")
```

---

## Compute 95% Confidence Interval

```r
data <- df$Weight[df$Sex=="F"]

t.test(data)
```

---

## Example Output

```
95 percent confidence interval:

62.23

66.41
```

---

## 📖 Interpretation

We are **95% confident** that the true mean weight of females lies between

```
62.23 kg

and

66.41 kg
```

---

## Sample Mean

```
Mean = 64.32 kg
```

The sample mean is our **best estimate** of the population mean.

---

# Change Confidence Level

For a **99% Confidence Interval**

```r
t.test(data,
       conf.level = 0.99)
```

---

## Common Confidence Levels

| Confidence Level |
|------------------|
| 90% |
| 95% |
| 99% |

---

# 📐 Interpretation of Confidence Intervals

A wider confidence interval means

✅ More confidence

but

❌ Less precision.

A narrower confidence interval means

✅ More precision

but

❌ Less confidence.

---

# ⚖️ 4. Confidence Interval for the Difference Between Means

Instead of estimating one mean, we can estimate the **difference between two means**.

Example:

Female weight

vs

Male weight

---

## R Code

```r
t.test(Weight ~ Sex,
       data = df)
```

---

## Example Output

```
95% Confidence Interval

[-26.03, -19.86]
```

---

## 📖 Interpretation

Notice that

```
0
```

is **NOT** inside the confidence interval.

Therefore,

✅ There is a statistically significant difference between the two group means.

---

## Why Does Zero Matter?

If the true difference between the two means were

```
0
```

then

Male mean = Female mean

There would be **no difference**.

---

### Case 1

```
[-26, -20]
```

Zero is **outside** the interval.

✅ Significant Difference

---

### Case 2

```
[-5, 5]
```

Zero is **inside** the interval.

❌ No Significant Difference

---

# 📚 Summary Table

| Confidence Interval | Conclusion |
|---------------------|------------|
| Includes 0 | No significant difference |
| Does NOT include 0 | Significant difference |

---

# 📋 Common R Functions

| Function | Purpose |
|----------|---------|
| `shapiro.test()` | Test for normality |
| `leveneTest()` | Test equality of variance |
| `t.test()` | Perform t-test and compute confidence interval |
| `library()` | Load an R package |
| `install.packages()` | Install a package |

---

# 🎯 Assumption Checklist Before a t-test

| Requirement | Test |
|-------------|------|
| Normality | `shapiro.test()` |
| Equal Variance | `leveneTest()` |
| Difference in Means | `t.test()` |

---

# 🚀 Key Takeaways

- 📈 **Shapiro-Wilk Test** checks whether data are normally distributed.
- 📊 **Levene's Test** checks whether two groups have equal variances.
- 📏 **Confidence Intervals** estimate the likely range of the true population mean.
- ⚖️ A confidence interval for the **difference between means** helps determine whether two groups differ significantly.
- 🎯 If the confidence interval for the difference **contains 0**, there is **no significant difference**.
- 🎯 If the confidence interval **does not contain 0**, there **is a significant difference**.
