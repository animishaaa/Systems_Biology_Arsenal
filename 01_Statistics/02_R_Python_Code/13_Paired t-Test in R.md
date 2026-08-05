# 🧪 Paired t-Test in R

> **SY768A – Data Analysis for Life Science**

The **Paired t-test** compares the **means of two related measurements** to determine whether they differ significantly.

---

# 📚 Table of Contents

1. Purpose
2. When to Use
3. Independent vs Paired Data
4. Data Requirements
5. Assumptions
6. Hypotheses
7. Example Dataset
8. Step 1 – Enter the Data
9. Step 2 – Explore the Data
10. Step 3 – Check Assumptions
11. Step 4 – Run the Paired t-Test
12. Understanding the Output
13. Reporting the Results
14. Common Mistakes
15. Related Tests
16. Decision Workflow
17. Quick R Cheat Sheet

---

# 🎯 Purpose

A **Paired t-test** compares **two related measurements**.

Instead of comparing two separate groups, it compares **the difference within each pair**.

Typical questions:

- Did blood pressure change after treatment?
- Did students improve after training?
- Is there a difference before and after exercise?

---

# 🧠 When to Use

Use a paired t-test when:

- ✅ The same subjects are measured twice.
- ✅ Measurements are naturally paired.
- ✅ The outcome variable is continuous.
- ✅ The differences are approximately normally distributed.

Examples:

| Before | After |
|---------|-------|
| Blood pressure | Blood pressure |
| Weight | Weight |
| Exam score | Exam score |

---

# 🔄 Independent vs Paired Data

## Independent Data

Different individuals in each group.

```text
Drug Group
Patient 1
Patient 2
Patient 3

Placebo Group
Patient 4
Patient 5
Patient 6
```

Use:

✅ Independent Two-Sample t-test

---

## Paired Data

The **same individuals** are measured twice.

```text
Patient 1
Before → After

Patient 2
Before → After

Patient 3
Before → After
```

Use:

✅ Paired t-test

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Number of groups | Two |
| Relationship | Paired |
| Outcome | Continuous |

---

# 📋 Assumptions

Before performing the test:

- Continuous data
- Paired observations
- Differences are approximately normal
- No serious outliers in the differences

---

# 🧪 Hypotheses

Suppose blood pressure is measured before and after treatment.

### Null Hypothesis

\[
H_0:\mu_{difference}=0
\]

No average change.

---

### Alternative Hypothesis

\[
H_1:\mu_{difference}\neq0
\]

The average change is not zero.

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

# 💻 Step 2 – Explore the Data

Calculate means:

```r
mean(Before)

mean(After)
```

Calculate SD:

```r
sd(Before)

sd(After)
```

---

## Calculate Differences

```r
diff <- Before - After

diff
```

Always inspect the differences because the paired t-test is performed on these values.

---

# 💻 Step 3 – Check Assumptions

## Histogram of Differences

```r
hist(diff)
```

---

## Q-Q Plot

```r
qqnorm(diff)

qqline(diff)
```

---

## Shapiro–Wilk Test

```r
shapiro.test(diff)
```

Interpretation:

- p > 0.05 → Differences are approximately normal
- p ≤ 0.05 → Consider the Wilcoxon Signed-Rank Test

---

# 💻 Step 4 – Run the Paired t-Test

```r
t.test(
Before,
After,
paired = TRUE
)
```

---

## One-Tailed Test

```r
t.test(
Before,
After,
paired = TRUE,
alternative = "greater"
)
```

---

# 📊 Understanding the Output

Example:

```text
Paired t-test

t = 2.79

df = 6

p-value = 0.03

95% confidence interval

0.4 to 5.3
```

---

## Test Statistic

```text
t = 2.79
```

A larger absolute t-value indicates stronger evidence against the null hypothesis.

---

## Degrees of Freedom

\[
df=n-1
\]

Example:

```text
7 observations

↓

df = 6
```

---

## P-value

```text
0.03
```

Since

```text
0.03 < 0.05
```

Reject H₀.

Blood pressure changed significantly after treatment.

---

## Confidence Interval

Suppose:

```text
0.4 to 5.3
```

Zero is **not** inside the interval.

↓

The difference is statistically significant.

---

# 📝 Reporting the Results

Example:

> A paired t-test showed that systolic blood pressure decreased significantly after treatment, *t*(6)=2.79, *p*=0.03.

---

# ⚠️ Common Mistakes

❌ Using a paired t-test for independent groups.

Use an Independent Two-Sample t-test instead.

---

❌ Checking normality of the raw data.

The assumption applies to the **differences**, not the original measurements.

---

❌ Forgetting `paired = TRUE`.

Without this argument, R performs an independent t-test.

---

❌ Pairing observations incorrectly.

Each "Before" value must correspond to the correct "After" value.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| One sample | One-Sample t-test |
| Two independent groups | Independent Two-Sample t-test |
| Two paired groups | ✅ Paired t-test |
| Paired non-normal data | Wilcoxon Signed-Rank Test |
| More than two paired measurements | Repeated-Measures ANOVA |

---

# 🌳 Decision Workflow

```text
Continuous outcome
        │
        ▼
Two measurements?
        │
        ▼
Are the measurements from
the SAME subjects?
      │        │
     YES       NO
      │        │
      ▼        ▼
Check normality  Independent t-test
of differences
      │
      ▼
Normal?
   │      │
  YES     NO
   │      │
   ▼      ▼
Paired   Wilcoxon
t-test   Signed-Rank Test
```

---

# ⚡ Quick R Cheat Sheet

| Task | R Code |
|------|--------|
| Mean | `mean(Before)` |
| SD | `sd(Before)` |
| Differences | `diff <- Before - After` |
| Histogram | `hist(diff)` |
| Q-Q plot | `qqnorm(diff)` |
| Shapiro–Wilk | `shapiro.test(diff)` |
| Paired t-test | `t.test(Before, After, paired = TRUE)` |
| One-tailed | `t.test(Before, After, paired = TRUE, alternative="greater")` |

---

# 🎯 Key Takeaways

- 🧪 Compares **two related measurements**.
- 👤 The same subjects are measured twice.
- 📊 Analyze the **differences**, not the raw measurements.
- 📈 Check normality of the **differences**.
- 💻 Always use `paired = TRUE`.
- 📉 If **p < 0.05**, reject the null hypothesis.
- 🔄 If the differences are not normally distributed, use the **Wilcoxon Signed-Rank Test**.
