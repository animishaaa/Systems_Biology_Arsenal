# 📂 Importing and Exporting Data

> **Reading, Inspecting, and Saving Data with Pandas**

Real-world statistical analysis begins by importing data into Python.

Pandas provides powerful functions for reading and writing data in many common formats, including CSV, Excel, text files, and JSON.

---

# 📚 Table of Contents

1. Why Import Data?
2. Common File Formats
3. Importing Pandas
4. Working Directory
5. Reading CSV Files
6. Reading Excel Files
7. Reading Text Files
8. Viewing Imported Data
9. Inspecting Data Types
10. Selecting Columns
11. Renaming Columns
12. Exporting Data
13. File Paths
14. R vs Python
15. Biological Examples
16. Common Mistakes
17. Key Takeaways

---

# 📖 Why Import Data?

Most datasets originate from:

- 🧬 Biological experiments
- 🏥 Clinical studies
- 📊 Surveys
- 🔬 Laboratory instruments
- 💻 Databases

Python imports these datasets into **Pandas DataFrames** for analysis.

---

# 📁 Common File Formats

| Format | Extension | Pandas Function |
|----------|-----------|----------------|
| CSV | `.csv` | `read_csv()` |
| Excel | `.xlsx` | `read_excel()` |
| Text | `.txt` | `read_table()` |
| JSON | `.json` | `read_json()` |

---

# 📦 Import Pandas

```python
import pandas as pd
```

---

# 📂 Working Directory

Display the current working directory.

```python
import os

os.getcwd()
```

Example output

```text
C:\Users\Student\Documents
```

---

Change the working directory.

```python
os.chdir("C:/Data")
```

---

# 📄 Reading CSV Files

```python
df = pd.read_csv("patients.csv")
```

Display the first rows.

```python
df.head()
```

---

## CSV with a Different Separator

Semicolon-separated file.

```python
df = pd.read_csv(
    "patients.csv",
    sep=";"
)
```

---

## CSV with a Different Decimal Symbol

European decimal format.

```python
df = pd.read_csv(
    "patients.csv",
    sep=";",
    decimal=","
)
```

---

# 📊 Reading Excel Files

```python
df = pd.read_excel(
    "patients.xlsx"
)
```

---

Read a specific worksheet.

```python
df = pd.read_excel(
    "patients.xlsx",
    sheet_name="Sheet2"
)
```

---

# 📄 Reading Text Files

```python
df = pd.read_table(
    "patients.txt"
)
```

---

Tab-separated text file.

```python
df = pd.read_table(
    "patients.txt",
    sep="\t"
)
```

---

# 📄 Reading JSON Files

```python
df = pd.read_json(
    "patients.json"
)
```

---

# 👀 Viewing Imported Data

First five rows.

```python
df.head()
```

---

Last five rows.

```python
df.tail()
```

---

Random sample.

```python
df.sample(5)
```

---

Display the entire DataFrame.

```python
print(df)
```

---

# 📋 DataFrame Information

```python
df.info()
```

Displays:

- Number of rows
- Number of columns
- Missing values
- Data types

---

Shape.

```python
df.shape
```

Example output

```text
(120, 6)
```

Meaning:

- 120 rows
- 6 columns

---

Column names.

```python
df.columns
```

---

Data types.

```python
df.dtypes
```

---

# 🔍 Selecting Columns

Single column.

```python
df["Age"]
```

---

Multiple columns.

```python
df[["Age", "BMI"]]
```

---

# ✏️ Renaming Columns

Rename one column.

```python
df.rename(
    columns={"BP":"BloodPressure"}
)
```

Permanent change.

```python
df = df.rename(
    columns={"BP":"BloodPressure"}
)
```

---

Rename all columns.

```python
df.columns = [

"Patient",

"Age",

"BMI",

"BloodPressure"

]
```

---

# ❌ Removing Columns

```python
df = df.drop(
    columns=["BMI"]
)
```

---

# 💾 Exporting CSV Files

```python
df.to_csv(
    "results.csv",
    index=False
)
```

---

# 💾 Exporting Excel Files

```python
df.to_excel(
    "results.xlsx",
    index=False
)
```

---

# 💾 Exporting Text Files

```python
df.to_csv(
    "results.txt",
    sep="\t",
    index=False
)
```

---

# 📂 Absolute vs Relative File Paths

## Relative Path

```python
pd.read_csv("patients.csv")
```

Python searches in the current working directory.

---

## Absolute Path

```python
pd.read_csv(
    "C:/Users/Student/Documents/Data/patients.csv"
)
```

---

# ⚖️ Python vs R

| Python | R |
|----------|----|
| `read_csv()` | `read.csv()` |
| `read_excel()` | `read_excel()` |
| `head()` | `head()` |
| `tail()` | `tail()` |
| `shape` | `dim()` |
| `columns` | `colnames()` |
| `dtypes` | `str()` |
| `to_csv()` | `write.csv()` |

---

# 🧬 Biological Example

Import patient data.

```python
import pandas as pd

df = pd.read_csv(
    "patient_data.csv"
)
```

Inspect the data.

```python
df.head()
```

Display summary.

```python
df.info()
```

Calculate average blood pressure.

```python
df["BloodPressure"].mean()
```

Filter patients older than 60 years.

```python
df[df["Age"] > 60]
```

Export the filtered dataset.

```python
df[df["Age"] > 60].to_csv(
    "elderly_patients.csv",
    index=False
)
```

---

# ⚠️ Common Mistakes

❌ Incorrect file path.

```python
pd.read_csv("patient.csv")
```

Verify that the file exists in the working directory.

---

❌ Forgetting quotation marks.

Incorrect.

```python
pd.read_csv(patient.csv)
```

Correct.

```python
pd.read_csv("patient.csv")
```

---

❌ Using the wrong separator.

European CSV files often require:

```python
sep=";"
```

---

❌ Ignoring missing values.

Always inspect the imported dataset.

```python
df.info()
```

---

# 💡 Tips

- 📂 Store datasets in a dedicated project folder.
- 📋 Inspect every imported dataset before analysis.
- 📊 Verify data types before performing statistics.
- 📥 CSV is the most common format for data exchange.
- 💾 Export cleaned datasets to preserve preprocessing steps.

---

# 🔄 Python vs R Workflow

| Step | Python | R |
|------|--------|----|
| Import CSV | `pd.read_csv()` | `read.csv()` |
| Import Excel | `pd.read_excel()` | `read_excel()` |
| View data | `head()` | `head()` |
| Data structure | `info()` | `str()` |
| Summary statistics | `describe()` | `summary()` |
| Export CSV | `to_csv()` | `write.csv()` |
| Export Excel | `to_excel()` | `write.xlsx()` |

---

# 🎯 Key Takeaways

- 📂 Most analyses begin by importing data into a Pandas DataFrame.
- 📄 Pandas supports CSV, Excel, text, and JSON files.
- 👀 Imported datasets should always be inspected using `head()`, `info()`, and `describe()`.
- 📊 Data types and missing values should be checked before statistical analysis.
- 💾 Cleaned datasets can be exported for reproducibility.
- 🔄 Pandas provides functionality similar to R's data import and export tools.

