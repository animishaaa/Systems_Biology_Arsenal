# 📊 Statistical Distributions 

## What is a Distribution?

A **distribution** describes **how data or probabilities are spread out**.

Think of it as the **shape of your data**.

Example:

Raw data:

```
170, 172, 168, 170, 171, 169, 170
```

When plotted, the data forms a shape (distribution).

---

# Types of Distributions

There are two broad categories:

```
Distributions
│
├── Frequency Distribution
│
└── Probability Distributions
      │
      ├── Normal
      ├── Z
      ├── t
      ├── Binomial
      ├── Poisson
      ├── Chi-Square
      └── F
```

---

# 1. Frequency Distribution

## Definition

Shows **how many times each value appears**.

Example

| Marks | Frequency |
|-------|----------|
|60|2|
|70|5|
|80|8|
|90|3|

It simply **counts observations**.

### Used for

- Organizing raw data
- Creating tables
- Histograms
- Bar charts

### Example

```
Apple : █████

Banana: ███

Orange: ██
```

✅ Counts only

❌ No probabilities

---

# 2. Probability Distribution

## Definition

Shows the **probability (chance)** of every possible outcome.

Instead of counting,

it answers:

> "How likely is this outcome?"

Example

| Outcome | Probability |
|---------|------------|
|A|0.20|
|B|0.50|
|C|0.30|

The probabilities always add up to **1 (100%)**.

### Used for

- Predicting outcomes
- Hypothesis testing
- Statistical inference

Every statistical test is based on a probability distribution.

---

# 3. Normal Distribution ⭐

The famous **Bell Curve**.

```
          *
       *     *
     *         *
   *             *
 *                 *
------------------------
```

## Characteristics

- Bell-shaped
- Symmetrical
- Mean = Median = Mode
- Continuous data

## Examples

- Height
- Weight
- Blood pressure
- IQ
- Exam scores

### Used for

- Continuous measurements
- Parametric statistics

### Statistical Tests

- Basis of Z-test
- Foundation of t-test
- Regression
- Pearson correlation
- ANOVA (through normality assumptions)

---

# 4. Z Distribution

A **standardized Normal Distribution**.

```
Mean = 0

Standard Deviation = 1
```

Every observation becomes a **Z-score**.

Example

Height =178 cm

Mean =170

SD=8

```
Z = (178-170)/8 = 1
```

Meaning

178 cm is **1 standard deviation above the mean.**

### Used for

- Standardization
- Large samples
- Known population SD

### Statistical Tests

- Z-test
- Confidence intervals
- Normal probability calculations

---

# 5. t Distribution ⭐

Looks like a Normal curve

but has **fatter tails**.

```
        **
      *    *
    *        *
  *            *
-------------------------
```

## Why?

Because the **population standard deviation is unknown**.

We estimate it using the sample.

This introduces uncertainty.

As sample size increases,

```
t Distribution

↓

Normal Distribution
```

### Used for

- Small sample sizes
- Unknown population SD

### Statistical Tests

- One-sample t-test
- Independent t-test
- Paired t-test
- Pearson correlation significance
- Regression coefficients

---

# 6. Binomial Distribution

Only **two possible outcomes**.

```
Yes / No

Success / Failure

Alive / Dead

Pass / Fail
```

Example

Flip a coin 10 times.

Possible heads:

```
0

1

2

...

10
```

### Used for

Binary outcomes.

### Statistical Tests

- Binomial test
- Logistic regression (related concept)

---

# 7. Poisson Distribution

Used for **counting events**.

Examples

- Number of emails per hour
- Number of mutations
- Number of accidents
- Number of bacteria colonies

```
*
**
****
******
********
******
***
*
```

### Characteristics

- Counts
- Discrete
- Cannot be negative

### Statistical Tests

- Poisson test
- Poisson regression

---

# 8. Chi-Square Distribution

Always starts at zero.

Always positive.

```
*
**
***
*****
*******
**********
```

### Used for

- Categorical variables
- Comparing observed vs expected frequencies
- Measuring variance

### Statistical Tests

- Chi-square Test
- McNemar Test
- Kruskal-Wallis (approximation)
- Friedman Test (approximation)

---

# 9. F Distribution

Compares **two variances**.

Always positive.

```
*
**
***
******
********
***********
```

### Used for

Comparing variability between groups.

### Statistical Tests

- One-Way ANOVA
- Repeated Measures ANOVA
- Overall Linear Regression
- ANCOVA

---

# Relationship Between Distributions and Statistical Tests

```
Raw Data
      │
      ▼
Frequency Distribution
      │
      ▼
Probability Distribution
      │
      ▼
Statistical Test
      │
      ▼
Test Statistic
(t, F, χ², Z)
      │
      ▼
Probability Distribution
      │
      ▼
p-value
      │
      ▼
Conclusion
```

---

# Which Test Uses Which Distribution?

| Statistical Test | Distribution Used |
|-----------------|-------------------|
| Z-test | Z Distribution |
| One-sample t-test | t Distribution |
| Independent t-test | t Distribution |
| Paired t-test | t Distribution |
| Pearson Correlation | t Distribution |
| Linear Regression (coefficients) | t Distribution |
| Linear Regression (overall model) | F Distribution |
| One-Way ANOVA | F Distribution |
| Repeated Measures ANOVA | F Distribution |
| Chi-square Test | Chi-square Distribution |
| McNemar Test | Chi-square Distribution |
| Kruskal-Wallis Test | Chi-square Distribution |
| Friedman Test | Chi-square Distribution |
| Mann-Whitney U Test | Normal (Z) approximation for larger samples; exact distribution for small samples |
| Wilcoxon Signed-Rank Test | Normal (Z) approximation for larger samples; exact distribution for small samples |
| Binomial Test | Binomial Distribution |
| Poisson Test | Poisson Distribution |

---

# Quick Summary

| Distribution | Used For | Main Statistical Tests |
|-------------|----------|------------------------|
| Frequency | Counting observations | Data summarization |
| Probability | Probability of outcomes | Foundation of all hypothesis tests |
| Normal | Continuous measurements | Basis for parametric tests |
| Z | Standardized values | Z-test |
| t | Small samples, unknown SD | t-tests, regression coefficients, Pearson correlation |
| Binomial | Yes/No outcomes | Binomial test |
| Poisson | Count data | Poisson regression |
| Chi-Square | Categorical data | Chi-square, McNemar, Kruskal-Wallis, Friedman |
| F | Comparing variances | ANOVA, overall regression |

---

# Key Takeaway ⭐

Think of distributions as **reference curves**.

Every statistical test follows the same idea:

```
Collect Data
      │
      ▼
Calculate a Test Statistic
      │
      ▼
Compare with a Probability Distribution
      │
      ▼
Calculate the p-value
      │
      ▼
Accept or Reject the Null Hypothesis
```

**Without probability distributions, statistical tests cannot determine whether an observed result is due to chance or represents a real effect.**
