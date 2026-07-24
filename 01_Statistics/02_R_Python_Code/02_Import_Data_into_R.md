# 📂 Importing Files into R (Quick Guide)

This guide covers the most common ways to import **CSV** and **Excel** files into R, along with troubleshooting tips and best practices.

---

# 📌 1. Pick the Right Function

## 📄 CSV File (Recommended)

### CSV Separated by Commas (,)

```r
df <- read.table(
  file.choose(),
  header = TRUE,
  sep = ","
)
```

### CSV Separated by Semicolons (;)

```r
df <- read.table(
  file.choose(),
  header = TRUE,
  sep = ";"
)
```

---

## 📄 Comma-Separated CSV with Dot Decimals

### Base R

```r
df <- read.csv("C:/path/my_data.csv")
```

### Using **readr** (Tidyverse)

```r
df <- readr::read_csv("C:/path/my_data.csv")
```

**Advantages of `readr`:**

- Faster
- Better parsing
- Cleaner output
- Doesn't convert text into factors

---

## 📄 Semicolon-Separated CSV with Comma Decimals (Common in Europe)

### Base R

```r
df <- read.csv2("C:/path/my_data.csv")
```

### Using **readr**

```r
df <- readr::read_csv2("C:/path/my_data.csv")
```

---

# 📊 Import Excel Files (.xlsx / .xls)

### Automatically Detect File Type

```r
df <- readxl::read_excel("C:/path/my_data.xlsx")
```

### Import a Specific Sheet

```r
df <- readxl::read_excel(
  "C:/path/my_data.xlsx",
  sheet = 1
)

# or

df <- readxl::read_excel(
  "C:/path/my_data.xlsx",
  sheet = "SheetName"
)
```

### Using the `readxl` Library

```r
library(readxl)

dataset <- read_excel(
  "C:/Users/APPLE/Downloads/rawdataexcel.xls"
)

View(dataset)
```

---

# 📂 Don't Know the File Path?

Use **file.choose()** to select the file interactively.

### CSV

```r
df <- readr::read_csv(file.choose())
```

### Excel

```r
df <- readxl::read_excel(file.choose())
```

---

# 🔄 2. `read.csv()` vs `read.csv2()`

| Function | Separator | Decimal |
|-----------|-----------|----------|
| `read.csv()` | `,` | `.` |
| `read.csv2()` | `;` | `,` |

### 📌 Use the function that matches your file format.

If you choose the wrong one, you may get:

- ❌ One huge column (wrong separator)
- ❌ Numbers imported as text
- ❌ `NA` values due to incorrect decimal format

---

# 🖱️ 3. Import Using RStudio (No Code)

If you prefer not to write code:

**Environment Pane → Import Dataset**

Choose:

- **From Text (base)** for CSV files
- **From Excel...** for Excel files

Then follow the import wizard.

---

# 🔍 4. Quick Checks After Importing

After importing your dataset, always inspect it.

```r
View(df)      # Spreadsheet view (RStudio)

head(df)      # First six rows

str(df)       # Structure and column data types

names(df)     # Column names
```

---

# ⚠️ 5. Common Fixes & Gotchas

## 📁 Path Errors

Error:

```text
cannot open file
```

### Solution

- Check the file path.
- Verify the file extension.
- On Windows, use:
  - Forward slashes `/`
  - OR double backslashes `\\`

Example:

```r
"C:/Users/Madhav/Documents/data.csv"
```

or

```r
"C:\\Users\\Madhav\\Documents\\data.csv"
```

---

## 🔢 Wrong Separator or Decimal

Specify them manually.

```r
df <- read.table(
  "C:/path/file.csv",
  header = TRUE,
  sep = ";",
  dec = ","
)
```

---

## 🏷️ Weird Column Names

Sometimes R changes names like:

```text
Weight (kg)
```

into

```text
Weight..kg.
```

### Option 1 (Recommended)

```r
df <- janitor::clean_names(df)
```

Result:

```text
weight_kg
```

### Option 2 (Rename Manually)

```r
colnames(df) <- c("Sex", "Weight")
```

---

## 🔤 Text Converted into Factors (Base R)

Older versions of R sometimes convert text into factors.

Prevent this using:

```r
df <- read.csv(
  "file.csv",
  stringsAsFactors = FALSE
)
```

> **Note:** `readr` never converts strings into factors by default.

---

# 📄 6. Excel Being Difficult?

Sometimes Excel files contain:

- Formulas
- Merged cells
- Hidden formatting

If importing fails:

1. Open the Excel file.
2. Choose **File → Save As**.
3. Save as **CSV (Comma Delimited)**.
4. Import using:

```r
read.csv()
```

or

```r
read.csv2()
```

depending on the separator.

---

# 💾 7. Save for Faster Reloading

Instead of importing the original file every time:

### Save

```r
saveRDS(df, "C:/path/my_data.rds")
```

### Load

```r
df <- readRDS("C:/path/my_data.rds")
```

This is much faster than repeatedly importing CSV or Excel files.

---

# 🚀 8. Minimal One-Liners to Remember

## CSV (Comma Separated)

```r
df <- read.csv("C:/path/file.csv")
```

---

## CSV (Semicolon Separated)

```r
df <- read.csv2("C:/path/file.csv")
```

---

## Excel

```r
df <- readxl::read_excel("C:/path/file.xlsx")
```

---

## Interactive File Picker

```r
df <- readxl::read_excel(file.choose())
```

---

# 📝 Summary Table

| File Type | Recommended Function |
|------------|----------------------|
| CSV (Comma) | `read.csv()` |
| CSV (Semicolon) | `read.csv2()` |
| Excel (.xlsx/.xls) | `readxl::read_excel()` |
| Interactive CSV | `readr::read_csv(file.choose())` |
| Interactive Excel | `readxl::read_excel(file.choose())` |
| Save Dataset | `saveRDS()` |
| Reload Dataset | `readRDS()` |

---

# ✅ Best Practices

- ✅ Prefer **CSV** over Excel for data analysis.
- ✅ Use **`readr`** for faster CSV imports.
- ✅ Use **`readxl`** for Excel files.
- ✅ Always inspect your data using `head()`, `str()`, and `View()`.
- ✅ Save cleaned datasets as **`.rds`** files for quick future loading.
