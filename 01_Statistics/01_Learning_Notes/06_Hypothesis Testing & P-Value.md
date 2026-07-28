# 📊 Hypothesis Testing

Hypothesis testing is a statistical method used to determine whether there is enough evidence from a sample to make a conclusion about a population.

The main goal is to decide whether the observed result is due to **chance** or whether there is a **real effect or difference**.

---

# 🎯 The Five Steps of Hypothesis Testing

1. 📝 State the hypotheses
2. 📏 Choose a significance level (α)
3. 📊 Collect data and choose a statistical test
4. 🧮 Perform the statistical test
5. 📖 Draw a conclusion

---

# 📝 Step 1: State the Hypotheses

A hypothesis is a statement about a population parameter that can be tested using sample data.

There are always **two hypotheses**.

## 🔹 Null Hypothesis (H₀)

The **null hypothesis** is the default assumption.

It usually states that:

- There is **no difference**
- There is **no effect**
- There is **no relationship**

The null hypothesis is assumed to be true unless there is strong evidence against it.

---

## 🔹 Alternative Hypothesis (H₁ or Hₐ)

The **alternative hypothesis** is what the researcher wants to investigate.

It states that:

- There **is** a difference.
- There **is** an effect.
- There **is** a relationship.

---

## 📌 Example

### Research Question

> Is the average height of Swedish adults different from **170 cm**?

### Null Hypothesis

```
H₀ : μ = 170 cm
```

The average height is **170 cm**.

---

### Alternative Hypothesis

```
H₁ : μ ≠ 170 cm
```

The average height is **not** 170 cm.

---

# 📏 Step 2: Choose a Significance Level (α)

The **significance level (α)** is the probability of making a **Type I Error**.

A **Type I Error** occurs when we reject the null hypothesis even though it is actually true.

---

## Common Significance Levels

| α | Meaning |
|---|---------|
| 0.10 | 10% chance of a false positive |
| 0.05 | 5% chance of a false positive ⭐ Most Common |
| 0.01 | 1% chance of a false positive |

---

### Example

```
α = 0.05
```

This means we accept a **5% risk** of incorrectly rejecting the null hypothesis.

---

# 📊 Step 3: Collect Data and Choose a Statistical Test

After stating the hypotheses, collect a sample from the population.

Next, choose the appropriate statistical test.

The choice depends on:

- 📈 Type of data (continuous or categorical)
- 👥 Number of groups
- 📏 Sample size
- 📊 Study design

---

## Example

Suppose we measure the height of **30 Swedish adults**.

Because we are comparing a sample mean with a known value (170 cm), we use a:

```
One-Sample t-test
```

---

# 🧮 Step 4: Perform the Statistical Test

Now calculate the test statistic and determine the p-value.

---

## Example

Sample Mean

```
172.3 cm
```

Sample Standard Deviation

```
7.8 cm
```

Sample Size

```
30
```

---

### Step 1: Calculate Standard Error

```
SE = SD / √n

SE = 7.8 / √30

SE ≈ 1.42
```

---

### Step 2: Calculate the t-value

```
t = (Sample Mean − Population Mean) / SE

t = (172.3 − 170) / 1.42

t ≈ 1.61
```

---

### Step 3: Find the p-value

Using a t-table or statistical software:

```
p ≈ 0.118
```

---

# 📖 Step 5: Draw a Conclusion

Compare the **p-value** with the significance level (α).

---

## Decision Rule (Using p-value)

| Condition | Decision |
|-----------|----------|
| p ≤ α | Reject H₀ |
| p > α | Do Not Reject H₀ |

---

## Example

```
p = 0.118

α = 0.05
```

Since

```
0.118 > 0.05
```

we **do not reject the null hypothesis**.

---

## Conclusion

There is **not enough evidence** to conclude that the average height of Swedish adults is different from **170 cm**.

---

# 📏 Decision Rule (Using Critical Value)

Instead of using the p-value, you can compare the **test statistic** with the **critical value**.

---

## Rule

```
If |Test Statistic| > Critical Value

➡ Reject H₀
```

```
If |Test Statistic| ≤ Critical Value

➡ Do Not Reject H₀
```

Both approaches lead to the same conclusion.

---

# 📊 Hypothesis Testing Flowchart

```text
Start
   │
   ▼
State H₀ and H₁
   │
   ▼
Choose α
   │
   ▼
Collect Sample Data
   │
   ▼
Choose Statistical Test
   │
   ▼
Calculate Test Statistic
   │
   ▼
Find P-value
   │
   ▼
Compare with α
   │
   ▼
Reject H₀ or Do Not Reject H₀
```

---

# 📚 Summary of the Five Steps

| Step | Description |
|------|-------------|
| 1️⃣ | State H₀ and H₁ |
| 2️⃣ | Choose α |
| 3️⃣ | Collect data and choose the test |
| 4️⃣ | Calculate the test statistic and p-value |
| 5️⃣ | Make a statistical decision |

---

# 📖 Hypothesis Testing in Plain Language

1. 📝 Make a prediction (**H₀**) and its opposite (**H₁**).
2. 📏 Decide how strict you want to be (**α**).
3. 📊 Collect data and choose the correct statistical test.
4. 🧮 Calculate the test statistic and p-value.
5. 📖 Decide whether the evidence is strong enough to reject the null hypothesis.

---

# 📊 Test Statistic vs. P-value

There are **two common ways** to make a statistical decision.

1. Using the **Test Statistic**
2. Using the **P-value**

Both methods always lead to the same conclusion.

---

# 🧮 Test Statistic (Manual Approach)

A **test statistic** is a number calculated directly from your sample data.

It tells you **how far your sample result is from what we would expect if the null hypothesis were true**.

Common test statistics include:

- **t-value**
- **z-value**
- **F-value**
- **χ² (Chi-square) value**

---

## Decision Rule

Compare the test statistic with a **critical value** from a statistical table.

```
If |Test Statistic| > Critical Value

➡ Reject H₀
```

```
If |Test Statistic| ≤ Critical Value

➡ Do Not Reject H₀
```

---

## Simple Definition

> **Test Statistic = The calculated score obtained from your sample data.**

---

# 📈 P-value (Software Approach)

Most statistical software automatically calculates the **p-value**.

The p-value answers the following question:

> **If the null hypothesis is true, what is the probability of obtaining a result this extreme (or more extreme) purely by chance?**

---

## Decision Rule

| P-value | Decision |
|----------|----------|
| p ≤ 0.05 | Reject H₀ |
| p > 0.05 | Do Not Reject H₀ |

---

## Interpretation

### Small p-value

- Result is unlikely to occur by chance.
- Strong evidence against H₀.
- Reject H₀.

---

### Large p-value

- Result is likely due to chance.
- Not enough evidence against H₀.
- Do not reject H₀.

---

## Simple Definition

> **P-value = The probability of observing your result (or a more extreme one) if the null hypothesis is true.**

---

# 🎓 Analogy: Taking an Exam

Imagine you are taking an exam.

---

### 🧮 Test Statistic

Your score is

```
82 / 100
```

This is your **test statistic**.

---

### 📏 Critical Value

The pass mark is

```
60
```

Since

```
82 > 60
```

you pass.

This is similar to:

```
Reject H₀
```

---

### 📈 P-value

Instead of comparing your score to the pass mark, imagine someone asks:

> **"If you guessed every answer randomly, what is the probability of scoring 82 or higher?"**

Suppose the probability is

```
2%
```

Since

```
2% < 5%
```

your score is very unlikely to be due to random guessing.

Therefore,

```
Reject H₀
```

---

# 🔍 Test Statistic vs. P-value

| Test Statistic | P-value |
|---------------|---------|
| Calculated directly from the data | Calculated from the test statistic |
| Compared with a critical value | Compared with α |
| Manual calculation | Usually provided by statistical software |
| Examples: t, z, F, χ² | Probability value between 0 and 1 |

---

# 🎯 Key Takeaways

- 📊 Hypothesis testing determines whether sample data provide enough evidence to support a claim.
- 📝 The **null hypothesis (H₀)** assumes no effect or no difference.
- 🔍 The **alternative hypothesis (H₁)** represents the claim being tested.
- 📏 The **significance level (α)** defines the threshold for deciding statistical significance.
- 🧮 The **test statistic** measures how far the sample result is from the null hypothesis.
- 📈 The **p-value** indicates how likely the observed result is if the null hypothesis is true.
- ✅ If **p ≤ α**, reject the null hypothesis.
- ❌ If **p > α**, do not reject the null hypothesis.
- 🎯 Both the **test statistic method** and the **p-value method** always lead to the same statistical decision.

---
---

# 📊 Understanding the P-Value

The **p-value** is one of the most important concepts in statistics.

It helps us determine whether the result we observed is likely due to **random chance** or whether there is **real evidence** against the null hypothesis.

> **A small p-value suggests that the observed result is unlikely to have occurred by chance alone.**

---

# 🤔 What is a P-Value?

A **p-value** is the probability of obtaining the observed result (or a more extreme result) **if the null hypothesis (H₀) is true**.

In simple words:

> **The p-value tells us how likely it is that our observed difference happened just by chance.**

---

## 🎲 Dice Analogy

Imagine rolling two dice.

Getting **double sixes (6️⃣6️⃣)** is possible, but it is rare.

If you roll double sixes:

- Did you cheat? ❌
- Or were you just lucky? ✅

A **p-value** works the same way.

It tells us how likely it is that our result happened **just by chance**.

---

# 🧪 Example

Suppose we compare two groups using a **two-sample t-test**.

The software reports:

```text
p = 0.02
```

This means:

> **If there were truly no difference between the two groups, there would only be a 2% chance of observing a difference this large (or larger) purely due to random sampling.**

Since

```
0.02 < 0.05
```

we reject the null hypothesis.

✅ The observed difference is **statistically significant**.

---

# 📖 Interpreting P-Values

| P-Value | Symbol | Interpretation |
|----------|:------:|----------------|
| **≥ 0.05** | ns | 😴 Not statistically significant |
| **0.05 – 0.01** | * | ⭐ Statistically significant |
| **0.01 – 0.001** | ** | 💪 Highly significant |
| **< 0.001** | *** | 🚀 Extremely significant |

---

# 📌 Decision Rule

| P-value | Decision |
|----------|----------|
| **p ≤ 0.05** | ✅ Reject the null hypothesis |
| **p > 0.05** | ❌ Do not reject the null hypothesis |

---

# 🧠 Quick Interpretation Guide

### Example 1

```
p = 0.21
```

Since

```
0.21 > 0.05
```

➡ Do **not** reject H₀.

There is **not enough evidence** to conclude that a real difference exists.

---

### Example 2

```
p = 0.03
```

Since

```
0.03 < 0.05
```

➡ Reject H₀.

There is evidence that the difference is **unlikely to be due to chance**.

---

### Example 3

```
p = 0.0004
```

This is **extremely significant**.

There is **very strong evidence** against the null hypothesis.

---

# 🎯 Remember

A **small p-value** means:

- ✅ The observed result is unlikely under the null hypothesis.
- ✅ There is stronger evidence against H₀.

A **large p-value** means:

- ❌ The observed result could easily happen by chance.
- ❌ There is not enough evidence to reject H₀.

---

# ⚖️ Statistical Significance vs. Scientific Significance

These two concepts are **not the same**.

---

## 📊 Statistical Significance

Statistical significance tells us whether the observed difference is **unlikely to be due to chance**.

It depends on:

- Sample size
- Variability
- P-value

---

## 🔬 Scientific Significance

Scientific significance asks:

> **Is the difference large enough to matter in the real world?**

---

### Example 1

A new medicine lowers blood pressure by

```
0.2 mmHg
```

The study includes

```
50,000 people
```

The result is

```
p < 0.001
```

It is **statistically significant**.

However,

a reduction of **0.2 mmHg** is so small that it has little practical importance.

---

### Example 2

A medicine lowers blood pressure by

```
20 mmHg
```

but only

```
5 patients
```

are studied.

The result is

```
p = 0.08
```

This is **not statistically significant**, but the effect is large.

A larger study may confirm that the medicine is truly effective.

---

# 📏 Always Consider Effect Size

Never rely only on the p-value.

Also consider:

- 📊 Effect size
- 📏 Confidence intervals
- 👥 Sample size
- 🧪 Study design

---

# 📚 Common Misconceptions

❌ **A p-value does NOT tell you that the null hypothesis is true.**

❌ **A p-value does NOT tell you the probability that your hypothesis is correct.**

❌ **A small p-value does NOT tell you how important the result is.**

Instead,

✅ It tells you how compatible your data are with the null hypothesis.

---

# 📈 How is a P-Value Calculated?

A p-value is calculated from a **test statistic**.

For example,

- t-test → t-value
- z-test → z-value
- ANOVA → F-value
- Chi-square test → χ²-value

The larger the test statistic, the farther it lies from the center of the sampling distribution.

A larger distance generally produces a **smaller p-value**.

---

# 💊 Example: Blood Pressure Study

Scientists want to test whether a new medicine lowers blood pressure.

---

## Study Design

### 👥 Control Group (No Medicine)

```text
155 151 152 147 149
149 152 149 151 145
```

---

### 💊 Treatment Group (Medicine)

```text
147 146 144 149 148
148 145 150 148 147
```

---

## Research Question

> Does the medicine really reduce blood pressure?

or

> Is the observed difference simply due to random chance?

---

# 🧮 Step 1: Calculate the Difference

First calculate the difference between the group means.

Suppose we obtain

```
Difference = -5 mmHg
```

---

# 🧮 Step 2: Calculate the Test Statistic

For a two-sample t-test,

```text
t = (Difference between means)
    ÷
(Standard Error)
```

Suppose

```
t = -3.2
```

---

# 📈 Step 3: Locate the Test Statistic on the t-Distribution

A **t-distribution** shows how likely different t-values are when the null hypothesis is true.

```text
                Normal / t Distribution

                 ^
                 |
              *****
            **     **
          **         **
--------**-----0------**---------
      -3     -2      2      3
```

Most values are close to

```
0
```

because if there is **no real difference**, the difference between groups should be close to zero.

---

# 🎯 Step 4: Calculate the P-Value

The p-value is the probability of observing a t-value **as extreme as** the one calculated.

If

```
t = -3.2
```

the probability is very small.

Example:

```
p = 0.003
```

Since

```
0.003 < 0.05
```

the observed result is unlikely to have occurred by chance.

---

# 🎈 Kid-Friendly Explanation

Imagine dropping a ball on a perfectly shaped hill.

```text
             🔴
          🔴🔴🔴
       🔴🔴🔴🔴🔴
    🔴🔴🔴🔴🔴🔴🔴
-------------------------
```

Most balls land near the **middle**.

If one lands **very far away**, you might wonder:

> "Something unusual happened!"

A p-value measures **how unusual** your result is.

- 🎯 Close to the middle → Large p-value → Probably just chance.
- 🚀 Far from the middle → Small p-value → Probably a real effect.

---

# 💡 Key Points to Remember

- 📊 A **p-value** measures how likely the observed result is if the null hypothesis is true.
- 🎯 A **small p-value** indicates stronger evidence against the null hypothesis.
- ❌ A **large p-value** does not prove the null hypothesis; it simply means there is insufficient evidence to reject it.
- 📏 Statistical significance does **not** always imply practical or scientific importance.
- 🧪 Always interpret the p-value together with the **effect size**, **confidence interval**, and **study design**.
- 📈 The p-value is calculated from a **test statistic** and the corresponding probability distribution.

---

# 🚀 Quick Summary

| Concept | Meaning |
|----------|---------|
| **P-value** | Probability of observing the data (or something more extreme) if H₀ is true |
| **Small p-value (< 0.05)** | Strong evidence against H₀ |
| **Large p-value (≥ 0.05)** | Insufficient evidence against H₀ |
| **Statistical significance** | Indicates whether a result is unlikely due to chance |
| **Scientific significance** | Indicates whether the result is meaningful in practice |
| **Decision Rule** | If **p ≤ α**, reject H₀; otherwise, do not reject H₀ |
