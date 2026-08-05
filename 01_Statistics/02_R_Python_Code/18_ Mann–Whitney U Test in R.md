# 🧪 Mann–Whitney U Test (Wilcoxon Rank-Sum Test) in R

> **Data Analysis for Life Science**

The **Mann–Whitney U Test** (also called the **Wilcoxon Rank-Sum Test**) is the **non-parametric alternative** to the **Independent Two-Sample t-test**.

Instead of comparing **means**, it compares the **distributions (or medians when distributions have similar shapes)** of **two independent groups**.

---

# 📚 Table of Contents

1. Purpose
2. Why Use the Mann–Whitney U Test?
3. When to Use
4. Parametric vs Non-Parametric
5. Data Requirements
6. Assumptions
7. Hypotheses
8. How the Test Works
9. Example Dataset
10. Step 1 – Enter the Data
11. Step 2 – Explore the Data
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

The **Mann–Whitney U Test** compares **two independent groups** when the data are **not normally distributed**.

It is commonly used instead of the Independent Two-Sample t-test.

---

# 🤔 Why Use the Mann–Whitney U Test?

The Independent t-test assumes that the data are approximately **normally distributed**.

If the data are:

- Skewed
- Contain outliers
- Ordinal
- Not normally distributed

the Mann–Whitney U Test is a better choice.

---

# 📌 When to Use

Use this test when:

- ✅ Two independent groups
- ✅ Continuous or ordinal data
- ✅ Data are not normally distributed
- ✅ Groups are unrelated

---

## Examples

- Drug vs Placebo
- Male vs Female
- Healthy vs Diseased
- Treatment A vs Treatment B

---

# ⚖️ Parametric vs Non-Parametric

| Parametric | Non-Parametric |
|------------|----------------|
| Independent Two-Sample t-test | ✅ Mann–Whitney U Test |
| Tests means | Tests distributions (or medians if distributions have similar shapes) |
| Requires normality | No normality assumption |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Groups | Two |
| Relationship | Independent |
| Outcome | Continuous or Ordinal |

---

# 📋 Assumptions

The Mann–Whitney U Test assumes:

- Independent observations
- Independent groups
- Continuous or ordinal data
- Similar distribution shapes if comparing medians

Unlike the t-test:

- ❌ Normality is **not required**

---

# 🧪 Hypotheses

Example:

Compare blood pressure between Drug and Placebo groups.

### Null Hypothesis

\[
H_0:
\]

The two groups come from the same distribution (no difference).

---

### Alternative Hypothesis

\[
H_1:
\]

The two groups come from different distributions.

---

# 🧠 How the Test Works

Unlike the Independent t-test, the Mann–Whitney U Test **does not compare means**.

Instead it:

1. Combines both groups.
2. Ranks every observation.
3. Gives the smallest value Rank = 1.
4. Adds the ranks for each group.
5. Calculates the **U statistic**.
6. Computes the p-value.

The more separated the rank sums are, the stronger the evidence that the groups differ.

---

## Example Ranking

| Value | Group | Rank |
|------:|-------|----:|
|131|Placebo|1|
|132|Placebo|2|
|134|Drug|3|
|135|Drug|4.5|
|135|Placebo|4.5|
|136|Drug|6|
|138|Drug|8|
|138|Placebo|8|
|138|Drug|8|
|139|Placebo|10|
|141|Drug|11.5|
|141|Placebo|11.5|
|142|Placebo|13|
|143|Drug|14.5|
|143|Placebo|14.5|
|144|Drug|16.5|
|144|Placebo|16.5|
|148|Drug|18|

The test compares the **sum of ranks**, not the raw values.

---

# 📂 Example Dataset

```r
Drug <- c(
138,141,143,148,135,
136,144,138,134,141
)

Placebo <- c(
142,139,144,138,143,
135,131,135,141,132
)
```

---

# 💻 Step 1 – Enter the Data

```r
Drug <- c(
138,141,143,148,135,
136,144,138,134,141
)

Placebo <- c(
142,139,144,138,143,
135,131,135,141,132
)
```

---

# 💻 Step 2 – Explore the Data

Summary

```r
summary(Drug)

summary(Placebo)
```

Median

```r
median(Drug)

median(Placebo)
```

Boxplots

```r
boxplot(
Drug,
Placebo,
names=c("Drug","Placebo")
)
```

---

# 💻 Step 3 – Run the Test

```r
wilcox.test(
Drug,
Placebo,
exact=FALSE,
correct=FALSE
)
```

---

## One-Tailed Tests

Drug > Placebo

```r
wilcox.test(
Drug,
Placebo,
alternative="greater"
)
```

Drug < Placebo

```r
wilcox.test(
Drug,
Placebo,
alternative="less"
)
```

---

# 📊 Example Output

```text
Wilcoxon rank sum test

W = 41

p-value = 0.49
```

---

# 🔍 Understanding the Output

## W

The Wilcoxon rank-sum statistic.

(Some textbooks report **U** instead of **W**.)

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
p = 0.49
```

Since

```text
0.49 > 0.05
```

Do not reject the null hypothesis.

Conclusion:

There is **no statistically significant difference** between the Drug and Placebo groups.

---

# 📝 Reporting Results

Example

> A Mann–Whitney U test showed no significant difference in systolic blood pressure between the Drug and Placebo groups (W = 41, p = 0.49).

---

# ⚠️ Common Mistakes

❌ Calling it a "paired" test.

The groups must be **independent**.

---

❌ Reporting means instead of medians.

---

❌ Thinking it compares means.

It compares **ranked observations** (or medians when distribution shapes are similar).

---

❌ Using it when data are normally distributed.

The Independent Two-Sample t-test is more powerful when its assumptions are satisfied.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| One sample | One-Sample Wilcoxon |
| Two independent (normal) | Independent Two-Sample t-test |
| Two independent (non-normal) | ✅ Mann–Whitney U Test |
| Two paired (non-normal) | Wilcoxon Signed-Rank Test |
| More than two independent (non-normal) | Kruskal–Wallis Test |

---

# 🌳 Decision Workflow

```text
Two groups
      │
      ▼
Independent?
      │
      ▼
Check normality
      │
 ┌────┴────┐
 │         │
 ▼         ▼
Normal?   Not normal?
 │         │
 ▼         ▼
Independent   Mann–Whitney
t-test        U Test
```

---

# ⚡ Quick R Cheat Sheet

```r
# Summary
summary(Drug)

summary(Placebo)

# Median
median(Drug)

median(Placebo)

# Boxplot
boxplot(
Drug,
Placebo
)

# Mann–Whitney U Test
wilcox.test(
Drug,
Placebo
)

# One-tailed
wilcox.test(
Drug,
Placebo,
alternative="greater"
)
```

---

# 📊 Parametric vs Non-Parametric Comparison

| Feature | Independent t-test | Mann–Whitney U |
|----------|--------------------|----------------|
| Groups | Two independent | Two independent |
| Tests | Means | Ranked observations (or medians if distributions have similar shapes) |
| Normality required | ✅ Yes | ❌ No |
| Uses raw values | ✅ Yes | ❌ No |
| Uses ranks | ❌ No | ✅ Yes |
| Robust to outliers | ❌ No | ✅ Yes |

---

# 🎯 Key Takeaways

- 🧪 The **Mann–Whitney U Test** is the **non-parametric alternative** to the Independent Two-Sample t-test.
- 📊 It compares **two independent groups**.
- 📈 It is based on **ranks rather than raw values**, making it robust to skewed data and outliers.
- ⚠️ It does **not require normally distributed data**.
- 💻 In R, use `wilcox.test(group1, group2)`.
- 🔍 If the p-value is less than 0.05, reject the null hypothesis.
