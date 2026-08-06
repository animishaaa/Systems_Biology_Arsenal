# 🧪 Chi-Square Test of Independence in R

> **Data Analysis for Life Science**

The **Chi-Square Test of Independence (χ² Test)** is used to determine whether **two categorical variables are associated** or **independent**.

Unlike t-tests or ANOVA, which compare **means**, the Chi-Square Test compares **frequencies (counts)**.

---

# 📚 Table of Contents

1. Purpose
2. Why Use the Chi-Square Test?
3. When to Use
4. Data Requirements
5. Assumptions
6. Hypotheses
7. How the Test Works
8. Example Dataset
9. Step 1 – Create a Contingency Table
10. Step 2 – Run the Chi-Square Test
11. Step 3 – Check Expected Frequencies
12. Understanding the Output
13. Interpretation
14. Reporting Results
15. Common Mistakes
16. Related Tests
17. Decision Workflow
18. Quick R Cheat Sheet
19. Key Takeaways

---

# 🎯 Purpose

The **Chi-Square Test of Independence** determines whether **two categorical variables are associated**.

It answers questions like:

> **Does one categorical variable depend on another?**

---

# 🤔 Why Use the Chi-Square Test?

Sometimes we want to compare **counts** rather than **numerical values**.

Examples:

- Does **smoking** depend on **sex**?
- Does **blood type** depend on **ethnicity**?
- Does **disease status** depend on **treatment group**?
- Does **vaccine response** depend on **age group**?

Since these variables are **categorical**, we use the **Chi-Square Test of Independence**.

---

# 📌 When to Use

Use this test when:

- ✅ Both variables are categorical.
- ✅ Observations are independent.
- ✅ Data are frequencies (counts).
- ✅ You want to determine whether two variables are associated.

---

## Examples

| Variable 1 | Variable 2 |
|------------|------------|
| Sex | Smoking Status |
| Treatment | Recovery |
| Blood Type | Disease |
| Vaccine | Infection Status |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Variable 1 | Categorical |
| Variable 2 | Categorical |
| Data | Counts (frequencies) |
| Observations | Independent |

---

# 📋 Assumptions

The Chi-Square Test assumes:

- Independent observations
- Two categorical variables
- Data are frequencies (counts), **not percentages**
- Expected frequency in each cell should generally be **≥ 5**

If expected frequencies are too small:

➡️ Use **Fisher's Exact Test** instead.

---

# 🧪 Hypotheses

Example:

Does smoking depend on sex?

### Null Hypothesis

\[
H_0:
\]

Smoking status and sex are **independent**.

(No association.)

---

### Alternative Hypothesis

\[
H_1:
\]

Smoking status and sex are **associated**.

---

# 🧠 How the Test Works

The Chi-Square Test compares:

- **Observed frequencies** (what you actually measured)
- **Expected frequencies** (what you would expect if the variables were independent)

If the observed counts are very different from the expected counts, the variables are likely associated.

---

## Example

Observed data

| | Smoker | Non-Smoker |
|---|---:|---:|
| Male | 30 | 20 |
| Female | 15 | 35 |

If smoking and sex were independent, the counts would be more evenly distributed.

The Chi-Square Test measures how different the observed counts are from the expected counts.

Large differences produce a **large χ² statistic**.

---

# 📂 Example Dataset

Suppose we have a CSV file containing:

| Sex | Smoker |
|------|---------|
| Male | Yes |
| Male | No |
| Female | Yes |
| Female | No |

---

# 💻 Step 1 – Import the Data

```r
df <- read.table(
file.choose(),
header = TRUE,
sep = ";"
)
```

---

# 💻 Step 2 – Create a Contingency Table

```r
my_table <- table(
df$Sex,
df$Smoker
)
```

View the table:

```r
my_table
```

Example output:

```text
           No   Yes

Female     35   15

Male       20   30
```

---

# 💻 Step 3 – Run the Chi-Square Test

```r
chisq.test(
my_table,
correct = FALSE
)
```

---

# 💻 Step 4 – Check Expected Frequencies

```r
result <- chisq.test(
my_table,
correct = FALSE
)

result$expected
```

Example:

```text
           No    Yes

Female    27.5  22.5

Male      27.5  22.5
```

Rule:

```text
Expected frequencies should generally be ≥ 5.
```

If not:

➡️ Use **Fisher's Exact Test**.

---

# 📊 Example Output

```text
Pearson's Chi-squared test

X-squared = 8.18

df = 1

p-value = 0.004
```

---

# 🔍 Understanding the Output

## χ² Statistic

Measures how different the observed counts are from the expected counts.

Large χ²

↓

Large difference

↓

Evidence against H₀.

---

## Degrees of Freedom

For a contingency table:

```text
df = (Rows − 1) × (Columns − 1)
```

Example:

2 × 2 table

```text
df = (2 − 1) × (2 − 1)

df = 1
```

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
χ² = 8.18

p = 0.004
```

Since

```text
0.004 < 0.05
```

Reject the null hypothesis.

Conclusion:

There is a statistically significant association between **sex** and **smoking status**.

---

# 📊 Row Proportions

To calculate proportions within each row:

```r
prop.table(
my_table,
1
)
```

Example output:

```text
            No    Yes

Female     0.70  0.30

Male       0.40  0.60
```

This helps interpret the direction of the association.

---

# 📝 Reporting Results

Example

> A Chi-Square Test of Independence showed a significant association between sex and smoking status, χ²(1) = 8.18, p = 0.004.

---

# ⚠️ Common Mistakes

❌ Using percentages instead of counts.

The Chi-Square Test requires **raw frequencies**.

---

❌ Using dependent observations.

Observations must be independent.

---

❌ Ignoring expected frequencies.

If expected counts are too small:

➡️ Use **Fisher's Exact Test**.

---

❌ Thinking Chi-Square measures strength.

It only tells you whether an association exists.

(Strength can be measured using **Cramér's V**.)

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| Two categorical variables | ✅ Chi-Square Test of Independence |
| One categorical variable vs expected distribution | Chi-Square Goodness-of-Fit |
| Paired categorical data | McNemar's Test |
| Small expected counts | Fisher's Exact Test |
| Two population proportions | Two-Proportion Z-Test |

---

# 🌳 Decision Workflow

```text
Categorical data
        │
        ▼
How many variables?
        │
 ┌──────┴────────┐
 │               │
 ▼               ▼
One variable   Two variables
 │               │
 ▼               ▼
Goodness-     Independent?
of-Fit            │
                  ▼
          Expected counts ≥ 5?
                  │
           ┌──────┴──────┐
           │             │
           ▼             ▼
     Chi-Square      Fisher's
     Independence    Exact Test
```

---

# ⚡ Quick R Cheat Sheet

```r
# Import data
df <- read.table(
file.choose(),
header = TRUE,
sep = ";"
)

# Contingency table
my_table <- table(
df$Sex,
df$Smoker
)

# Chi-Square Test
chisq.test(
my_table,
correct = FALSE
)

# Expected frequencies
result <- chisq.test(
my_table,
correct = FALSE
)

result$expected

# Row proportions
prop.table(
my_table,
1
)
```

---

# 📊 Chi-Square vs Other Categorical Tests

| Situation | Test |
|------------|------|
| Two independent categorical variables | ✅ Chi-Square Independence |
| One categorical variable | Chi-Square Goodness-of-Fit |
| Paired categorical variables | McNemar's Test |
| Small expected frequencies | Fisher's Exact Test |
| Two population proportions | Two-Proportion Z-Test |

---

# 🎯 Key Takeaways

- 🧪 The **Chi-Square Test of Independence** tests whether **two categorical variables are associated**.
- 📊 It compares **observed frequencies** with **expected frequencies**.
- 📋 Both variables must be **categorical**.
- ⚠️ Expected frequencies should generally be **5 or greater**.
- 🐟 If expected counts are too small, use **Fisher's Exact Test**.
- 💻 In R, use `chisq.test()`.
- 🔍 If the p-value is less than 0.05, reject the null hypothesis and conclude that an association exists.
