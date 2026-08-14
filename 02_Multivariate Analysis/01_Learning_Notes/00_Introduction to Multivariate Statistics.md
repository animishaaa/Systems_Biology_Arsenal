# 📊 Introduction to Multivariate Statistics

## 1. 🔍 What is Multivariate Statistics?

**Multivariate statistics** deals with the analysis of data where **multiple variables are measured for each observation, subject, or sample**.

### 📌 Example

Suppose we collect the following information from each patient:

* 📏 Height
* ⚖️ Weight
* ❤️ Blood pressure

Because several variables describe the same patient, the dataset is **multivariate data**.

> 💡 **Key idea:** Multivariate statistics helps us study several variables together and understand the relationships among them.

---

## 2. 📈 Univariate vs. Multivariate Analysis

### 🔹 Univariate Analysis

**Univariate analysis** analyzes **one outcome variable at a time**.

Examples:

* 🧬 Comparing mean tumor size between patient groups
* 📊 Performing a standard ANOVA on tumor size
* 🩸 Studying cholesterol level as a single outcome

### 🔸 Multivariate Analysis

**Multivariate analysis** considers **two or more outcome variables simultaneously**.

Example:

* 🧬 Tumor size
* 🩸 PSA level

Instead of studying them independently, we can analyze **tumor size and PSA level together** across patient groups.

This allows us to investigate:

* 🔗 Relationships between variables
* 📈 Correlations
* 👥 Differences between groups
* 🧩 Joint patterns in the data

### 🆚 Comparison

| Feature                      | 🔹 Univariate             | 🔸 Multivariate  |
| ---------------------------- | ------------------------- | ---------------- |
| Outcome variables            | One                       | Two or more      |
| Relationships among outcomes | ❌ Not directly considered | ✅ Considered     |
| Example                      | Tumor size                | Tumor size + PSA |
| Typical method               | ANOVA                     | MANOVA           |

---

## 3. 🤖 Multivariate Statistics, Machine Learning, and AI

Multivariate statistical concepts provide an important foundation for many techniques used in **Machine Learning (ML)** and **Artificial Intelligence (AI)**.

### 🧠 Common Methods

* 📉 **PCA** - Principal Component Analysis
* 🎯 **LDA** - Linear Discriminant Analysis
* 📊 **PLS** - Partial Least Squares
* 🧱 **SVM** - Support Vector Machines
* 🧠 **ANN** - Artificial Neural Networks
* 🌳 **RF** - Random Forest
* 📈 **MANOVA** - Multivariate Analysis of Variance
* 🧪 **Hotelling's T² Test**

> 💡 Some of these are traditional statistical methods, while others are commonly classified as machine-learning methods.

---

## 4. 📚 Understanding Multivariate Data

Multivariate data contains **multiple variables measured on each observation**.

### 👨‍⚕️ Example: Patient Data

| Patient | Height | Weight | Blood Pressure |
| ------- | -----: | -----: | -------------: |
| 1       | 175 cm |  72 kg |         120/80 |
| 2       | 182 cm |  85 kg |         135/88 |
| 3       | 168 cm |  65 kg |         115/75 |

Each **row** represents one patient.

Each **column** represents a variable.

➡️ Therefore, every patient is described by a **multivariate profile**.

---

## 5. 🧩 Multivariate Analysis Explained Simply

Multivariate analysis studies **multiple variables jointly**.

### ❤️ Example: Blood Pressure

Blood pressure contains two related measurements:

* 🔴 Systolic blood pressure
* 🔵 Diastolic blood pressure

Instead of analyzing them separately, we can analyze them **together**.

This helps us understand:

* 🔗 Their correlation
* 📊 Their joint variation
* 👥 Patterns among patients
* 🧪 Differences between patient groups

> 💡 **Main idea:** Multivariate analysis allows us to understand how several variables behave **together**, rather than looking at each variable independently.

---

## 6. 🔗 Correlation and Bivariate Analysis

**Correlation** measures the **strength and direction of the relationship between two variables**.

### 📌 Examples

* 📏 Height ↔️ Weight
* ❤️ Systolic BP ↔️ Diastolic BP
* 🌸 Petal length ↔️ Petal width

When exactly **two variables** are studied together, this is more precisely called **bivariate analysis**.

> 📝 **Note:** Bivariate analysis can be considered the simplest special case of analysis involving multiple variables. However, some textbooks reserve the term *multivariate* for analyses involving multiple response variables.

### ➕ Positive Correlation

When one variable increases, the other tends to increase.

```text
Height ↑  →  Weight ↑
```

### ➖ Negative Correlation

When one variable increases, the other tends to decrease.

```text
Variable A ↑  →  Variable B ↓
```

---

## 7. 📐 Regression: Univariate vs. Multivariate

Having multiple **predictors** does not automatically make an analysis multivariate.

### 🔹 Multiple Regression

Consider:

```text
Cholesterol = Weight + Blood Pressure + Age
```

Here:

* 🎯 Outcome = Cholesterol
* 📥 Predictors = Weight, blood pressure, age
* 🔢 Number of outcomes = **1**

Therefore, this is **multiple regression with a univariate outcome**.

### 🔸 Multivariate Regression

Now consider:

```text
Cholesterol + Body Fat = Weight + Blood Pressure + Age
```

Here:

* 🎯 Outcomes = Cholesterol + body fat
* 📥 Predictors = Weight + blood pressure + age
* 🔢 Number of outcomes = **2**

Therefore, this is **multivariate regression**.

> 🧠 **Remember**
>
> **Multiple regression** = Multiple predictors + **one outcome**
> **Multivariate regression** = **Multiple outcomes**

---

## 8. 📊 ANOVA vs. MANOVA

### 🔹 ANOVA

**ANOVA (Analysis of Variance)** tests whether groups differ with respect to **one dependent variable**.

### 📌 Example

> Does mean **tumor size** differ between treatment groups?

```text
Groups
   ↓
Tumor Size
```

### 🔸 MANOVA

**MANOVA (Multivariate Analysis of Variance)** extends ANOVA to **multiple dependent variables**.

### 📌 Example

> Do treatment groups differ jointly in **tumor size and PSA level**?

```text
Groups
   ↓
 ┌────────────┐
 ↓            ↓
Tumor Size   PSA Level
```

### 🆚 ANOVA vs. MANOVA

| Method    | Dependent Variables | Example          |
| --------- | ------------------: | ---------------- |
| 📊 ANOVA  |                   1 | Tumor size       |
| 📈 MANOVA |           2 or more | Tumor size + PSA |

MANOVA is particularly useful when the dependent variables are **correlated**.

> 🖼️ **Figure:** Add ANOVA vs. MANOVA comparison figure from **PDF page 11**.

---

# 🌸 The Iris Dataset

## 9. 🌺 Introduction to the Iris Dataset

The **Iris dataset** is one of the most famous datasets used to demonstrate **statistical classification and multivariate analysis**.

It contains three Iris species:

* 🌷 *Iris setosa*
* 🌺 *Iris versicolor*
* 🌸 *Iris virginica*

Each species contains:

```text
50 observations
```

Therefore:

```text
3 species × 50 observations = 150 observations
```

The dataset was collected by **Edgar Anderson** and became famous through **Ronald Fisher's 1936 work on discriminant analysis**.

---

## 10. 📏 Variables in the Iris Dataset

Four numerical variables are measured for each flower:

1. 📏 Sepal length
2. ↔️ Sepal width
3. 📐 Petal length
4. ↔️ Petal width

There is also one categorical variable:

5. 🌸 Species

### 📋 Dataset Structure

| Sepal.Length | Sepal.Width | Petal.Length | Petal.Width | Species    |
| -----------: | ----------: | -----------: | ----------: | ---------- |
|          5.1 |         3.5 |          1.4 |         0.2 | setosa     |
|          7.0 |         3.2 |          4.7 |         1.4 | versicolor |
|          6.3 |         3.3 |          6.0 |         2.5 | virginica  |

The four flower measurements form the **multivariate feature space**.

---

# 💻 Exploring the Iris Dataset in R

## 11. 📂 Loading and Viewing the Iris Dataset

The Iris dataset is already built into **R**.

### 💻 R Code

```r
data(iris)

head(iris)
```

To examine its structure:

```r
str(iris)
```

### 📋 Variables

```text
Sepal.Length
Sepal.Width
Petal.Length
Petal.Width
Species
```

The `iris` object is an R **data frame**.

> 💡 Since `iris` is a built-in dataset, you do not need to download it separately.

---

## 12. 📈 Simple Scatter Plot

A **scatter plot** can be used to examine the relationship between two variables.

For example:

* Petal width
* Petal length

### 💻 R Code

```r
plot(
  iris$Petal.Width,
  iris$Petal.Length,
  xlab = "Petal Width (cm)",
  ylab = "Petal Length (cm)"
)
```

### 🔍 What Does the Plot Show?

Each point represents **one flower**.

The plot can help determine whether:

* 📈 Petal width increases with petal length
* 🔗 A relationship exists between the variables
* 📊 The relationship appears linear
* 🧩 Different clusters exist
* ⚠️ Outliers are present

> 📌 This is a **bivariate visualization** because only two variables are displayed.

---

## 13. 🎨 Scatter Plot with Species Coloring

Species information can be added using different colors.

### 💻 R Code

```r
plot(
  iris$Petal.Width,
  iris$Petal.Length,
  col = iris$Species,
  xlab = "Petal Width (cm)",
  ylab = "Petal Length (cm)"
)

legend(
  "bottomright",
  legend = levels(iris$Species),
  pch = 1,
  col = c(1, 2, 3)
)
```

### 🔍 Why Is This Useful?

Adding species information reveals **species-specific clustering**.

We can observe that:

* 🌷 *Iris setosa* is strongly separated from the other species
* 🌺 *Iris versicolor* and *Iris virginica* are closer together
* 📏 Petal measurements appear useful for distinguishing species

> 🖼️ **Figure:** Add colored scatter plot from **PDF page 15**.

---

## 14. 🔢 Pairwise Scatter Plots

When we have several numerical variables, looking at only one scatter plot may hide important relationships.

A **scatterplot matrix** displays pairwise relationships among several variables.

### 💻 R Code

```r
pairs(
  iris[, 1:4],
  col = iris$Species,
  upper.panel = NULL
)
```

The four numerical variables are:

```text
Sepal.Length
Sepal.Width
Petal.Length
Petal.Width
```

### 🎯 Purpose

Pairwise scatter plots help us:

* 🔗 Examine relationships between variables
* 📈 Identify correlations
* 🧩 Detect clusters
* 🌸 Compare species
* 🎯 Identify useful classification variables
* ⚠️ Detect unusual observations

> 💡 A scatterplot matrix is an important **exploratory multivariate visualization**.

> 🖼️ **Figure:** Add pairs plot from **PDF page 16**.

---

## 15. 📉 Profile / Pattern Plot

A **profile plot** can be used to compare how several measurements vary across groups.

### 💻 R Code

```r
library(viopoints)

boxplot(
  iris[1:4],
  border = "white",
  ylab = "Length or Width (cm)"
)

viopoints(
  as.matrix(iris[1:4]) ~ iris[, 5],
  col = 2:4,
  at = 1:4,
  lines = TRUE,
  line.col = 2:4,
  add = TRUE
)

legend(
  "topright",
  legend = levels(iris[, 5]),
  pch = 1,
  col = 2:4
)
```

### 🎯 Purpose

The profile plot helps visualize:

* 🌸 Differences among species
* 📊 Patterns across multiple variables
* 🎯 Variables that separate groups most clearly
* 🔗 Similarities between multivariate profiles

> 🖼️ **Figure:** Add profile plot from **PDF page 17**.

---

# 🧠 Key Concepts to Remember

| Concept                     | 💡 Meaning                                                       |
| --------------------------- | ---------------------------------------------------------------- |
| **Univariate data**         | One variable is analyzed                                         |
| **Bivariate analysis**      | Two variables are analyzed together                              |
| **Multivariate data**       | Multiple variables describe each observation                     |
| **Multivariate analysis**   | Multiple variables are analyzed jointly                          |
| **Correlation**             | Measures association between two variables                       |
| **Multiple regression**     | Multiple predictors with one outcome                             |
| **Multivariate regression** | Multiple outcomes modeled simultaneously                         |
| **ANOVA**                   | Compares groups using one dependent variable                     |
| **MANOVA**                  | Compares groups using multiple dependent variables               |
| **PCA**                     | Reduces dimensionality while retaining major variation           |
| **LDA**                     | Finds combinations of variables that discriminate between groups |

---

# 🩺 Quick Medical Example

Suppose a medical study records:

```text
Age
Weight
Blood Pressure
Cholesterol
Body Fat
```

### 1️⃣ Univariate

If we analyze only:

```text
Cholesterol
```

➡️ **Univariate analysis**

### 2️⃣ Bivariate

If we study:

```text
Cholesterol ↔ Body Fat
```

➡️ **Bivariate analysis**

### 3️⃣ Multivariate Regression

If we jointly model:

```text
Cholesterol + Body Fat
```

using:

```text
Age + Weight + Blood Pressure
```

➡️ **Multivariate regression analysis**

---

# 🎯 Summary

Multivariate statistics provides methods for analyzing datasets where observations are described by **multiple variables**.

Its major advantage is that it allows us to study:

* 🔗 Relationships between variables
* 📈 Correlations
* 🧩 Joint patterns
* 👥 Differences between groups
* 🎯 Classification patterns
* 📉 High-dimensional datasets

The **Iris dataset 🌸** is a classic example because every flower is described by **four numerical measurements** and a **species label**.

Exploratory techniques such as:

* 📈 Scatter plots
* 🔢 Scatterplot matrices
* 📉 Profile plots

help us understand the structure of multivariate data before applying more advanced methods such as:

* 📉 PCA
* 🎯 LDA
* 📊 MANOVA
* 📐 PLS
* 🧱 SVM
* 🌳 Random Forest
* 🧠 Artificial Neural Networks

> 🚀 **Takeaway:** Understanding multivariate statistics provides an important foundation for advanced statistics, data science, machine learning, and AI.
