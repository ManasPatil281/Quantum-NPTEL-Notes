# Quantum Information Theory — Lecture Notes
## Bell Inequality · CNOT Gate · Dense Coding · Quantum Teleportation · Entangled Photons

---

## Lecture 26 — Bell's Inequality: Violation and the CNOT Gate

### Quantum Probability Formula

For a singlet-like state, after Alice measures along axis $A$ and obtains $+1$, the probability that Bob measures $+1$ along axis $B$ (at angle $\theta_{AB}$) is:

$$P(A^+B^+) = \frac{1}{2}\sin^2\!\left(\frac{\theta_{AB}}{2}\right)$$

This follows from the Bloch sphere parametrisation of spin states:

$$|{+n}\rangle = \cos\tfrac{\theta}{2}|0\rangle + e^{i\phi}\sin\tfrac{\theta}{2}|1\rangle, \qquad |{-n}\rangle = \sin\tfrac{\theta}{2}|0\rangle - e^{i\phi}\cos\tfrac{\theta}{2}|1\rangle$$

---

### Explicit Violation of Bell's Inequality

Bell's inequality in angular form:

$$\sin^2\!\left(\frac{\theta_{AB}}{2}\right) \leq \sin^2\!\left(\frac{\theta_{AC}}{2}\right) + \sin^2\!\left(\frac{\theta_{CB}}{2}\right)$$

Setting $A$, $B$, $C$ coplanar with $\theta_{AB} = 2\theta$, $\theta_{AC} = \theta_{CB} = \theta$:

$$\sin^2\theta \leq 2\sin^2\!\left(\frac{\theta}{2}\right)$$

**At $\theta = 60°$:**

$$\sin^2 60° = \frac{3}{4} \qquad \text{vs} \qquad 2\sin^2 30° = 2\times\frac{1}{4} = \frac{1}{2}$$

Since $\frac{3}{4} > \frac{1}{2}$, **Bell's inequality is violated** — quantum mechanics is incompatible with local realism.

> The 2022 Nobel Prize in Physics was awarded to **Alain Aspect**, **John Clauser**, and **Anton Zeilinger** for experimentally confirming this violation. Zeilinger's group also demonstrated **quantum teleportation** using entangled photons.

---

### The CNOT Gate

The **Controlled-NOT (CNOT)** gate acts on a control qubit and a target qubit:

- Control $= |0\rangle$ → target unchanged
- Control $= |1\rangle$ → target **flipped**

**Matrix** (basis order $|00\rangle, |01\rangle, |10\rangle, |11\rangle$):

$$\mathrm{CNOT} = \begin{pmatrix}1&0&0&0\\0&1&0&0\\0&0&0&1\\0&0&1&0\end{pmatrix}$$

**Truth table:**

| Input (ctrl, tgt) | Output (ctrl, tgt) |
|-------------------|--------------------|
| $|00\rangle$ | $|00\rangle$ |
| $|01\rangle$ | $|01\rangle$ |
| $|10\rangle$ | $|11\rangle$ |
| $|11\rangle$ | $|10\rangle$ |

CNOT can transform separable superposition states into **entangled Bell states** — an essential resource for quantum computation and teleportation.

---

---

## Lecture 27 — Bell States, Dense Coding, and Bell State Measurement

### Key Single-Qubit Gates

| Gate | Action |
|------|--------|
| Hadamard $H$ | $|0\rangle \to \frac{|0\rangle+|1\rangle}{\sqrt{2}}$, $\quad|1\rangle \to \frac{|0\rangle-|1\rangle}{\sqrt{2}}$ |
| $\sigma_x$ (X / bit-flip) | $|0\rangle\leftrightarrow|1\rangle$ |
| $\sigma_z$ (Z / phase-flip) | $|0\rangle\to|0\rangle$, $|1\rangle\to-|1\rangle$ |

---

### Generating Bell States

Starting from computational basis state $|xy\rangle$:

1. Apply $H$ to the first qubit: $|x\rangle \to \frac{|0\rangle + (-1)^x|1\rangle}{\sqrt{2}}$
2. Apply CNOT (first qubit = control, second = target)
3. Result: Bell state $|\beta_{xy}\rangle$

| Label | Bell State | Expression |
|-------|-----------|------------|
| $|\beta_{00}\rangle = |\Phi^+\rangle$ | from $|00\rangle$ | $\frac{1}{\sqrt{2}}(|00\rangle+|11\rangle)$ |
| $|\beta_{01}\rangle = |\Psi^+\rangle$ | from $|01\rangle$ | $\frac{1}{\sqrt{2}}(|01\rangle+|10\rangle)$ |
| $|\beta_{10}\rangle = |\Phi^-\rangle$ | from $|10\rangle$ | $\frac{1}{\sqrt{2}}(|00\rangle-|11\rangle)$ |
| $|\beta_{11}\rangle = |\Psi^-\rangle$ | from $|11\rangle$ | $\frac{1}{\sqrt{2}}(|01\rangle-|10\rangle)$ |

General compact form: $|\beta_{xy}\rangle = \frac{1}{\sqrt{2}}\!\left(|0,y\rangle + (-1)^x|1,\bar{y}\rangle\right)$ where $\bar{y}$ is the bit-flip of $y$.

---

### Bell State Measurement (Decoding)

The **inverse** of Bell state preparation:

1. Apply CNOT
2. Apply $H$ to the first qubit
3. Measure in computational basis

| Bell State Input | Computational Basis Output |
|-----------------|---------------------------|
| $|\beta_{00}\rangle$ | $|00\rangle$ |
| $|\beta_{01}\rangle$ | $|01\rangle$ |
| $|\beta_{10}\rangle$ | $|10\rangle$ |
| $|\beta_{11}\rangle$ | $|11\rangle$ |

---

### Quantum Dense Coding

**Goal:** Alice sends **2 classical bits** to Bob by transmitting only **1 qubit**, using pre-shared entanglement.

**Protocol:**
1. Alice and Bob share $|\beta_{00}\rangle$
2. Alice applies a local Pauli operation on her qubit to encode 2 bits
3. Alice sends her qubit to Bob
4. Bob performs a Bell state measurement on both qubits → reads 2 bits

| Alice's Operation | Resulting State | Bits Encoded |
|-------------------|----------------|-------------|
| $I$ | $|\beta_{00}\rangle$ | 00 |
| $\sigma_x \otimes I$ | $|\beta_{01}\rangle$ | 01 |
| $\sigma_z \otimes I$ | $|\beta_{10}\rangle$ | 10 |
| $i\sigma_y \otimes I$ | $|\beta_{11}\rangle$ | 11 |

> **Key insight:** 2 classical bits encoded into 1 qubit transmission — only possible because of the pre-shared entanglement. Global phase factors from $i\sigma_y$ are physically irrelevant.

---

### Gate Summary

| Gate | Type | Function | Role |
|------|------|----------|------|
| $H$ | Single-qubit | Creates superposition | Prepares Bell state / measures in Bell basis |
| CNOT | Two-qubit | Flips target if control $=1$ | Generates entanglement |
| $\sigma_x$ | Single-qubit | Bit flip | Encoding (bits 01) |
| $\sigma_z$ | Single-qubit | Phase flip | Encoding (bits 10) |
| $i\sigma_y$ | Single-qubit | Bit + phase flip | Encoding (bits 11) |

---

---

## Lecture 28–29 — Quantum Teleportation

### Dense Coding vs Teleportation

| Protocol | What is sent | What is communicated |
|----------|-------------|---------------------|
| Dense coding | 1 qubit (physical) | 2 classical bits |
| Teleportation | 2 classical bits | 1 unknown qubit state |

---

### Setup

- Alice holds an **unknown qubit** $|\psi\rangle_1 = \alpha|0\rangle + \beta|1\rangle$ (with $|\alpha|^2+|\beta|^2=1$)
- Alice and Bob share Bell state $|\beta_{00}\rangle_{23} = \frac{1}{\sqrt{2}}(|00\rangle+|11\rangle)$
- Qubits 1, 2 belong to Alice; qubit 3 belongs to Bob

---

### Protocol Steps

| Step | Action | Detail |
|------|--------|--------|
| 1 | Combine states | Total state: $|\Psi\rangle_{123} = |\psi\rangle_1 \otimes |\beta_{00}\rangle_{23}$ |
| 2 | Rewrite in Bell basis | Express $|\Psi\rangle_{123}$ in terms of Alice's Bell basis states $\{|\beta_{xy}\rangle_{12}\}$ |
| 3 | Bell measurement | Alice measures qubits 1 & 2 in the Bell basis — projects Bob's qubit into a correlated state |
| 4 | Classical communication | Alice sends her 2-bit result to Bob over a classical channel (LOCC) |
| 5 | Bob's correction | Bob applies a unitary based on Alice's message to recover $|\psi\rangle$ |

---

### Bob's Correction Operations

| Alice Measures | Bob's Qubit State | Bob Applies | Result |
|---------------|-------------------|------------|--------|
| $|\beta_{00}\rangle$ | $\alpha|0\rangle+\beta|1\rangle$ | $I$ (nothing) | $|\psi\rangle$ ✓ |
| $|\beta_{01}\rangle$ | $\alpha|0\rangle-\beta|1\rangle$ | $\sigma_z$ | $|\psi\rangle$ ✓ |
| $|\beta_{10}\rangle$ | $\alpha|1\rangle+\beta|0\rangle$ | $\sigma_x$ | $|\psi\rangle$ ✓ |
| $|\beta_{11}\rangle$ | $\alpha|1\rangle-\beta|0\rangle$ | $i\sigma_y = \sigma_z\sigma_x$ | $|\psi\rangle$ ✓ |

> **No physical qubit is transferred.** The quantum state is reconstructed at Bob's location via entanglement + classical communication. This protocol is foundational to the **BB84** framework (Bennett & Brassard 1984).

---

---

## Lecture 30 — Entangled Photon Generation and Bell State Analysis

### Nonlinear Optics: Polarisation Expansion

The polarisation of a material in an electric field $E$:

$$P_i = \chi^{(1)}_{ij}E_j + \chi^{(2)}_{ijk}E_jE_k + \chi^{(3)}_{ijkl}E_jE_kE_l + \cdots$$

- $\chi^{(1)}$ — linear (dominant at low intensity)
- $\chi^{(2)}$ — second-order (enables PDC); requires **high intensity** and **non-centrosymmetric crystal**
- Since $\chi^{(1)} \gg \chi^{(2)} \gg \chi^{(3)}$, **pulsed high-intensity lasers** are needed for appreciable nonlinear effects

---

### Parametric Down-Conversion (PDC)

A pulsed UV laser (400 nm) pumps a **beta barium borate (BBO) crystal**:

$$\omega_p = \omega_1 + \omega_2, \qquad \mathbf{k}_p = \mathbf{k}_1 + \mathbf{k}_2$$

One high-energy pump photon → two entangled daughter photons (~800 nm each), with **orthogonal polarisations** (type-II phase matching). The down-converted photons emerge in two intersecting cones; **entangled states form at the intersection**, where polarisation is in superposition.

---

### Polarisation as Qubit

| Polarisation | Symbol | Quantum State |
|-------------|--------|---------------|
| Horizontal (H) | $|0\rangle$ | Spin-up analogue |
| Vertical (V) | $|1\rangle$ | Spin-down analogue |
| $+45°$ linear | $|{+}\rangle$ | $\frac{1}{\sqrt{2}}(|H\rangle+|V\rangle)$ |
| $-45°$ linear | $|{-}\rangle$ | $\frac{1}{\sqrt{2}}(|H\rangle-|V\rangle)$ |
| Right circular | $|R\rangle$ | $\frac{1}{\sqrt{2}}(|H\rangle+i|V\rangle)$ |
| Left circular | $|L\rangle$ | $\frac{1}{\sqrt{2}}(|H\rangle-i|V\rangle)$ |

---

### Two-Photon Entangled State

The state generated by PDC:

$$|\psi\rangle = \frac{1}{\sqrt{2}}\!\left(|H\rangle_1|V\rangle_2 + e^{i\phi}|V\rangle_1|H\rangle_2\right)$$

The relative phase $\phi$ is controlled by a **compensator crystal** (BBO crystal of half thickness, rotated 90°) inserted into one beam path. A **half-wave plate** enables generation of other Bell states from this initial state.

---

### Bell State Analysis via Photon Symmetry

Photons are **bosons** — the total two-photon wavefunction must be **symmetric** under particle exchange:

$$|\Psi_{\text{total}}\rangle = |\Psi_{\text{spatial}}\rangle \otimes |\Psi_{\text{spin}}\rangle \quad \text{(must be symmetric overall)}$$

Spatial states at a beam splitter with input modes $A$ and $B$:

$$|\psi_s\rangle = \frac{1}{\sqrt{2}}\!\left(|A\rangle_1|B\rangle_2 + |B\rangle_1|A\rangle_2\right) \quad \text{(symmetric)}$$

$$|\psi_a\rangle = \frac{1}{\sqrt{2}}\!\left(|A\rangle_1|B\rangle_2 - |B\rangle_1|A\rangle_2\right) \quad \text{(antisymmetric)}$$

| Bell State | Spin Symmetry | Required Spatial Symmetry | Photon Behaviour |
|-----------|--------------|--------------------------|-----------------|
| $|\Phi^+\rangle$, $|\Phi^-\rangle$, $|\Psi^+\rangle$ | Symmetric | Symmetric | Photons **bunch** (same output port) |
| $|\Psi^-\rangle$ (EPR singlet) | Antisymmetric | Antisymmetric | Photons **separate** (different ports) |

> The **singlet $|\Psi^-\rangle$ is the only antisymmetric Bell state**. Its unique spatial behaviour (photons exit different ports) makes it directly distinguishable at a beam splitter — the basis for Bell state analysers in quantum communication experiments.

---

### Key Takeaways

- **Parametric down-conversion in BBO crystals** is the standard laboratory method for producing entangled photon pairs.
- **Polarisation encodes the qubit** — all four Bell states are accessible through phase control and wave plates.
- **Bosonic symmetry of photons** governs Bell state detection: the singlet is uniquely identified by anti-bunching at a beam splitter.
- These techniques underpin the Nobel Prize-winning experiments and are the physical foundation of **quantum teleportation, dense coding, and quantum key distribution**.

---

*Keywords: Bell inequality violation, CNOT gate, Bell states, Hadamard gate, Dense coding, Quantum teleportation, LOCC, Pauli operators, Parametric down-conversion, BBO crystal, Nonlinear optics, Photon entanglement, Bosonic symmetry, Bell state analyser.*
