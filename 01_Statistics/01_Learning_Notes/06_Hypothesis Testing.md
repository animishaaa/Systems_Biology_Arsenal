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
