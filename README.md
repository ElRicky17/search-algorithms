# Search Algorithms

A Python-based educational notebook implementing and comparing classical **blind** and **informed** search algorithms using a tree-based node abstraction. Algorithms are demonstrated on the classic **Water Jug Problem**.

---

##  Table of Contents

- [Overview](#overview)
- [Algorithms Implemented](#algorithms-implemented)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Example: Water Jug Problem](#example-water-jug-problem)
- [Requirements](#requirements)

---

## Overview

This project provides a modular, object-oriented framework for implementing search algorithms in Python. A generic `Node` class serves as the base for any search problem, making it easy to extend and apply to different domains. The notebook walks through both uninformed and informed strategies, including tree visualization of the search process.

---

## Algorithms Implemented

| Algorithm | Type | Strategy |
|---|---|---|
| **Breadth-First Search (BFS)** | Blind | Explores nodes level by level |
| **Depth-First Search (DFS)** | Blind | Explores as deep as possible first |
| **Uniform Cost Search (UCS)** | Blind | Expands the lowest-cost node |
| **Best-First Search** | Informed | Uses only the heuristic `h(n)` |
| **A\*** | Informed | Combines cost `g(n)` + heuristic `h(n)` |

---

## Project Structure

```
search-algorithms/
│
├── AlgoritmosDeBusqueda.ipynb   # Main notebook with all algorithms
└── README.md
```

### Core Classes & Functions

**`Node` (Base Class)**

| Attribute / Method | Description |
|---|---|
| `state` | Current state representation |
| `parent` | Parent node in the search tree |
| `operator` | Operator that generated this node |
| `level` | Depth in the search tree |
| `getchildrens()` | Returns child nodes by applying all operators |
| `repeatStatePath()` | Detects cycles to avoid infinite loops |
| `pathObjective()` | Returns the path from root to current node |
| `cost()` | Step cost (default: 1) |
| `f()` | Evaluation function: `g(n) + h(n)` |

---

## Getting Started

### Prerequisites

- Python 3.8+
- Jupyter Notebook or Google Colab

### Installation

```bash
pip install pydot numpy
```

> **Note:** `pydot` is used for tree visualization. You may also need [Graphviz](https://graphviz.org/download/) installed on your system.

### Run the Notebook

```bash
jupyter notebook AlgoritmosDeBusqueda.ipynb
```

---

## Usage

To apply these algorithms to a new problem, subclass `Node` and implement `getState()`:

```python
class MyProblem(Node):
    def getState(self, index):
        # Define what each operator does
        # Return the resulting state or None if the operator is not applicable
        pass
```

Then call any search algorithm:

```python
root = MyProblem(value="start", state=initial_state, operators=operators)
tree, objective = A(root, end_state)
objective.printPath()
```

---

## Example: Water Jug Problem

Given a **3L jug** and a **4L jug** with no markings, find a way to obtain exactly **2L** in the 4L jug.

**State representation:** `[amount_in_3L_jug, amount_in_4L_jug]`

**Operators:**

| # | Action |
|---|---|
| 0 | Fill the 3L jug |
| 1 | Fill the 4L jug |
| 2 | Empty the 3L jug |
| 3 | Empty the 4L jug |
| 4 | Pour from 3L into 4L |
| 5 | Pour from 4L into 3L |

**Heuristic:** `|current_4L - 2|` (absolute difference from goal)

Running **A\*** on this problem produces an optimal solution path and a color-coded search tree visualization (red = solution path).

---

## Requirements

```txt
numpy
pydot
jupyter
```

---

## 📚 Concepts

- **Blind Search:** No domain knowledge used — explores all nodes systematically.
- **Informed Search:** Uses a heuristic function to guide the search toward the goal more efficiently.
- **A\*:** Guarantees the optimal path when the heuristic is admissible (never overestimates).
