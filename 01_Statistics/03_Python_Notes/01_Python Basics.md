# 🐍 Python Basics

> **A Beginner's Guide to Python for Statistics, Data Science, and Bioinformatics**

Python is one of the most popular programming languages in science and engineering. This guide introduces the fundamental concepts need before learning statistical analysis with Python.

---

# 📚 Table of Contents

1. What is Python?
2. Why Learn Python?
3. Python vs R
4. Running Python
5. Variables
6. Data Types
7. Printing Output
8. Comments
9. Checking Variable Types
10. Mathematical Operators
11. Example Program
12. Key Takeaways

---

# 🐍 What is Python?

Python is a **general-purpose programming language** widely used in:

- 📊 Data Science
- 🧬 Bioinformatics
- 🧫 Systems Biology
- 🤖 Machine Learning
- 🧠 Artificial Intelligence
- 📈 Statistics
- 🔬 Scientific Computing
- 🌐 Web Development
- ⚙️ Automation

Python is easy to read, beginner-friendly, and has thousands of scientific libraries.

---

# 🚀 Why Learn Python?

Python allows to:

- 📥 Import data
- 🧹 Clean data
- 📊 Analyze data
- 📈 Create figures
- 📉 Perform statistical tests
- 🤖 Build machine learning models
- 🧬 Analyze biological datasets

---

# ⚖️ Python vs R

| 🐍 Python | 📊 R |
|-----------|------|
| General-purpose programming language | Programming language for statistics |
| Excellent for Machine Learning & AI | Excellent for statistical analysis |
| Used in Data Science & Bioinformatics | Widely used in research |
| Uses packages like NumPy & Pandas | Uses packages like dplyr & ggplot2 |

---

# 📦 Python Libraries for Statistics

Python uses libraries (packages) to perform different tasks.

| 📚 Library | 🎯 Purpose |
|------------|------------|
| NumPy | Numerical computing and arrays |
| Pandas | DataFrames and data manipulation |
| SciPy | Statistical tests |
| Matplotlib | Data visualization |
| Seaborn | Statistical graphics |
| Statsmodels | Regression and statistical models |

---

# ▶️ Running Python

## 📓 Jupyter Notebook

A Jupyter Notebook consists of **cells** that can contain:

- 📝 Python code
- 📖 Markdown notes
- 📊 Tables
- 📈 Figures

Run the current cell using:

```text
Shift + Enter
```

---

# 📝 Variables

Variables store information.

### Python

```python
x = 5
```

### R

```r
x <- 5
```

Unlike R, Python uses the **equals sign (`=`)** to assign values.

---

## 📌 Examples

```python
age = 35
```

```python
height = 178
```

```python
weight = 91
```

Variables can store numbers, text, or logical values.

---

# 🔢 Data Types

Python has several built-in data types.

## 🔹 Integer (`int`)

Whole numbers.

```python
5
```

Example:

```python
age = 35
```

---

## 🔹 Float (`float`)

Decimal numbers.

```python
5.4
```

Example:

```python
temperature = 37.5
```

---

## 🔹 String (`str`)

Text enclosed in quotation marks.

```python
"Hello"
```

Example:

```python
species = "E. coli"
```

---

## 🔹 Boolean (`bool`)

Logical values.

```python
True
```

or

```python
False
```

Example:

```python
passed = True
```

---

# 🖨️ Printing Output

Use `print()` to display information.

```python
print("Hello World")
```

Output

```text
Hello World
```

---

Print variables.

```python
age = 35

print(age)
```

Output

```text
35
```

---

Print text together with variables.

```python
age = 35

print("Age =", age)
```

Output

```text
Age = 35
```

---

# 💬 Comments

Comments are ignored by Python.

They are used to explain your code.

```python
# This is a comment
```

Example

```python
# Patient blood pressure
bp = 142
```

---

# 🔍 Checking Variable Types

Use the `type()` function.

```python
x = 5

type(x)
```

Output

```text
<class 'int'>
```

---

Another example

```python
name = "Animish"

type(name)
```

Output

```text
<class 'str'>
```

---

# ➕ Mathematical Operators

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `+` | ➕ Addition | `5 + 3` | `8` |
| `-` | ➖ Subtraction | `5 - 3` | `2` |
| `*` | ✖️ Multiplication | `5 * 3` | `15` |
| `/` | ➗ Division | `10 / 2` | `5.0` |
| `**` | 🔼 Power | `2 ** 3` | `8` |
| `//` | 🔢 Integer Division | `7 // 2` | `3` |
| `%` | 🧮 Modulus (Remainder) | `7 % 2` | `1` |

---

# 💻 Example Program

```python
age = 35
height = 178
weight = 91

print(age)
print(height)
print(weight)
```

Output

```text
35
178
91
```

---

# 🧬 Biological Example

```python
species = "E. coli"
temperature = 37
pH = 7.4
concentration = 2.5

print("Species:", species)
print("Temperature:", temperature)
print("pH:", pH)
print("Concentration:", concentration)
```

Output

```text
Species: E. coli
Temperature: 37
pH: 7.4
Concentration: 2.5
```

---

# 💡 Tips

- ✅ Variable names are **case-sensitive**.
- ✅ Use meaningful names (`blood_pressure`) instead of (`x`).
- ✅ Comments improve code readability.
- ✅ Use `print()` to check your results while learning.
- ✅ Run one Jupyter cell at a time using **Shift + Enter**.

---

# 🎯 Key Takeaways

- 🐍 Python is one of the most widely used programming languages in science.
- 📦 Scientific work relies on libraries such as **NumPy**, **Pandas**, **SciPy**, **Matplotlib**, **Seaborn**, and **Statsmodels**.
- 📝 Variables are assigned using the **`=`** operator.
- 🔢 Python supports integers, floats, strings, and Boolean values.
- 🖨️ Use `print()` to display output.
- 💬 Use `#` to add comments to your code.
- 🔍 Use `type()` to determine a variable's data type.
- ➕ Python includes built-in mathematical operators for arithmetic calculations.
- 📓 Jupyter Notebook is an excellent environment for learning Python because it combines code, output, figures, and notes in a single document.
