# 🎨 Seaborn

> **Statistical Data Visualization with Python**

Seaborn is a Python library built on top of **Matplotlib** that creates beautiful, informative, and publication-quality statistical graphics.

It is specifically designed for **exploratory data analysis (EDA)** and is widely used in statistics, bioinformatics, machine learning, and data science.

---

# 📚 Table of Contents

1. What is Seaborn?
2. Why Use Seaborn?
3. Installing Seaborn
4. Importing Seaborn
5. Built-in Datasets
6. Scatter Plots
7. Line Plots
8. Histograms
9. Boxplots
10. Violin Plots
11. Bar Plots
12. Count Plots
13. Pair Plots
14. Heatmaps
15. Regression Plots
16. Themes and Styles
17. Seaborn vs Matplotlib
18. R vs Python
19. Biological Examples
20. Common Mistakes
21. Key Takeaways

---

# 📖 What is Seaborn?

Seaborn is a high-level visualization library for Python.

It provides:

- 📊 Better default graphics
- 📈 Statistical visualizations
- 🎨 Attractive color palettes
- 📋 Easy plotting with Pandas DataFrames

Seaborn is built directly on **Matplotlib**.

---

# 🚀 Why Use Seaborn?

Seaborn simplifies common statistical plots.

Advantages include:

- 📊 Publication-quality figures
- 📈 Fewer lines of code
- 🎨 Better default themes
- 📋 Native support for DataFrames
- 📉 Built-in statistical summaries

---

# 📦 Installing Seaborn

```bash
pip install seaborn
```

Most Anaconda installations already include Seaborn.

---

# 📥 Importing Seaborn

```python
import seaborn as sns
import matplotlib.pyplot as plt
```

---

# 📂 Built-in Datasets

Seaborn provides several example datasets.

List available datasets.

```python
sns.get_dataset_names()
```

Load the famous Iris dataset.

```python
iris = sns.load_dataset("iris")
```

View the first rows.

```python
iris.head()
```

---

# 🎨 Themes

Set a theme.

```python
sns.set_theme()
```

Dark grid.

```python
sns.set_style("darkgrid")
```

White grid.

```python
sns.set_style("whitegrid")
```

White background.

```python
sns.set_style("white")
```

Ticks.

```python
sns.set_style("ticks")
```

---

# 📉 Scatter Plot

```python
sns.scatterplot(
    data=iris,
    x="sepal_length",
    y="petal_length"
)

plt.show()
```

---

## Color by Group

```python
sns.scatterplot(
    data=iris,
    x="sepal_length",
    y="petal_length",
    hue="species"
)

plt.show()
```

---

# 📈 Line Plot

```python
sns.lineplot(
    data=iris,
    x="sepal_length",
    y="petal_length"
)

plt.show()
```

---

# 📋 Histogram

```python
sns.histplot(
    data=iris,
    x="sepal_length"
)

plt.show()
```

---

## Histogram with Density Curve

```python
sns.histplot(
    data=iris,
    x="sepal_length",
    kde=True
)

plt.show()
```

---

# 📦 Boxplot

```python
sns.boxplot(
    data=iris,
    x="species",
    y="petal_length"
)

plt.show()
```

Useful for:

- Detecting outliers
- Comparing groups
- Viewing medians

---

# 🎻 Violin Plot

A violin plot combines:

- Boxplot
- Density distribution

```python
sns.violinplot(
    data=iris,
    x="species",
    y="petal_length"
)

plt.show()
```

---

# 📊 Bar Plot

Displays the mean and confidence interval.

```python
sns.barplot(
    data=iris,
    x="species",
    y="petal_length"
)

plt.show()
```

---

# 🔢 Count Plot

Displays frequencies of categories.

```python
sns.countplot(
    data=iris,
    x="species"
)

plt.show()
```

Useful for categorical variables.

---

# 📈 Pair Plot

Shows relationships between all numerical variables.

```python
sns.pairplot(
    iris,
    hue="species"
)
```

Useful for:

- Correlation
- Clustering
- Pattern recognition

---

# 🔥 Heatmap

Create a correlation matrix.

```python
corr = iris.corr(
    numeric_only=True
)
```

Plot the heatmap.

```python
sns.heatmap(
    corr,
    annot=True,
    cmap="coolwarm"
)

plt.show()
```

Useful for:

- Correlation analysis
- Feature selection

---

# 📉 Regression Plot

```python
sns.regplot(
    data=iris,
    x="sepal_length",
    y="petal_length"
)

plt.show()
```

Automatically adds:

- Scatter plot
- Regression line
- Confidence interval

---

# 🎨 Figure Size

```python
plt.figure(figsize=(8,6))

sns.scatterplot(
    data=iris,
    x="sepal_length",
    y="petal_length"
)

plt.show()
```

---

# 💾 Saving Figures

```python
plt.savefig(
    "iris_plot.png",
    dpi=300,
    bbox_inches="tight"
)
```

Always call `savefig()` before `show()`.

---

# ⚖️ Seaborn vs Matplotlib

| Feature | Matplotlib | Seaborn |
|----------|------------|----------|
| Ease of use | Moderate | Easy |
| Default appearance | Basic | Professional |
| Statistical graphics | Limited | Excellent |
| DataFrame support | Limited | Native |
| Themes | Manual | Built-in |

---

# 🔄 Python vs R

| Python | R |
|----------|----|
| `sns.scatterplot()` | `plot()` |
| `sns.histplot()` | `hist()` |
| `sns.boxplot()` | `boxplot()` |
| `sns.violinplot()` | `vioplot()` |
| `sns.pairplot()` | `pairs()` |
| `sns.heatmap()` | `heatmap()` |

---

# 🧬 Biological Example

Gene expression by treatment.

```python
sns.boxplot(
    data=df,
    x="Treatment",
    y="Expression"
)

plt.show()
```

---

Patient age distribution.

```python
sns.histplot(
    data=df,
    x="Age",
    kde=True
)

plt.show()
```

---

Correlation between BMI and cholesterol.

```python
sns.regplot(
    data=df,
    x="BMI",
    y="Cholesterol"
)

plt.show()
```

---

Species comparison.

```python
sns.countplot(
    data=df,
    x="Species"
)

plt.show()
```

---

# ⚠️ Common Mistakes

❌ Forgetting to import Matplotlib.

```python
import matplotlib.pyplot as plt
```

---

❌ Calling `plt.show()` before `savefig()`.

Correct order:

```python
plt.savefig("figure.png")

plt.show()
```

---

❌ Using incorrect column names.

Always check:

```python
df.columns
```

---

# 💡 Tips

- 🎨 Use Seaborn for almost all statistical graphics.
- 📊 Pair plots quickly reveal relationships among variables.
- 🔥 Heatmaps are excellent for correlation matrices.
- 📦 Boxplots and violin plots are ideal for comparing groups.
- 📉 Regression plots simplify exploratory regression analysis.

---

# 🎯 Key Takeaways

- 🎨 Seaborn is built on top of Matplotlib.
- 📊 It creates publication-quality statistical graphics with minimal code.
- 📈 Native support for Pandas DataFrames simplifies plotting.
- 📦 Boxplots, violin plots, and histograms are valuable for exploratory analysis.
- 🔥 Heatmaps visualize correlation matrices.
- 📉 Regression plots combine scatter plots with fitted regression lines.
- 🧬 Seaborn is widely used in bioinformatics, statistics, and machine learning.

