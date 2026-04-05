# Quantum Mechanics Lecture Notes
## Rotations, Density Matrices & Bloch Sphere

---

## Lecture 6 — Rotations on the Bloch Sphere

### Introduction

This lecture focuses on the fundamental concepts of **rotations in coordinate systems**, particularly as they relate to the **Bloch sphere** in quantum mechanics. The discussion begins with classical rotation concepts and moves toward quantum mechanical rotations involving spin operators.

---

### Core Concepts

#### Rotation Types

- **Active Rotation** — The system or vector itself is rotated while the coordinate axes remain fixed.
- **Passive Rotation** — The coordinate axes are rotated while the system/vector remains fixed.

#### Coordinate Systems

- Original coordinate system: $(X, Y, Z)$
- Rotated coordinate system: $(X', Y', Z')$
- Rotation is considered about the $Z$-axis, so $Z' = Z$ remains unchanged.

---

### Rotation Matrix about the $Z$-axis

The 3D rotation matrix for an angle $\phi$ about the $Z$-axis:

$$
R_Z(\phi) =
\begin{bmatrix}
\cos \phi & -\sin \phi & 0 \\
\sin \phi & \cos \phi & 0 \\
0 & 0 & 1
\end{bmatrix}
$$

---

### Mathematical Formulation

#### Vector Transformation

For **passive rotation**:
$$\vec{R}' = R_Z(\phi)\, \vec{R}$$

For **active rotation** (rotating the vector clockwise by $\phi$):
$$\vec{R}' = R_Z(-\phi)\, \vec{R}$$

Inverting gives:
$$\vec{R} = R_Z(\phi)\, \vec{R}'$$

#### Isotropy of Space

The wave function $\psi$ is invariant under rotation of coordinate systems:
$$\psi'(\vec{R}') = \psi(\vec{R})$$

Substituting $\vec{R} = R_Z(\phi)\vec{R}'$:
$$\psi'(\vec{R}') = \psi\!\left(R_Z(\phi)\,\vec{R}'\right)$$

---

### Infinitesimal Rotations and Angular Momentum

For an infinitesimal rotation $\delta\phi$:

$$
R_Z(\delta\phi) \approx
\begin{bmatrix}
1 & -\delta\phi & 0 \\
\delta\phi & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
$$

Applying this to the wave function and using a Taylor expansion:

$$
\psi'(\vec{r}) = \psi(\vec{r}) - \delta\phi \left(y\frac{\partial}{\partial x} - x\frac{\partial}{\partial y}\right)\psi(\vec{r})
$$

Using the momentum operators $p_x = \frac{\hbar}{i}\frac{\partial}{\partial x}$, $p_y = \frac{\hbar}{i}\frac{\partial}{\partial y}$, the bracket is identified as the $z$-component of angular momentum:

$$L_z = x\,p_y - y\,p_x$$

The transformation becomes:

$$\psi' = \left(1 - \frac{i\,\delta\phi}{\hbar}\,L_z\right)\psi$$

Taking the limit $\phi = n\,\delta\phi$ as $n \to \infty$:

$$\boxed{\psi' = e^{-\frac{i}{\hbar}\phi\, L_z}\,\psi}$$

> **Conclusion:** $L_z$ is the **generator of rotations** about the $Z$-axis.

---

### Rotations on the Bloch Sphere

For spin-$\frac{1}{2}$ states, the generator of rotation replaces $L_z$ with the spin operator $S_z = \frac{\hbar}{2}\sigma_z$. The rotation operator about $Z$ is:

$$R_Z(\phi) = e^{-\frac{i}{2}\phi\,\sigma_z}$$

The **general rotation** about an arbitrary unit vector $\hat{n} = (n_x, n_y, n_z)$:

$$R_{\hat{n}}(\phi) = e^{-\frac{i}{2}\phi\,(\hat{n}\cdot\vec{\sigma})}$$

where $\vec{\sigma} = \sigma_x\,\hat{i} + \sigma_y\,\hat{j} + \sigma_z\,\hat{k}$.

**Example** — Rotation about the $X$-axis:
$$R_X(\phi) = e^{-\frac{i}{2}\phi\,\sigma_x}$$

---

### Timeline

| Time | Topic | Key Result |
|------|-------|-----------|
| 00:00–00:04 | Passive vs active rotations | $R_Z(\phi)$ defined |
| 00:08–00:13 | Active rotations & inverse | $\vec{R}' = R_Z(-\phi)\vec{R}$ |
| 00:13–00:19 | Isotropy & wave function | $\psi'(\vec{R}') = \psi(R_Z(\phi)\vec{R}')$ |
| 00:19–00:26 | Infinitesimal rotations, $L_z$ | $\psi' = (1 - \frac{i\delta\phi}{\hbar}L_z)\psi$ |
| 00:25–00:29 | Bloch sphere spin operators | $R_Z(\phi) = e^{-\frac{i}{2}\phi\sigma_z}$ |
| 00:27–00:30 | General rotation about arbitrary axis | $R_{\hat{n}}(\phi) = e^{-\frac{i}{2}\phi(\hat{n}\cdot\vec{\sigma})}$ |

---

---

## Lecture 7 — Rotation Operators on the Bloch Sphere (Part 2)

### Bloch Sphere Representation

A qubit state $|\psi\rangle$ on the Bloch sphere:

$$|\psi\rangle = \cos\tfrac{\theta}{2}\,|0\rangle + e^{i\phi}\sin\tfrac{\theta}{2}\,|1\rangle$$

The corresponding unit vector $\mathbf{n}$:
$$n_x = \sin\theta\cos\phi, \quad n_y = \sin\theta\sin\phi, \quad n_z = \cos\theta, \quad n_x^2+n_y^2+n_z^2=1$$

---

### Rotation Operator Expansion

The rotation operator about $\mathbf{n}$ by angle $\alpha$:

$$R_{\mathbf{n}}(\alpha) = e^{-\frac{i\alpha}{2}\,\mathbf{n}\cdot\boldsymbol{\sigma}}$$

Using the key identity $(\mathbf{n}\cdot\boldsymbol{\sigma})^2 = I$ (since $\mathbf{n}$ is a unit vector), the exponential expands to:

$$\boxed{R_{\mathbf{n}}(\alpha) = \cos\tfrac{\alpha}{2}\,I - i\sin\tfrac{\alpha}{2}\,(\mathbf{n}\cdot\boldsymbol{\sigma})}$$

The **Pauli product identity** for arbitrary vectors $\mathbf{a}$, $\mathbf{b}$:

$$(\mathbf{a}\cdot\boldsymbol{\sigma})(\mathbf{b}\cdot\boldsymbol{\sigma}) = (\mathbf{a}\cdot\mathbf{b})\,I + i\,\boldsymbol{\sigma}\cdot(\mathbf{a}\times\mathbf{b})$$

---

### The Hadamard Gate as a Rotation

The Hadamard matrix:

$$H = \frac{1}{\sqrt{2}}\begin{pmatrix}1 & 1\\1 & -1\end{pmatrix}, \qquad H|0\rangle = |{+}\rangle = \frac{|0\rangle+|1\rangle}{\sqrt{2}}$$

This corresponds to a **$\pi/2$ rotation about the $y$-axis**, flipping $|0\rangle$ (along $z$) to $|+\rangle$ (along $x$):

$$R_y\!\left(\tfrac{\pi}{2}\right) = \cos\tfrac{\pi}{4}\,I - i\sin\tfrac{\pi}{4}\,\sigma_y = \frac{1}{\sqrt{2}}(I - i\sigma_y)$$

The gate can also be decomposed as:

$$H = R_x(\pi)\,R_y\!\left(\tfrac{\pi}{2}\right)$$

where $R_x(\pi)$ acts as the NOT (bit-flip) gate and $R_y(\pi/2)$ creates superposition. Overall phase factors are physically irrelevant and ignored.

---

### Key Identities

| Identity | Description |
|----------|-------------|
| $\sigma_x\,R_y(\theta)\,\sigma_x = R_y(-\theta)$ | Conjugation by $\sigma_x$ flips the rotation angle |
| $R_z(\theta)\,\sigma_x\,R_z^\dagger(\theta) = \cos\theta\,\sigma_x + \sin\theta\,\sigma_y$ | $R_z$ rotates $\sigma_x$ into a combination of $\sigma_x$ and $\sigma_y$ |

---

### Rotation Operators Summary

| Operator | Axis | Angle | Quantum Gate | Notes |
|----------|------|-------|-------------|-------|
| $R_{\mathbf{n}}(\alpha)$ | Arbitrary $\mathbf{n}$ | $\alpha$ | General single-qubit rotation | Fundamental for all single-qubit gates |
| $R_y(\pi/2)$ | $y$ | $\pi/2$ | Superposition $|0\rangle\to|{+}\rangle$ | Basis for Hadamard |
| $R_x(\pi)$ | $x$ | $\pi$ | NOT (bit-flip) | $|0\rangle\leftrightarrow|1\rangle$ |
| $H = R_x(\pi)\,R_y(\pi/2)$ | — | — | Hadamard gate | Combination of rotations |

---

---

## Lecture 8 — Rotation Operators and Euler Decomposition

### Rotation Operator Reference

For $\alpha \in \{x, y, z\}$:

$$R_\alpha(\theta) = \cos\tfrac{\theta}{2}\,I - i\sin\tfrac{\theta}{2}\,\sigma_\alpha$$

---

### Pauli & Rotation Operator Identities

| # | Identity | Explanation |
|---|----------|-------------|
| 1 | $\sigma_x\,R_y(\theta)\,\sigma_x = R_y(-\theta)$ | $\sigma_x$ inverts rotation about $y$ |
| 2 | $\sigma_x\,R_z(\theta)\,\sigma_x = R_z(-\theta)$ | $\sigma_x$ inverts rotation about $z$ |
| 3 | $R_z(\theta)\,\sigma_z\,R_z^\dagger(\theta) = \sigma_z$ | $\sigma_z$ commutes with $R_z$ |
| 4 | $R_x(\theta)\,\sigma_y\,R_x^\dagger(\theta) = \cos\theta\,\sigma_y - \sin\theta\,\sigma_z$ | $\sigma_y$ rotated about $x$ |
| 5 | $R_y(\theta)\,\sigma_x\,R_y^\dagger(\theta) = \cos\theta\,\sigma_x + \sin\theta\,\sigma_z$ | $\sigma_x$ rotated about $y$ |
| 6 | $R_z(\theta)\,\sigma_x\,R_z^\dagger(\theta) = \cos\theta\,\sigma_x + \sin\theta\,\sigma_y$ | $\sigma_x$ rotated about $z$ |
| 7 | $R_y(\theta)\,\sigma_z\,R_y^\dagger(\theta) = \cos\theta\,\sigma_z + \sin\theta\,\sigma_x$ | Derived in lecture |

#### Proof Sketch: Identity 7

Starting from $R_y(\theta) = \cos\frac{\theta}{2}I - i\sin\frac{\theta}{2}\sigma_y$, expand $R_y(\theta)\,\sigma_z\,R_y^\dagger(\theta)$ and simplify using $\sigma_y^2 = I$ and the commutation rules:

$$\sigma_z\sigma_y = -i\sigma_x, \qquad \sigma_y\sigma_z = i\sigma_x$$

Result:
$$R_y(\theta)\,\sigma_z\,R_y^\dagger(\theta) = \cos\theta\,\sigma_z + \sin\theta\,\sigma_x$$

---

### Euler Decomposition

Any single-qubit rotation $R_{\mathbf{n}}(\alpha)$ about arbitrary axis $\mathbf{n}$ can be decomposed into rotations about the $z$ and $y$ axes:

$$\boxed{R_{\mathbf{n}}(\alpha) = R_z(\phi)\,R_y(\theta)\,R_z(\alpha)\,R_y^\dagger(\theta)\,R_z^\dagger(\phi)}$$

where the axis is parametrized as:

$$\mathbf{n} = \sin\theta\cos\phi\,\hat{i} + \sin\theta\sin\phi\,\hat{j} + \cos\theta\,\hat{k}$$

#### Geometric Interpretation

1. $R_z(-\phi)$ — rotates $\mathbf{n}$ onto the $xz$-plane
2. $R_y(-\theta)$ — rotates $\mathbf{n}$ onto the $z$-axis
3. $R_z(\alpha)$ — applies the rotation about $z$
4. Inverse rotations return to the original axis $\mathbf{n}$

#### Practical Importance

Any single-qubit gate can be implemented using only rotations about $y$ and $z$ axes — critical for physical quantum hardware that supports only fixed-axis rotations.

---

---

## Lecture 9 — Density Matrices

### Pure States

A pure state $|\psi\rangle$ in a Hilbert space:

$$|\psi\rangle = \sum_i c_i\,|f_i\rangle, \qquad \sum_i|c_i|^2 = 1$$

The **density matrix for a pure state**:

$$\rho = |\psi\rangle\langle\psi|, \qquad \rho_{ij} = c_i\,c_j^*$$

For a qubit $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$ with $|\alpha|^2+|\beta|^2=1$:

$$\rho = \begin{pmatrix}|\alpha|^2 & \alpha\beta^* \\ \alpha^*\beta & |\beta|^2\end{pmatrix}$$

- **Diagonal elements** $\rho_{ii}$ → **populations** (measurement probabilities)
- **Off-diagonal elements** $\rho_{ij}$ → **coherences** (phase information)

---

### Mixed States

A mixed state represents a statistical ensemble of pure states. For example, 6 spins up and 4 spins down out of 10:

$$p_\uparrow = \tfrac{3}{5}, \qquad p_\downarrow = \tfrac{2}{5}$$

$$\rho = p_\uparrow\,|0\rangle\langle0| + p_\downarrow\,|1\rangle\langle1| = \begin{pmatrix}\frac{3}{5} & 0 \\ 0 & \frac{2}{5}\end{pmatrix}$$

Off-diagonal elements vanish — no coherence, no phase information.

---

### Properties of Density Matrices

| # | Property | Implication |
|---|----------|-------------|
| 1 | $\mathrm{Tr}(\rho) = 1$ | Total probability normalization |
| 2 | $\mathrm{Tr}(\rho^2) = 1$ → pure; $\mathrm{Tr}(\rho^2) < 1$ → mixed | Distinguishes pure from mixed |
| 3 | $\rho^2 = \rho$ (idempotent) | Pure state condition; $\rho$ is a projector |
| 4 | $\rho = \rho^\dagger$ (Hermitian) | All eigenvalues are real and non-negative |
| 5 | $\sum_i\lambda_i = 1$, $\lambda_i \geq 0$ | Eigenvalues as probabilities |

---

### Expectation Values

For an observable $\hat{O}$:

$$\langle O\rangle = \mathrm{Tr}(\rho\,\hat{O})$$

For a pure state $\rho = |\psi\rangle\langle\psi|$, this reduces to:

$$\langle O\rangle = \langle\psi|\hat{O}|\psi\rangle$$

---

---

## Lecture 10 — Density Matrix & Bloch Sphere Representation

### Expectation Value for Mixed States

$$\rho = \sum_i p_i\,|\psi_i\rangle\langle\psi_i|, \qquad \langle O\rangle = \sum_i p_i\,\langle\psi_i|O|\psi_i\rangle = \mathrm{Tr}(\rho\,O)$$

---

### General Qubit Density Matrix

The most general Hermitian, trace-1 density matrix for a qubit has **three real independent parameters**:

$$\rho = \begin{pmatrix}A & B+iC \\ B-iC & 1-A\end{pmatrix}, \qquad A, B, C \in \mathbb{R}$$

---

### Bloch Sphere Representation

The density matrix can be written compactly as:

$$\boxed{\rho = \frac{1}{2}\left(I + \vec{\alpha}\cdot\vec{\sigma}\right)}$$

where $\vec{\alpha} = (\alpha_1, \alpha_2, \alpha_3)$ is the **Bloch vector** and the components relate to the parameters by:

$$A = \frac{1+\alpha_3}{2}, \quad B = \frac{\alpha_1}{2}, \quad C = -\frac{\alpha_2}{2}$$

The Pauli matrices:

$$\sigma_x = \begin{pmatrix}0&1\\1&0\end{pmatrix}, \qquad \sigma_y = \begin{pmatrix}0&-i\\i&0\end{pmatrix}, \qquad \sigma_z = \begin{pmatrix}1&0\\0&-1\end{pmatrix}$$

---

### Eigenvalues and Purity

The eigenvalues of $\rho$:

$$\lambda_{1,2} = \frac{1 \pm |\vec{\alpha}|}{2}$$

Since $\rho$ is positive semidefinite:

$$0 \leq |\vec{\alpha}| \leq 1$$

| State | $|\vec{\alpha}|$ | Bloch vector location | Eigenvalues |
|-------|-----------------|----------------------|-------------|
| Pure  | $= 1$ | Surface of Bloch sphere | $\{1,\, 0\}$ |
| Mixed | $< 1$ | Interior of Bloch sphere | Both in $(0,1)$ |

---

### Pure State on the Bloch Sphere

$$|\psi\rangle = \cos\tfrac{\theta}{2}\,|0\rangle + e^{i\phi}\sin\tfrac{\theta}{2}\,|1\rangle$$

Bloch vector:
$$\alpha_1 = \sin\theta\cos\phi, \quad \alpha_2 = \sin\theta\sin\phi, \quad \alpha_3 = \cos\theta, \qquad \alpha_1^2+\alpha_2^2+\alpha_3^2=1$$

Explicit density matrix:

$$\rho = \frac{1}{2}\begin{pmatrix}1+\cos\theta & \sin\theta\,e^{-i\phi} \\ \sin\theta\,e^{i\phi} & 1-\cos\theta\end{pmatrix}$$

---

### Key Takeaways

- Density matrices provide a **unified framework** for pure and mixed states.
- **Diagonal elements** are populations; **off-diagonal elements** encode quantum coherence.
- The **Bloch vector norm** directly signals purity: $|\vec{\alpha}|=1$ for pure, $|\vec{\alpha}|<1$ for mixed.
- The **trace formula** $\langle O\rangle = \mathrm{Tr}(\rho O)$ is foundational for quantum information and statistical mechanics.
- **Pauli matrices** are natural generators for decomposing the qubit density matrix.

---

*Keywords: Rotation matrix, Active/Passive rotation, Angular momentum $L_z$, Pauli matrices, Bloch sphere, Spin operators, Euler decomposition, Density matrix, Pure state, Mixed state, Coherence, Expectation value.*
