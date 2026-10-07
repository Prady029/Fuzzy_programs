# Fuzzy Programs — Fuzzy Computing Course (CURAJ)

[![Python](https://img.shields.io/badge/Python-3.x-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Course](https://img.shields.io/badge/Course-Fuzzy%20Computing-green.svg)]()
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A collection of **Jupyter Notebooks** implementing fuzzy set theory concepts and operations for the **Fuzzy Computing Course at CURAJ** (Central University of Rajasthan).

---

## 📚 Course Coverage

| Lab | Topic | Notebook |
|-----|-------|----------|
| **Lab 03** | Fuzzy Set Elementary Operations | `Fuzzy set elementary.ipynb`, `Fuzzy Lab 3.ipynb` |
| **Lab 04** | Advanced Set Operations | `Fuzzy Lab 04.ipynb` |
| **Lab 05** | Membership Functions & Visualization | `Fuzzy Lab 05.ipynb`, `Fuzzy Lab 05 2.ipynb`, `Fuzzy Lab 05 3.ipynb` |

---

## 🔬 Key Concepts Implemented

### 1. Fuzzy Set Properties
- **Height**: `max(μ(x))` — maximum membership value
- **Core**: `{x | μ(x) = 1}` — elements with full membership
- **Support**: `{x | μ(x) > 0}` — elements with non-zero membership
- **Crossover Points**: `{x | μ(x) = 0.5}`
- **Bandwidth**: Distance between crossover points

### 2. Alpha-Cuts (α-cuts)
```python
def alpha_cut(f_set, cut):
    strong_alpha = {x: μ for x, μ in f_set.items() if μ > cut}
    weak_alpha   = {x: μ for x, μ in f_set.items() if μ <= cut}
    return strong_alpha, weak_alpha
```

### 3. Membership Functions Visualized
| Function | Parameters | Plot |
|----------|------------|------|
| **Bell** | `a, b, c, d` | `bell(x, a, b, c, d)` |
| **Gaussian** | `mean, sigma` | `gaussian(x, mean, sigma)` |
| **Sigmoid** | `a, c` | `sigmoid(x, a, c)` |
| **Trapezoidal** | `a, b, c, d` | `trapezoidal(x, a, b, c, d)` |
| **Triangular** | `a, b, c` | `triangular(x, a, b, c)` |

### 4. Linguistic Hedges (Modifiers)
- **Concentration** (Very): `μ²(x)`
- **Dilation** (More or less): `√μ(x)`
- **Contrast Intensification**: Sharpens membership boundaries

### 5. Fuzzy Logic Operations
| Operation | Formula | Implementation |
|-----------|---------|----------------|
| **Union** | `max(μ₁, μ₂)` | `np.maximum(a, b)` |
| **Intersection** | `min(μ₁, μ₂)` | `np.minimum(a, b)` |
| **Complement** | `1 - μ(x)` | `1 - a` |
| **Difference** | `min(μ₁, 1-μ₂)` | `np.minimum(a, 1-b)` |

---

## 📁 Repository Structure

```
Fuzzy_programs/
├── README.md                           # This file
├── Fuzzy set elementary.ipynb          # Lab 3: Basic fuzzy set properties
├── Fuzzy Lab 3.ipynb                   # Lab 3 (alternate)
├── Fuzzy Lab 04.ipynb                  # Lab 4: Advanced operations
├── Fuzzy Lab 05.ipynb                  # Lab 5: Membership functions
├── Fuzzy Lab 05 2.ipynb                # Lab 5: Linguistic hedges & visualization
└── Fuzzy Lab 05 3.ipynb                # Lab 5: Additional examples
```

---

## 🚀 Quick Start

### Prerequisites
```bash
Python 3.x
Jupyter Notebook / JupyterLab / Google Colab
```

### Required Packages
```bash
pip install numpy matplotlib
```

### Run Notebooks
```bash
cd Fuzzy_programs
jupyter notebook
```

**Or open in Google Colab:**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Prady029/Fuzzy_programs)

---

## 💡 Code Examples

### Basic Fuzzy Set Operations
```python
import numpy as np

# Define fuzzy set as dictionary {element: membership}
f_set = {1: 1.0, 2: 0.2, 3: 0.3, 4: 0.4, 5: 0.5, 6: 0.6, 7: 0.7}

# Height
height = max(f_set.values())  # 1.0

# Core
core = {k: v for k, v in f_set.items() if v == 1.0}  # {1: 1.0}

# Alpha-cut at 0.5
strong, weak = alpha_cut(f_set, 0.5)
# strong: {1: 1.0, 6: 0.6, 7: 0.7}
# weak:   {2: 0.2, 3: 0.3, 4: 0.4, 5: 0.5}
```

### Membership Function Visualization
```python
import numpy as np
import matplotlib.pyplot as plt

def bell(x, a, b, c, d):
    """Bell-shaped membership function"""
    return 1 / (1 + abs((x - c) / a) ** (2 * b))

x = np.arange(0, 101, 5)
# "Young" concept
young = bell(x, a=20, b=2, c=0, d=0.5)
# "Old" concept
old = bell(x, a=30, b=3, c=100, d=1)

plt.plot(x, young, label='Young')
plt.plot(x, old, label='Old')
plt.plot(x, np.minimum(young, 1-old), label='Young but not old')
plt.legend()
plt.show()
```

### Linguistic Hedges
```python
# "Very young" = concentration
very_young = young ** 2

# "More or less young" = dilation
more_or_less_young = np.sqrt(young)

# "Not young" = complement
not_young = 1 - young

# "Not young and not old"
not_young_not_old = np.minimum(not_young, 1 - old)
```

---

## 📊 Sample Visualizations

The notebooks generate plots for:
- **Bell curves** for age concepts (Young, Old, Middle-aged)
- **Hedge modifications** (Very, More or less, Not)
- **Compound concepts** (Young but not too young, Not young and not old)
- **Membership function comparisons**

---

## 📖 Theory Background

### Fuzzy Set Definition
A fuzzy set `A` in universe `X` is characterized by a membership function `μ_A: X → [0,1]` where:
- `μ_A(x) = 1` → x definitely belongs to A
- `μ_A(x) = 0` → x definitely does not belong to A
- `0 < μ_A(x) < 1` → x partially belongs to A

### Key Properties
| Property | Crisp Set | Fuzzy Set |
|----------|-----------|-----------|
| Membership | Binary {0,1} | Continuous [0,1] |
| Boundaries | Sharp | Gradual transition |
| Operations | Boolean logic | Fuzzy logic (t-norms, t-conorms) |

---

## 🎓 Learning Outcomes

After completing these labs, you will understand:
- ✅ Fuzzy vs. crisp sets
- ✅ Membership function design
- ✅ Alpha-cut decomposition
- ✅ Fuzzy set operations (union, intersection, complement)
- ✅ Linguistic hedges and modifiers
- ✅ Visualization of fuzzy concepts
- ✅ Python implementation with NumPy/Matplotlib

---

## 📜 License

MIT License — feel free to use for learning and research.

---

## 👤 Author

**Prady029** — [GitHub](https://github.com/Prady029)

> *Fuzzy Computing Course — Central University of Rajasthan (CURAJ)*

---

*Last updated: October 2024*