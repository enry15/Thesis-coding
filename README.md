# Thesis Coding – Indecomposable Modules Computed in GAP with QPA

This repository contains all code-related material from the thesis. It includes two files:

- `codes`: the GAP script with the main function used to compute indecomposable additive set-realizable representations;
- `E_6_representations.pdf`: the computed representations used to complete the proof in the thesis concerning the classification of orientations of the Dynkin diagram $E_6$.

To run the code, you need the [QPA – Quivers and Path Algebras](https://docs.gap-system.org/pkg/qpa/doc/chap6.html#X87EFC38F7BC77B27) package for GAP.

---

## 📌 Code Description

The file codes contains three GAP functions:

- The first two are auxiliary functions needed by the main one.
- The third, `FindIndecomposableModule(P, dims)`, is the core function. It searches for an indecomposable additive set-realizable representation over the quiver of the given path algebra.

### 🔧 How to Use `FindIndecomposableModule`

```gap
FindIndecomposableModule(P, dims);
```

- `P` is a *path algebra* over a quiver, defined using QPA.
- `dims` is a list of 10 integers specifying the dimensions of the column matrices (by row) of the indecomposable module to be found, in the same order as the arrows were inserted into the path algebra.

📌 **Note**: The code is written for a quiver with **5 arrows** (as required for $E_6$), but it is easily adjustable. To handle a quiver with more or fewer arrows, you can modify the matrix construction section after **line 65**, and adapt the input list `dims` accordingly.

### ⚙️ Parameters and Field

- The **base field** is set to the field of rational numbers ℚ by default.
- You can change the field at the beginning of the `FindIndecomposableModule` function.

## 🔄 Function Behavior

The function randomly generates **additive, set-realizable representations** with the given dimensions until it finds one that is **indecomposable**.

- At each attempt (each iteration of the `while` loop), the string `cicle` is printed.
- Once successful, the matrices of the representation are printed.
- Note: in GAP, **modules are right modules**, so matrices are **transposed**.
- The generated representations are additive and set-realizable because each matrix has at most one 1 per column and all other entries equal to 0. Therefore, the resulting representation comes with a **multiplicative basis** by construction.

---

## 🧱 Requirements

- [GAP system](https://www.gap-system.org/)
- QPA package installed and loaded:

```gap
LoadPackage("qpa");
```

For details on how to define a path algebra in QPA, refer to the [official documentation](https://docs.gap-system.org/pkg/qpa/doc/chap6.html#X87EFC38F7BC77B27).

---

## 📄 Mathematical Context and Role in the Thesis

The file `E_6_representations.pdf` contains the six additive, set-realizable representations used in the computer-assisted part of the proof of the classification of orientations of the Dynkin diagram **$E_6$**, as presented in the thesis.

Specifically, in the proof, the existence of a **multiplicative basis** for the representations corresponding to the last two positive roots in the three remaining orientations (labeled 11, 20, and 31) is verified through explicit constructions using the `FindIndecomposableModule` function.

Each diagram in `E_6_representations.pdf` shows a **representation** for one of these six indecomposable modules. These were manually extracted from the output of the function and reformatted for clarity and readability.

The representations were initially computed over the field of rational numbers ℚ (as set in `FindIndecomposableModule`). However, in each case, the **endomorphism ring** was computed to verify that it contains **no non-trivial idempotents** for any field, which ensures that each representation remains **indecomposable over any field**.

These representations are also presented with a **multiplicative basis** by construction, since all matrices have entries equal to 0 in every column except for one entry equal to 1. This completes the classification of the remaining cases in the thesis.
