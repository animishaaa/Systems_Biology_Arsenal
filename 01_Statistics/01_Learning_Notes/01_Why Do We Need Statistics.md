# Introduction to Statistics

## Why Do We Need Statistics?

Suppose we want to know:

> What is the average height of human beings in the world?

There are billions of people in the world.

Measuring the height of every person would be extremely difficult, expensive, and time-consuming.

Instead, we randomly select about **10,000 people**.

#### Population vs. Sample

| Population | Sample |
|------------|--------|
| Entire group we want to study | Small group selected from the population |
| **Symbol:** μ (mu) | **Symbol:** x̄ (x-bar) |

**Example**

- **Population:** All 8 billion humans.
- **Sample:** 10,000 randomly selected people.

The goal of statistics is to use the **sample mean (x̄)** to estimate the **population mean (μ).**

---

**Here is the problem:**

What if we looked at people from only a few countries and concluded that the average height of all human beings is **170 cm**?

What about basketball players, whose average height may be around **180 cm**?

What about children, whose average height may be around **135 cm**?

So how do we solve this problem?

This is where **Statistics** comes into the picture.

It works like a detective.

The detective never sees the whole crime.

He only gets clues:

- A footprint
- A fingerprint
- A CCTV video

Using those clues, he makes the best possible conclusion.

Statistics works exactly the same way.

It never knows everything.

It only has a **sample**.

Using mathematics, it figures out:

- What is most likely true.
- How uncertain the answer is.
- Whether the evidence is strong enough.

---

## So how does statistics handle this problem?

By using:

- Confidence Interval
- Hypothesis Testing

### Confidence Interval

If we measure the height of **10,000 randomly selected people** around the world, statistics says:

> "I am not 100% sure, but I estimate that the true average height is around **170 cm**, with a margin of error of about **±10 cm**."

So the true average height could reasonably lie anywhere between **160 cm and 180 cm**.

This range is called the **confidence interval**.

Statistics does **not** confidently say the value is exactly between **160 cm and 180 cm**.

Instead, it says that, based on the sample, we are **95% confident** that the true population average lies within that interval.

---

### Hypothesis Testing

Hypothesis testing checks whether an observed difference is **real** or whether it could have happened **just by chance**.

**Example**

Suppose we measure:

- Average height in India = **168 cm**
- Average height in Sweden = **176 cm**

Is this **8 cm difference** a real difference between the populations?

Or did we simply happen to choose taller people from Sweden and shorter people from India?

Hypothesis testing helps answer this question mathematically.

If the probability of getting such a difference by chance is very small (typically **less than 5%**), we conclude that the difference is **statistically significant**.

Without statistics, we might say:

> "The average height of all people in the world is 170 cm."

That is an overconfident conclusion.

With statistics, we say:

> "Based on our sample, the estimated average height is 170 cm, and we are 95% confident that the true average lies within the confidence interval."

Statistics acknowledges uncertainty and provides mathematical tools to measure it instead of simply guessing.

---

## How does statistics help?

Statistics helps us:

- **Estimate:** How close our sample is to the true population.
- **Measure:** How much we could be wrong.
- **Compare:** Different groups (e.g., average height in India vs. Sweden).

Statistics is a smart way of learning about **large groups (populations)** by studying **small groups (samples)** while keeping track of how certain we are about our conclusions.

---

## Types of Data

### **1. Qualitative (Categorical)**

Describes qualities or categories (**not numbers**).

**Examples**

- Eye color (blue, green, black)
- Blood group
- Nationality

---

### **2. Quantitative (Numerical)**

Contains numerical values.

**Examples**

- Height
- Weight
- Number of siblings

*Quantitative data is divided into:*

#### **Discrete**

Things we **count**.

**Examples**

- Number of cars
- Number of children
- Number of apples

Only whole numbers are possible.

#### **Continuous**

Things we **measure**.

**Examples**

- Height = 172.3445 cm
- Weight = 63.5678 kg
- Time = 12.3451 seconds

Any value within a range is possible.

**Example: Apples**

- **Discrete:** Count apples (1, 2, 3...)
- **Continuous:** Measure the weight of apples.

---

## Scales of Measurement

### **Nominal**

Names or categories only.

**Examples**

- Gender
- Nationality
- Blood type

### **Ordinal**

Categories with an order.

**Examples**

- Happy, Neutral, Sad
- Low, Medium, High
- 1st, 2nd, 3rd

### **Interval**

Ordered values with equal intervals but **no true zero**.

**Example**

- Temperature in °C

### **Ratio**

Ordered values with equal intervals and a **true zero**.

**Examples**

- Height
- Weight
- Age
- Income

---

#### Why is Celsius an Interval Scale?

Imagine you have:

**₹0**

How much money do you have?

**None.**

Zero is a **true zero**.

Now think about weight.

**0 kg**

How much weight do you have?

**None.**

Again, a **true zero**.

Now consider temperature.

Suppose it is **0°C**.

Does that mean there is **no temperature**?

**No.**

Water can still be liquid (depending on pressure and impurities), molecules are still moving, and objects still contain thermal energy.

So **0°C** is simply an arbitrary reference point on the Celsius scale, chosen because pure water freezes there under standard atmospheric pressure.

---

### Relationship Between Data Types and Measurement Scales

| Qualitative (Categorical) | Quantitative (Numerical) |
|---------------------------|--------------------------|
| Nominal | Interval |
| Ordinal | Ratio |

---

#### Converting Ratio/Interval Data into Ordinal Data

Sometimes **ratio** (or **interval**) data is converted into ordinal categories.

**Example: Weight**

Continuous (ratio):

- 70 kg
- 38 kg
- 55 kg
- 105 kg
- 90 kg

Converted into ordinal categories:

- Underweight (<40 kg)
- Normal weight (40–100 kg)
- Overweight (>100 kg)

| Patient | Weight (kg) | Category (Ordinal) |
|---------:|------------:|-------------------|
| 1 | 70 | Normal |
| 2 | 38 | Underweight |
| 3 | 55 | Normal |
| 4 | 105 | Overweight |
| 5 | 90 | Normal |

**Why do this?**

- Easier interpretation — doctors may find **"Normal weight"** more meaningful than **"70 kg."**
- Easier comparison between groups.
- Some statistical methods require categorical or ordinal data (e.g., the **Chi-square test**).

**But there is a trade-off.**

When continuous data is converted into categories, **information is lost.**

**For example**

- Patient A = 41 kg
- Patient B = 99 kg

Both are classified as **Normal**, even though one is close to being underweight and the other is close to being overweight.

Therefore, researchers usually keep continuous data whenever possible and only categorize it when it is useful for analysis or communication.

**Summary**

- **Continuous (Interval/Ratio):** Most detailed and flexible.
- **Ordinal:** Easier to interpret but less precise.

---

## Two Main Purposes of Statistics

### 1. Descriptive Statistics

**Descriptive** = *"What does the data I collected look like?"*

It summarizes and describes the data.

**Examples**

- Mean
- Median
- Mode
- Standard deviation
- Charts and graphs

### 2. Inferential Statistics

**Inferential** = *"What can my sample tell me about the whole population?"*

It uses a sample to make conclusions about a population.

**Examples**

- Confidence intervals
- Hypothesis testing
- Regression
- ANOVA
