# Quantum Information Theory — Lecture Notes
## Von Neumann Entropy · Entanglement · Reduced Density Matrices · Schmidt Decomposition

---

## Lecture 16 — Von Neumann Entropy

### From Shannon to Von Neumann

**Shannon entropy** (classical):

$$H(P_X) = -\sum_i p_{x_i}\log p_{x_i}$$

- Maximum when all outcomes are equally likely (maximal uncertainty)
- Zero when the outcome is known with certainty

**Von Neumann entropy** (quantum):

$$\boxed{S(\rho) = -\mathrm{Tr}(\rho\log\rho)}$$

The density matrix $\rho$ replaces the probability distribution $P$. Von Neumann entropy measures **quantum uncertainty** of a state.

---

### Evaluating $S(\rho)$ via Diagonalisation

Any density matrix can be diagonalised by a unitary $P$:

$$\rho = P\,\rho_{\mathrm{diag}}\,P^{-1}, \qquad \rho_{\mathrm{diag}} = \mathrm{diag}(\lambda_1,\ldots,\lambda_n)$$

Using the cyclic property of the trace, the entropy reduces to:

$$S(\rho) = -\sum_i \lambda_i\log\lambda_i$$

where $\lambda_i$ are the **eigenvalues** of $\rho$.

#### Matrix Functions (Reference)

For a diagonalisable matrix $A = P A_D P^{-1}$ with $A_D = \mathrm{diag}(\lambda_1,\ldots,\lambda_n)$:

$$e^A = P\,\mathrm{diag}(e^{\lambda_1},\ldots,e^{\lambda_n})\,P^{-1}$$
$$\log A = P\,\mathrm{diag}(\log\lambda_1,\ldots,\log\lambda_n)\,P^{-1}$$

---

### Key Examples

| State | Eigenvalues $\lambda_i$ | $S(\rho)$ | Interpretation |
|-------|------------------------|-----------|----------------|
| Pure | $\{1, 0, 0,\ldots\}$ | $0$ | No uncertainty; state fully known |
| Mixed (example) | $\{\frac{3}{4}, \frac{1}{4}\}$ | $\approx 0.81$ bits | Partial uncertainty |
| Maximally mixed | $\{\frac{1}{2}, \frac{1}{2}\}$ | $1$ bit | Maximum uncertainty |

For a **pure state** $|\psi\rangle$, $\rho = |\psi\rangle\langle\psi|$ has one eigenvalue equal to 1, so:

$$S(\rho) = -1\cdot\log 1 = 0$$

---

### Key Formulas

| Quantity | Formula |
|----------|---------|
| Shannon entropy | $H = -\sum_i p_i\log p_i$ |
| Von Neumann entropy | $S(\rho) = -\mathrm{Tr}(\rho\log\rho)$ |
| Via eigenvalues | $S(\rho) = -\sum_i\lambda_i\log\lambda_i$ |
| Matrix exponential | $e^A = P\,e^{A_D}\,P^{-1}$ |
| Matrix logarithm | $\log A = P\,\log A_D\,P^{-1}$ |

---

---

## Lecture 17 — Two Qubits and Entanglement

### Two-Qubit Hilbert Space

The joint Hilbert space is a tensor product:

$$\mathcal{H} = \mathcal{H}_A \otimes \mathcal{H}_B, \qquad \dim = 2^2 = 4$$

For $n$ qubits: $\dim = 2^n$.

**Computational basis:**

$$|00\rangle = (1,0,0,0)^T, \quad |01\rangle = (0,1,0,0)^T, \quad |10\rangle = (0,0,1,0)^T, \quad |11\rangle = (0,0,0,1)^T$$

#### Physical Realisation

Two-level systems (e.g. electron spin, nuclear spin) serve as qubits. The energy gap between levels is given by **Zeeman splitting**:

$$\Delta E = g\,\mu\,B$$

where $g$ is the gyromagnetic ratio, $\mu$ the magnetic moment, and $B$ the external field.

---

### Separable vs. Entangled States

A pure two-qubit state $|\psi_{AB}\rangle$ is **separable** if:

$$|\psi_{AB}\rangle = |\psi_A\rangle \otimes |\psi_B\rangle$$

Otherwise it is **entangled**.

**Separable examples:**

$$\frac{1}{2}(|00\rangle+|01\rangle+|10\rangle+|11\rangle) = \left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)_{\!A} \otimes \left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)_{\!B}$$

$$\frac{1}{2}(|00\rangle-|01\rangle+|10\rangle-|11\rangle) = \left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)_{\!A} \otimes \left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)_{\!B}$$

**Entangled example** (a single sign change breaks factorability):

$$\frac{1}{2}(|00\rangle - |01\rangle + |10\rangle + |11\rangle) \quad \text{— cannot be factorised}$$

---

### Bell States (Maximally Entangled)

The four Bell states form an orthonormal basis for the two-qubit space:

| State | Definition | Notes |
|-------|-----------|-------|
| $|\Phi^+\rangle$ | $\frac{1}{\sqrt{2}}(|00\rangle+|11\rangle)$ | Symmetric |
| $|\Phi^-\rangle$ | $\frac{1}{\sqrt{2}}(|00\rangle-|11\rangle)$ | |
| $|\Psi^+\rangle$ | $\frac{1}{\sqrt{2}}(|01\rangle+|10\rangle)$ | Symmetric |
| $|\Psi^-\rangle$ | $\frac{1}{\sqrt{2}}(|01\rangle-|10\rangle)$ | Singlet (antisymmetric) |

None of these can be written as a tensor product.

#### Entropy of Bell States

The density matrix for $|\Phi^+\rangle$:

$$\rho = |\Phi^+\rangle\langle\Phi^+| = \frac{1}{2}\begin{pmatrix}1&0&0&1\\0&0&0&0\\0&0&0&0\\1&0&0&1\end{pmatrix}$$

Eigenvalues: $\{1,0,0,0\}$ → $S(\rho) = 0$

> **Pure states have zero von Neumann entropy, even when entangled.**

---

---

## Lecture 18 — Reduced Density Matrices and Entanglement

### Partial Trace

For a bipartite system $AB$ with full density matrix $\rho_{AB} = |\psi_{AB}\rangle\langle\psi_{AB}|$, the **reduced density matrices** are:

$$\rho_A = \mathrm{Tr}_B(\rho_{AB}), \qquad \rho_B = \mathrm{Tr}_A(\rho_{AB})$$

Explicit formula:

$$\rho_A = \mathrm{Tr}_B(\rho_{AB}) = \sum_b \left(I_A\otimes\langle b|\right)\rho_{AB}\left(I_A\otimes|b\rangle\right)$$

The partial trace **sums over one subsystem's degrees of freedom**, leaving an effective state for the other.

---

### Example: Bell State $|\Phi^+\rangle$

Full state:
$$|\psi\rangle = \frac{1}{\sqrt{2}}(|00\rangle+|11\rangle), \qquad S(\rho_{AB}) = 0$$

After tracing out $B$:

$$\rho_A = \frac{1}{2}\begin{pmatrix}1&0\\0&1\end{pmatrix} = \frac{I}{2}$$

This is a **maximally mixed state** with $S(\rho_A) = 1$ bit.

| Property | $\rho_{AB}$ | $\rho_A$ |
|----------|-------------|----------|
| Pure state? | Yes | No |
| $S(\rho)$ | $0$ | $1$ bit |
| Entanglement | — | Maximally entangled |

The reduced density matrix satisfies $\rho_A^2 \neq \rho_A$, confirming it is mixed.

---

### Entanglement Criterion

> A pure bipartite state is **entangled** if and only if the reduced density matrix of either subsystem is **mixed**.

- **Separable pure state** → $\rho_A$ is pure → $S(\rho_A) = 0$
- **Entangled pure state** → $\rho_A$ is mixed → $S(\rho_A) > 0$

The entropy $S(\rho_A)$ **quantifies the entanglement** of a pure bipartite state.

> This connection was confirmed experimentally by Alain Aspect, John Clauser, and Anton Zeilinger (Nobel Prize in Physics 2022).

---

### Partial Trace Procedure (Computational Basis)

1. Write $\rho_{AB}$ in the basis $\{|00\rangle, |01\rangle, |10\rangle, |11\rangle\}$.
2. To get $\rho_A$: sum diagonal blocks where the $B$-index matches on bra and ket.
3. Only terms where the traced-out subsystem indices coincide survive.

---

---

## Lecture 19 — Schmidt Decomposition

### Separable vs. Entangled: Partial Trace Behaviour

| State type | $\rho_A$ after partial trace | $S(\rho_A)$ |
|------------|------------------------------|-------------|
| Separable pure | Pure | $0$ |
| Entangled pure | Mixed | $> 0$ |

**Separable example:**

$$|\psi_{AB}\rangle = \frac{1}{2}(|00\rangle+|01\rangle+|10\rangle+|11\rangle) = |{+}\rangle_A\otimes|{+}\rangle_B$$

Tracing out $B$ leaves $\rho_A = |{+}\rangle\langle{+}|$ — a pure state with $S(\rho_A) = 0$.

---

### Schmidt Decomposition

Any **pure bipartite state** $|\psi_{AB}\rangle \in \mathcal{H}_A\otimes\mathcal{H}_B$ can be written as:

$$\boxed{|\psi_{AB}\rangle = \sum_i \alpha_i\,|u_i\rangle_A\otimes|v_i\rangle_B}$$

where:
- $\{|u_i\rangle_A\}$ and $\{|v_i\rangle_B\}$ are orthonormal sets in $\mathcal{H}_A$ and $\mathcal{H}_B$ respectively
- $\alpha_i \in \mathbb{R}^+$ are the **Schmidt coefficients**
- Normalisation: $\sum_i |\alpha_i|^2 = 1$

The Schmidt coefficients are the **singular values** of the coefficient matrix — obtained via **Singular Value Decomposition (SVD)**.

---

### Properties of Schmidt Decomposition

| Property | Detail |
|----------|--------|
| Applies to | Pure bipartite states only |
| Relation to SVD | Schmidt coefficients = singular values of coefficient matrix |
| Separable iff | Exactly **one** non-zero $\alpha_i$ |
| Entangled iff | **More than one** non-zero $\alpha_i$ |
| Reduced density matrices | $\rho_A = \sum_i|\alpha_i|^2\,|u_i\rangle\langle u_i|$, $\rho_B = \sum_i|\alpha_i|^2\,|v_i\rangle\langle v_i|$ |
| Symmetry | $S(\rho_A) = S(\rho_B)$ always |

---

### Entanglement Entropy via Schmidt Coefficients

Setting $p_i = |\alpha_i|^2$ (Schmidt populations):

$$S(\rho_A) = -\sum_i p_i\log p_i = S(\rho_B)$$

This is the **entanglement entropy** of the pure bipartite state — a complete characterisation of how entangled the state is.

---

### Separable State in Schmidt Form

For $|\psi_{AB}\rangle = |{+}\rangle_A\otimes|{+}\rangle_B$:

- Schmidt decomposition has exactly **one** term: $\alpha_1 = 1$, all others zero.
- $S(\rho_A) = -1\cdot\log 1 = 0$ → confirmed separable.

For Bell state $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle+|11\rangle)$:

- Two Schmidt coefficients: $\alpha_1 = \alpha_2 = \frac{1}{\sqrt{2}}$
- $S(\rho_A) = -2\times\frac{1}{2}\log\frac{1}{2} = 1$ bit → maximally entangled.

---

### Key Takeaways

- **Schmidt decomposition diagonalises** any pure bipartite state into a sum of orthogonal product states.
- The **number of non-zero Schmidt coefficients** (the Schmidt rank) directly signals separability vs. entanglement.
- **Entanglement entropy** $S(\rho_A) = -\sum_i p_i\log p_i$ quantifies entanglement for pure states and is equal for both subsystems.
- Partial tracing **preserves purity for separable states** but maps entangled pure states to mixed reduced states.
- Schmidt decomposition can be computed numerically via SVD.

---

### Summary of Entanglement Measures

| Measure | Formula | Applies to |
|---------|---------|-----------|
| Von Neumann entropy | $S(\rho) = -\mathrm{Tr}(\rho\log\rho)$ | Any state |
| Entanglement entropy | $S(\rho_A) = -\sum_i p_i\log p_i$ | Pure bipartite states |
| Schmidt rank | Number of non-zero $\alpha_i$ | Pure bipartite states |

---

*Keywords: Von Neumann entropy, Density matrix, Diagonalisation, Pure state, Mixed state, Bell states, Entanglement, Partial trace, Reduced density matrix, Schmidt decomposition, SVD, Entanglement entropy, Separable states.*
