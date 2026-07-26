# 🔍 Inferential Statistics

Inferential statistics are statistical methods used to **make conclusions about a population based on information collected from a sample**.

Instead of studying every individual in a population, researchers collect data from a **smaller representative sample** and use it to estimate what is likely true for the entire population.

---

# 🌍 Population vs Sample

## 👥 Population

### Definition

A **population** is the complete group of individuals or observations that we want to study.

### Example

```text
All adults living in Sweden
```

---

## 👨‍👩‍👧‍👦 Sample

### Definition

A **sample** is a smaller subset selected from the population.

Researchers collect data from the sample because studying the entire population is usually expensive, time-consuming, or impossible.

### Example

```text
100 adults selected from Sweden
```

Researchers may calculate the **average height** of these 100 adults and use it to estimate the **average height of all Swedish adults**.

---

# 🔹 What Is Inferential Statistics?

## 📖 Definition

**Inferential statistics** uses sample data to make **estimates, predictions, or conclusions** about a larger population.

Unlike **descriptive statistics**, which only summarize the data you collected, inferential statistics helps answer questions about the entire population.

---

## 🎯 Main Goal

```text
Sample
   │
   ▼
Estimate
   │
   ▼
Population
```

The goal is to use a **sample** to make reliable inferences about the **population**.

---

## 📝 Example

Suppose we measure the height of **100 Swedish adults**.

```text
Sample mean height = 173 cm
```

We use this sample mean to estimate the **average height of all Swedish adults**.

However, if we choose a different random sample of 100 adults, we may obtain a different sample mean.

For example:

```text
Sample 1 mean = 173.0 cm

Sample 2 mean = 172.4 cm

Sample 3 mean = 174.1 cm

Sample 4 mean = 172.8 cm
```

Each sample contains different individuals, so the calculated sample mean changes slightly.

This natural variation between samples is called **sampling variability**.

---

# 🎲 Sampling Variability

## Definition

**Sampling variability** refers to the natural differences that occur between sample statistics because every random sample contains different individuals.

Even when all samples come from the same population, they will usually produce slightly different results.

### Example

Suppose the true average height of Swedish adults is unknown.

Four different random samples produce:

```text
Sample 1 → 173.0 cm

Sample 2 → 172.4 cm

Sample 3 → 174.1 cm

Sample 4 → 172.8 cm
```

Each sample gives a slightly different estimate of the population mean.

This variation is expected and is the reason inferential statistics is needed.

---

# ⚠️ The Main Challenge

A sample usually **does not give the exact population value**.

For example,

```text
Sample Mean ≠ Population Mean
```

This happens because we only observe **part of the population**, not everyone.

Therefore, every estimate contains **uncertainty**.

The larger and more representative the sample, the smaller this uncertainty usually becomes.

---

# 🧰 How Inferential Statistics Handles Uncertainty

Inferential statistics provides tools to measure and quantify this uncertainty.

The two most important tools are:

1. 📏 **Standard Error (SE)**
2. 📐 **Confidence Interval (CI)**

These tools help us answer questions such as:

- 🎯 How precise is our sample estimate?
- 📊 How much could our estimate vary if we repeated the study?
- 🌍 What is the likely value of the true population mean?

---

# 📝 Quick Summary

| Concept | Description |
|---------|-------------|
| 🌍 Population | The entire group we want to study |
| 👥 Sample | A smaller group selected from the population |
| 🔍 Inferential Statistics | Uses a sample to make conclusions about a population |
| 🎲 Sampling Variability | Different samples produce slightly different results |
| ⚠️ Main Challenge | Sample estimates are never exactly equal to population values |
| 📏 Standard Error | Measures the precision of the sample estimate |
| 📐 Confidence Interval | Provides a likely range for the true population value |

---

# 🧠 Easy Memory Tricks

- 🌍 **Population** = Everyone
- 👥 **Sample** = A few people chosen from the population
- 🔍 **Inferential Statistics** = Using a sample to learn about the population
- 🎲 **Sampling Variability** = Different samples → Different answers
- 📏 **Standard Error (SE)** = Precision of the estimate
- 📐 **Confidence Interval (CI)** = Likely range of the true population value

---

## ✅ Key Takeaway

Inferential statistics allows researchers to **generalize findings from a sample to an entire population**.

Since every sample is different, there is always some uncertainty. Tools such as the **Standard Error (SE)** and **Confidence Interval (CI)** help us measure and communicate that uncertainty in a scientifically meaningful way.

---

# 📏 Standard Error (SE)

The **Standard Error (SE)** is one of the most important concepts in **Inferential Statistics**.

It tells us **how precise our sample estimate is** and helps us understand **how much a sample statistic (such as the sample mean) would vary if we repeated the study many times.**

---

# 🔹 What Is Standard Error?

## 📖 Definition

The **Standard Error (SE)** measures **how much a sample estimate is expected to vary from sample to sample**.

For the **sample mean**, it describes the **spread of sample means around the true population mean**.

### In simple words

> **Standard Error tells us how precise our sample mean is as an estimate of the true population mean.**

---

# 👉 Formula for the Standard Error of the Mean

## Formula

```math
SE=\frac{s}{\sqrt{n}}
```

Where:

- **SE** = Standard Error of the Mean
- **s** = Sample Standard Deviation
- **n** = Sample Size
- **√n** = Square Root of the Sample Size

---

# 🧮 Standard Error Example

Suppose we collect the following information:

```text
Sample Size (n) = 100 adults

Sample Mean = 173 cm

Sample Standard Deviation (s) = 8.8 cm
```

### Step 1: Write the formula

```math
SE=\frac{s}{\sqrt{n}}
```

---

### Step 2: Substitute the values

```math
SE=\frac{8.8}{\sqrt{100}}
```

---

### Step 3: Calculate the square root

```math
\sqrt{100}=10
```

---

### Step 4: Divide

```math
SE=\frac{8.8}{10}
```

```math
SE=0.88\text{ cm}
```

✅ **Standard Error = 0.88 cm**

---

# 💡 Interpretation

An **SE of 0.88 cm** means that:

> If we repeatedly selected random samples of **100 adults** and calculated the **mean height** of each sample, the sample means would typically vary by about **0.88 cm**.

A more statistical definition is:

> **The Standard Error is the standard deviation of the sampling distribution of the sample mean.**

---

# 🎯 Sampling Distribution of the Mean

To understand Standard Error, imagine repeating the same study many times.

For example:

```text
Take 1,000 random samples

Each sample contains 50 adults
```

Each sample will produce a slightly different mean.

Example:

```text
Sample 1 Mean = 171.8 cm

Sample 2 Mean = 173.1 cm

Sample 3 Mean = 172.6 cm

Sample 4 Mean = 174.0 cm

Sample 5 Mean = 172.9 cm
```

If we plotted all these sample means on a graph, they would form another distribution called the:

## 📊 Sampling Distribution of the Mean

Characteristics:

- 📍 Centre → Close to the true population mean
- 📏 Spread → Measured by the **Standard Error (SE)**

---

# 📉 Effect of Sample Size on Standard Error

The Standard Error formula is:

```math
SE=\frac{s}{\sqrt{n}}
```

Notice that the sample size (**n**) is in the denominator.

As the sample size increases:

- The denominator becomes larger.
- The Standard Error becomes smaller.

---

## Example

Suppose:

```text
Sample Standard Deviation = 8.8 cm
```

| Sample Size (n) | Standard Error |
|----------------:|---------------:|
| 25 | 1.76 cm |
| 100 | 0.88 cm |
| 400 | 0.44 cm |

### Calculations

For **n = 25**

```math
SE=\frac{8.8}{\sqrt{25}}

=\frac{8.8}{5}

=1.76
```

---

For **n = 100**

```math
SE=\frac{8.8}{\sqrt{100}}

=\frac{8.8}{10}

=0.88
```

---

For **n = 400**

```math
SE=\frac{8.8}{\sqrt{400}}

=\frac{8.8}{20}

=0.44
```

---

### Conclusion

- 👥 Larger sample → Smaller Standard Error
- 🎯 Smaller Standard Error → More precise estimate
- 👤 Smaller sample → Larger Standard Error
- ⚠️ Larger Standard Error → Less precise estimate

---

# 📊 Standard Deviation vs Standard Error

Although the names sound similar, **Standard Deviation (SD)** and **Standard Error (SE)** measure different things.

---

## 📏 Standard Deviation (SD)

### Definition

Standard Deviation measures **how spread out individual observations are around the sample mean**.

### Example

```text
Mean Height = 172.3 cm

Standard Deviation = 7.8 cm
```

This means:

> Individual people's heights vary around the mean by approximately **7.8 cm**.

✅ Standard Deviation is about **individual observations**.

---

## 🎯 Standard Error (SE)

### Definition

Standard Error measures **how much the sample mean would vary if we repeatedly selected different samples from the same population**.

### Example

Suppose:

```text
Sample Standard Deviation = 7.8 cm

Sample Size = 5
```

### Step 1

```math
SE=\frac{7.8}{\sqrt{5}}
```

### Step 2

```math
SE\approx\frac{7.8}{2.236}
```

### Step 3

```math
SE\approx3.49\text{ cm}
```

✅ **Standard Error ≈ 3.5 cm**

This means:

> If we repeatedly selected samples of **five people**, the **sample means** would vary by approximately **3.5 cm**.

✅ Standard Error is about **sample means**, **not individual people**.

---

# ✅ Key Difference: Standard Deviation vs Standard Error

| Feature | Standard Deviation (SD) | Standard Error (SE) |
|----------|-------------------------|---------------------|
| Describes | Spread of individual values | Spread of sample estimates |
| Main Question | How different are individuals? | How precise is the sample mean? |
| Affected by Sample Size? | ❌ Not directly | ✅ Yes |
| Decreases when Sample Size Increases? | ❌ Not necessarily | ✅ Yes |
| Units | Same as original data | Same as original data |

---

# 🧠 Easy Memory Trick

## Standard Deviation (SD)

```text
SD = Spread of Data
```

Think:

> **How much do individual observations vary?**

---

## Standard Error (SE)

```text
SE = Sampling Error
```

Think:

> **How precise is my sample estimate?**

---

# 🏹 Analogy: Archery Target

Imagine each arrow represents the **mean from one random sample**.

---

## 🎯 Small Standard Error

```text
       ✖ ✖
      ✖ 🎯 ✖
       ✖ ✖
```

The sample means are tightly clustered around the true population mean.

✅ High precision

---

## 🎯 Large Standard Error

```text
✖               ✖

        🎯

    ✖                ✖
```

The sample means are widely scattered.

❌ Low precision

---

# 📌 Summary

Standard Error answers one important question:

> **"If I repeated this study many times, how much would my sample mean change?"**

### Remember:

- 📏 **Standard Deviation** → Variation among individual observations
- 🎯 **Standard Error** → Variation among sample means
- 👥 Larger Sample → Smaller Standard Error
- 📉 Smaller Standard Error → More precise estimate
- 📈 Larger Standard Error → Less precise estimate

---

# 📝 Quick Revision

| Concept | Meaning |
|---------|---------|
| **Standard Error (SE)** | Measures the precision of the sample mean |
| **Formula** | `SE = s / √n` |
| **Small SE** | Sample mean is more precise |
| **Large SE** | Sample mean is less precise |
| **Large Sample Size** | Smaller SE |
| **Small Sample Size** | Larger SE |
| **Used In** | Confidence Intervals, Hypothesis Testing, Inferential Statistics |

---

# 📐 Confidence Interval (CI)

A **Confidence Interval (CI)** is one of the most important concepts in **Inferential Statistics**.

Instead of reporting only a single estimate (such as the sample mean), a confidence interval provides a **range of plausible values** for the true population parameter.

---

# 🔹 What Is a Confidence Interval?

## 📖 Definition

A **Confidence Interval (CI)** is a range of plausible values for an **unknown population parameter**.

For example, it can be used to estimate the **true population mean**.

A confidence interval combines three important components:

- 📊 The sample estimate
- 📏 The standard error (SE)
- 🎯 A critical value

---

# 📐 General Form

A confidence interval can be written as:

```text
Confidence Interval = Estimate ± Margin of Error
```

For a **large-sample 95% confidence interval** for the population mean:

```math
CI=\bar{x}\pm1.96\times SE
```

Where:

| Symbol | Meaning |
|---------|---------|
| **x̄** | Sample mean |
| **SE** | Standard Error |
| **1.96** | Critical value for an approximate 95% confidence level |

---

# 🧮 Confidence Interval Example

Suppose researchers measure the heights of **100 adults** and find:

```text
Sample Mean = 173 cm

Standard Error = 0.88 cm
```

### Step 1: Write the formula

```math
CI=\bar{x}\pm1.96\times SE
```

---

### Step 2: Substitute the values

```math
CI=173\pm1.96\times0.88
```

---

### Step 3: Calculate the Margin of Error

```math
1.96\times0.88=1.7248
```

Approximately,

```text
Margin of Error ≈ 1.72 cm
```

---

### Step 4: Calculate the Confidence Interval

```math
CI=173\pm1.72
```

Lower limit:

```math
173-1.72=171.28
```

Upper limit:

```math
173+1.72=174.72
```

Rounded to one decimal place:

```text
95% Confidence Interval

171.3 cm – 174.7 cm
```

✅ **95% Confidence Interval = 171.3 cm to 174.7 cm**

---

# 🧠 How to Interpret a 95% Confidence Interval

### Common (Informal) Interpretation

> We are **95% confident** that the true population mean lies between **171.3 cm and 174.7 cm**.

---

### More Statistically Precise Interpretation

A confidence interval is a **procedure**, not a probability statement about one specific interval.

A better interpretation is:

> If we repeatedly selected random samples and calculated a 95% confidence interval from each sample using the same method, **approximately 95% of those intervals would contain the true population mean.**

---

# ⚠️ What a 95% Confidence Interval Does NOT Mean

A common misconception is:

> ❌ "95% of individual people have heights between 171.3 cm and 174.7 cm."

This is **incorrect**.

A confidence interval estimates **where the population mean is likely to be**.

It **does not describe the spread of individual observations**.

The spread of individual observations is measured by the **Standard Deviation (SD)**.

---

# 🔁 Repeated-Sampling Interpretation

Imagine repeating the same study many times.

```text
Take 100 random samples.

Calculate a 95% confidence interval for each sample.
```

Some intervals might be:

```text
Sample 1 → 171.1 – 174.5 cm

Sample 2 → 172.0 – 175.2 cm

Sample 3 → 170.8 – 174.0 cm

Sample 4 → 171.6 – 175.0 cm
```

Most intervals will capture the true population mean.

Approximately:

- ✅ 95 out of 100 intervals contain the true mean.
- ❌ About 5 out of 100 intervals miss it.

This is why it is called a **95% confidence procedure**.

---

# 📏 Margin of Error

## Definition

The **Margin of Error (MOE)** is the amount added to and subtracted from the sample estimate.

For a **95% confidence interval**:

```math
\text{Margin of Error}=1.96\times SE
```

Using our example:

```math
1.96\times0.88=1.72\text{ cm}
```

Therefore,

```text
173 ± 1.72 cm
```

The confidence interval extends **1.72 cm below** and **1.72 cm above** the sample mean.

---

# 📉 Narrow vs Wide Confidence Intervals

## 📏 Narrow Confidence Interval

Example:

```text
172.5 – 173.5 cm
```

A narrow confidence interval suggests:

- ✅ Small Standard Error
- ✅ Greater precision
- ✅ Usually a larger sample size

---

## 📐 Wide Confidence Interval

Example:

```text
165 – 181 cm
```

A wide confidence interval suggests:

- ⚠️ Large Standard Error
- ⚠️ Lower precision
- ⚠️ Usually a smaller sample or highly variable data

---

# 💡 Why Does Confidence Interval Width Matter?

The width of a confidence interval tells us **how precise our estimate is**.

| Narrow CI | Wide CI |
|------------|----------|
| More precise estimate | Less precise estimate |
| Smaller SE | Larger SE |
| Usually larger sample | Usually smaller sample |

---

# 📝 Quick Summary

| Concept | Description |
|---------|-------------|
| **Confidence Interval (CI)** | A plausible range for the true population parameter |
| **Formula** | `Estimate ± Margin of Error` |
| **95% CI Formula** | `x̄ ± 1.96 × SE` |
| **Margin of Error** | `1.96 × SE` |
| **Narrow CI** | More precise estimate |
| **Wide CI** | Less precise estimate |
| **95% Interpretation** | About 95% of confidence intervals from repeated samples would contain the true population mean |

---

# 🧠 Easy Memory Tricks

- 📐 **Confidence Interval (CI)** = Plausible range for the population value
- 📏 **Margin of Error** = Distance from the estimate to each end of the interval
- 📊 **Small SE → Narrow CI**
- 👥 **Large Sample → Smaller SE → Narrower CI**
- 🎯 **Narrow CI → More Precise Estimate**
- ⚠️ **Wide CI → Less Precise Estimate**

---

# ✅ Key Takeaway

A **Confidence Interval (CI)** provides a range of plausible values for the true population parameter rather than relying on a single sample estimate.

A **narrow confidence interval** indicates greater precision, while a **wide confidence interval** indicates more uncertainty. The width of the interval is largely determined by the **Standard Error (SE)**, which depends on the variability of the data and the sample size.

---
# 📏 What Affects Confidence Interval Width?

The **width of a Confidence Interval (CI)** tells us **how precise our estimate is**.

A **narrow confidence interval** indicates a more precise estimate, while a **wide confidence interval** indicates greater uncertainty.

The width of a confidence interval is mainly influenced by **three factors**:

1. 👥 Sample Size
2. 📊 Standard Deviation
3. 🎯 Confidence Level

---

# 1️⃣ Sample Size

The **sample size (n)** has a major impact on the width of a confidence interval.

A larger sample size reduces the **Standard Error (SE)**, producing a narrower confidence interval.

### Relationship

```text
Larger Sample Size
        ↓
Smaller Standard Error
        ↓
Narrower Confidence Interval
```

### Summary

- 👥 Larger Sample → Smaller SE → Narrower CI
- 👤 Smaller Sample → Larger SE → Wider CI

---

# 2️⃣ Standard Deviation (SD)

The **Standard Deviation (SD)** measures the variability of individual observations.

If the data are highly variable, the Standard Error becomes larger, resulting in a wider confidence interval.

### Relationship

```text
Larger Standard Deviation
          ↓
Larger Standard Error
          ↓
Wider Confidence Interval
```

### Summary

- 📊 Larger SD → Larger SE → Wider CI
- 📉 Smaller SD → Smaller SE → Narrower CI

---

# 3️⃣ Confidence Level

The **confidence level** determines how confident we want to be that the interval contains the true population parameter.

Higher confidence requires a wider interval.

### Comparison

| Confidence Level | Interval Width |
|-----------------:|---------------|
| **90%** | Narrower |
| **95%** | Wider |
| **99%** | Widest |

A wider interval provides greater confidence that the procedure captures the true population parameter.

---

# 📌 Summary

| Factor | Effect on Confidence Interval |
|---------|------------------------------|
| Larger Sample Size | Narrower CI |
| Larger Standard Deviation | Wider CI |
| Higher Confidence Level | Wider CI |

---

# 🔗 Relationship Between SD, SE and CI

The concepts of **Standard Deviation (SD)**, **Standard Error (SE)**, and **Confidence Interval (CI)** are closely related.

---

## 📊 Standard Deviation (SD)

Measures the **variation among individual observations**.

---

## 📏 Standard Error (SE)

Measures the **uncertainty or precision of the sample estimate**.

---

## 📐 Confidence Interval (CI)

Uses the **sample estimate** and its **Standard Error** to calculate a plausible range for the true population parameter.

---

## Relationship

```text
Standard Deviation
        ↓
Standard Error
        ↓
Confidence Interval
```

More specifically,

### Step 1: Calculate the Standard Error

```math
SE=\frac{SD}{\sqrt{n}}
```

### Step 2: Calculate the Confidence Interval

```math
CI=\text{Estimate}\pm\text{Critical Value}\times SE
```

---

# 📋 Complete Worked Example

Suppose researchers measure the heights of **100 adults**.

They obtain:

```text
Sample Mean = 173 cm

Sample Standard Deviation = 8.8 cm

Sample Size = 100
```

---

## Step 1: Calculate the Standard Error

Formula:

```math
SE=\frac{SD}{\sqrt{n}}
```

Substitute the values:

```math
SE=\frac{8.8}{\sqrt{100}}
```

Since

```math
\sqrt{100}=10
```

Therefore,

```math
SE=\frac{8.8}{10}=0.88\text{ cm}
```

✅ **Standard Error = 0.88 cm**

---

## Step 2: Calculate the Margin of Error

For a **95% confidence interval**,

```math
\text{Margin of Error}=1.96\times SE
```

Substitute the values:

```math
1.96\times0.88=1.72
```

✅ **Margin of Error = 1.72 cm**

---

## Step 3: Calculate the Confidence Interval

```math
CI=173\pm1.72
```

Lower limit:

```math
173-1.72=171.28
```

Upper limit:

```math
173+1.72=174.72
```

Rounded to one decimal place:

```text
95% Confidence Interval

171.3 cm – 174.7 cm
```

---

# 💡 Interpretation

From this example:

- 📊 Sample Mean = **173 cm**
- 📏 Standard Deviation = **8.8 cm**
- 🎯 Standard Error = **0.88 cm**
- 📐 95% Confidence Interval = **171.3–174.7 cm**

This suggests that the **true population mean height** is plausibly between **171.3 cm and 174.7 cm**.

---

# 🔬 Why Standard Error and Confidence Interval Matter

## 📏 Standard Error

The **Standard Error** measures the precision of the sample estimate.

| Small SE | Large SE |
|-----------|----------|
| More precise estimate | Less precise estimate |

---

## 📐 Confidence Interval

The **Confidence Interval** provides a plausible range for the population parameter.

| Narrow CI | Wide CI |
|------------|---------|
| Greater precision | Lower precision |

Together, **SE** and **CI** allow researchers to make informed conclusions about populations instead of relying only on sample values.

---

# 💊 Medical Research Example

Suppose researchers test a medicine on **100 patients**.

### Study 1

```text
Mean Blood Pressure Reduction = 10 mmHg

95% Confidence Interval = 8–12 mmHg
```

This suggests that the **true average reduction** is plausibly between **8 mmHg and 12 mmHg**.

---

### Study 2

```text
Mean Blood Pressure Reduction = 10 mmHg

95% Confidence Interval = -2–22 mmHg
```

Although both studies have the same sample mean, the second study has a **much wider confidence interval**.

This indicates:

- Lower precision
- Greater uncertainty
- Less confidence in the estimate

---

# ⚠️ Important Statistical Note

The familiar confidence interval formula

```math
CI=\bar{x}\pm1.96\times SE
```

is appropriate when:

- ✅ The sample size is large.
- ✅ The sampling distribution is approximately normal.
- ✅ A normal-distribution critical value is appropriate.

---

For **smaller samples**, especially when the **population standard deviation is unknown**, researchers usually use the **t-distribution**.

```math
CI=\bar{x}\pm t^*\times SE
```

Where:

- **t\*** is the critical value from the **t-distribution**.
- Its value depends on the **sample size** and **degrees of freedom**.

---

# ✅ Quick Comparison

| Measure | What It Describes | Example Interpretation |
|---------|-------------------|------------------------|
| **Mean** | Centre of the sample | Average height is **173 cm** |
| **Standard Deviation (SD)** | Variation among individuals | Individual heights vary around the mean |
| **Standard Error (SE)** | Precision of the sample mean | Sample means vary across repeated samples |
| **Confidence Interval (CI)** | Plausible range for the population mean | True mean is estimated to be **171.3–174.7 cm** |

---

# 🧠 Easy Memory Tricks

- 🌍 **Population** = Everyone of interest
- 👥 **Sample** = Smaller selected group
- 📊 **Standard Deviation (SD)** = Spread of individual data
- 🎯 **Standard Error (SE)** = Precision of the sample estimate
- 📐 **Confidence Interval (CI)** = Plausible range for the population value
- 👥 **Larger Sample** → Smaller SE
- 📏 **Smaller SE** → Narrower CI
- ✅ **Narrower CI** → More precise estimate

---

# 📝 Final Summary

Inferential statistics allows researchers to **use a sample to draw conclusions about an entire population**.

Since different samples produce different results, every estimate contains **uncertainty**.

The **Standard Error (SE)** measures how much a sample statistic is expected to vary across repeated samples.

The **Confidence Interval (CI)** uses the sample estimate and its Standard Error to provide a **plausible range** for the true population parameter.

---

## 🎯 Remember

```text
Standard Deviation (SD)
        ↓
Variation among individuals

Standard Error (SE)
        ↓
Precision of the sample mean

Confidence Interval (CI)
        ↓
Plausible range for the population mean
```

---

# 📚 Key Takeaways

- 📊 **Standard Deviation (SD)** measures variability among individual observations.
- 📏 **Standard Error (SE)** measures the precision of the sample estimate.
- 📐 **Confidence Interval (CI)** estimates a plausible range for the true population parameter.
- 👥 Larger samples produce **smaller SEs** and **narrower confidence intervals**.
- 🎯 Narrow confidence intervals indicate **more precise estimates**.
- ⚠️ Wider confidence intervals indicate **greater uncertainty**.

