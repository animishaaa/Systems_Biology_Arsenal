# 🧪 Wilcoxon Signed-Rank Test (Paired Samples) in R

> **Data Analysis for Life Science**

The **Wilcoxon Signed-Rank Test** is the **non-parametric alternative** to the **Paired t-test**.

It compares **two related (paired) samples** when the differences are **not normally distributed**.

Instead of comparing **means**, it compares the **median of the paired differences**.

---

# 📚 Table of Contents

1. Purpose
2. Why Use the Wilcoxon Signed-Rank Test?
3. When to Use
4. Parametric vs Non-Parametric
5. Data Requirements
6. Assumptions
7. Hypotheses
8. How the Test Works
9. Example Dataset
10. Step 1 – Enter the Data
11. Step 2 – Check the Assumptions
12. Step 3 – Run the Test
13. Understanding the Output
14. Interpretation
15. Reporting Results
16. Common Mistakes
17. Related Tests
18. Decision Workflow
19. Quick R Cheat Sheet
20. Key Takeaways

---

# 🎯 Purpose

The **Wilcoxon Signed-Rank Test** compares **two related measurements**.

Each observation in one group is paired with one observation in the other group.

Typical examples include:

- Before vs After treatment
- Left eye vs Right eye
- Same patient measured twice
- Matched pairs

---

# 🤔 Why Use the Wilcoxon Signed-Rank Test?

The Paired t-test assumes that the **differences between pairs are normally distributed**.

If the paired differences are:

- Skewed
- Not normally distributed
- Contain outliers

then the **Wilcoxon Signed-Rank Test** is preferred.

---

# 📌 When to Use

Use this test when:

- ✅ Two related measurements
- ✅ Same subjects measured twice
- ✅ Matched pairs
- ✅ Continuous or ordinal data
- ✅ Differences are not normally distributed

---

## Examples

- Blood pressure before and after treatment
- Weight before and after diet
- Pain score before and after surgery
- Cholesterol before and after exercise

---

# ⚖️ Parametric vs Non-Parametric

| Parametric | Non-Parametric |
|------------|----------------|
| Paired t-test | ✅ Wilcoxon Signed-Rank Test |
| Tests mean difference | Tests median difference |
| Requires normal differences | No normality assumption |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Groups | Two |
| Relationship | Paired (Dependent) |
| Outcome | Continuous or Ordinal |

---

# 📋 Assumptions

The Wilcoxon Signed-Rank Test assumes:

- Paired observations
- Independent pairs
- Continuous or ordinal data
- Differences are approximately **symmetrical**

Unlike the Paired t-test:

- ❌ Normality is **not required**

---

# 🧪 Hypotheses

Example:

Blood pressure measured **before** and **after** treatment.

### Null Hypothesis

\[
H_0:
\]

The median difference is zero.

(No change.)

---

### Alternative Hypothesis

\[
H_1:
\]

The median difference is not zero.

(A change occurred.)

---

# 🧠 How the Test Works

Unlike the Paired t-test, the Wilcoxon Signed-Rank Test **does not compare the means**.

Instead it:

1. Calculate the difference for each pair.
2. Ignore differences equal to zero.
3. Take the absolute value of each difference.
4. Rank the absolute differences.
5. Give each rank the original positive (+) or negative (−) sign.
6. Sum all positive ranks.
7. Sum all negative ranks.
8. The smaller rank sum becomes the test statistic (**W**).

Because it uses **ranks**, it is more robust to outliers.

---

# 📂 Example Dataset

```r
Before <- c(
143,141,143,143,
142,143,142
)

After <- c(
139,140,138,140,
143,142,140
)
```

---

# 💻 Step 1 – Enter the Data

```r
Before <- c(
143,141,143,143,
142,143,142
)

After <- c(
139,140,138,140,
143,142,140
)
```

---

# 💻 Step 2 – Check the Assumptions

## Calculate the Differences

```r
diff <- Before - After
```

---

## Summary

```r
summary(diff)
```

---

## Histogram

```r
hist(diff)
```

---

## Boxplot

```r
boxplot(diff)
```

---

## Check Symmetry

The Wilcoxon Signed-Rank Test assumes that the paired differences are **approximately symmetrical**.

If the differences are **highly asymmetrical**, use the **Sign Test** instead.

---

# 💻 Step 3 – Run the Test

```r
wilcox.test(
Before,
After,
paired = TRUE,
exact = FALSE,
correct = FALSE
)
```

---

## One-Tailed Tests

Treatment decreases blood pressure

```r
wilcox.test(
Before,
After,
paired = TRUE,
alternative = "greater"
)
```

Treatment increases blood pressure

```r
wilcox.test(
Before,
After,
paired = TRUE,
alternative = "less"
)
```

---

# 📊 Example Output

```text
Wilcoxon signed rank test

V = 26

p-value = 0.04
```

---

# 🔍 Understanding the Output

## V

The Wilcoxon Signed-Rank statistic.

(Some books call this **W**.)

---

## p-value

Compare with α = 0.05.

If

```text
p < 0.05
```

Reject H₀.

If

```text
p ≥ 0.05
```

Do not reject H₀.

---

# 📈 Interpretation

Suppose

```text
p = 0.04
```

Since

```text
0.04 < 0.05
```

Reject the null hypothesis.

Conclusion:

There is a statistically significant difference between the **Before** and **After** measurements.

---

# 📝 Reporting Results

Example

> A Wilcoxon Signed-Rank Test showed a significant reduction in systolic blood pressure after treatment (V = 26, p = 0.04).

---

# ⚠️ Common Mistakes

❌ Using this test for independent groups.

Use the **Mann–Whitney U Test** instead.

---

❌ Forgetting `paired = TRUE`.

Without this argument, R performs the wrong test.

---

❌ Ignoring symmetry.

If the paired differences are highly asymmetrical, use the **Sign Test**.

---

❌ Reporting the mean.

The Wilcoxon Signed-Rank Test is based on the **median difference**.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| One sample | One-Sample Wilcoxon |
| Two independent | Mann–Whitney U |
| Two paired (normal) | Paired t-test |
| Two paired (non-normal) | ✅ Wilcoxon Signed-Rank Test |
| Paired, highly asymmetrical | Sign Test |

---

# 🌳 Decision Workflow

```text
Two groups
      │
      ▼
Paired?
      │
      ▼
Check normality of differences
      │
 ┌────┴────┐
 │         │
 ▼         ▼
Normal?   Not normal?
 │         │
 ▼         ▼
Paired      Wilcoxon
t-test      Signed-Rank
```

---

# ⚡ Quick R Cheat Sheet

```r
# Differences
diff <- Before - After

# Summary
summary(diff)

# Histogram
hist(diff)

# Boxplot
boxplot(diff)

# Wilcoxon Signed-Rank Test
wilcox.test(
Before,
After,
paired = TRUE
)

# One-tailed
wilcox.test(
Before,
After,
paired = TRUE,
alternative = "greater"
)
```

---

# 📊 Parametric vs Non-Parametric Comparison

| Feature | Paired t-test | Wilcoxon Signed-Rank |
|----------|---------------|----------------------|
| Groups | Two paired | Two paired |
| Tests | Mean difference | Median difference |
| Normality required | ✅ Yes | ❌ No |
| Uses raw values | ✅ Yes | ❌ No |
| Uses ranks | ❌ No | ✅ Yes |
| Robust to outliers | ❌ No | ✅ Yes |

---

# 🆚 Wilcoxon Signed-Rank vs Sign Test

| Feature | Wilcoxon Signed-Rank | Sign Test |
|----------|----------------------|-----------|
| Uses magnitude of differences | ✅ Yes | ❌ No |
| Uses ranks | ✅ Yes | ❌ No |
| Uses only + / − signs | ❌ No | ✅ Yes |
| Requires symmetry | ✅ Yes | ❌ No |
| Statistical power | Higher | Lower |

---

# 🎯 Key Takeaways

- 🧪 The **Wilcoxon Signed-Rank Test** is the **non-parametric alternative** to the Paired t-test.
- 👥 It compares **two related (paired) samples**.
- 📊 It tests whether the **median difference** between paired observations is zero.
- 📈 It uses **ranks**, making it more robust to outliers and skewed data.
- ⚠️ It assumes the paired differences are approximately **symmetrical**.
- 💻 In R, use `wilcox.test(..., paired = TRUE)`.
- 🔍 If the p-value is less than 0.05, reject the null hypothesis.
