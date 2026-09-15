# AMS 598 — Final Exam Study Guide

Lecture notes and final-exam review for AMS 598 (Big Data Analysis) at Stony Brook
University, written in LaTeX and compiled to an 18-page PDF.

The guide covers the second half of the course: MapReduce algorithm design, penalized
regression solved by ADMM in a distributed setting, support vector machines, and random
forests.

📄 **[AMS578_Final_Guide.pdf](AMS578_Final_Guide.pdf)** — the compiled guide
📝 **[main.tex](main.tex)** — LaTeX source

---

## Contents

### 1. MapReduce Algorithms

The map/reduce paradigm as a way of expressing computations so that they parallelize,
then four worked algorithm designs in that style.

- **The paradigm** — key–value pairs, the map phase, grouping by key, the reduce phase,
  and why independence between tasks is what makes parallelism possible.
- **TF–IDF** — the full four-job pipeline: per-document word frequency, max word count
  per document, document frequency per term, and the final TF–IDF computation, with the
  mapper and reducer written out for each job plus notes on scalability.
- **Relational algebra** — selection, projection, union, intersection, difference, and
  natural join, each expressed as a mapper/reducer pair.
- **Matrix multiplication** — the standard two-pass algorithm, and a sketch of the
  one-pass approach.
- **PageRank** — the basic formulation without teleportation, the dead-end and
  spider-trap failure modes, taxation as the fix, and a MapReduce implementation outline.

### 2. Penalty-Based Methods and ADMM

The longest section, and the one built for a specific kind of exam question.

- **Ridge and LASSO** — objectives, the ridge closed form
  $\hat\beta = (X^TX + \lambda I)^{-1}X^Ty$, and why the $\ell_1$ geometry produces
  sparsity.
- **Penalized logistic regression** — the log-likelihood, and the equivalence between
  maximizing penalized likelihood and minimizing negative log-likelihood plus a penalty.
- **ADMM** — the general constrained form, the augmented Lagrangian, the three-step
  iteration (x-update, z-update, dual update), and the scaled form.
- **Consensus optimization** — splitting a loss across data partitions with local copies
  and a global variable, which is what makes the method work at scale.
- **Logistic regression with a custom penalty** — the full derivation from problem setup
  through consensus formulation, scaled augmented Lagrangian, and the general updates.
- **Special cases** — the consensus step solved in closed form for L2 (a simple
  shrinkage factor), L1 (elementwise soft-thresholding), separable penalties
  (coordinate-wise proximal steps), and group penalties (block soft-thresholding).
- **Template answer** — a compact, ready-to-write version of the whole ADMM algorithm
  for the exam, with the instruction to then state the closed form for whichever penalty
  the question asks about.

### 3. Support Vector Machines

- Linear separating hyperplanes and the geometry of the margin.
- Hard-margin and soft-margin formulations, with slack variables and the role of $C$.
- The dual problem, the KKT conditions, and why only support vectors carry nonzero
  $\alpha_i$.
- The kernel trick: replacing $\phi(x_i)^T\phi(x_j)$ with $K(x_i, x_j)$ in the dual and
  the decision function, plus the linear, polynomial, and Gaussian RBF kernels.

### 4. Random Forests

- **CART** — recursive partitioning, choosing $(j, s)$ to minimize squared error for
  regression, Gini or deviance for classification, and pruning.
- **The algorithm** — bootstrap sampling, selecting $m$ of $p$ predictors at each split,
  growing without pruning, then averaging or majority vote.
- **Out-of-bag error** — why roughly a third of observations are OOB for any given tree,
  and why aggregating over them gives an unbiased estimate of test error.
- **Permutation importance** — permuting a predictor and measuring the increase in OOB
  error.
- **Big-data considerations** — training trees on separate nodes over distributed data,
  and why many smaller trees can beat one tree trained on everything.

---

## Building from source

The document is a single-file `article` with no external figures, so it compiles with a
standard TeX distribution. Run twice so the table of contents resolves:

```bash
pdflatex main.tex
pdflatex main.tex
```

Packages used: `geometry`, `amsmath`, `amssymb`, `amsthm`, `mathtools`, `bm`,
`enumerate`, `enumitem`, `graphicx`, `booktabs`, `hyperref`.

---

## A note on scope

These are one student's review notes, organized around what seemed likely to be tested.
They are not a substitute for the lecture slides or the textbook, and no claim is made
that the coverage is complete. If you spot an error, an issue or pull request is welcome.
