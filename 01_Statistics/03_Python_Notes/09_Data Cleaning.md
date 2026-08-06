# 🧹 Data Cleaning

> **Preparing Data for Statistical Analysis with Python**

Data cleaning is the process of identifying and correcting errors, inconsistencies, and missing values before performing statistical analysis.

High-quality data are essential for obtaining reliable and reproducible results.

---

# 📚 Table of Contents

1. What is Data Cleaning?
2. Why is Data Cleaning Important?
3. Importing Libraries
4. Inspecting Data
5. Checking Data Types
6. Missing Values
7. Removing Missing Values
8. Filling Missing Values
9. Duplicate Records
10. Renaming Columns
11. Changing Data Types
12. Replacing Values
13. Filtering Data
14. Sorting Data
15. Creating New Variables
16. Saving Cleaned Data
17. Python vs R
18. Biological Examples
19. Common Mistakes
20. Key Takeaways

---

# 📖 What is Data Cleaning?

Data cleaning is the process of preparing raw data for analysis.

Typical tasks include:

- 🧹 Removing errors
- ❌ Handling missing values
- 🔄 Removing duplicates
- 📝 Renaming variables
- 🔤 Correcting data types
- 📊 Standardizing values

---

# 🎯 Why is Data Cleaning Important?

Clean data improve:

- 📊 Statistical accuracy
- 📈 Model performance
- 🔬 Scientific reproducibility
- 📋 Data consistency
- 📉 Reliability of conclusions

---

# 📦 Import Libraries

```python
import pandas as pd
import numpy as np
```

---

# 📊 Example Dataset

```python
df = pd.DataFrame({

    "Patient":[1,2,2,4,5],

    "Age":[35,np.nan,42,29,51],

    "Sex":["M","F","F","M","M"],

    "BMI":[24.5,27.8,np.nan,22.1,30.2],

    "BloodPressure":[142,145,145,138,np.nan]

})

df
```

---

# 👀 Inspecting Data

Display the first rows.

```python
df.head()
```

---

Display the last rows.

```python
df.tail()
```

---

Display information.

```python
df.info()
```

---

Summary statistics.

```python
df.describe()
```

---

# 🔍 Checking Data Types

```python
df.dtypes
```

Example output

```text
Patient             int64
Age               float64
Sex                object
BMI               float64
BloodPressure     float64
```

---

# ❓ Missing Values

Count missing values.

```python
df.isna().sum()
```

Alternative.

```python
df.isnull().sum()
```

---

Display rows containing missing values.

```python
df[df.isna().any(axis=1)]
```

---

# ❌ Removing Missing Values

Remove rows with missing values.

```python
df.dropna()
```

Permanent removal.

```python
df = df.dropna()
```

---

Remove columns containing missing values.

```python
df.dropna(axis=1)
```

---

# 🔄 Filling Missing Values

Replace missing values with zero.

```python
df.fillna(0)
```

---

Replace with the column mean.

```python
df["BMI"] = df["BMI"].fillna(

    df["BMI"].mean()

)
```

---

Replace with the median.

```python
df["Age"] = df["Age"].fillna(

    df["Age"].median()

)
```

---

Replace with the most common value.

```python
df["Sex"] = df["Sex"].fillna(

    df["Sex"].mode()[0]

)
```

---

# 📋 Duplicate Records

Find duplicate rows.

```python
df.duplicated()
```

---

Count duplicates.

```python
df.duplicated().sum()
```

---

Remove duplicates.

```python
df = df.drop_duplicates()
```

---

# ✏️ Renaming Columns

Rename one column.

```python
df.rename(

    columns={

        "BloodPressure":"BP"

    }

)
```

Permanent change.

```python
df = df.rename(

    columns={

        "BloodPressure":"BP"

    }

)
```

---

Rename all columns.

```python
df.columns = [

"Patient",

"Age",

"Sex",

"BMI",

"BP"

]
```

---

# 🔤 Changing Data Types

Convert to integer.

```python
df["Age"] = df["Age"].astype(int)
```

---

Convert to float.

```python
df["BMI"] = df["BMI"].astype(float)
```

---

Convert to string.

```python
df["Patient"] = df["Patient"].astype(str)
```

---

Convert to category.

```python
df["Sex"] = df["Sex"].astype("category")
```

---

# 🔄 Replacing Values

Replace one value.

```python
df.replace(

    "M",

    "Male"

)
```

---

Replace multiple values.

```python
df.replace({

    "M":"Male",

    "F":"Female"

})
```

---

# 🔍 Filtering Data

Patients older than 40.

```python
df[df["Age"] > 40]
```

---

Female patients.

```python
df[df["Sex"] == "Female"]
```

---

Multiple conditions.

```python
df[

    (df["Age"] > 40)

    &

    (df["BMI"] > 25)

]
```

---

# 🔃 Sorting Data

Ascending.

```python
df.sort_values(

    "Age"

)
```

---

Descending.

```python
df.sort_values(

    "Age",

    ascending=False

)
```

---

# ➕ Creating New Variables

Body Mass Index category.

```python
df["BMI_Category"] = np.where(

    df["BMI"] >= 25,

    "Overweight",

    "Normal"

)
```

---

Age group.

```python
df["Age_Group"] = np.where(

    df["Age"] >= 50,

    "Older",

    "Younger"

)
```

---

# 💾 Saving Cleaned Data

CSV.

```python
df.to_csv(

    "clean_data.csv",

    index=False

)
```

---

Excel.

```python
df.to_excel(

    "clean_data.xlsx",

    index=False

)
```

---

# ⚖️ Python vs R

| Python | R |
|----------|----|
| `dropna()` | `na.omit()` |
| `fillna()` | `replace()` |
| `duplicated()` | `duplicated()` |
| `drop_duplicates()` | `unique()` |
| `rename()` | `rename()` |
| `astype()` | `as.numeric()` / `factor()` |
| `replace()` | `replace()` |

---

# 🧬 Biological Example

Import patient data.

```python
df = pd.read_csv(

    "patients.csv"

)
```

Inspect the dataset.

```python
df.info()
```

Count missing values.

```python
df.isna().sum()
```

Replace missing BMI values.

```python
df["BMI"] = df["BMI"].fillna(

    df["BMI"].mean()

)
```

Remove duplicate patients.

```python
df = df.drop_duplicates()
```

Rename columns.

```python
df = df.rename(

    columns={

        "BloodPressure":"BP"

    }

)
```

Export the cleaned dataset.

```python
df.to_csv(

    "patients_clean.csv",

    index=False

)
```

---

# ⚠️ Common Mistakes

❌ Performing statistical tests before cleaning the data.

Always inspect the dataset first.

---

❌ Deleting missing values without considering the amount of missing data.

Consider imputation when appropriate.

---

❌ Forgetting to save cleaned datasets.

Export cleaned data for reproducibility.

---

❌ Ignoring incorrect data types.

Verify data types using:

```python
df.dtypes
```

---

# 💡 Tips

- 🧹 Always inspect data immediately after importing.
- 📊 Check for missing values before calculating statistics.
- 🔄 Remove duplicate observations.
- 🔤 Convert variables to the correct data type.
- 💾 Save cleaned datasets before analysis.
- 📋 Keep a copy of the original raw data.

---

# 🔄 Typical Data Cleaning Workflow

```text
Import Data
      │
      ▼
Inspect Data
      │
      ▼
Check Data Types
      │
      ▼
Find Missing Values
      │
      ▼
Handle Missing Values
      │
      ▼
Remove Duplicates
      │
      ▼
Rename Variables
      │
      ▼
Create New Variables
      │
      ▼
Export Clean Dataset
      │
      ▼
Statistical Analysis
```

---

# 🎯 Key Takeaways

- 🧹 Data cleaning is the foundation of reliable statistical analysis.
- 📊 Missing values should always be identified before analysis.
- 🔄 Duplicate observations should be detected and removed when appropriate.
- 🔤 Variables should have correct and consistent data types.
- 📝 Meaningful variable names improve code readability.
- 📋 Cleaned datasets should be exported and preserved for reproducibility.
- 📈 Well-prepared data lead to more accurate statistical analyses.

