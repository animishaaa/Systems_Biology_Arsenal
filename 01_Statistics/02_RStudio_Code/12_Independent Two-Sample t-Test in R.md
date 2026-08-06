# 🧪 Independent Two-Sample t-Test in R

> **Data Analysis for Life Science**

The **Independent Two-Sample t-test** compares the **means of two independent groups** to determine whether they are significantly different.

---

# 📚 Table of Contents

1. Purpose
2. When to Use
3. Data Requirements
4. Assumptions
5. Hypotheses
6. Example Dataset
7. Step 1 – Enter the Data
8. Step 2 – Explore the Data
9. Step 3 – Check Assumptions
10. Step 4 – Test Equal Variances
11. Step 5 – Run the Independent t-Test
12. Understanding the Output
13. Welch vs Student's t-test
14. Reporting the Results
15. Common Mistakes
16. Related Tests
17. Quick R Cheat Sheet

---

# 🎯 Purpose

The Independent Two-Sample t-test is used to compare the **means of two independent groups**.

It answers questions like:

- Does a drug lower blood pressure compared to placebo?
- Are males taller than females?
- Is cholesterol different between smokers and non-smokers?

---

# 🧠 When to Use

Use this test when:

- ✅ Two independent groups
- ✅ Continuous outcome variable
- ✅ Groups are unrelated
- ✅ Population SD is unknown

Examples

| Group 1 | Group 2 |
|----------|----------|
| Drug | Placebo |
| Male | Female |
| Healthy | Diseased |

---

# ❌ When NOT to Use

Do **NOT** use this test when:

- The same people are measured twice
- Data are paired
- More than two groups
- Data are highly non-normal (small sample)

Instead use:

- Paired t-test
- One-Way ANOVA
- Mann–Whitney U test

---

# 📊 Data Requirements

| Requirement | Description |
|------------|-------------|
| Groups | Two |
| Relationship | Independent |
| Outcome | Continuous |

---

# 📋 Assumptions

Before running the test, check:

- Continuous data
- Independent observations
- Approximately normal data
- Similar variances (Student's t-test only)
- No serious outliers

---

# 🧪 Hypotheses

Suppose we compare Drug vs Placebo.

### Null hypothesis

\[
H_0:\mu_1=\mu_2
\]

No difference between the means.

---

### Alternative hypothesis

\[
H_1:\mu_1\neq\mu_2
\]

The means are different.

---

# 📂 Example Dataset

```r
BP <- c(
138,141,143,148,135,
136,144,138,134,141,
142,139,144,138,143,
135,131,135,141,132
)

Group <- factor(
c(rep("Drug",10),
rep("Placebo",10))
)

df <- data.frame(BP, Group)
```

---

# 💻 Step 1 – Enter the Data

```r
BP <- c(
138,141,143,148,135,
136,144,138,134,141,
142,139,144,138,143,
135,131,135,141,132
)

Group <- factor(
c(rep("Drug",10),
rep("Placebo",10))
)

df <- data.frame(BP, Group)
```

---

# 💻 Step 2 – Explore the Data

```r
summary(df)
```

Mean per group

```r
tapply(df$BP, df$Group, mean)
```

Standard deviation

```r
tapply(df$BP, df$Group, sd)
```

Sample size

```r
table(df$Group)
```

---

# 💻 Step 3 – Check Assumptions

## Histogram

```r
hist(df$BP[df$Group=="Drug"])

hist(df$BP[df$Group=="Placebo"])
```

---

## Q-Q Plot

```r
qqnorm(df$BP[df$Group=="Drug"])
qqline(df$BP[df$Group=="Drug"])

qqnorm(df$BP[df$Group=="Placebo"])
qqline(df$BP[df$Group=="Placebo"])
```

---

## Shapiro–Wilk Test

```r
shapiro.test(df$BP[df$Group=="Drug"])

shapiro.test(df$BP[df$Group=="Placebo"])
```

Interpretation:

- p > 0.05 → approximately normal
- p ≤ 0.05 → evidence of non-normality

---

# 💻 Step 4 – Test Equal Variances

Student's t-test assumes equal variances.

Use Levene's Test.

```r
library(car)

leveneTest(BP ~ Group,
           data=df,
           center=mean)
```

Interpretation

- p > 0.05 → Equal variances
- p ≤ 0.05 → Unequal variances

---

# 💻 Step 5 – Run the Independent t-Test

## Default (Welch)

```r
t.test(BP ~ Group,
       data=df)
```

Welch's t-test **does not assume equal variances**.

---

## Student's t-test

Use only when Levene's test indicates equal variances.

```r
t.test(BP ~ Group,
       data=df,
       var.equal=TRUE)
```

---

# 📊 Understanding the Output

Example

```text
Welch Two Sample t-test

t = 0.89

df = 17.97

p-value = 0.38

95% CI

-2.8 to 7.1
```

---

## Interpretation

### Test statistic

```text
t = 0.89
```

Small t-value

↓

Small difference between groups

---

### Degrees of freedom

```text
17.97
```

Welch's test estimates the degrees of freedom.

Student's test gives:

```text
n₁+n₂−2
```

---

### P-value

```text
0.38
```

Since

```text
0.38 > 0.05
```

Do **not** reject H₀.

No evidence that the means differ.

---

### Confidence Interval

Suppose

```text
-2.8 to 7.1
```

Because zero lies inside the interval

↓

No significant difference.

Remember

✅ CI contains 0

↓

Not significant

---

# ⚖️ Welch vs Student's t-test

## Welch's t-test

```r
t.test(BP ~ Group)
```

- Default in R
- Unequal variances allowed
- Usually recommended

---

## Student's t-test

```r
t.test(
BP ~ Group,
var.equal=TRUE
)
```

Requires:

- Equal variances

Always perform Levene's Test first.

---

# 📝 Reporting the Results

Example

> An independent two-sample t-test showed **no significant difference** in systolic blood pressure between the Drug and Placebo groups, *t*(17.97)=0.89, *p*=0.38.

---

Example (significant)

> An independent two-sample t-test showed that systolic blood pressure was significantly lower in the Drug group than the Placebo group, *t*(18)=2.64, *p*=0.017.

---

# ⚠️ Common Mistakes

❌ Using paired data

Use a Paired t-test.

---

❌ Ignoring normality

Always check:

- Histogram
- Q-Q plot
- Shapiro–Wilk

---

❌ Ignoring equal variances

Run Levene's Test.

---

❌ Using Student's t-test without checking variances

Prefer Welch's test unless equal variances are supported.

---

❌ Confusing independent and paired groups

Independent:

Different people

Paired:

Same people

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| One sample | One-Sample t-test |
| Two independent groups | ✅ Independent Two-Sample t-test |
| Two paired groups | Paired t-test |
| >2 independent groups | One-Way ANOVA |
| Two independent non-normal groups | Mann–Whitney U |

---

# ⚡ Quick R Cheat Sheet

| Task | R Code |
|------|--------|
| Mean by group | `tapply(BP, Group, mean)` |
| SD by group | `tapply(BP, Group, sd)` |
| Sample size | `table(Group)` |
| Histogram | `hist()` |
| Q-Q plot | `qqnorm(); qqline()` |
| Shapiro test | `shapiro.test()` |
| Levene's test | `leveneTest()` |
| Welch t-test | `t.test(BP ~ Group)` |
| Student's t-test | `t.test(BP ~ Group, var.equal=TRUE)` |

---

# 🎯 Key Takeaways

- 🧪 Compares the means of **two independent groups**.
- 📊 Outcome variable must be **continuous**.
- 📈 Check **normality** before running the test.
- ⚖️ Check **equal variances** using Levene's Test.
- 💻 R uses **Welch's t-test by default**.
- 📉 If **p < 0.05**, reject the null hypothesis.
- 📋 If the **95% CI contains 0**, there is no significant difference.
