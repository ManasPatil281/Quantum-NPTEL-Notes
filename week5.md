# Quantum Information Theory — Lecture Notes
## SVD & Schmidt Decomposition · EPR Paradox · Bell's Inequality

---

## Lecture 20 — Schmidt Decomposition: Worked Example and SVD

### Example State

$$|\psi\rangle = \frac{1}{\sqrt{3}}\left(|00\rangle + |01\rangle + |10\rangle\right)$$

---

### Step 1: Reduced Density Matrix $\rho_A$

Trace over subsystem $B$:

$$\rho_A = \mathrm{Tr}_B\!\left(|\psi\rangle\langle\psi|\right) = \frac{1}{3}\begin{pmatrix}2 & 1\\1 & 1\end{pmatrix}$$

---

### Step 2: Eigenvalues of $\rho_A$

Solve $\det(\rho_A - \lambda I) = 0$:

$$9\lambda^2 - 9\lambda + 1 = 0$$

$$\lambda_{1,2} = \frac{3 \pm \sqrt{5}}{6}$$

These are also the **squared Schmidt coefficients**: $\alpha_i = \sqrt{\lambda_i}$.

---

### Step 3: Eigenvectors (Schmidt Bases)

| Eigenvalue | Eigenvector $|u_i\rangle_A$ (unnormalised) |
|------------|-------------------------------------------|
| $\lambda_1 = \frac{3+\sqrt{5}}{6}$ | $\propto\begin{pmatrix}1+\frac{\sqrt{5}}{2}\\-1\end{pmatrix}$ |
| $\lambda_2 = \frac{3-\sqrt{5}}{6}$ | $\propto\begin{pmatrix}1-\frac{\sqrt{5}}{2}\\-1\end{pmatrix}$ |

Eigenvectors for subsystem $B$, $\{|v_i\rangle_B\}$, are found analogously.

---

### Step 4: Schmidt Form

$$|\psi\rangle = \sqrt{\lambda_1}\,|u_1\rangle_A|v_1\rangle_B + \sqrt{\lambda_2}\,|u_2\rangle_A|v_2\rangle_B$$

Two non-zero Schmidt coefficients → state is **entangled**.

---

### Connection to Singular Value Decomposition

The Schmidt decomposition is a **special case of SVD** applied to the coefficient matrix of the quantum state.

For any matrix $\beta$ (the coefficient matrix in the product basis):

$$\beta = U_A\,\Sigma\,U_B^T$$

- $U_A$, $U_B$ are unitary matrices (change of basis to Schmidt bases)
- $\Sigma$ is diagonal with non-negative entries = Schmidt coefficients
- If $\dim\mathcal{H}_A \neq \dim\mathcal{H}_B$, $\Sigma$ is **rectangular**

| SVD Quantity | Schmidt Interpretation |
|-------------|----------------------|
| Singular values of $\beta$ | Schmidt coefficients $\alpha_i$ |
| Columns of $U_A$ | Schmidt basis $\{|u_i\rangle_A\}$ |
| Columns of $U_B$ | Schmidt basis $\{|v_i\rangle_B\}$ |
| Rank $r$ of $\beta$ | Number of non-zero Schmidt coefficients |

---

---

## Lecture 22 — Singular Value Decomposition (Algorithm)

### SVD Definition

For any $m\times n$ matrix $A$:

$$A = U\,\Sigma\,V^T$$

- $U$: $m\times m$ orthogonal matrix
- $\Sigma$: $m\times n$ diagonal matrix with **singular values** $\sigma_j \geq 0$
- $V$: $n\times n$ orthogonal matrix

Singular values are square roots of eigenvalues of $A^T A$:

$$\sigma_j = \sqrt{\lambda_j(A^T A)}, \qquad \lambda_1 \geq \lambda_2 \geq \cdots \geq 0$$

The **rank** $r$ = number of non-zero singular values.

---

### Algorithm

| Step | Action |
|------|--------|
| 1 | Compute $A^T A$ ($n\times n$) and find its eigenvalues $\lambda_j$ |
| 2 | Sort eigenvalues descending; rank $r$ = number of non-zero ones |
| 3 | Find eigenvectors $v_j$ of $A^T A$ → columns of $V$ |
| 4 | Build $\Sigma$ with $\sigma_j = \sqrt{\lambda_j}$ on diagonal |
| 5 | Compute $u_j = \frac{1}{\sigma_j}Av_j$ for $j=1,\ldots,r$ → first $r$ columns of $U$ |
| 6 | Gram–Schmidt to complete $U$ with remaining $m-r$ orthonormal vectors |

---

### Worked Example

$$A = \begin{bmatrix}1&1&0\\1&1&0\end{bmatrix}$$

$$A^T A = \begin{bmatrix}2&2&0\\2&2&0\\0&0&0\end{bmatrix}$$

Eigenvalues: $\lambda^2 - 4\lambda + 3 = 0 \Rightarrow \lambda_1=4,\ \lambda_2=0,\ \lambda_3=0$

Wait — correcting via $\lambda^2(λ-4)=0$: $\lambda_1=4,\lambda_2=0,\lambda_3=0$; rank $r=1$.

$$\Sigma = \begin{bmatrix}2 & 0 & 0\end{bmatrix}$$

(One non-zero singular value → **separable** quantum state if this were a coefficient matrix.)

---

### SVD ↔ Quantum Entanglement

| Matrix Property | Quantum State |
|-----------------|--------------|
| Rank $r=1$ | Separable (non-entangled) |
| Rank $r>1$ | Entangled |
| Singular values $\sigma_j$ | Schmidt coefficients $\alpha_j$ |
| $\sum_j\sigma_j^2 = 1$ | Normalisation condition |

---

---

## Lecture 23 — EPR Paradox and Bell's Inequality (Part 1)

### The Singlet State

The **singlet Bell state** (EPR pair):

$$|\psi^-\rangle = \frac{1}{\sqrt{2}}\left(|0\rangle_A|1\rangle_B - |1\rangle_A|0\rangle_B\right)$$

- Represents **total spin $S=0$** for two spin-$\frac{1}{2}$ particles
- **Rotationally invariant** — its form is unchanged under any rotation of the measurement basis
- Exhibits **perfect anti-correlation**: measuring the same component always gives opposite results

#### Spin States Summary

| Total Spin | $m_s$ | State |
|-----------|-------|-------|
| $S=1$ (triplet) | $+1$ | $|00\rangle$ |
| $S=1$ (triplet) | $0$ | $\frac{1}{\sqrt{2}}(|01\rangle+|10\rangle)$ |
| $S=1$ (triplet) | $-1$ | $|11\rangle$ |
| $S=0$ (singlet) | $0$ | $\frac{1}{\sqrt{2}}(|01\rangle-|10\rangle)$ |

---

### Measurement Correlations

| Alice's Axis | Alice's Result | Bob's Axis | Bob's Result |
|-------------|---------------|-----------|-------------|
| $S_z$ | $+1$ | $S_z$ | $-1$ (perfect anti-correlation) |
| $S_z$ | $+1$ | $S_x$ | Random ($\pm 1$, 50/50) |
| $S_x$ | $+1$ | $S_x$ | $-1$ (perfect anti-correlation) |
| No measurement | — | Any | Random |

> **Key insight:** Bob's outcome depends on Alice's choice of measurement axis, even at arbitrarily large separations.

---

### The EPR Paradox

**Locality principle:** A measurement on system $A$ cannot instantaneously affect a causally disconnected system $B$:

$$\Delta x^2 > c^2\,\Delta t^2$$

**Reality principle:** If a physical quantity can be predicted with certainty without disturbing the system, it corresponds to an element of physical reality.

**The paradox:** Quantum mechanics predicts that Alice's choice of axis changes the correlations Bob observes — yet locality forbids any instantaneous influence. EPR concluded that quantum mechanics must be **incomplete**, and proposed **hidden variables** to restore local realism.

---

### Non-Commutativity and Simultaneous Reality

Spin operators along different axes do not commute:

$$[S_z, S_x] \neq 0$$

Therefore $S_z$ and $S_x$ cannot simultaneously possess definite values — no local hidden variable can assign definite pre-existing values to both.

---

### Polarisation ↔ Spin Correspondence

| Polarisation | Spin Operator | Spin States |
|-------------|--------------|------------|
| Horizontal / Vertical | $\sigma_z$ | $|0\rangle$, $|1\rangle$ |
| Diagonal $\pm 45°$ | $\sigma_x$ | $\frac{1}{\sqrt{2}}(|0\rangle\pm|1\rangle)$ |
| Right / Left Circular | $\sigma_y$ | $\frac{1}{\sqrt{2}}(|0\rangle\pm i|1\rangle)$ |

---

---

## Lecture 24 — EPR Paradox (Part 2) and Bell's Inequality Setup

### Entanglement as Higher-Dimensional Superposition

The singlet state $|\psi^-\rangle$ is a superposition in the **four-dimensional** two-qubit Hilbert space, not separable into any product of single-qubit states.

Expressing in the $\sigma_x$ basis confirms the same perfect anti-correlation — a direct consequence of **rotational invariance**.

### EPR Conclusion vs Quantum Mechanics

| View | Position |
|------|---------|
| EPR / Local Realism | QM is incomplete; hidden variables exist that determine outcomes locally |
| Quantum Mechanics | No hidden variables; non-local correlations are fundamental |
| Bell (1964) | Local realism leads to inequalities that QM **violates** |

---

### Setup for Bell's Test (Wigner's Approach)

- Alice and Bob each receive one particle from an entangled EPR pair
- They independently measure spin along one of three axes: $A$, $B$, or $C$ (not necessarily orthogonal)
- Each measures only **one** axis per particle
- By the **reality principle**, local realism allows assigning pre-determined values $\pm 1$ to all three axes simultaneously, even though only one is measured

---

---

## Lecture 25 — Bell's Inequality: Derivation and Violation

### Eight Outcome Groups (Local Realism)

Under local realism, each particle pair has pre-assigned values for all three axes. The singlet's perfect anti-correlation means Bob's values are always opposite to Alice's.

| Group | Alice $(A,B,C)$ | Bob $(A,B,C)$ |
|-------|----------------|--------------|
| $n_1$ | $+++$ | $---$ |
| $n_2$ | $++-$ | $--+$ |
| $n_3$ | $+-+$ | $-+-$ |
| $n_4$ | $+--$ | $-++$ |
| $n_5$ | $-++$ | $+--$ |
| $n_6$ | $-+-$ | $+-+$ |
| $n_7$ | $--+$ | $++-$ |
| $n_8$ | $---$ | $+++$ |

Total: $N = \sum_{i=1}^8 n_i$. Probabilities are $P(A^+ B^+) = (n_1+n_2)/N$, etc.

---

### Bell's Inequality (Wigner Form)

Using non-negativity of all $n_i$, the following inequality holds under **any** local realistic theory:

$$\boxed{P(A^+B^+) \leq P(A^+C^+) + P(C^+B^+)}$$

---

### Quantum Mechanical Prediction

After Alice measures axis $A$ and gets $+1$, Bob's particle collapses to spin $-1$ along $A$. The probability that Bob then measures $+1$ along axis $B$ (separated by angle $\theta_{AB}$) is:

$$P(\sigma_B = +1) = \sin^2\!\left(\frac{\theta_{AB}}{2}\right)$$

For the singlet state:

$$P(A^+B^+) = \frac{1}{2}\sin^2\!\left(\frac{\theta_{AB}}{2}\right)$$

---

### Classical vs Quantum Comparison

| Quantity | Local Realism | Quantum Mechanics |
|---------|--------------|-------------------|
| Outcome of Bob's measurement | Pre-assigned (hidden variable) | Collapses upon Alice's measurement |
| $P(\sigma_B=+1)$ | Fixed by hidden variable | $\sin^2(\theta_{AB}/2)$ |
| Bell's inequality | Always satisfied | **Violated** for certain angles |

---

### Significance

- For specific angle choices (e.g. $\theta_{AB}=\theta_{BC}=\theta_{AC}/2$), quantum mechanics predicts probabilities that **exceed** the Bell bound.
- Experimental violations (Aspect, Clauser, Zeilinger — Nobel 2022) confirm that **no local hidden variable theory** can reproduce quantum predictions.
- Conclusion: Nature is either **non-local** or **non-real** (or both) — classical intuitions about causality and pre-existing properties break down.

---

### Key Takeaways Across Lectures 23–25

- The **singlet state** is the canonical EPR pair: rotationally invariant, perfect anti-correlation along any common axis.
- **Non-commutativity** ($[S_z, S_x]\neq 0$) forbids simultaneous definite values, undermining local realism.
- **Bell's inequalities** translate local realism into a testable mathematical bound.
- **Quantum mechanics violates that bound** — confirmed experimentally — establishing the non-local nature of entanglement.
- These results are foundational for quantum cryptography, quantum teleportation, and quantum computing.

---

*Keywords: Schmidt decomposition, SVD, Singular values, Partial trace, Entanglement entropy, Singlet state, Bell states, EPR paradox, Local realism, Reality principle, Locality principle, Bell's inequality, Wigner's inequality, Hidden variables, Quantum non-locality.*
