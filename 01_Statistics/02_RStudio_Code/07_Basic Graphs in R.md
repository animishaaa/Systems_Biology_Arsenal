# 📊 Basic Graphs in R

Graphs are one of the most important ways to **summarize and visualize data**.

R provides several built-in functions to create graphs, such as:

- 📊 Bar Plot
- 📈 Histogram
- 📉 Box Plot
- 📍 Scatter Plot
- 📐 Q-Q Plot
- 📦 Pie Chart

---

# 📝 Example Dataset

```r
Sex <- c("M","F","F","F","M","M","F","M","F","M")
Sex <- factor(Sex)

Weight <- c(80,58,65,70,90,100,50,91,75,87)

df <- data.frame(Sex, Weight)
```

| Person | Sex | Weight (kg) |
|-------:|:---:|------------:|
|1|M|80|
|2|F|58|
|3|F|65|
|4|F|70|
|5|M|90|
|6|M|100|
|7|F|50|
|8|M|91|
|9|F|75|
|10|M|87|

---

# 🎯 Why do we use graphs?

Graphs help us

- 📊 summarize data
- 👀 identify patterns
- 📈 compare groups
- 📉 detect outliers
- 🔍 understand distributions
- 🧪 check assumptions before statistical tests

---

# 📚 Types of Graphs

| Graph | Used For |
|---------|------------|
| Bar Plot | Compare categories |
| Histogram | Distribution of continuous data |
| Box Plot | Spread and outliers |
| Scatter Plot | Relationship between two variables |
| Q-Q Plot | Check normality |

---
---

# 📊 Bar Plot in R

A **bar plot** compares numerical values between different groups.

In this example, we compare the **mean weight** of males and females.

---

# Step 1: Calculate Mean

```r
means <- tapply(Weight, Sex, mean)

means
```

Output

```
F    M
63.6 89.6
```

---

# Step 2: Create a Bar Plot

```r
pp <- barplot(means)
```

---

# Step 3: Add Labels

```r
pp <- barplot(
  means,
  ylim=c(0,120),
  xlab="Sex",
  ylab="Mean Weight (kg)",
  names.arg=c("Female","Male")
)
```

## 📌 Arguments

| Argument | Meaning |
|-----------|----------|
| ylim | Y-axis range |
| xlab | X-axis label |
| ylab | Y-axis label |
| names.arg | Labels below bars |

---

# Step 4: Add a Border

```r
box()
```

Adds a border around the graph.

---

# Step 5: Change Colors

```r
barplot(
  means,
  ylim=c(0,120),
  xlab="Sex",
  ylab="Mean Weight (kg)",
  names.arg=c("Female","Male"),
  col=c("red","blue")
)
```

---

# 🎨 Common Colors

```r
col="red"
col="blue"
col="green"
col="yellow"
col="orange"
col="pink"
col="gray"
col="black"
col="purple"
```

---

# 📚 Help Page

```r
help(barplot)
```

or

```r
?barplot
```

---

# 🎯 Key Points

✅ Used for categorical comparisons

✅ Height = numerical value

✅ Width has no meaning

✅ Easy to customize

---

# 📏 Error Bars

Bar plots should usually include **error bars**.

Error bars show variability in the data.

There are two common choices:

| Error Bar | Represents |
|------------|------------|
| SD | Variation of the data |
| SE | Precision of the mean |

---

# Step 1: Calculate SD

```r
std <- tapply(Weight, Sex, sd)

std
```

Output

```
F 9.86

M 7.23
```

---

# Step 2: Draw Error Bars

```r
arrows(
pp,
means+std,
pp,
means-std,
angle=90,
code=3,
length=0.2
)
```

---

# Explanation

| Argument | Meaning |
|-----------|----------|
| pp | X-position of bars |
| means+std | Upper limit |
| means-std | Lower limit |
| angle=90 | Horizontal cap |
| code=3 | Both directions |
| length=0.2 | Cap size |

---

# 📌 Why Error Bars?

Without error bars

📊 Mean only

With error bars

📊 Mean + variability

Much more informative.

---
---

# 📈 Histogram

A histogram shows the **distribution** of a continuous variable.

Each bar is called a **bin**.

Unlike bar plots:

- Bars touch each other.
- Order matters.
- Width represents an interval.

---

# Histogram of Male Weights

```r
hist(df$Weight[df$Sex=="M"])
```

---

# Better Labels

```r
hist(
df$Weight[df$Sex=="F"],
xlab="Weight (kg)",
main="Histogram of Female Weights"
)
```

---

# Change Bin Width

```r
dat <- df$Weight[df$Sex=="F"]

w <- 10

hist(
dat,
breaks=seq(min(dat),max(dat)+w,by=w)
)
```

---

# Choosing Bin Width

Smaller bins

✅ More detail

Larger bins

✅ Smoother graph

---

# Rule of Thumb

Number of bins ≈

```
√n
```

Example

100 observations

```
√100 = 10 bins
```

---

# 📈 Add a Normal Curve

```r
x <- df$Weight[df$Sex=="M"]

h <- hist(x)

xfit <- seq(65,110)

yfit <- dnorm(
xfit,
mean=mean(x),
sd=sd(x)
)

width <- diff(h$mids[1:2])
height <- length(x)

yfit <- yfit*width*height

lines(
xfit,
yfit,
col="blue",
lwd=2
)
```

---

# Interpretation

If the histogram follows the blue curve,

✅ Data are approximately normally distributed.

---
---

# 📐 Normal Q-Q Plot

A Q-Q plot compares your data with a theoretical normal distribution.

---

## Create Q-Q Plot

```r
x <- df$Weight[df$Sex=="F"]

qqnorm(x)

qqline(x)
```

---

# Interpretation

✅ Points close to the line

→ Normal distribution

❌ Strong curve away from line

→ Not normally distributed

---

# Rule

| Pattern | Interpretation |
|----------|----------------|
| Straight line | Normal |
| Curved | Non-normal |
| S-shaped | Skewed |
| Extreme points | Outliers |

---

# Why is Q-Q Plot Useful?

Many statistical tests assume

- Normality
- Equal variance

Always check before performing:

- t-test
- ANOVA
- Linear Regression

---
---

# 📚 R Graph Cheat Sheet

A quick reference for the most commonly used graphing functions in **Base R**.

---

## 📊 Graph Functions

| Function | Purpose | Example |
|----------|---------|---------|
| `barplot()` | 📊 Create a bar plot | `barplot(means)` |
| `hist()` | 📈 Create a histogram | `hist(df$Weight)` |
| `boxplot()` | 📦 Create a box plot | `boxplot(Weight ~ Sex)` |
| `plot()` | 📍 Create a scatter plot or line plot | `plot(x, y)` |
| `qqnorm()` | 📐 Generate a Normal Q-Q Plot | `qqnorm(x)` |
| `qqline()` | 📏 Add a reference line to a Q-Q plot | `qqline(x)` |
| `lines()` | 📉 Add lines to an existing graph | `lines(x, y)` |
| `arrows()` | 📏 Add error bars or arrows | `arrows(x0, y0, x1, y1)` |
| `box()` | 🖼️ Add a border around the graph | `box()` |
| `help()` or `?` | 📖 Open the help page for a function | `help(barplot)` or `?barplot` |

---

# 🎨 Common Graph Customization Options

| Argument | Purpose | Example |
|----------|---------|---------|
| `main` | Graph title | `main="Histogram"` |
| `xlab` | X-axis label | `xlab="Weight"` |
| `ylab` | Y-axis label | `ylab="Frequency"` |
| `col` | Bar or point color | `col="blue"` |
| `ylim` | Set Y-axis limits | `ylim=c(0,120)` |
| `xlim` | Set X-axis limits | `xlim=c(0,100)` |
| `names.arg` | Labels for bars | `names.arg=c("Female","Male")` |
| `cex.axis` | Axis label size | `cex.axis=1.4` |
| `cex.lab` | Axis title size | `cex.lab=1.6` |
| `cex.main` | Main title size | `cex.main=1.5` |

---

# 📏 Error Bar Functions

| Function | Purpose |
|----------|---------|
| `sd()` | Calculate Standard Deviation (SD) |
| `mean()` | Calculate Mean |
| `arrows()` | Draw Error Bars |
| `tapply()` | Calculate statistics by groups |

---

# 📈 Distribution Functions

| Function | Purpose |
|----------|---------|
| `hist()` | Histogram |
| `qqnorm()` | Q-Q Plot |
| `qqline()` | Reference Line |
| `dnorm()` | Normal Distribution Density |
| `lines()` | Draw Normal Curve |

---

# 📋 Helpful Commands

```r
help(barplot)

?hist

help(plot)

help(qqnorm)
```

---

# 🎯 Most Frequently Used Functions

| ⭐ Function | Why It Is Used |
|------------|----------------|
| `barplot()` | Compare group means |
| `hist()` | Check data distribution |
| `plot()` | Visualize relationships |
| `boxplot()` | Detect outliers and compare distributions |
| `qqnorm()` | Assess normality |
| `qqline()` | Compare data to a normal distribution |
| `arrows()` | Add error bars |
| `box()` | Add a border around the plot |
| `lines()` | Add fitted curves or trend lines |
| `help()` | Learn function syntax and options |

---

# 🚀 Quick Summary

| Goal | Function |
|------|----------|
| 📊 Compare categories | `barplot()` |
| 📈 Show data distribution | `hist()` |
| 📦 Detect outliers | `boxplot()` |
| 📍 Show relationships | `plot()` |
| 📐 Check normality | `qqnorm()` + `qqline()` |
| 📏 Add error bars | `arrows()` |
| 🎨 Customize graph | `col`, `main`, `xlab`, `ylab`, `ylim` |
| 📖 Get documentation | `help()` or `?function_name` |
