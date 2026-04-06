# Quantum Information Theory — Lecture Notes
## Quantum Fourier Transform: Formal Definition · Notation · Circuit Construction

---

## Lecture 36 — QFT: Formal Definition and Basic Examples

### From DFT to QFT

The **Quantum Fourier Transform (QFT)** applies the classical Discrete Fourier Transform to the **amplitudes** of a quantum state.

For a state $|\psi\rangle = \sum_{n=0}^{N-1} c_n|n\rangle$ (with $\sum_i|c_i|^2=1$), the QFT maps:

$$|\psi\rangle \xrightarrow{F} |\tilde{\psi}\rangle = \sum_{k=0}^{N-1} b_k|k\rangle$$

where the new amplitudes are:

$$b_k = \frac{1}{\sqrt{N}}\sum_{n=0}^{N-1} c_n\,e^{2\pi i\frac{nk}{N}}$$

Action on a single computational basis state:

$$\boxed{F|j\rangle = \frac{1}{\sqrt{2^n}}\sum_{k=0}^{2^n-1} e^{2\pi i\frac{jk}{2^n}}|k\rangle}$$

For general input $|\psi\rangle = \sum_j x_j|j\rangle$:

$$F|\psi\rangle = \sum_{k=0}^{2^n-1} y_k|k\rangle, \qquad y_k = \frac{1}{\sqrt{2^n}}\sum_{j=0}^{2^n-1} x_j\,e^{2\pi i\frac{jk}{2^n}}$$

---

### Key Properties

- **Unitary**: $F^\dagger F = I$ — physically realisable and reversible
- **Basis transformation**: from computational basis $\{|0\rangle,|1\rangle,\ldots\}$ to Fourier basis
- **Norm-preserving**: inner products and probabilities are unchanged
- For $n$ qubits: Hilbert space dimension $N = 2^n$

---

### Examples

#### Single-Qubit QFT ($n=1$) — Equivalent to Hadamard

$$F|0\rangle = \frac{|0\rangle+|1\rangle}{\sqrt{2}} = |+\rangle$$

$$F|1\rangle = \frac{|0\rangle-|1\rangle}{\sqrt{2}} = |-\rangle$$

> The single-qubit QFT **is** the Hadamard gate.

#### Three-Qubit QFT ($n=3$) of $|000\rangle$

With $x_j = 1$ for $j=0$ only, all $b_k = \frac{1}{\sqrt{8}}$:

$$F|000\rangle = \frac{1}{\sqrt{8}}\!\left(|000\rangle+|001\rangle+\cdots+|111\rangle\right)$$

An equal superposition of all 8 basis states — equivalent to $H^{\otimes 3}|000\rangle$.

---

### Equation Reference

| # | Formula | Description |
|---|---------|-------------|
| 1 | $|\psi\rangle = \sum_{n=0}^{N-1}c_n|n\rangle$ | Quantum state in computational basis |
| 2 | $b_k = \frac{1}{\sqrt{N}}\sum_n c_n e^{2\pi i nk/N}$ | QFT amplitudes (DFT of $c_n$) |
| 3 | $F|j\rangle = \frac{1}{\sqrt{2^n}}\sum_k e^{2\pi i jk/2^n}|k\rangle$ | QFT on basis state $|j\rangle$ |

---

---

## Lecture 37 — QFT: Binary Notation and Tensor Product Structure

### Binary Decomposition

Any integer $y \in [0, 2^n-1]$ is written in binary as:

$$y = \sum_{k=1}^n y_k\,2^{n-k}, \qquad y_k \in \{0,1\}$$

so $|y\rangle = |y_1 y_2 \cdots y_n\rangle$.

---

### QFT as a Tensor Product

Using $e^{a+b} = e^a e^b$, the sum over $y$ in the QFT factorises over individual qubits:

$$\tilde{x} = \frac{1}{\sqrt{2^n}}\sum_{y_1=0}^1\cdots\sum_{y_n=0}^1\prod_{k=1}^n e^{2\pi i x y_k/2^k}|y_1\cdots y_n\rangle$$

This yields the **tensor product form**:

$$\boxed{\tilde{x} = \bigotimes_{k=1}^n \frac{|0\rangle + e^{2\pi i x/2^k}|1\rangle}{\sqrt{2}}}$$

Each qubit $k$ acquires a phase $e^{2\pi i x/2^k}$ on its $|1\rangle$ component — a fractional rotation.

---

### Three-Qubit Summary

| Component | Expression |
|-----------|-----------|
| Basis state | $|y\rangle = |y_1 y_2 y_3\rangle$ |
| Integer decomposition | $y = y_1\cdot 4 + y_2\cdot 2 + y_3\cdot 1$ |
| QFT state | $\tilde{x} = \frac{1}{\sqrt{8}}\sum_{y=0}^7 e^{2\pi i xy/8}|y\rangle$ |
| Factorised form | $\tilde{x} = \frac{1}{\sqrt{8}}\bigotimes_{k=1}^3(|0\rangle + e^{2\pi i x/2^k}|1\rangle)$ |

---

### Example: $x = 5$ (binary $101$)

$x = 1\cdot 4 + 0\cdot 2 + 1\cdot 1 = 5$

The three tensor factors:

| Qubit $k$ | Phase $e^{2\pi i\cdot 5/2^k}$ | Simplification |
|----------|------------------------------|---------------|
| $k=1$ | $e^{2\pi i\cdot 5/2} = e^{5\pi i} = -1$ | $|0\rangle - |1\rangle$ |
| $k=2$ | $e^{2\pi i\cdot 5/4} = e^{5\pi i/2} = i$ | $|0\rangle + i|1\rangle$ |
| $k=3$ | $e^{2\pi i\cdot 5/8}$ | $|0\rangle + e^{5\pi i/4}|1\rangle$ |

$$\tilde{x}_{x=5} = \frac{1}{\sqrt{8}}\!\left(|0\rangle-|1\rangle\right)\otimes\!\left(|0\rangle+i|1\rangle\right)\otimes\!\left(|0\rangle+e^{5\pi i/4}|1\rangle\right)$$

---

### Core Insight

The tensor product structure shows that **each qubit in the QFT output can be prepared independently** using a Hadamard gate and controlled phase rotations — the foundation of the efficient QFT circuit.

---

---

## Lecture 39 — QFT Circuit: Gates and 3-Qubit Construction

### Building Block Gates

#### Unitary Rotation Gate $U_{\mathrm{rot},k}$

$$U_{\mathrm{rot},k} = \begin{pmatrix}1 & 0\\0 & e^{2\pi i/2^k}\end{pmatrix}$$

- $k=1$: $U_{\mathrm{rot},1} = \begin{pmatrix}1&0\\0&-1\end{pmatrix}$ — this is $\sigma_z$
- Applied after $H$, builds the phase $e^{2\pi i x/2^k}$ on $|1\rangle$

The Hadamard gate is $U_{\mathrm{rot},1}$ in the QFT sense:

$$H|x_k\rangle = \frac{|0\rangle + e^{2\pi i x_k/2}|1\rangle}{\sqrt{2}}$$

#### Controlled Rotation Gate $C\text{-}R_k$

Two-qubit gate: applies $U_{\mathrm{rot},k}$ to the target **only if** the control qubit is $|1\rangle$:

$$C\text{-}R_k = \begin{pmatrix}I & 0\\0 & U_{\mathrm{rot},k}\end{pmatrix}$$

This is the CNOT generalisation — instead of flipping, it **phase-rotates**.

---

### 3-Qubit QFT Circuit

Input: $|x_1 x_2 x_3\rangle$. Steps:

| Step | Gate | Control / Target | Effect |
|------|------|-----------------|--------|
| 1 | $H$ | — / $x_1$ | $|0\rangle+e^{2\pi i x_1/2}|1\rangle$ on qubit 1 |
| 2 | $C\text{-}R_2$ | $x_2$ / $x_1$ | Adds phase $e^{2\pi i x_2/4}$ to qubit 1 |
| 3 | $C\text{-}R_3$ | $x_3$ / $x_1$ | Adds phase $e^{2\pi i x_3/8}$ to qubit 1 |
| 4 | $H$ | — / $x_2$ | Creates superposition on qubit 2 |
| 5 | $C\text{-}R_2$ | $x_3$ / $x_2$ | Adds phase $e^{2\pi i x_3/4}$ to qubit 2 |
| 6 | $H$ | — / $x_3$ | Creates superposition on qubit 3 |
| 7 | SWAP | $x_1 \leftrightarrow x_3$ | Reverses qubit order |

---

### Output State

After all gates (before swap), the state is:

$$|\tilde{x}\rangle = \frac{1}{\sqrt{8}}\left(|0\rangle+e^{2\pi i(0.x_1)}|1\rangle\right)\otimes\left(|0\rangle+e^{2\pi i(0.x_2 x_1)}|1\rangle\right)\otimes\left(|0\rangle+e^{2\pi i(0.x_3 x_2 x_1)}|1\rangle\right)$$

where $0.x_1 = x_1/2$, $0.x_2 x_1 = x_2/2 + x_1/4$, etc. (binary fractional notation). The swap corrects the qubit ordering to match the standard QFT output.

---

---

## Lecture 40 — QFT Circuit: Generalisation to $n$ Qubits

### Mathematical Foundation

Binary-to-decimal:

$$x = \sum_{k=1}^n x_k\,2^{n-k} \implies \frac{x}{2^n} = \sum_{k=1}^n \frac{x_k}{2^k}$$

The QFT implements:

$$|x\rangle \xrightarrow{F} \frac{1}{\sqrt{2^n}}\sum_{y=0}^{2^n-1} e^{2\pi i\frac{xy}{2^n}}|y\rangle = \bigotimes_{k=1}^n\frac{|0\rangle+e^{2\pi i x/2^k}|1\rangle}{\sqrt{2}}$$

The circuit phases match exactly — confirming the circuit **is** the QFT.

---

### General $n$-Qubit QFT Circuit Algorithm

| Step | Action |
|------|--------|
| 0 | Initialise: $|x_1 x_2\cdots x_n\rangle$ |
| 1 | Apply $H$ to qubit 1; then $C\text{-}R_2$ (ctrl: $x_2$), $C\text{-}R_3$ (ctrl: $x_3$), $\ldots$, $C\text{-}R_n$ (ctrl: $x_n$) on qubit 1 |
| 2 | Apply $H$ to qubit 2; then $C\text{-}R_2$ (ctrl: $x_3$), $\ldots$, $C\text{-}R_{n-1}$ (ctrl: $x_n$) on qubit 2 |
| $\vdots$ | Continue: qubit $j$ gets $H$ followed by $C\text{-}R_2$ through $C\text{-}R_{n-j+1}$ |
| $n$ | Apply $H$ to qubit $n$ (no controlled rotations) |
| $n+1$ | Apply SWAP gates to reverse qubit order: qubit 1 $\leftrightarrow$ qubit $n$, qubit 2 $\leftrightarrow$ qubit $n-1$, $\ldots$ |

---

### Gate Count

| Gate type | Number used |
|-----------|-------------|
| Hadamard ($H$) | $n$ |
| Controlled rotations $C\text{-}R_k$ | $\frac{n(n-1)}{2}$ |
| SWAP | $\lfloor n/2\rfloor$ |
| **Total** | $O(n^2)$ |

Classical DFT requires $O(N\log N) = O(n\cdot 2^n)$ operations. The QFT requires only $O(n^2)$ gates — an **exponential speedup** in circuit size.

---

### Gate Definitions Reference

| Gate | Matrix | Action |
|------|--------|--------|
| $H$ | $\frac{1}{\sqrt{2}}\begin{pmatrix}1&1\\1&-1\end{pmatrix}$ | Superposition; single-qubit QFT |
| $U_{\mathrm{rot},k}$ | $\begin{pmatrix}1&0\\0&e^{2\pi i/2^k}\end{pmatrix}$ | Phase rotation by $2\pi/2^k$ |
| $C\text{-}R_k$ | $\mathrm{diag}(1,1,1,e^{2\pi i/2^k})$ | Controlled phase rotation |
| SWAP | $\begin{pmatrix}1&0&0&0\\0&0&1&0\\0&1&0&0\\0&0&0&1\end{pmatrix}$ | Exchange two qubit states |

---

### Key Takeaways

- **QFT = tensor product of phase-rotated superpositions**, one per qubit.
- **The circuit builds each qubit's phase factor layer by layer**: $H$ creates the superposition; controlled $R_k$ gates accumulate the fractional phase bits.
- **Swap gates** correct the reversed bit ordering inherent in the circuit structure.
- **QFT uses $O(n^2)$ gates** — exponentially fewer than the classical FFT for the same $N = 2^n$ inputs.
- The QFT is the **core sub-routine of Shor's algorithm**, enabling efficient period extraction from the modular exponentiation oracle.

---

*Keywords: Quantum Fourier Transform, DFT, Unitary transformation, Hadamard gate, Controlled rotation $R_k$, SWAP gate, Binary fraction notation, Tensor product structure, Shor's algorithm, Period finding, $n$-qubit circuit, $O(n^2)$ gates.*
