# 📊 Statistical Analysis with Python

> **Practical notes for parametric tests, non-parametric tests, categorical analysis, correlation, and regression**

These notes provide a compact workflow for statistical analysis in Python using **NumPy**, **Pandas**, **SciPy**, **Statsmodels**, **Matplotlib**, and **Seaborn**.

---

## 📚 Table of Contents

1. [Required libraries](#-required-libraries)
2. [Core data structures](#-core-data-structures)
3. [Descriptive statistics](#-descriptive-statistics)
4. [Choosing a statistical test](#-choosing-a-statistical-test)
5. [Parametric tests](#-parametric-tests)
6. [Categorical tests](#-categorical-tests)
7. [Non-parametric tests](#-non-parametric-tests)
8. [Correlation](#-correlation)
9. [Regression](#-regression)
10. [Regression diagnostics](#-regression-diagnostics)
11. [R-to-Python reference](#-r-to-python-reference)
12. [Common mistakes](#-common-mistakes)
13. [Key takeaways](#-key-takeaways)

---

## 📥 Required Libraries

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

from scipy import stats
import statsmodels.api as sm
import statsmodels.formula.api as smf
```

Additional functions used later:

```python
from scipy.stats import f_oneway
from statsmodels.stats.anova import AnovaRM
from statsmodels.stats.contingency_tables import mcnemar
from statsmodels.stats.multicomp import pairwise_tukeyhsd
from statsmodels.stats.outliers_influence import variance_inflation_factor
```

| Statistical task | Main Python package |
|---|---|
| Numeric arrays | NumPy |
| Data frames | Pandas |
| Plots | Matplotlib / Seaborn |
| Classical hypothesis tests | SciPy |
| Regression and ANOVA | Statsmodels |

---

## 🧱 Core Data Structures

### NumPy array

```python
weights = np.array([80, 58, 65, 70, 90])
```

```python
weights[2]            # third value
np.mean(weights)      # mean
np.sum(weights)       # sum
len(weights)          # number of values
```

Append and remove values:

```python
weights = np.append(weights, 85)
weights = np.delete(weights, 4)
```

### Matrix

```python
sex = np.array([1, 2, 2, 2, 1, 1, 2, 1, 2, 1])
weight = np.array([80, 58, 65, 70, 90, 100, 50, 91, 75, 87])

matrix = np.column_stack((sex, weight))
```

```python
matrix[3]       # fourth row
matrix[3, 1]    # value in fourth row, second column
matrix[:, 1]    # second column
```

### Pandas DataFrame

```python
df = pd.DataFrame({
    "Sex": ["M", "F", "F", "F", "M", "M", "F", "M", "F", "M"],
    "Weight": [80, 58, 65, 70, 90, 100, 50, 91, 75, 87]
})
```

```python
df["Weight"]
df["Sex"]
df.head()
df.info()
```

---

## 📈 Descriptive Statistics

```python
df.describe()
```

```python
mean_weight = df["Weight"].mean()
median_weight = df["Weight"].median()
sd_weight = df["Weight"].std()
```

Standard error:

```python
n = len(df)
se_weight = sd_weight / np.sqrt(n)
```

> [!NOTE]
> Pandas `.std()` uses the sample standard deviation by default. With NumPy, specify `ddof=1` to obtain the sample standard deviation.

```python
np.std(df["Weight"], ddof=1)
```

---

## 🧭 Choosing a Statistical Test

| Research question | Data structure | Recommended test |
|---|---|---|
| Compare one sample with a reference value | One numeric sample | One-sample t-test |
| Compare two independent groups | Two independent numeric samples | Welch's t-test |
| Compare two paired measurements | Paired numeric measurements | Paired t-test |
| Compare three or more independent groups | Numeric outcome, independent groups | One-way ANOVA |
| Compare three or more repeated conditions | Numeric repeated measurements | Repeated-measures ANOVA |
| Association between two categorical variables | Contingency table | Chi-square independence test |
| Compare observed and expected category counts | One categorical variable | Chi-square goodness-of-fit |
| Paired binary outcomes | Matched 2 × 2 table | McNemar's test |
| Non-normal independent groups | Two independent samples | Mann-Whitney U |
| Non-normal paired measurements | Two paired samples | Wilcoxon signed-rank |
| Non-normal data across three or more independent groups | Independent groups | Kruskal-Wallis |
| Non-normal repeated measurements | Repeated groups | Friedman test |
| Linear association | Two continuous variables | Pearson correlation |
| Monotonic or ordinal association | Numeric or ordinal variables | Spearman correlation |

---

# 🧪 Parametric Tests

## One-Sample t-Test

Use when one numeric sample is compared with a known or hypothesized population mean.

```python
sb = np.array([
    142, 142, 144, 140, 141,
    140, 142, 148, 140, 137,
    144, 138, 142, 139, 144,
    144, 141, 134, 143, 148
])

result = stats.ttest_1samp(
    sb,
    popmean=140
)

print("t statistic:", result.statistic)
print("p-value:", result.pvalue)
```

One-sided alternative:

```python
result = stats.ttest_1samp(
    sb,
    popmean=140,
    alternative="greater"
)
```

### Hypotheses

- **H₀:** population mean = 140
- **H₁:** population mean ≠ 140, unless a directional alternative is specified

---

## Independent Two-Sample t-Test

```python
drug = np.array([138, 141, 143, 148, 135, 136, 144, 138, 134, 141])
placebo = np.array([142, 139, 144, 138, 143, 135, 131, 135, 141, 132])

result = stats.ttest_ind(
    drug,
    placebo,
    equal_var=False
)

print(result)
```

`equal_var=False` performs **Welch's t-test**, which does not assume equal population variances.

Optional variance check:

```python
levene_result = stats.levene(drug, placebo)
print(levene_result)
```

---

## Paired t-Test

Use when the same subjects are measured twice or observations are naturally matched.

```python
before = np.array([143, 141, 143, 143, 142, 143, 142])
after = np.array([139, 140, 138, 140, 143, 142, 140])

result = stats.ttest_rel(before, after)
print(result)
```

Check normality of the paired differences:

```python
differences = before - after
stats.shapiro(differences)
```

---

## One-Way ANOVA

```python
control = np.array([7, 8, 10, 11])
neurohib = np.array([4, 5, 7, 8])
mitostop = np.array([1, 2, 4, 5])

result = stats.f_oneway(
    control,
    neurohib,
    mitostop
)

print(result)
```

For a full ANOVA table:

```python
anova_df = pd.DataFrame({
    "response": [7, 8, 10, 11, 4, 5, 7, 8, 1, 2, 4, 5],
    "group": [
        "Control", "Control", "Control", "Control",
        "Neurohib", "Neurohib", "Neurohib", "Neurohib",
        "Mitostop", "Mitostop", "Mitostop", "Mitostop"
    ]
})

model = smf.ols("response ~ C(group)", data=anova_df).fit()
anova_table = sm.stats.anova_lm(model, typ=2)

print(anova_table)
```

### Tukey post-hoc test

Run a post-hoc test after a significant omnibus ANOVA to identify which groups differ.

```python
posthoc = pairwise_tukeyhsd(
    endog=anova_df["response"],
    groups=anova_df["group"]
)

print(posthoc)
```

---

## Repeated-Measures ANOVA

```python
rm_df = pd.DataFrame({
    "subject": [1, 2, 3, 4] * 3,
    "condition": (
        ["Before"] * 4
        + ["DrugA"] * 4
        + ["DrugB"] * 4
    ),
    "response": [
        64, 77, 63, 71,
        81, 82, 77, 80,
        79, 76, 78, 76
    ]
})

result = AnovaRM(
    data=rm_df,
    depvar="response",
    subject="subject",
    within=["condition"]
).fit()

print(result)
```

---

# 📦 Categorical Tests

## Chi-Square Test of Independence

```python
table = np.array([
    [35, 15],
    [20, 30]
])

chi2, p_value, dof, expected = stats.chi2_contingency(
    table,
    correction=False
)

print("Chi-square:", chi2)
print("p-value:", p_value)
print("Degrees of freedom:", dof)
print("Expected frequencies:\n", expected)
```

### Hypotheses

- **H₀:** the categorical variables are independent
- **H₁:** the categorical variables are associated

---

## Chi-Square Goodness-of-Fit

```python
observed = np.array([4, 10, 6])
expected = np.array([5, 10, 5])

result = stats.chisquare(
    f_obs=observed,
    f_exp=expected
)

print(result)
```

Expected probabilities can also be converted to counts:

```python
expected_probabilities = np.array([0.25, 0.50, 0.25])
expected_counts = expected_probabilities * observed.sum()

stats.chisquare(observed, f_exp=expected_counts)
```

---

## Fisher's Exact Test

Useful for a small 2 × 2 contingency table.

```python
table = np.array([
    [8, 2],
    [3, 7]
])

result = stats.fisher_exact(table)

print("Odds ratio:", result.statistic)
print("p-value:", result.pvalue)
```

---

## McNemar's Test

Use for paired binary outcomes.

```python
table = [
    [20, 10],
    [5, 15]
]

result = mcnemar(
    table,
    exact=False,
    correction=False
)

print(result)
```

---

# 📉 Non-Parametric Tests

## One-Sample Wilcoxon Signed-Rank Test

Compare a sample median with a reference value by testing the differences from that value.

```python
result = stats.wilcoxon(sb - 140)
print(result)
```

---

## Mann-Whitney U Test

Non-parametric alternative to the independent two-sample t-test.

```python
result = stats.mannwhitneyu(
    drug,
    placebo,
    alternative="two-sided"
)

print(result)
```

---

## Wilcoxon Signed-Rank Test

Non-parametric alternative to the paired t-test.

```python
result = stats.wilcoxon(
    before,
    after,
    alternative="two-sided"
)

print(result)
```

---

## Sign Test

A simple paired test based only on the direction of non-zero differences.

```python
differences = before - after
non_zero = differences[differences != 0]

positive = np.sum(non_zero > 0)
n = len(non_zero)

result = stats.binomtest(
    positive,
    n=n,
    p=0.5
)

print(result)
```

> [!IMPORTANT]
> Use `stats.binomtest()`. The older `stats.binom_test()` function has been replaced in current SciPy versions.

---

## Kruskal-Wallis Test

Non-parametric alternative to one-way ANOVA.

```python
result = stats.kruskal(
    control,
    neurohib,
    mitostop
)

print(result)
```

---

## Friedman Test

Non-parametric alternative to repeated-measures ANOVA.

```python
before_rm = np.array([64, 77, 63, 71])
drug_a = np.array([81, 82, 77, 80])
drug_b = np.array([79, 76, 78, 76])

result = stats.friedmanchisquare(
    before_rm,
    drug_a,
    drug_b
)

print(result)
```

---

# 📈 Correlation

## Pearson Correlation

Use for a linear relationship between two continuous variables.

```python
weight = np.array([55, 60, 63, 65, 68, 70, 73, 75, 78, 82])
cholesterol = np.array([3.8, 4.0, 4.2, 4.3, 4.5, 4.8, 5.0, 5.2, 5.4, 5.7])

result = stats.pearsonr(weight, cholesterol)

print("r:", result.statistic)
print("p-value:", result.pvalue)
```

## Spearman Correlation

Use for monotonic relationships, ordinal data, or data that do not meet Pearson assumptions.

```python
result = stats.spearmanr(weight, cholesterol)

print("rho:", result.statistic)
print("p-value:", result.pvalue)
```

> [!CAUTION]
> Correlation does not establish causation.

---

# 📉 Regression

## Simple Linear Regression

```python
regression_df = pd.DataFrame({
    "Weight": weight,
    "Cholesterol": cholesterol
})

model = smf.ols(
    "Cholesterol ~ Weight",
    data=regression_df
).fit()

print(model.summary())
```

Regression plot:

```python
plt.scatter(
    regression_df["Weight"],
    regression_df["Cholesterol"]
)

plt.plot(
    regression_df["Weight"],
    model.predict(regression_df)
)

plt.xlabel("Weight")
plt.ylabel("Cholesterol")
plt.title("Simple Linear Regression")
plt.show()
```

---

## Multiple Linear Regression

```python
multiple_df = pd.DataFrame({
    "Cholesterol": [5.1, 5.4, 4.8, 6.0, 5.7, 6.2, 4.9, 5.5, 5.8, 6.1],
    "BMI": [22, 24, 21, 28, 26, 30, 23, 25, 27, 29],
    "Smoker": ["No", "No", "No", "Yes", "Yes", "Yes", "No", "No", "Yes", "Yes"]
})

model = smf.ols(
    "Cholesterol ~ BMI + C(Smoker)",
    data=multiple_df
).fit()

print(model.summary())
```

`C(Smoker)` tells Statsmodels to treat `Smoker` as a categorical predictor.

---

# 🔍 Regression Diagnostics

## Residual Normality

```python
residuals = model.resid
stats.shapiro(residuals)
```

Residual plot:

```python
plt.scatter(model.fittedvalues, residuals)
plt.axhline(0)
plt.xlabel("Fitted values")
plt.ylabel("Residuals")
plt.title("Residuals vs Fitted Values")
plt.show()
```

## Cook's Distance

```python
influence = model.get_influence()
cooks_distance = influence.cooks_distance[0]

print(cooks_distance)
```

Cook's distance helps identify observations with strong influence on the fitted model.

## Variance Inflation Factor

VIF is used to assess multicollinearity among numeric predictors.

```python
x = multiple_df[["BMI"]].copy()
x = sm.add_constant(x)

vif = pd.DataFrame({
    "variable": x.columns,
    "VIF": [
        variance_inflation_factor(x.values, i)
        for i in range(x.shape[1])
    ]
})

print(vif)
```

For categorical predictors, encode them before calculating VIF:

```python
x = pd.get_dummies(
    multiple_df[["BMI", "Smoker"]],
    drop_first=True,
    dtype=float
)

x = sm.add_constant(x)

vif = pd.DataFrame({
    "variable": x.columns,
    "VIF": [
        variance_inflation_factor(x.values, i)
        for i in range(x.shape[1])
    ]
})
```

---

# 🔄 R-to-Python Reference

| Statistical method | R | Python |
|---|---|---|
| One-sample t-test | `t.test(x, mu=140)` | `stats.ttest_1samp(x, popmean=140)` |
| Independent t-test | `t.test(x, y)` | `stats.ttest_ind(x, y, equal_var=False)` |
| Paired t-test | `t.test(x, y, paired=TRUE)` | `stats.ttest_rel(x, y)` |
| One-way ANOVA | `aov(y ~ group)` | `stats.f_oneway(...)` or Statsmodels |
| Repeated-measures ANOVA | `aov(... + Error())` | `AnovaRM(...)` |
| Mann-Whitney U | `wilcox.test(x, y)` | `stats.mannwhitneyu(x, y)` |
| Wilcoxon paired | `wilcox.test(x, y, paired=TRUE)` | `stats.wilcoxon(x, y)` |
| Kruskal-Wallis | `kruskal.test(...)` | `stats.kruskal(...)` |
| Friedman test | `friedman.test(...)` | `stats.friedmanchisquare(...)` |
| Chi-square independence | `chisq.test(table)` | `stats.chi2_contingency(table)` |
| Chi-square goodness-of-fit | `chisq.test(obs, p=...)` | `stats.chisquare(obs, expected)` |
| Fisher exact | `fisher.test(table)` | `stats.fisher_exact(table)` |
| Pearson correlation | `cor.test(x, y)` | `stats.pearsonr(x, y)` |
| Spearman correlation | `cor.test(x, y, method="spearman")` | `stats.spearmanr(x, y)` |
| Linear regression | `lm(y ~ x)` | `smf.ols("y ~ x", data=df).fit()` |
| Multiple regression | `lm(y ~ x1 + x2)` | `smf.ols("y ~ x1 + x2", data=df).fit()` |

---

# ⚠️ Common Mistakes

### Using population standard deviation for sample data

Incorrect:

```python
np.std(data)
```

Correct:

```python
np.std(data, ddof=1)
```

### Interpreting `p < 0.05` as proof

A small p-value indicates evidence against the null hypothesis. It does not measure effect size, biological importance, or the probability that the hypothesis is true.

### Ignoring assumptions

Before selecting a test, consider:

- independence of observations
- distribution of residuals or differences
- equality of variances when relevant
- measurement scale
- paired versus independent design

### Running multiple pairwise tests without correction

Use a planned post-hoc procedure such as Tukey's test after ANOVA rather than many uncorrected t-tests.

### Applying numeric regression directly to text categories

Categorical variables must be handled using formulas such as `C(Smoker)` or encoded as dummy variables.

### Using undefined DataFrame columns

Code such as `df["Chol"]`, `df["Age"]`, or `df["BMI"]` requires those columns to exist in the current DataFrame. Define the dataset before running the analysis.

---

# ✅ Reporting Template

A statistical result should normally include:

1. the test used
2. the test statistic
3. degrees of freedom, when applicable
4. the p-value
5. an effect size and confidence interval, when available
6. a conclusion stated in the context of the research question

Example:

> Welch's independent-samples t-test was used to compare the drug and placebo groups. The analysis produced the test statistic and p-value shown by `stats.ttest_ind(..., equal_var=False)`. The result should be interpreted together with group means, uncertainty, and an appropriate effect size.

---

# 🎯 Key Takeaways

- Start every analysis with data inspection and descriptive statistics.
- Match the test to the study design, measurement scale, and assumptions.
- Use Welch's t-test as a robust default for two independent groups.
- Use paired tests only when measurements are genuinely matched.
- ANOVA tests an overall group difference; post-hoc tests locate specific differences.
- Non-parametric tests are useful when parametric assumptions are not defensible.
- Correlation quantifies association, while regression models an outcome using one or more predictors.
- Inspect residuals, influential observations, and multicollinearity before trusting a regression model.
- Report effect sizes and confidence intervals in addition to p-values whenever possible.
