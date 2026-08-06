# 🐼 Pandas DataFrames

> **Data Manipulation and Analysis with Python**

Pandas is the most widely used Python library for working with tabular data.

It provides two main data structures:

- 📋 **Series** (one-dimensional data)
- 📊 **DataFrame** (two-dimensional tables)

A **Pandas DataFrame** is the Python equivalent of an **R data frame** and is the foundation of almost all data analysis in Python.

---

# 📚 Table of Contents

1. What is Pandas?
2. Why Use Pandas?
3. Installing Pandas
4. Importing Pandas
5. Series
6. DataFrames
7. Creating DataFrames
8. Viewing Data
9. Selecting Columns
10. Selecting Rows
11. Filtering Data
12. Adding Columns
13. Removing Columns
14. Summary Statistics
15. Sorting Data
16. Missing Values
17. Exporting Data
18. R vs Pandas
19. Biological Examples
20. Common Mistakes
21. Key Takeaways

---

# 📖 What is Pandas?

Pandas is a Python library used for:

- 📊 Data manipulation
- 📈 Statistical analysis
- 📋 Working with spreadsheets
- 📥 Reading CSV and Excel files
- 🧹 Cleaning datasets

Almost every data science project uses Pandas.

---

# 🚀 Why Use Pandas?

Pandas makes it easy to:

- Import data
- Organize data
- Filter observations
- Calculate statistics
- Prepare datasets
- Export results

---

# 📦 Installing Pandas

```bash
pip install pandas
```

Most Anaconda installations already include Pandas.

---

# 📥 Importing Pandas

```python
import pandas as pd
```

The alias `pd` is the standard convention.

---

# 📋 Pandas Series

A Series stores one column of data.

```python
import pandas as pd

bp = pd.Series([142,145,139,141])
```

Display the series.

```python
print(bp)
```

Output

```text
0    142
1    145
2    139
3    141
dtype: int64
```

---

# 📊 Pandas DataFrame

A DataFrame is a table consisting of rows and columns.

```python
import pandas as pd

df = pd.DataFrame({

    "Patient":[1,2,3,4],

    "BP":[142,145,139,141],

    "Age":[35,42,29,50]

})
```

Display the DataFrame.

```python
print(df)
```

Output

```text
   Patient   BP   Age
0        1  142    35
1        2  145    42
2        3  139    29
3        4  141    50
```

---

# 👀 Viewing Data

First rows

```python
df.head()
```

First 10 rows

```python
df.head(10)
```

Last rows

```python
df.tail()
```

---

# 📐 DataFrame Information

```python
df.info()
```

Displays:

- Number of rows
- Number of columns
- Data types
- Missing values

---

Shape

```python
df.shape
```

Output

```text
(4,3)
```

Meaning:

- 4 rows
- 3 columns

---

Column names

```python
df.columns
```

---

Data types

```python
df.dtypes
```

---

# 📌 Selecting Columns

Single column

```python
df["BP"]
```

or

```python
df.BP
```

---

Multiple columns

```python
df[["BP","Age"]]
```

---

# 📌 Selecting Rows

First row

```python
df.iloc[0]
```

---

Third row

```python
df.iloc[2]
```

---

Rows 2–4

```python
df.iloc[1:4]
```

---

# 🔍 Filtering Data

Patients older than 40

```python
df[df["Age"] > 40]
```

---

Blood pressure greater than 140

```python
df[df["BP"] > 140]
```

---

Multiple conditions

```python
df[
    (df["Age"] > 35)
    &
    (df["BP"] > 140)
]
```

---

# ➕ Adding Columns

```python
df["BMI"] = [22.5,27.1,24.0,29.4]
```

Display

```python
df
```

---

# ❌ Removing Columns

```python
df.drop(
    columns=["BMI"]
)
```

Permanent removal

```python
df = df.drop(
    columns=["BMI"]
)
```

---

# 📊 Summary Statistics

```python
df.describe()
```

Calculates:

- Mean
- Standard deviation
- Minimum
- Maximum
- Quartiles

---

Mean blood pressure

```python
df["BP"].mean()
```

Median

```python
df["BP"].median()
```

Standard deviation

```python
df["BP"].std()
```

Variance

```python
df["BP"].var()
```

Maximum

```python
df["BP"].max()
```

Minimum

```python
df["BP"].min()
```

---

# 🔃 Sorting Data

Ascending

```python
df.sort_values(
    "Age"
)
```

Descending

```python
df.sort_values(
    "Age",
    ascending=False
)
```

---

# ⚠️ Missing Values

Count missing values

```python
df.isna().sum()
```

Remove missing rows

```python
df.dropna()
```

Fill missing values

```python
df.fillna(0)
```

Fill with column mean

```python
df["BP"] = df["BP"].fillna(
    df["BP"].mean()
)
```

---

# 💾 Importing Data

CSV

```python
df = pd.read_csv(
    "patients.csv"
)
```

---

Excel

```python
df = pd.read_excel(
    "patients.xlsx"
)
```

---

# 💾 Exporting Data

CSV

```python
df.to_csv(
    "results.csv",
    index=False
)
```

---

Excel

```python
df.to_excel(
    "results.xlsx",
    index=False
)
```

---

# ⚖️ Pandas vs R

| Pandas | R |
|----------|----|
| `DataFrame` | `data.frame()` |
| `head()` | `head()` |
| `describe()` | `summary()` |
| `mean()` | `mean()` |
| `std()` | `sd()` |
| `read_csv()` | `read.csv()` |
| `read_excel()` | `read_excel()` |

---

# 🧬 Biological Example

```python
df = pd.DataFrame({

    "Patient":[1,2,3,4,5],

    "Age":[35,41,28,54,47],

    "BP":[142,148,139,150,144],

    "BMI":[24.2,28.1,22.9,30.5,27.0]

})
```

Average blood pressure

```python
df["BP"].mean()
```

Patients over 40

```python
df[df["Age"] > 40]
```

Highest BMI

```python
df["BMI"].max()
```

---

# ⚠️ Common Mistakes

❌ Forgetting quotation marks around column names.

Incorrect

```python
df[BP]
```

Correct

```python
df["BP"]
```

---

❌ Using parentheses instead of brackets.

Incorrect

```python
df("BP")
```

Correct

```python
df["BP"]
```

---

❌ Forgetting to save changes.

Incorrect

```python
df.drop(columns=["BMI"])
```

Correct

```python
df = df.drop(columns=["BMI"])
```

---

# 💡 Tips

- 📊 DataFrames are the standard data structure in Python.
- 📥 Import CSV or Excel files directly into Pandas.
- 📈 Most statistical libraries use DataFrames.
- 📋 Column names should be short and descriptive.
- 🧹 Always check for missing values before analysis.

---

# 🎯 Key Takeaways

- 🐼 Pandas is the primary library for working with tabular data.
- 📊 A DataFrame is the Python equivalent of an R data frame.
- 📋 DataFrames consist of rows and columns.
- 🔍 Data can be filtered, sorted, and summarized efficiently.
- 📥 Pandas supports direct import and export of CSV and Excel files.
- 📈 Built-in methods calculate descriptive statistics quickly.
- 🤖 Most Python statistics and machine learning libraries use Pandas DataFrames.

