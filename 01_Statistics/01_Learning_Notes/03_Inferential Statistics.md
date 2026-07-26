# 📊 Inferential Statistics

Inferential statistics uses **sample data** to make conclusions about a **population**.

Instead of studying everyone, we study a **sample** and estimate what is true for the whole population.

---

# 🌍 Population vs Sample

| Population | Sample |
|------------|--------|
| Entire group of interest | Small group selected from the population |
| Usually impossible to study completely | Easier and cheaper to collect |

### Example

Population:

```text
All adults living in Sweden
```

Sample:

```text
100 adults selected from Sweden
```

---

# 🎯 Why Inferential Statistics?

Different samples produce different results.

Example:

```text
Sample 1 Mean = 173.0 cm

Sample 2 Mean = 172.4 cm

Sample 3 Mean = 174.1 cm
```

This natural variation is called **sampling variability**.

Inferential statistics helps us measure this uncertainty.

---

# 📏 Standard Error (SE)

## Definition

Standard Error measures **how precise the sample mean is**.

Small SE → More precise estimate

Large SE → Less precise estimate

---

## Formula

```math
SE=\frac{s}{\sqrt{n}}
```

Where

- **s** = Sample Standard Deviation
- **n** = Sample Size

---

## Example

Given

```text
Sample Size = 100

SD = 8.8 cm
```

```math
SE=\frac{8.8}{\sqrt{100}}

=\frac{8.8}{10}

=0.88\text{ cm}
```

---

## Remember

Larger Sample

↓

Smaller SE

↓

More Precise Estimate

---

# 📐 Confidence Interval (CI)

A Confidence Interval gives a **range of plausible values** for the true population mean.

---

## Formula

```math
CI=\bar{x}\pm1.96\times SE
```

---

## Example

```text
Sample Mean = 173 cm

SE = 0.88 cm
```

Margin of Error

```math
1.96\times0.88=1.72
```

Confidence Interval

```text
173 ± 1.72

↓

171.3 cm – 174.7 cm
```

---

## Interpretation

A 95% confidence interval means:

> If we repeated the study many times, about **95% of the confidence intervals** would contain the true population mean.

---

# 📊 SD vs SE vs CI

| Measure | Purpose |
|---------|---------|
| SD | Spread of individual observations |
| SE | Precision of the sample mean |
| CI | Plausible range for the population mean |

---

# 🧠 Memory Tricks

📊 SD → Spread of Data

🎯 SE → Precision of Estimate

📐 CI → Plausible Range

---

# ✅ Key Takeaways

- Inferential statistics uses a **sample** to learn about a **population**.
- Different samples produce different results.
- **SE** measures the precision of the estimate.
- **CI** gives a plausible range for the true population value.
- Larger samples produce **smaller SE** and **narrower confidence intervals**.
