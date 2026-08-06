# 📦 Python Collections

> **A Beginner's Guide to Python Collections for Statistics and Data Science**

Python collections are used to **store multiple pieces of information**. They are the foundation of data analysis, scientific computing, and machine learning.

In this chapter, you'll learn the four built-in Python collections:

- 📋 Lists
- 📦 Tuples
- 📖 Dictionaries
- 🎯 Sets

---

# 📚 Table of Contents

1. What are Collections?
2. Overview of Python Collections
3. Lists
4. Tuples
5. Dictionaries
6. Sets
7. Accessing Data
8. Modifying Collections
9. Useful Functions
10. Comparison Table
11. When to Use Each Collection
12. Biological Examples
13. Key Takeaways

---

# 🤔 What are Collections?

A collection stores **multiple values** inside a single variable.

Instead of writing:

```python
patient1 = 142
patient2 = 145
patient3 = 139
patient4 = 141
```

We can write:

```python
blood_pressure = [142, 145, 139, 141]
```

Much simpler!

---

# 📊 Overview of Python Collections

| Collection | Ordered | Changeable | Allows Duplicates |
|------------|----------|------------|-------------------|
| 📋 List | ✅ | ✅ | ✅ |
| 📦 Tuple | ✅ | ❌ | ✅ |
| 📖 Dictionary | ✅ | ✅ | Keys must be unique |
| 🎯 Set | ❌ | ✅ | ❌ |

---

# 📋 Lists

Lists are the **most commonly used collection** in Python.

Lists are:

- Ordered
- Changeable
- Allow duplicate values

---

## Creating a List

```python
blood_pressure = [142, 145, 139, 141]
```

---

## Printing a List

```python
print(blood_pressure)
```

Output

```text
[142, 145, 139, 141]
```

---

## List with Different Data Types

```python
sample = [37, "E. coli", True, 4.5]
```

Although possible, scientific datasets usually contain one data type.

---

# 📏 Length of a List

```python
len(blood_pressure)
```

Output

```text
4
```

---

# 🔍 Accessing Elements

Python starts counting at **0**.

| Position | Value |
|----------|-------|
| 0 | 142 |
| 1 | 145 |
| 2 | 139 |
| 3 | 141 |

---

First value

```python
blood_pressure[0]
```

Output

```text
142
```

---

Third value

```python
blood_pressure[2]
```

Output

```text
139
```

---

Last value

```python
blood_pressure[-1]
```

Output

```text
141
```

---

# ✏️ Changing Values

```python
blood_pressure[1] = 150

print(blood_pressure)
```

Output

```text
[142, 150, 139, 141]
```

---

# ➕ Adding Items

Add to the end

```python
blood_pressure.append(148)
```

Result

```text
[142,150,139,141,148]
```

---

Insert at a specific position

```python
blood_pressure.insert(1, 143)
```

---

# ❌ Removing Items

Remove by value

```python
blood_pressure.remove(150)
```

---

Remove by position

```python
blood_pressure.pop(2)
```

---

Delete entire list

```python
del blood_pressure
```

---

# 📦 Tuples

Tuples are similar to lists but **cannot be changed**.

Use parentheses.

```python
days = ("Monday", "Tuesday", "Wednesday")
```

---

Access elements

```python
days[0]
```

Output

```text
Monday
```

---

Trying to modify a tuple

```python
days[0] = "Sunday"
```

Produces an error.

---

When should you use tuples?

- Dates
- DNA codons
- Coordinates
- Constants

---

# 📖 Dictionaries

Dictionaries store information as **key : value** pairs.

```python
patient = {

    "Name": "Alice",

    "Age": 35,

    "BP": 142
}
```

---

Access a value

```python
patient["Age"]
```

Output

```text
35
```

---

Add a new value

```python
patient["Weight"] = 72
```

---

Update

```python
patient["BP"] = 138
```

---

Print dictionary

```python
print(patient)
```

---

# 🎯 Sets

Sets store **unique values**.

Duplicates are automatically removed.

```python
genes = {

"TP53",

"BRCA1",

"TP53",

"EGFR"

}
```

Output

```text
{'TP53','BRCA1','EGFR'}
```

Notice

TP53 appears only once.

---

Add a value

```python
genes.add("MYC")
```

---

Remove a value

```python
genes.remove("EGFR")
```

---

# 🔧 Useful List Functions

Sort

```python
blood_pressure.sort()
```

---

Reverse

```python
blood_pressure.reverse()
```

---

Maximum

```python
max(blood_pressure)
```

---

Minimum

```python
min(blood_pressure)
```

---

Sum

```python
sum(blood_pressure)
```

---

# 🧬 Biological Example

```python
genes = [

"TP53",

"BRCA1",

"EGFR",

"MYC"

]

print(genes)
```

---

Patient information

```python
patient = {

"ID":101,

"Species":"Human",

"Age":35,

"Diagnosis":"Asthma"

}

print(patient)
```

---

DNA bases

```python
bases = ("A","T","G","C")
```

---

Unique proteins

```python
proteins = {

"P53",

"AKT",

"P53",

"EGFR"

}
```

---

# 📊 Comparison Table

| Feature | List | Tuple | Dictionary | Set |
|----------|------|--------|------------|-----|
| Ordered | ✅ | ✅ | ✅ | ❌ |
| Changeable | ✅ | ❌ | ✅ | ✅ |
| Duplicates | ✅ | ✅ | Keys ❌ | ❌ |
| Indexing | ✅ | ✅ | Keys | ❌ |

---

# 🎯 When Should I Use Each?

| Situation | Best Collection |
|------------|-----------------|
| Store numerical data | 📋 List |
| Fixed values | 📦 Tuple |
| Patient records | 📖 Dictionary |
| Unique genes | 🎯 Set |

---

# 🔬 Statistics Examples

Blood pressure measurements

```python
bp = [142,144,139,141]
```

Patient information

```python
patient = {

"Age":35,

"Sex":"Male",

"BMI":28

}
```

Treatment groups

```python
groups = ("Control","Drug A","Drug B")
```

Unique mutations

```python
mutations = {

"TP53",

"KRAS",

"EGFR"

}
```

---

# 💡 Tips

- ✅ Lists are the most commonly used collection in data science.
- ✅ Dictionaries are excellent for storing patient metadata.
- ✅ Tuples are useful when values should never change.
- ✅ Sets automatically remove duplicate values.

---

# 🎯 Key Takeaways

- 📦 Collections store multiple values in a single variable.
- 📋 Lists are ordered, changeable, and the most commonly used collection.
- 📦 Tuples are ordered but immutable.
- 📖 Dictionaries store information as **key–value pairs**.
- 🎯 Sets store only **unique values** and automatically remove duplicates.
- 🔍 Python indexing starts at **0**, unlike R, where indexing starts at **1**.
- 🧬 Collections are widely used in biological and statistical data analysis.
