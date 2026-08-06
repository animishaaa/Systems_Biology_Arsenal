# 📊 Matplotlib

> **Data Visualization with Python**

Matplotlib is the fundamental plotting library in Python.

It is used to create:

- 📈 Line plots
- 📊 Bar charts
- 📉 Scatter plots
- 📦 Boxplots
- 📋 Histograms
- 🥧 Pie charts

Almost every scientific visualization library in Python (including Seaborn) is built on top of Matplotlib.

---

# 📚 Table of Contents

1. What is Matplotlib?
2. Why Use Matplotlib?
3. Installing Matplotlib
4. Importing Matplotlib
5. Line Plots
6. Scatter Plots
7. Bar Charts
8. Histograms
9. Boxplots
10. Pie Charts
11. Figure Customization
12. Saving Figures
13. Matplotlib vs R Graphics
14. Biological Examples
15. Common Mistakes
16. Key Takeaways

---

# 📖 What is Matplotlib?

Matplotlib is the standard Python library for creating scientific figures.

It allows creation of:

- Publication-quality figures
- Statistical graphics
- Exploratory visualizations
- Presentation figures

---

# 🚀 Why Use Matplotlib?

Matplotlib is used to:

- 📊 Explore data
- 📈 Identify trends
- 📉 Detect outliers
- 📦 Visualize distributions
- 🧬 Present scientific results

---

# 📦 Installing Matplotlib

```bash
pip install matplotlib
```

Most Anaconda installations already include Matplotlib.

---

# 📥 Importing Matplotlib

```python
import matplotlib.pyplot as plt
```

`plt` is the standard alias.

---

# 📈 Line Plot

A line plot displays changes over time or ordered observations.

```python
import matplotlib.pyplot as plt

days = [1,2,3,4,5]

bp = [142,145,139,141,144]

plt.plot(days, bp)

plt.show()
```

---

# 📊 Adding Labels

```python
plt.plot(days, bp)

plt.title("Blood Pressure Over Time")

plt.xlabel("Day")

plt.ylabel("Blood Pressure (mmHg)")

plt.show()
```

---

# 🎨 Customizing Lines

Change line color.

```python
plt.plot(days, bp, color="red")
```

---

Change line style.

```python
plt.plot(days, bp, linestyle="--")
```

---

Change line width.

```python
plt.plot(days, bp, linewidth=3)
```

---

Add markers.

```python
plt.plot(days, bp, marker="o")
```

---

Combine options.

```python
plt.plot(
    days,
    bp,
    color="blue",
    marker="o",
    linewidth=2
)

plt.show()
```

---

# 📉 Scatter Plot

Scatter plots display relationships between two continuous variables.

```python
weight = [55,60,63,65,68]

chol = [3.8,4.0,4.2,4.4,4.7]

plt.scatter(weight, chol)

plt.show()
```

---

Add labels.

```python
plt.scatter(weight, chol)

plt.title("Weight vs Cholesterol")

plt.xlabel("Weight (kg)")

plt.ylabel("Cholesterol (mmol/L)")

plt.show()
```

---

# 📊 Bar Chart

```python
groups = [

"Control",

"Drug"

]

means = [

145,

138

]

plt.bar(groups, means)

plt.show()
```

---

# 📋 Histogram

Histograms display the distribution of continuous data.

```python
bp = [

142,

145,

139,

141,

148,

150,

143,

144

]

plt.hist(bp)

plt.show()
```

---

Change number of bins.

```python
plt.hist(bp, bins=5)

plt.show()
```

---

# 📦 Boxplot

Boxplots summarize a distribution and identify potential outliers.

```python
plt.boxplot(bp)

plt.show()
```

---

# 🥧 Pie Chart

```python
labels = [

"Male",

"Female"

]

sizes = [

45,

55

]

plt.pie(

sizes,

labels=labels,

autopct="%1.1f%%"

)

plt.show()
```

---

# 🎨 Figure Size

```python
plt.figure(figsize=(8,5))
```

---

Example

```python
plt.figure(figsize=(8,5))

plt.plot(days, bp)

plt.show()
```

---

# 🎨 Grid

```python
plt.grid(True)
```

---

# 🎨 Legend

```python
plt.plot(days, bp, label="Treatment")

plt.legend()

plt.show()
```

---

# 💾 Saving Figures

PNG

```python
plt.savefig(

"figure.png",

dpi=300

)
```

---

PDF

```python
plt.savefig(

"figure.pdf"

)
```

---

Always call `savefig()` **before** `show()`.

---

# ⚖️ Matplotlib vs R

| Python | R |
|----------|------|
| `plt.plot()` | `plot()` |
| `plt.hist()` | `hist()` |
| `plt.boxplot()` | `boxplot()` |
| `plt.bar()` | `barplot()` |
| `plt.scatter()` | `plot()` |

---

# 🧬 Biological Example

Blood pressure over time.

```python
days = [1,2,3,4,5]

bp = [142,144,143,141,139]

plt.plot(

days,

bp,

marker="o"

)

plt.xlabel("Day")

plt.ylabel("Blood Pressure")

plt.show()
```

---

Gene expression.

```python
genes = [

"A",

"B",

"C",

"D"

]

expression = [

4.2,

3.8,

5.1,

2.9

]

plt.bar(

genes,

expression

)

plt.show()
```

---

Distribution of cholesterol.

```python
chol = [

4.2,

4.8,

5.1,

4.6,

5.4,

5.0,

4.7,

5.3

]

plt.hist(chol)

plt.show()
```

---

# ⚠️ Common Mistakes

❌ Forgetting `plt.show()`.

The figure may not appear in some environments.

---

❌ Calling `savefig()` after `show()`.

Always save first.

Correct

```python
plt.savefig("plot.png")

plt.show()
```

---

❌ Forgetting labels.

Every scientific figure should include:

- Title
- X-axis label
- Y-axis label

---

# 💡 Tips

- 📊 Histograms are useful for assessing normality.
- 📦 Boxplots help identify outliers.
- 📉 Scatter plots are essential before correlation or regression.
- 📈 Line plots are suitable for repeated measurements or time-series data.
- 💾 Save publication figures with `dpi=300`.

---

# 🎯 Key Takeaways

- 📊 Matplotlib is the primary plotting library in Python.
- 📈 Line plots display trends over ordered observations.
- 📉 Scatter plots visualize relationships between continuous variables.
- 📦 Boxplots summarize distributions and highlight potential outliers.
- 📋 Histograms show the distribution of continuous data.
- 🥧 Pie charts display proportions.
- 💾 Figures can be exported as high-resolution PNG or PDF files for publication.

