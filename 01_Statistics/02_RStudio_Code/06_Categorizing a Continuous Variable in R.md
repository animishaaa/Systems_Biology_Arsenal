# 📊 Categorizing a Continuous Variable in R

Sometimes, a **continuous variable** (e.g., weight, height, age) is converted into **categories** to simplify statistical analysis or data visualization.

In this example, we will convert the continuous variable **Weight** into three categories:

- 🟢 Low Weight
- 🟡 Medium Weight
- 🔴 High Weight

---

# 📝 Step 1: Create the Dataset

```r
sex <- c("M", "F", "F", "F", "M", "M", "F", "M", "F", "M")
sex <- factor(sex)

weight <- c(80, 58, 65, 70, 90, 100, 50, 91, 75, 87)

df <- data.frame(sex, weight)
```

### 📋 Dataset

| ID | Sex | Weight |
|---:|:---:|-------:|
|1|M|80|
|2|F|58|
|3|F|65|
|4|F|70|
|5|M|90|
|6|M|100|
|7|F|50|
|8|M|91|
|9|F|75|
|10|M|87|

---

# 🎯 Step 2: Create a New Variable

We will create a new variable called **Weight_group**.

Initially, we classify only individuals whose weight is **less than 59.9 kg**.

```r
df$Weight_group[df$weight < 59.9] <- "low_weight"
```

### 💡 Explanation

This command checks every value in the **weight** column.

If the weight is **less than 59.9 kg**, the corresponding value in **Weight_group** becomes:

```text
low_weight
```

All remaining observations are temporarily assigned:

```text
<NA>
```

---

# 📊 Output

| Sex | Weight | Weight_group |
|:---:|-------:|:-------------|
|M|80|NA|
|F|58|low_weight|
|F|65|NA|
|F|70|NA|
|M|90|NA|
|M|100|NA|
|F|50|low_weight|
|M|91|NA|
|F|75|NA|
|M|87|NA|

---

# 🎯 Step 3: Assign Medium and High Weight Categories

Next, classify the remaining observations.

```r
df$Weight_group[df$weight > 59.9 & df$weight < 79.9] <- "medium_weight"

df$Weight_group[df$weight > 79.9] <- "high_weight"
```

### 📌 Classification Rules

| Weight (kg) | Category |
|-------------|----------|
| < 59.9 | 🟢 low_weight |
| 59.9 – 79.9 | 🟡 medium_weight |
| > 79.9 | 🔴 high_weight |

---

# 📊 Updated Dataset

| ID | Sex | Weight | Weight_group |
|---:|:---:|-------:|:-------------|
|1|M|80|high_weight|
|2|F|58|low_weight|
|3|F|65|medium_weight|
|4|F|70|medium_weight|
|5|M|90|high_weight|
|6|M|100|high_weight|
|7|F|50|low_weight|
|8|M|91|high_weight|
|9|F|75|medium_weight|
|10|M|87|high_weight|

---

# 🧠 Understanding the Classification

Example:

- Person **1**
  - Sex = Male
  - Weight = 80 kg
  - Category = **high_weight**

Similarly,

- Weight = 58 kg → **low_weight**
- Weight = 65 kg → **medium_weight**
- Weight = 100 kg → **high_weight**

---

# 🔍 Check the Variable Type

Use the `class()` function.

```r
class(df$Weight_group)
```

### Output

```text
[1] "character"
```

### 💡 Interpretation

Currently, **Weight_group** is stored as a **character vector**, not as a categorical variable.

---

# 🔄 Convert to an Ordered Factor

Since **Weight_group** has a natural order:

```
low_weight
    ↓
medium_weight
    ↓
high_weight
```

Convert it into an **ordered factor**.

```r
df$Weight_group <- ordered(df$Weight_group)
```

---

# ✅ Check Again

```r
class(df$Weight_group)
```

### Output

```text
[1] "ordered" "factor"
```

### 💡 Interpretation

R now understands that the categories have a meaningful order.

---

# 📊 Frequency of Each Category

Use the `summary()` function.

```r
summary(df$Weight_group)
```

### Output

```text
high_weight      low_weight      medium_weight
      5                2                 3
```

### 📋 Interpretation

| Category | Frequency |
|-----------|----------:|
| 🔴 High Weight | 5 |
| 🟢 Low Weight | 2 |
| 🟡 Medium Weight | 3 |

---

# 📈 Calculate Proportions

Use:

```r
prop.table(table(df$Weight_group))
```

### Output

```text
high_weight      low_weight      medium_weight

0.5              0.2             0.3
```

### 📋 Interpretation

| Category | Proportion | Percentage |
|-----------|-----------:|-----------:|
| 🔴 High Weight | 0.5 | 50% |
| 🟢 Low Weight | 0.2 | 20% |
| 🟡 Medium Weight | 0.3 | 30% |

---

# 📚 Functions Used

| Function | Purpose |
|----------|---------|
| `data.frame()` | Create a data frame |
| `factor()` | Convert to a factor |
| `ordered()` | Create an ordered factor |
| `class()` | Check the variable type |
| `summary()` | Display category frequencies |
| `table()` | Count observations in each category |
| `prop.table()` | Calculate proportions |
| `&` | Logical AND operator |

---

# 🎯 Key Takeaways

- 📈 Continuous variables can be converted into categorical variables.
- 🏷️ Categories make statistical analysis and visualization easier.
- 🔤 A newly created category variable is usually stored as a **character**.
- 📊 Use `ordered()` when categories have a natural order.
- 📋 Use `summary()` to count observations in each category.
- 📈 Use `prop.table(table())` to calculate proportions.
- 🧮 Ordered factors are especially useful for ordinal data analysis.
