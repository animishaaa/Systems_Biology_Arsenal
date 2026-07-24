# 🧾 R Notes — Vectors, Matrices, and Data Frames

## 🟢 1. Vector — "A Single Line of Data"

### 💡 What is a Vector?

A **vector** is the simplest form of data structure in R.

- It is **one-dimensional (1D)**.
- It stores a sequence of values.
- **All elements must be of the same data type** (all numeric, all character, all logical, etc.).

### 🧩 Example

```r
# Create a numeric vector
w <- c(80, 58, 65, 70, 90)

# Print the vector
w
```

### 🖨️ Output

```r
[1] 80 58 65 70 90
```

### 🧠 Think of it as

A vector is like:

- 🛒 A shopping list
- 📝 A row of marks
- 📋 A list of related values

---

## 🔵 2. Matrix — "A Table Made of Vectors"

### 💡 What is a Matrix?

A **matrix** is a **two-dimensional (2D)** data structure with rows and columns.

All values inside a matrix **must be of the same data type**.

You can create a matrix by:

- Providing data with the number of rows and columns using `matrix()`
- Combining vectors using:
  - `cbind()` → Combine as columns
  - `rbind()` → Combine as rows

---

### 🧩 Example 1: Create a Matrix from Numbers

```r
m <- matrix(c(80, 58, 65, 70, 90, 85),
            nrow = 2,
            ncol = 3)

m
```

### 🖨️ Output

```r
     [,1] [,2] [,3]
[1,]   80   65   90
[2,]   58   70   85
```

### 📌 Notes

- `nrow = 2` → 2 rows
- `ncol = 3` → 3 columns
- By default, R fills the matrix **column-wise**.

---

### 🧩 Example 2: Combine Two Vectors into a Matrix

```r
# Two vectors
math <- c(80, 58, 65, 70, 90)
science <- c(75, 60, 68, 72, 88)

# Combine as columns
marks_matrix <- cbind(math, science)

marks_matrix
```

### 🖨️ Output

```r
     math science
[1,]   80      75
[2,]   58      60
[3,]   65      68
[4,]   70      72
[5,]   90      88
```

### ✅ Matrix Rules

- ✅ All values can be numeric
- ✅ All values can be text
- ❌ Cannot mix numbers and text in the same matrix

---

## 🟣 3. Data Frame — "A Real-World Data Table"

### 💡 What is a Data Frame?

A **data frame** is the most commonly used data structure in R.

It is similar to an **Excel spreadsheet**.

Unlike a matrix, **each column can have a different data type**.

For example:

- Text
- Numbers
- TRUE/FALSE values
- Dates

---

### 🧩 Example

```r
students <- data.frame(
  Name = c("Alice", "Bob", "Charlie", "David", "Eve"),
  Math = c(80, 58, 65, 70, 90),
  Science = c(75, 60, 68, 72, 88)
)

students
```

### 🖨️ Output

```r
     Name    Math Science
1    Alice     80      75
2      Bob     58      60
3  Charlie     65      68
4    David     70      72
5      Eve     90      88
```

### ✅ Data Frames Can Mix Data Types

| Column | Type |
|---------|------|
| Name | Character (Text) |
| Math | Numeric |
| Science | Numeric |

---

# ⚖️ Summary Table

| Feature | Vector | Matrix | Data Frame |
|---------|--------|--------|------------|
| Dimension | 1D | 2D | 2D |
| Data Types | Same type | Same type | Different types |
| Looks Like | A list | A grid | A spreadsheet |
| Created With | `c()` | `matrix()`, `cbind()`, `rbind()` | `data.frame()` |
| Best Used For | Simple lists | Mathematical calculations | Real-world datasets |

---

# 🎯 Quick Example to See the Difference

```r
# Vector
v <- c(10, 20, 30)

# Matrix
m <- cbind(v, c(40, 50, 60))

# Data Frame
df <- data.frame(
  Name = c("A", "B", "C"),
  Score = v
)

v
m
df
```

### 🖨️ Output

#### ✅ Vector

```r
[1] 10 20 30
```

#### ✅ Matrix

```r
     v
[1,] 10 40
[2,] 20 50
[3,] 30 60
```

#### ✅ Data Frame

```r
  Name Score
1    A    10
2    B    20
3    C    30
```

---

# 📝 Key Takeaways

### ✅ Vector

- One-dimensional (1D)
- Stores one type of data
- Created using `c()`

### ✅ Matrix

- Two-dimensional (2D)
- Stores one type of data
- Created using `matrix()`, `cbind()`, or `rbind()`

### ✅ Data Frame

- Two-dimensional (2D)
- Stores different data types in different columns
- Created using `data.frame()`
- Most commonly used structure for data analysis in R
