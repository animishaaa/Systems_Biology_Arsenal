# ➕ Sign Test in R

> **Data Analysis for Life Science**

The **Sign Test** is the **simplest non-parametric test for paired data**.

It is used when the assumptions of the **Wilcoxon Signed-Rank Test** are **not met**, particularly when the paired differences are **not symmetrical**.

Unlike the Wilcoxon Signed-Rank Test, the Sign Test **completely ignores the size of the differences** and only considers whether each difference is **positive (+)** or **negative (−)**.

---

# 📚 Table of Contents

1. Purpose
2. Why Use the Sign Test?
3. When to Use
4. Parametric vs Non-Parametric
5. Data Requirements
6. Assumptions
7. Hypotheses
8. How the Test Works
9. Example Dataset
10. Step 1 – Enter the Data
11. Step 2 – Calculate the Signs
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

The **Sign Test** compares **two paired measurements**.

Instead of measuring **how much** the values changed, it only asks:

> **Did the value increase or decrease?**

---

# 🤔 Why Use the Sign Test?

Suppose we measure blood pressure before and after treatment.

| Patient | Before | After |
|---------|--------|-------|
|1|145|140|
|2|150|149|
|3|142|138|

Wilcoxon asks:

> "How large are the differences?"

The Sign Test asks:

> "Did blood pressure go up or down?"

It ignores the size of the change.

---

# 📌 When to Use

Use the Sign Test when:

- ✅ Two paired measurements
- ✅ Differences are **not symmetrical**
- ✅ Continuous or ordinal data
- ✅ Wilcoxon assumptions are violated

---

## Examples

- Before vs After treatment
- Weight before and after dieting
- Pain score before and after surgery
- Matched pairs

---

# ⚖️ Parametric vs Non-Parametric

| Parametric | Non-Parametric |
|------------|----------------|
| Paired t-test | Wilcoxon Signed-Rank |
| Wilcoxon assumptions violated | ✅ Sign Test |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Groups | Two |
| Relationship | Paired |
| Outcome | Continuous or Ordinal |

---

# 📋 Assumptions

The Sign Test assumes:

- Paired observations
- Independent pairs
- Continuous or ordinal data

Unlike the Wilcoxon Signed-Rank Test:

- ❌ No symmetry assumption
- ❌ No normality assumption

---

# 🧪 Hypotheses

Example:

Before vs After treatment

### Null Hypothesis

\[
H_0:
\]

Positive and negative differences occur equally often.

---

### Alternative Hypothesis

\[
H_1:
\]

Positive and negative differences do not occur equally often.

---

# 🧠 How the Test Works

Instead of ranking differences, the Sign Test simply looks at whether each difference is:

- Positive (+)
- Negative (−)
- Zero (ignored)

---

## Example

| Before | After | Difference | Sign |
|---------|--------|-----------|------|
|145|140|+5|+|
|150|149|+1|+|
|142|145|-3|-|
|138|136|+2|+|
|140|140|0|Ignored|

Result:

```text
Positive = 3

Negative = 1
```

The test asks:

> Is **3 vs 1** different enough that it probably didn't happen by chance?

---

# 📂 Example Dataset

```r
Before <- c(
145,150,142,
138,140,141,144
)

After <- c(
140,149,145,
136,140,142,146
)
```

---

# 💻 Step 1 – Enter the Data

```r
Before <- c(
145,150,142,
138,140,141,144
)

After <- c(
140,149,145,
136,140,142,146
)
```

---

# 💻 Step 2 – Calculate the Signs

Calculate the differences

```r
diff <- Before - After
```

View them

```r
diff
```

Convert to signs

```r
sign(diff)
```

Positive differences

```r
sum(diff > 0)
```

Negative differences

```r
sum(diff < 0)
```

---

# 💻 Step 3 – Run the Test

The Sign Test is performed using the **binomial test**.

```r
binom.test(
x = 3,
n = 4
)
```

Where:

- `x` = number of positive signs
- `n` = total non-zero differences

---

# 📊 Example Output

```text
Exact binomial test

p-value = 0.63
```

---

# 🔍 Understanding the Output

The Sign Test does **not** produce:

- t
- U
- W
- χ²

Instead, it produces only a **binomial p-value**.

---

# 📈 Interpretation

Suppose

```text
Positive = 3

Negative = 1

p = 0.63
```

Since

```text
0.63 > 0.05
```

Do not reject H₀.

Conclusion:

There is **no statistically significant difference** between the paired measurements.

---

# 📝 Reporting Results

Example

> A Sign Test showed no significant difference between blood pressure before and after treatment (p = 0.63).

---

# ⚠️ Common Mistakes

❌ Using the Sign Test when the Wilcoxon Signed-Rank Test is appropriate.

The Wilcoxon test has **greater statistical power**.

---

❌ Forgetting to remove zero differences.

Zero differences are ignored.

---

❌ Thinking the Sign Test uses the size of the differences.

It only counts **positive** and **negative** signs.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| One sample | One-Sample Wilcoxon |
| Two independent | Mann–Whitney U |
| Two paired (normal) | Paired t-test |
| Two paired (non-normal, symmetrical) | Wilcoxon Signed-Rank |
| Two paired (non-symmetrical) | ✅ Sign Test |

---

# 🌳 Decision Workflow

```text
Two paired groups
        │
        ▼
Check symmetry
        │
 ┌──────┴──────┐
 │             │
 ▼             ▼
Symmetrical?  Not symmetrical?
 │             │
 ▼             ▼
Wilcoxon      Sign Test
Signed-Rank
```

---

# ⚡ Quick R Cheat Sheet

```r
# Differences
diff <- Before - After

# Signs
sign(diff)

# Positive signs
sum(diff > 0)

# Negative signs
sum(diff < 0)

# Sign Test
binom.test(
x = 3,
n = 4
)
```

---

# 📊 Wilcoxon Signed-Rank vs Sign Test

| Feature | Wilcoxon Signed-Rank | Sign Test |
|----------|----------------------|-----------|
| Uses differences | ✅ Yes | ❌ No |
| Uses ranks | ✅ Yes | ❌ No |
| Uses only signs | ❌ No | ✅ Yes |
| Symmetry required | ✅ Yes | ❌ No |
| Statistical power | Higher | Lower |
| Preferred when possible | ✅ Yes | ❌ No |

---

# 🎯 Key Takeaways

- ➕ The **Sign Test** is the simplest non-parametric test for paired data.
- 📊 It only counts **positive (+)** and **negative (−)** differences.
- 📈 It ignores the magnitude of the differences.
- ⚠️ It is used when the **Wilcoxon Signed-Rank Test assumptions are not satisfied**, especially when the paired differences are not symmetrical.
- 💻 In R, the Sign Test is performed using `binom.test()`.
- 🔍 If the p-value is less than 0.05, reject the null hypothesis.
