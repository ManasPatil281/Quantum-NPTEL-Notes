# Quantum Information Theory — Lecture Notes
## Decoherence · Open Quantum Systems · Superoperators · Kraus Operators

---

## Lecture 46 — Introduction to Decoherence and Open Quantum Systems

### Coherence and the Density Matrix

A pure qubit state:

$$|\psi\rangle = \cos\tfrac{\theta}{2}|0\rangle + e^{i\phi}\sin\tfrac{\theta}{2}|1\rangle$$

has density matrix:

$$\rho = \begin{pmatrix}\cos^2\frac{\theta}{2} & e^{-i\phi}\sin\frac{\theta}{2}\cos\frac{\theta}{2}\\e^{i\phi}\sin\frac{\theta}{2}\cos\frac{\theta}{2} & \sin^2\frac{\theta}{2}\end{pmatrix}$$

- **Diagonal elements** $\rho_{00}$, $\rho_{11}$ → **populations**
- **Off-diagonal elements** $\rho_{01}$, $\rho_{10}$ → **coherences** (quantum superposition)
- $\mathrm{Tr}(\rho) = 1$ always

**Decoherence** = loss of off-diagonal elements → transition from pure to mixed state.

---

### Closed vs Open System Dynamics

**Closed system** (system $S$ + reservoir $R$ together):

$$H_{\text{total}} = H_S + H_R + H_{SR}$$

$$\rho(t) = U(t)\,\rho(0)\,U^\dagger(t), \qquad U(t) = e^{-iH_{\text{total}}t/\hbar}$$

$$\frac{d\rho}{dt} = -\frac{i}{\hbar}[H,\rho] \quad \text{(Liouville–von Neumann equation)}$$

**Open system** — focusing on system $S$ alone by tracing out $R$:

$$\rho_S(t) = \mathrm{Tr}_R\!\left[\rho(t)\right]$$

This reduced evolution is **non-unitary** — information leaks to the environment.

---

### Classification

| Type | Condition | Physical Effect | QIP Channel |
|------|-----------|----------------|-------------|
| Quantum Non-Demolition (QND) | $[H_S, H_{SR}] = 0$ | Decoherence without energy loss | Phase damping |
| Quantum Dissipative | $[H_S, H_{SR}] \neq 0$ | Decoherence with energy loss | Amplitude damping |

**Dissipation** = relaxation from excited to ground state; Bloch vector shrinks toward centre/pole.

---

### Bloch Sphere Representation

$$\rho(t) = \frac{1}{2}\!\left(I + \langle\sigma_x\rangle\sigma_x + \langle\sigma_y\rangle\sigma_y + \langle\sigma_z\rangle\sigma_z\right)$$

$$\langle\sigma_x\rangle = \sin\theta\cos\phi, \quad \langle\sigma_y\rangle = \sin\theta\sin\phi, \quad \langle\sigma_z\rangle = \cos\theta$$

---

### Phenomenological Decoherence Model

Time-dependent off-diagonal element:

$$\rho_{01}(t) = e^{-i(\omega t+\phi)}\,e^{-\gamma t}\sin\tfrac{\theta}{2}\cos\tfrac{\theta}{2}$$

The factor $e^{-\gamma t}$ describes **exponential decay of coherence** at rate $\gamma$ (to be derived rigorously later).

---

---

## Lecture 47 — System-Environment Entanglement and Decoherence

### Raising and Lowering Operators

$$\sigma_+ = \sigma_x + i\sigma_y, \qquad \sigma_- = \sigma_x - i\sigma_y$$

### Quantum Circuit Model of Decoherence

Model the environment as a single ancilla qubit, initially $|0\rangle$.

**Initial joint state:**

$$|\Psi_{\text{init}}\rangle = (\alpha|0\rangle + \beta|1\rangle) \otimes |0\rangle$$

After a **CNOT gate** (system = control, environment = target):

$$|\Psi_{\text{final}}\rangle = \alpha|0,0\rangle + \beta|1,1\rangle$$

This is a **Bell-type entangled state** (for $\alpha = \beta = 1/\sqrt{2}$).

**Tracing out the environment:**

$$\rho'_S = \mathrm{Tr}_{\text{env}}\!\left(|\Psi_{\text{final}}\rangle\langle\Psi_{\text{final}}|\right) = \begin{pmatrix}|\alpha|^2 & 0\\0 & |\beta|^2\end{pmatrix}$$

Off-diagonal elements **vanish** — coherence is destroyed.

---

### Before and After Decoherence

| Property | Before | After (env traced out) |
|----------|--------|----------------------|
| $\rho$ | Pure; non-zero off-diagonal | Mixed; diagonal only |
| $\rho_{01}$ | $\alpha\beta^*$ | $0$ |
| $|\mathbf{n}|$ | $1$ (surface of Bloch sphere) | $< 1$ (interior) |

> **Key insight:** Decoherence = entanglement of system with environment → measuring the environment would reveal the system's state → coherence is irreversibly lost from the system's perspective (Markovian approximation).

**Maximally mixed state** ($\langle\sigma_i\rangle = 0$ for all $i$) → centre of Bloch sphere → complete loss of information.

---

---

## Lecture 48 — Operator Sum Representation (Kraus Formalism)

### Setup

- System Hilbert space: $\mathcal{H}_1$; Environment Hilbert space: $\mathcal{H}_2$
- Initial state: separable, environment in pure state $|0\rangle_2$:

$$\rho_0 = \rho_S \otimes |0\rangle\langle 0|$$

- Total unitary evolution: $\rho(t) = U_t\,\rho_0\,U_t^\dagger$
- Reduced system state: $\rho_S(t) = \mathrm{Tr}_{\mathcal{H}_2}\!\left[U_t\,\rho_0\,U_t^\dagger\right]$

---

### Kraus (Cross) Operators

Project the unitary onto the environment basis $\{|k\rangle_2\}$:

$$E_k = \langle k|_2\, U_t\, |0\rangle_2$$

$E_k$ acts only on $\mathcal{H}_1$.

---

### Operator Sum Representation (OSR)

$$\boxed{\rho_S(t) = \sum_k E_k\,\rho_S(0)\,E_k^\dagger}$$

**Completeness condition** (from unitarity of $U_t$):

$$\sum_k E_k^\dagger E_k = I$$

This guarantees trace preservation and is a **completely positive trace-preserving (CPTP) map** — also called a **quantum channel** or **superoperator**.

---

### Key Equations

| # | Description | Formula |
|---|-------------|---------|
| 1 | Initial total state | $\rho_0 = \rho_S\otimes|0\rangle\langle 0|$ |
| 2 | Unitary evolution | $\rho(t) = U_t\rho_0 U_t^\dagger$ |
| 3 | Reduced system state | $\rho_S(t) = \mathrm{Tr}_{\mathcal{H}_2}[\rho(t)]$ |
| 4 | Kraus operator | $E_k = \langle k|U_t|0\rangle$ |
| 5 | **OSR** | $\rho_S(t) = \sum_k E_k\rho_S(0)E_k^\dagger$ |
| 6 | Completeness | $\sum_k E_k^\dagger E_k = I$ |

---

---

## Lecture 49 — Superoperator Properties and Unitary Dilation

### Three Key Properties of Superoperators

#### 1. Hermiticity Preservation

$$\rho(t)^\dagger = \left(\sum_k E_k\rho(0)E_k^\dagger\right)^\dagger = \sum_k E_k\rho(0)E_k^\dagger = \rho(t) \quad \checkmark$$

#### 2. Trace Preservation

Using cyclic property of trace:

$$\mathrm{Tr}[\rho(t)] = \mathrm{Tr}\!\left[\rho(0)\sum_k E_k^\dagger E_k\right] = \mathrm{Tr}[\rho(0)] = 1 \quad \checkmark$$

#### 3. Positivity Preservation

For any $|\psi\rangle$:

$$\langle\psi|\rho(t)|\psi\rangle = \sum_k \langle\psi|E_k\rho(0)E_k^\dagger|\psi\rangle \geq 0 \quad \checkmark$$

since $\rho(0) \geq 0$ and $E_k^\dagger|\psi\rangle\in\mathcal{H}_1$.

---

### Unitary Dilation (Purification)

**Converse question:** Given Kraus operators $\{E_k\}$, can one find a unitary $U$ on $\mathcal{H}_1\otimes\mathcal{H}_2$ that generates them?

**Construction:** Define $U$ via its action on the product state:

$$U\!\left(|\psi\rangle_1\otimes|0\rangle_2\right) = \sum_k E_k|\psi\rangle_1\otimes|k\rangle_2$$

**Verification of unitarity:** Using orthonormality of $\{|k\rangle_2\}$ and completeness of $\{E_k\}$:

$$\langle\psi_1, 0|U^\dagger U|\phi_1, 0\rangle = \sum_k\langle\psi_1|E_k^\dagger E_k|\phi_1\rangle = \langle\psi_1|\phi_1\rangle \quad \checkmark$$

**Recovery of OSR:**

$$\rho_1' = \mathrm{Tr}_2\!\left[U(\rho_1\otimes|0\rangle\langle 0|)U^\dagger\right] = \sum_k E_k\rho_1 E_k^\dagger$$

> **Conclusion:** Every CPTP map can be realised as a **unitary operation on an extended Hilbert space** — open system dynamics is always a "shadow" of closed system unitary evolution.

---

### Summary

| Property | Statement |
|----------|-----------|
| Hermiticity | Superoperator maps Hermitian to Hermitian |
| Trace preservation | $\sum_k E_k^\dagger E_k = I$ |
| Positivity | $\rho(t)\geq 0$ if $\rho(0)\geq 0$ |
| Unitary dilation | Any CPTP map $\leftrightarrow$ unitary on $\mathcal{H}_1\otimes\mathcal{H}_2$ |
| Dimension of $\mathcal{H}_2$ | Equals number of Kraus operators |

---

---

## Lecture 50 — Kraus Operators, Dimension Bounds, and the Depolarising Channel

### Dimension Bound

For a system with $\dim\mathcal{H}_1 = n$:

- Dimension of auxiliary space $\mathcal{H}_2 \geq$ number of Kraus operators
- **Maximum number of Kraus operators** for any superoperator: $n^2$
- Choosing $\dim\mathcal{H}_2 = n^2$ allows representation of **all** possible quantum channels

For a **single qubit** ($n=2$): at most **4 Kraus operators**.

---

### Pauli Basis Expansion

Any qubit density matrix:

$$\rho = \frac{1}{2}\!\left(I + c_x\sigma_x + c_y\sigma_y + c_z\sigma_z\right), \qquad c_i = \mathrm{Tr}(\rho\,\sigma_i)$$

Relevant anticommutation relations:

$$\sigma_x\sigma_y = -\sigma_y\sigma_x, \qquad \sigma_x\sigma_z = -\sigma_z\sigma_x$$

---

### Depolarising Channel

The most symmetric single-qubit noise channel — applies each Pauli error with equal probability $p/4$, leaves state unchanged with probability $1-3p/4$.

**Kraus operators:**

$$E_0 = \sqrt{1-\tfrac{3p}{4}}\,I, \quad E_1 = \sqrt{\tfrac{p}{4}}\,\sigma_x, \quad E_2 = \sqrt{\tfrac{p}{4}}\,\sigma_y, \quad E_3 = \sqrt{\tfrac{p}{4}}\,\sigma_z$$

**Completeness check:** $\sum_{k=0}^3 E_k^\dagger E_k = \left(1-\tfrac{3p}{4}\right)I + \tfrac{p}{4}(I+I+I) = I$ ✓

**Evolved state:**

$$\boxed{\rho' = \left(1-\tfrac{3p}{4}\right)\rho + \tfrac{p}{4}\!\left(\sigma_x\rho\,\sigma_x + \sigma_y\rho\,\sigma_y + \sigma_z\rho\,\sigma_z\right)}$$

---

### Effect on Bloch Vector

For $\rho = \frac{1}{2}(I + \mathbf{n}\cdot\boldsymbol{\sigma})$, applying the depolarising channel:

$$\mathbf{n}' = \left(1 - p\right)\mathbf{n}$$

The Bloch vector **shrinks uniformly** toward the origin by factor $(1-p)$:

- $p = 0$: no noise, $\rho$ unchanged
- $p = 1$: fully depolarised → $\rho' = \frac{I}{2}$ (maximally mixed state, centre of Bloch sphere)

---

### Summary of Quantum Channels (Single Qubit)

| Channel | Kraus Operators | Physical Effect | Bloch Sphere Effect |
|---------|----------------|-----------------|---------------------|
| Unitary | $\{U\}$ | Rotation | Pure rotation of vector |
| Phase damping | $\{|0\rangle\langle 0|,\, |1\rangle\langle 1|\}$ | Loss of phase (coherence) | Contraction toward $z$-axis |
| Amplitude damping | $\left\{\begin{pmatrix}1&0\\0&\sqrt{1-\gamma}\end{pmatrix},\begin{pmatrix}0&\sqrt{\gamma}\\0&0\end{pmatrix}\right\}$ | Relaxation to $|0\rangle$ | Contraction toward north pole |
| Depolarising | $\sqrt{1-3p/4}\,I,\; \sqrt{p/4}\,\sigma_{x,y,z}$ | Symmetric noise | Uniform shrinkage toward centre |

---

### Key Takeaways

- **Decoherence** arises from system-environment entanglement; tracing out the environment yields a mixed state.
- The **OSR / Kraus formalism** is the correct mathematical language for open quantum system dynamics.
- Every quantum channel is CPTP and admits a **unitary dilation** on a larger Hilbert space.
- **At most $n^2$ Kraus operators** suffice to describe any channel on an $n$-dimensional system.
- The **depolarising channel** is the paradigmatic noise model — symmetric in all directions, shrinks the Bloch vector uniformly.

---

*Keywords: Decoherence, Open quantum system, Density matrix, Coherence, Populations, Von Neumann equation, Liouville–von Neumann, Phase damping, Amplitude damping, Reduced density matrix, Partial trace, Kraus operators, Operator sum representation, CPTP map, Superoperator, Unitary dilation, Purification, Depolarising channel, Bloch sphere, Pauli matrices.*
