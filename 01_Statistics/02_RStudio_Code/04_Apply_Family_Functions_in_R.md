# 🔟 Apply Family Functions in R

The **Apply Family** is a collection of functions in R that help you perform the **same operation repeatedly** on data without writing loops (`for` loops).

💡 These functions make your code:

- ✅ Shorter
- ✅ Faster
- ✅ Easier to read
- ✅ More efficient

---

# 📌 Common Apply Family Functions

| Function | Purpose | Works On |
|----------|----------|----------|
| `apply()` | Apply a function to rows or columns of a matrix | Matrix / Array |
| `tapply()` | Apply a function to groups of data | Vectors |
| `by()` | Apply a function to subsets of a data frame | Data Frames |
| `aggregate()` | Summarize grouped data | Data Frames |
| `sapply()` | Apply a function to each element of a list or vector and simplify the output | Lists / Vectors |

---

# 1️⃣ apply()

## 💡 What is `apply()`?

`apply()` applies a function to **every row or every column** of a matrix.

### Syntax

```r
apply(X, MARGIN, FUN)
```

Where:

- `X` → Matrix or array
- `MARGIN = 1` → Apply by **rows**
- `MARGIN = 2` → Apply by **columns**
- `FUN` → Function to apply (e.g., `mean`, `sum`, `max`)

---

## 🧩 Example

```r
mat <- matrix(
  c(80, 58, 65,
    70, 90, 85),
  nrow = 2
)

mat
```

Output:

```text
     [,1] [,2] [,3]
[1,]   80   65   90
[2,]   58   70   85
```

### Calculate Mean of Each Row

```r
apply(mat, 1, mean)
```

Output

```r
[1] 78.33 71.00
```

### Calculate Mean of Each Column

```r
apply(mat, 2, mean)
```

Output

```r
[1] 69.0 67.5 87.5
```

📝 **Remember**

- `1` = Rows
- `2` = Columns

---

# 2️⃣ tapply()

## 💡 What is `tapply()`?

`tapply()` applies a function to **groups** within a vector.

It is commonly used to calculate:

- Mean
- Sum
- Median
- Standard deviation

for each category.

### Syntax

```r
tapply(vector, group, function)
```

---

## 🧩 Example

```r
df <- data.frame(
  Sex = c("M","F","F","M","M"),
  Weight = c(80,58,65,90,100)
)

tapply(df$Weight, df$Sex, mean)
```

Output

```r
       F        M
61.5   90.0
```

📝 **Explanation**

R groups the weights by **Sex** and calculates the mean separately.

- Female Mean = 61.5 kg
- Male Mean = 90 kg

---

# 3️⃣ by()

## 💡 What is `by()`?

`by()` performs a function on **subsets of a data frame**.

It is similar to `tapply()`, but it prints results in a more readable grouped format.

### Syntax

```r
by(data, group, function)
```

---

## 🧩 Example

```r
by(df$Weight, df$Sex, mean)
```

Output

```text
df$Sex: F
[1] 61.5

------------------------------------------------

df$Sex: M
[1] 90
```

📝 **When to use `by()`?**

Use it when you want grouped summaries that are easy to read.

---

# 4️⃣ aggregate()

## 💡 What is `aggregate()`?

`aggregate()` groups data and calculates summary statistics.

It is one of the most commonly used functions in data analysis.

### Syntax

```r
aggregate(formula, data, function)
```

---

## 🧩 Example

```r
aggregate(
  Weight ~ Sex,
  data = df,
  mean
)
```

Output

```text
  Sex Weight
1   F   61.5
2   M   90.0
```

📝 **Explanation**

The formula

```r
Weight ~ Sex
```

means:

> "Calculate the summary of **Weight** for each **Sex**."

---

# 5️⃣ sapply()

## 💡 What is `sapply()`?

`sapply()` applies a function to every element of a **list** or **vector** and returns a simplified result.

It is commonly used together with `split()`.

---

## 🧩 Example

### Split the data

```r
sp <- split(df$Weight, df$Sex)

sp
```

Output

```r
$F
[1] 58 65

$M
[1] 80 90 100
```

Now calculate the mean for each group.

```r
sapply(sp, mean)
```

Output

```r
   F    M
61.5 90.0
```

📝 **Explanation**

Step 1:

```r
split(df$Weight, df$Sex)
```

creates a list.

Step 2:

```r
sapply()
```

calculates the mean of each list element.

---

# 📊 Comparison of Apply Functions

| Function | Works On | Groups Data? | Common Use |
|-----------|----------|--------------|------------|
| `apply()` | Matrix | ❌ No | Row/Column operations |
| `tapply()` | Vector | ✅ Yes | Group summaries |
| `by()` | Data Frame | ✅ Yes | Readable grouped summaries |
| `aggregate()` | Data Frame | ✅ Yes | Statistical summaries |
| `sapply()` | List / Vector | Depends | Apply functions to list elements |

---

# 🎯 Which Function Should You Use?

| If you want to... | Use |
|-------------------|-----|
| Calculate row means | `apply()` |
| Calculate column sums | `apply()` |
| Calculate mean by groups | `tapply()` |
| Produce grouped summaries | `by()` |
| Summarize a data frame | `aggregate()` |
| Apply a function to every list element | `sapply()` |

---

# 🧠 Memory Trick

Think of the Apply Family like this:

- 📊 **`apply()`** → Works across **rows or columns**
- 👥 **`tapply()`** → Works across **groups**
- 📄 **`by()`** → Works by **subsets**
- 📈 **`aggregate()`** → Creates **summary tables**
- 📦 **`sapply()`** → Works on **lists** and returns a simple output

---

# 📝 Key Takeaways

- ✅ Use **`apply()`** for matrices.
- ✅ Use **`tapply()`** to summarize grouped vectors.
- ✅ Use **`by()`** for readable grouped analysis.
- ✅ Use **`aggregate()`** to create grouped summary tables.
- ✅ Use **`sapply()`** to apply a function to each element of a list.
- 🚀 These functions help you write cleaner, shorter, and more efficient R code without using loops.
