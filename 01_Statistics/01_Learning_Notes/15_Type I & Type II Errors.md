# 🚨 Type I & Type II Errors

---

# 📖 What are Errors in Hypothesis Testing?

When we perform a statistical test, our conclusion may be correct or incorrect.

There are **two possible mistakes**:

- ❌ Type I Error (False Positive)
- ❌ Type II Error (False Negative)

---

# 🎯 Type I Error (α)

## Definition

A **Type I Error** occurs when we **reject the null hypothesis (H₀)** even though it is actually **true**.

This is also called a **False Positive**.

---

## Example

### Hypotheses

- H₀: The medicine has **no effect**.
- H₁: The medicine **works**.

Reality:

The medicine **does not work**.

But your statistical test concludes that it **does work**.

❌ This is a **Type I Error**.

---

## Probability

The probability of making a Type I Error is called:

\[
\alpha
\]

Usually:

\[
\alpha = 0.05
\]

Meaning:

There is a **5% chance** of falsely claiming a significant effect.

---

# 🎯 Type II Error (β)

## Definition

A **Type II Error** occurs when we **do not reject the null hypothesis** even though it is actually **false**.

This is also called a **False Negative**.

---

## Example

### Hypotheses

- H₀: The medicine has **no effect**.
- H₁: The medicine **works**.

Reality:

The medicine **does work**.

But your statistical test concludes that it **does not work**.

❌ This is a **Type II Error**.

---

## Probability

The probability is called:

\[
\beta
\]

---

# 💪 Statistical Power

Statistical Power tells us how likely we are to detect a real effect.

\[
Power = 1-\beta
\]

Higher power means:

- Less chance of a Type II Error
- Better ability to detect true differences

---

# 📊 Summary Table

| Reality | Decision | Result |
|---------|----------|--------|
| H₀ True | Do not reject H₀ | ✅ Correct |
| H₀ True | Reject H₀ | ❌ Type I Error |
| H₀ False | Reject H₀ | ✅ Correct |
| H₀ False | Do not reject H₀ | ❌ Type II Error |

---

# 🧠 Memory Trick

## Type I

Reject a true H₀

False Alarm 🚨

---

## Type II

Accept (or fail to reject) a false H₀

Missed Detection 🔍

---

# 🎯 Easy Way to Remember

Imagine a fire alarm.

### Type I Error

🔥 Alarm rings.

No fire.

False alarm.

---

### Type II Error

🔥 Real fire.

Alarm never rings.

Very dangerous.

---

# ⭐ Useful Tips

Type I Error

↓

False Positive

↓

Reject a true H₀

---

Type II Error

↓

False Negative

↓

Do not reject a false H₀
