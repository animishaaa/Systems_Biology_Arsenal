# 📊 Descriptive Statistics in R

This section demonstrates how to calculate **descriptive statistics** in R using a simple dataset containing **sex** and **weight**.

---

# 📝 Step 1: Create the Dataset

```r
sex <- c("M", "F", "M", "F", "M", "M", "F", "M", "M", "M")
sex <- factor(sex)

weight <- c(80, 90, 65, 101, 88, 71, 86, 98, 66, 87)

df <- data.frame(sex, weight)
```

### 📋 Dataset

| Sex | Weight |
|------|--------|
| M | 80 |
| F | 90 |
| M | 65 |
| F | 101 |
| M | 88 |
| M | 71 |
| F | 86 |
| M | 98 |
| M | 66 |
| M | 87 |

---

# 📈 Summary Statistics

```r
summary(df)
```

### ✅ Output

```
 sex       weight
 F:3   Min.   : 65.00
 M:7   1st Qu.: 73.25
       Median : 86.50
       Mean   : 83.20
       3rd Qu.: 89.50
       Max.   :101.00
```

### 💡 Interpretation

- 👨 Males = **7**
- 👩 Females = **3**
- ⚖️ Mean Weight = **83.2 kg**
- 📍 Median = **86.5 kg**
- ⬇️ Minimum = **65 kg**
- ⬆️ Maximum = **101 kg**

---

# 👩 Summary Statistics for Females Only

```r
summary(df$weight[df$sex == "F"])
```

### ✅ Output

```
Min.    : 86
1st Qu. : 88
Median  : 90
Mean    : 92.33
3rd Qu. : 95.50
Max.    :101
```

---

# 👥 Group-wise Summary Using `tapply()`

## 📌 Weight Summary by Sex

```r
tapply(df$weight, df$sex, summary)
```

### ✅ Output

### 👩 Female

```
Min.    : 86
1st Qu. : 88
Median  : 90
Mean    : 92.33
3rd Qu. : 95.50
Max.    :101
```

### 👨 Male

```
Min.    : 65
1st Qu. : 68.50
Median  : 80
Mean    : 79.29
3rd Qu. : 87.50
Max.    : 98
```

### 💡 Observation

- 👩 Females have a **higher average weight (92.33 kg)**.
- 👨 Males have a **lower average weight (79.29 kg)**.

---

# 📊 Basic Statistical Functions

## Mean

```r
mean(df$weight)
```

```
83.2
```

---

## Median

```r
median(df$weight)
```

```
86.5
```

---

## Minimum

```r
min(df$weight)
```

```
65
```

---

## Maximum

```r
max(df$weight)
```

```
101
```

---

## Quantiles

```r
quantile(df$weight)
```

### ✅ Output

```
0%    25%    50%    75%    100%
65.00 73.25 86.50 89.50 101.00
```

---

## Interquartile Range (IQR)

```r
IQR(df$weight)
```

```
16.25
```

### 💡 What is IQR?

IQR measures the spread of the **middle 50%** of the data.

**Formula**

```
IQR = Q3 - Q1
```

```
89.50 - 73.25 = 16.25
```

---

# 📊 Frequency and Proportion

## Frequency Table

```r
my_table <- table(df$weight)

my_table
```

### ✅ Output

```
65 66 71 80 86 87 88 90 98 101
 1  1  1  1  1  1  1  1  1   1
```

Each weight appears **once**.

---

## ❌ Common Mistake

```r
prop. table(my_table)
```

```
Error: unexpected symbol
```

The function name is **`prop.table()`**, not `prop. table()`.

---

## Proportion Table

```r
prop.table(my_table)
```

### ✅ Output

```
65 66 71 80 86 87 88 90 98 101

0.1 0.1 0.1 0.1 0.1 0.1 0.1 0.1 0.1 0.1
```

### 💡 Interpretation

Each weight represents

```
1 / 10 = 0.1 = 10%
```

---

# 📌 Margin Table

## Total Count

```r
margin.table(my_table)
```

### Output

```
10
```

There are **10 observations**.

---

## Margin by Dimension

```r
margin.table(my_table, 1)
```

### Output

```
65 66 71 80 86 87 88 90 98 101

1  1  1  1  1  1  1  1  1   1
```

---

# 📏 Standard Deviation (SD)

## Overall SD

```r
sd(df$weight)
```

### Output

```
12.53262
```

### 💡 Interpretation

The weights vary by approximately **12.53 kg** from the mean.

---

## SD by Sex

```r
tapply(df$weight, df$sex, sd)
```

### Output

```
F  7.767453
M 12.486183
```

### 📊 Interpretation

- 👩 Female weights are **less variable**.
- 👨 Male weights are **more spread out**.

---

# 📐 Standard Error (SE)

Standard Error estimates how accurately the **sample mean** represents the **population mean**.

### Formula

\[
SE = \frac{SD}{\sqrt{n}}
\]

---

## R Code

```r
n <- 10
SD <- sd(df$weight)

SE <- SD / sqrt(n)

SE
```

### Output

```
3.963164
```

### 💡 Interpretation

The sample mean is expected to vary by about **3.96 kg** from the true population mean.

---

# 📚 Summary of Functions

| Function | Purpose |
|----------|---------|
| `summary()` | Overall descriptive statistics |
| `mean()` | Average |
| `median()` | Middle value |
| `min()` | Minimum value |
| `max()` | Maximum value |
| `quantile()` | Quartiles |
| `IQR()` | Interquartile Range |
| `table()` | Frequency table |
| `prop.table()` | Relative frequency (proportion) |
| `margin.table()` | Total frequency |
| `sd()` | Standard deviation |
| `tapply()` | Apply a function to groups |
| `sqrt()` | Square root |
| `SE = SD/sqrt(n)` | Standard error |

---

# 🎯 Key Takeaways

- 📊 `summary()` provides a quick overview of your data.
- 👥 `tapply()` is useful for calculating statistics by groups.
- 📈 `mean()` and `median()` describe the center of the data.
- 📉 `sd()` measures variability.
- 📏 `IQR()` measures the spread of the middle 50% of the data.
- 🔢 `table()` and `prop.table()` summarize frequencies and proportions.
- 📐 Standard Error (SE) estimates the precision of the sample mean.
