# 📒 Statistics Handbook
# Chapter 5: Scientific Methodology & Experimental Design

---

# 📖 Introduction

Statistics is only useful if an experiment is **designed correctly**.

A poorly designed experiment can produce misleading conclusions,
even if the statistical analysis is perfect.

This chapter explains how to design valid scientific experiments.

---

# 📚 Topics Covered

| Topic | Purpose |
|--------|----------|
| Scientific Method | Steps of scientific research |
| Research Hypothesis vs Theory | Understand scientific evidence |
| Prediction vs Hypothesis | Learn the difference |
| Accuracy vs Precision | Measurement quality |
| Confounding Variables | Identify hidden variables |
| Controls | Remove bias |
| Placebo & Double-Blind Studies | Reduce psychological bias |
| Technical vs Biological Replicates | Correct replication |
| Paired vs Unpaired Data | Choosing statistical tests |
| Randomization | Reduce selection bias |
| Choosing Statistical Tests | Decision making |

---

# 🔬 Scientific Method

Scientific research follows a systematic process.

```text
Observation
      ↓
Research Question
      ↓
Research Hypothesis
      ↓
Prediction
      ↓
Experiment
      ↓
Collect Data
      ↓
Statistical Analysis
      ↓
Conclusion
      ↓
Accept or Reject Hypothesis
```

---

# 🧠 Example

Observation

↓

Garlic may improve immunity.

↓

Hypothesis

↓

Garlic increases TNF-α production.

↓

Prediction

↓

Cells treated with garlic will produce more TNF-α.

↓

Experiment

↓

Compare treated vs untreated cells.

---

# 📖 Research Hypothesis vs Theory

| Research Hypothesis | Theory |
|----------------------|--------|
| Educated guess | Well-supported explanation |
| Tested by one study | Supported by many studies |
| Easily rejected | Difficult to reject |
| Beginning of research | Built from years of evidence |

---

# 🎯 Hypothesis vs Prediction

## Research Hypothesis

Explains **why** something happens.

Example

Garlic stimulates immune cells.

---

## Prediction

States **what will happen** if the hypothesis is correct.

Example

Garlic-treated cells will produce more TNF-α.

---

# 🧪 Hypothesis Testing

Null Hypothesis (H₀)

No difference.

No effect.

---

Alternative Hypothesis (H₁)

Difference exists.

Effect exists.

---

Example

H₀

Drug has no effect.

H₁

Drug reduces blood pressure.

---

# 📌 Important Scientific Principle

Science **never proves** a hypothesis.

It only

- Supports it
- Or fails to support it

Future evidence can always change conclusions.

---

# 🎯 Accuracy vs Precision

## Accuracy

How close a measurement is to the **true value**.

---

## Precision

How close repeated measurements are to each other.

---

## Comparison

| Accurate | Precise |
|-----------|----------|
| Close to truth | Consistent |

---

## Four Possibilities

### 🎯 Accurate & Precise

```
●●
●●
```

Best case.

---

### 🎯 Accurate but Not Precise

```
●   ●

  ●

●
```

Correct on average.

---

### 🎯 Precise but Not Accurate

```
●●
●●
```

All measurements are wrong but consistent.

---

### 🎯 Neither

Random everywhere.

---

# ⚠️ Confounding Variables

## Definition

A confounder is a variable that influences **both**

- Independent variable
- Dependent variable

creating a false association.

---

## Example 1

People carrying matches

↓

Higher lung cancer

Did matches cause cancer?

❌ No

Confounder

↓

Smoking

---

## Example 2

Ice cream sales

↓

Drowning deaths

Did ice cream cause drowning?

❌ No

Confounder

↓

Summer

---

# 🧪 Controls

## Why?

Controls ensure that any observed difference is due to the treatment.

---

## Example

Treatment

Garlic extract

↓

Immune cells

Control

Immune cells

+

Same solvent

No garlic

Everything should be identical except the treatment.

---

# ❌ Poor Experimental Design

Treatment

↓

Incubator A

Control

↓

Incubator B

Different incubators introduce bias.

---

# 💊 Placebo Effect

Sometimes patients improve because they believe they received treatment.

Not because the treatment works.

---

## Example

Sugar pill

↓

Patient feels better.

This is the placebo effect.

---

# 👨‍⚕️ Double-Blind Study

Best clinical design.

Neither

- Patient

nor

- Doctor

knows who receives treatment.

This minimizes bias.

---

# 🧬 Technical vs Biological Replicates

## Technical Replicates

Same sample measured multiple times.

Purpose

Measure instrument precision.

Example

Same blood sample measured 3 times.

---

## Biological Replicates

Different biological samples.

Purpose

Measure biological variation.

Example

Blood collected from

Mouse 1

Mouse 2

Mouse 3

---

## Comparison

| Technical | Biological |
|------------|------------|
| Same sample | Different samples |
| Instrument precision | Biological variation |
| Not used for statistics | Used for statistics |

---

# 👥 Paired vs Unpaired Data

## Unpaired (Independent)

Different participants.

Example

Drug group

Control group

↓

Independent t-test

---

## Paired (Dependent)

Same participant.

Before

↓

After

↓

Paired t-test

---

# 🎲 Randomization

## Why?

Prevents selection bias.

Makes groups comparable.

---

## Simple Randomization

Examples

- Coin toss
- Random number generator

---

## Stratified Randomization

Useful when groups should have equal proportions.

Example

Male

↓

Randomize

Female

↓

Randomize

Combine groups.

---

# 📊 Choosing the Correct Statistical Test

Always ask these questions.

## Question 1

What type of data?

- Continuous
- Ordinal
- Categorical

---

## Question 2

Normal distribution?

Yes

↓

Parametric

No

↓

Non-parametric

---

## Question 3

How many groups?

- One
- Two
- Three or more

---

## Question 4

Independent?

or

Paired?

---

## Question 5

Relationship?

Prediction?

Difference?

---

# 🌳 Master Decision Tree

```text
What is the data type?

│

├── Continuous

│      │

│      ├── Normal?

│      │      │

│      │      ├── Yes

│      │      │      │

│      │      │      ├── One Sample

│      │      │      ├── Independent t-test

│      │      │      ├── Paired t-test

│      │      │      ├── One-Way ANOVA

│      │      │      └── Repeated Measures ANOVA

│      │      │

│      │      └── No

│      │             │

│      │             ├── Mann-Whitney

│      │             ├── Wilcoxon

│      │             ├── Sign Test

│      │             ├── Kruskal-Wallis

│      │             └── Friedman

│      │

│      ├── Relationship

│      │      │

│      │      ├── Pearson

│      │      └── Spearman

│      │

│      └── Prediction

│             │

│             └── Regression

│

└── Categorical

       │

       ├── Chi-Square Independence

       ├── Chi-Square Goodness-of-Fit

       ├── Fisher Exact

       ├── McNemar

       └── Two-Proportion Z-test
```

---

# 🧠 Common Mistakes

## ❌ Mistake 1

Thinking

Correlation

=

Causation

No.

Correlation only measures association.

---

## ❌ Mistake 2

Using technical replicates for statistics.

Always use biological replicates.

---

## ❌ Mistake 3

Ignoring confounders.

Always ask

"What else could explain this?"

---

## ❌ Mistake 4

No control group.

Impossible to know whether treatment caused the effect.

---

## ❌ Mistake 5

Choosing statistical tests after collecting data.

Statistical planning should happen **before** the experiment.

---

# ⭐ Favourite Questions

✔ Difference between

- Accuracy
- Precision

---

✔ Difference between

- Technical
- Biological replicates

---

✔ Difference between

- Research hypothesis
- Prediction

---

✔ Difference between

- Independent
- Paired data

---

✔ Difference between

- Correlation
- Causation

---

# 📋 Final Summary

| Topic | Key Idea |
|--------|----------|
| Scientific Method | Observation → Hypothesis → Prediction → Experiment |
| Research Hypothesis | Explains why |
| Prediction | States what will happen |
| Accuracy | Correct measurement |
| Precision | Consistent measurement |
| Confounder | Hidden variable affecting both X and Y |
| Control | Removes bias |
| Placebo | Psychological improvement |
| Double-Blind | Neither doctor nor patient knows treatment |
| Technical Replicates | Same sample measured repeatedly |
| Biological Replicates | Different biological samples |
| Randomization | Prevents selection bias |

---

# 🎯 Golden Rules

✅ Good experiments require good controls.

✅ Correlation does not imply causation.

✅ Biological replicates are used for statistical tests.

✅ Statistical tests should be chosen **before** collecting data.

✅ The quality of an experiment is just as important as the statistical analysis.
