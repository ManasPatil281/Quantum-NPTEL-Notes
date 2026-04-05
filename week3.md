# Quantum & Classical Information Theory — Lecture Notes
## Density Matrix Time Evolution · Classical Information Theory · Reversible Gates

---

## Lecture 11 — Density Matrix Properties and Time Evolution

### Bloch Sphere Recap

The density matrix for a qubit:

$$\rho = \frac{1}{2}\left(I + \vec{\alpha}\cdot\vec{\sigma}\right)$$

Eigenvalues:

$$\lambda_1 = \frac{1+|\vec{\alpha}|}{2}, \qquad \lambda_2 = \frac{1-|\vec{\alpha}|}{2}$$

Bloch vector components in spherical coordinates:

$$\alpha_1 = \sin\theta\cos\phi, \quad \alpha_2 = \sin\theta\sin\phi, \quad \alpha_3 = \cos\theta$$

Pure-state density matrix:

$$\rho = \frac{1}{2}\begin{pmatrix}1+\cos\theta & \sin\theta\,e^{-i\phi}\\\sin\theta\,e^{i\phi} & 1-\cos\theta\end{pmatrix}$$

---

### State Classification on the Bloch Sphere

| State | $\lambda_1$ | $\lambda_2$ | $|\vec{\alpha}|$ | Location |
|-------|-------------|-------------|-----------------|----------|
| Pure | $1$ | $0$ | $1$ | Surface |
| Mixed | $<1$ | $<1$ | $<1$ | Interior |
| Maximally Mixed | $\frac{1}{2}$ | $\frac{1}{2}$ | $0$ | Centre |

The **maximally mixed state** conveys no information about the system:

$$\rho = \frac{1}{2}I = \frac{1}{2}\begin{pmatrix}1&0\\0&1\end{pmatrix}$$

---

### Population and Coherence

- **Diagonal elements** → populations (measurement probabilities)
- **Off-diagonal elements** → coherences (quantum superposition / phase info)

Expectation values of Pauli matrices:

$$\langle\sigma_x\rangle = \sin\theta\cos\phi, \quad \langle\sigma_y\rangle = \sin\theta\sin\phi, \quad \langle\sigma_z\rangle = \cos\theta$$

Recovery of Bloch vector components:

$$\alpha_i = \mathrm{Tr}(\rho\,\sigma_i), \quad i = 1, 2, 3$$

---

### Time Evolution

In the **Schrödinger picture**, with unitary evolution operator $U(t) = e^{-iHt/\hbar}$:

$$\rho(t) = U(t)\,\rho(0)\,U^\dagger(t)$$

The **Heisenberg equation of motion** for an operator $A$:

$$\frac{dA}{dt} = \frac{1}{i\hbar}[A,\,H]$$

Differentiating $\rho(t)$ yields the **Liouville–von Neumann equation**:

$$\boxed{\frac{d\rho}{dt} = \frac{1}{i\hbar}[H,\,\rho] + \left(\frac{d\rho}{dt}\right)_{\!\text{explicit}}}$$

> This is the quantum analogue of the classical Liouville equation, with the commutator replacing the Poisson bracket.

---

### Key Equations Summary

| Description | Formula |
|-------------|---------|
| Bloch sphere density matrix | $\rho = \frac{1}{2}(I + \vec{\alpha}\cdot\vec{\sigma})$ |
| Eigenvalues | $\lambda_{1,2} = \frac{1\pm|\vec{\alpha}|}{2}$ |
| Bloch vector from $\rho$ | $\alpha_i = \mathrm{Tr}(\rho\,\sigma_i)$ |
| Time evolution of $\rho$ | $\rho(t) = U(t)\rho(0)U^\dagger(t)$ |
| Liouville–von Neumann | $\dot{\rho} = \frac{1}{i\hbar}[H,\rho]$ |

---

---

## Lecture 12 — Introduction to Classical Information Theory

### What Is Information?

- **Information content** = the amount of knowledge gained when an event is observed.
- A predictable sequence (e.g. `111111`) carries **no information**; a random sequence (e.g. `10110010`) carries **non-zero information**.
- Information is closely tied to **uncertainty** and **surprise**.

---

### Encoding Messages

Given $m$ possible messages, the number of bits $n$ needed satisfies:

$$2^n \geq m \implies n = \log_2 m$$

Example: $m = 8$ messages require $n = 3$ bits.

---

### Hartley's Formula (1927)

$$I = \log_2 m$$

Information content grows **logarithmically** with the number of possible messages.

---

### Probability and Information

- **Unlikely events** → high information content
- **Likely events** → low information content

For an event with probability $p$:

$$\boxed{I = -\log_2 p}$$

The negative sign keeps $I > 0$ since $\log_2 p < 0$ for $0 < p < 1$.

Additivity for independent events $A$, $B$:

$$I(A \text{ and } B) = I(A) + I(B)$$

#### Example

| Event | $p$ | $I = -\log_2 p$ (bits) |
|-------|-----|------------------------|
| Rain in Thar Desert | $0.005$ | $7.64$ |
| No rain in Thar Desert | $0.995$ | $0.007$ |
| Certain event | $1$ | $0$ |

---

### Shannon Entropy

The **entropy** $H$ is the expected (average) information content of a random variable:

$$H = -\sum_i p_i \log_2 p_i$$

For two equally likely outcomes ($p_1 = p_2 = \frac{1}{2}$):

$$H = -2\times\frac{1}{2}\log_2\frac{1}{2} = 1 \text{ bit}$$

This is the **maximum entropy** case — complete randomness, equal probabilities.

---

### Key Definitions

| Term | Definition |
|------|------------|
| Information content | $I = -\log_2 p$ |
| Shannon entropy | $H = -\sum_i p_i\log_2 p_i$ |
| Maximally mixed state | All outcomes equally likely; maximum entropy |
| Encoding | $n$ bits for $m$ messages where $2^n \geq m$ |

---

---

## Lecture 13 — Information Functional and Shannon Entropy

### Channel Model

- Input random variable $X$, output $Y$
- Input distribution: $P(X)$; channel behaviour: $P(Y|X)$
- Alphabet size: $|\mathcal{X}| = N$ (e.g. $N=2$ for a qubit)

---

### Properties of the Information Functional $H(P)$

| # | Property | Meaning |
|---|----------|---------|
| 1 | **Continuity** | Small changes in $P$ → small changes in $H$ |
| 2 | **Non-negativity**: $H \geq 0$; $H = 0$ iff one outcome is certain | Zero uncertainty = zero entropy |
| 3 | **Boundedness**: $H \leq C(N)$ | Max entropy achieved by uniform distribution |
| 4 | **Additivity**: $H(P,Q) = H(P)+H(Q)$ for independent $P$, $Q$ | Joint entropy splits for independent sources |

---

### Shannon Entropy

$$H(P) = -\sum_{i=1}^N p_i\log p_i$$

For a **uniform distribution** $p_i = \frac{1}{N}$:

$$H = \log N$$

This mirrors the **Boltzmann entropy** $S = k\ln\Omega$.

---

### Uniqueness

The additivity property implies $H(P^r) = r\,H(P)$ for rational $r$; continuity extends this to all real $r$. Shannon entropy is therefore the **unique** functional satisfying all four properties.

---

### Towards Noiseless Coding

For $n$ i.i.d. draws $X_1,\ldots,X_n$ from $P$:

$$P(X_1,\ldots,X_n) = \prod_{j=1}^n P(X_j) = \prod_{i=1}^N p_i^{n_i}$$

where $n_i$ = count of symbol $i$ in the string. This grouping leads directly to the noiseless coding theorem (continued next lecture).

---

---

## Lecture 14 — Asymptotic Equipartition and Data Compression

### Joint Probability of a Sequence

For an i.i.d. source with alphabet $\mathcal{X}$:

$$P(X_1,\ldots,X_N) = \prod_{i=1}^{|\mathcal{X}|} p_i^{n_i}$$

By the **law of large numbers**, $n_i/N \to p_i$ as $N\to\infty$, giving:

$$-\frac{1}{N}\log_2 P(X_1,\ldots,X_N) \approx H(X) = -\sum_i p_i\log_2 p_i$$

Equivalently:

$$\boxed{P(X_1,\ldots,X_N) \approx 2^{-N\,H(X)}}$$

---

### Asymptotic Equipartition Property (AEP)

For large $N$, almost all sequences have roughly **equal probability** $2^{-NH(X)}$.

| Quantity | Value |
|----------|-------|
| Effective number of **typical** sequences | $2^{N\,H(X)}$ |
| Total number of possible sequences | $|\mathcal{X}|^N = 2^{N\log_2|\mathcal{X}|}$ |

Since $H(X) \leq \log_2|\mathcal{X}|$, typical sequences are an exponentially small fraction of all sequences — this is what makes compression possible.

---

### Shannon's Noiseless Coding Theorem

> The average number of bits per symbol for **lossless** encoding of a source with entropy $H(X)$ is at least $H(X)$, and can be made arbitrarily close to $H(X)$.

Compression gain per $N$ symbols:

$$N\log_2|\mathcal{X}| - N\,H(X)$$

---

### Example: Four-Symbol Source

| Symbol | $p_i$ | Naive code | Length | Prefix code | Length |
|--------|--------|-----------|--------|-------------|--------|
| 1 | $\frac{1}{2}$ | 00 | 2 | 0 | 1 |
| 2 | $\frac{1}{4}$ | 01 | 2 | 10 | 2 |
| 3 | $\frac{1}{8}$ | 10 | 2 | 110 | 3 |
| 4 | $\frac{1}{8}$ | 11 | 2 | 111 | 3 |

Entropy:

$$H(X) = -\!\left(\tfrac{1}{2}\log_2\tfrac{1}{2} + \tfrac{1}{4}\log_2\tfrac{1}{4} + 2\times\tfrac{1}{8}\log_2\tfrac{1}{8}\right) = 1.75 \text{ bits}$$

Average code length (prefix code):

$$L = \tfrac{1}{2}(1) + \tfrac{1}{4}(2) + \tfrac{1}{8}(3) + \tfrac{1}{8}(3) = 1.75 \text{ bits}$$

Average code length matches entropy — **optimal compression achieved**.

---

---

## Lecture 15 — Noiseless Coding Examples and the Toffoli Gate

### Eight-Symbol Example

| Symbol | $p_i$ | Codeword | Length $l_i$ |
|--------|--------|----------|-------------|
| $C_1$ | $\frac{1}{2}$ | `0` | 1 |
| $C_2$ | $\frac{1}{4}$ | `10` | 2 |
| $C_3$ | $\frac{1}{8}$ | `110` | 3 |
| $C_4$ | $\frac{1}{16}$ | `1110` | 4 |
| $C_5$ | $\frac{1}{64}$ | `111100` | 6 |
| $C_6$ | $\frac{1}{64}$ | `111101` | 6 |
| $C_7$ | $\frac{1}{64}$ | `111110` | 6 |
| $C_8$ | $\frac{1}{64}$ | `111111` | 6 |

Entropy: $H = 2$ bits. Average code length: $L = 2$ bits. Fixed-length code would need 3 bits → **1 bit per symbol saved**.

---

### Entropy of Common Distributions

**Unbiased six-sided die** ($p_i = \frac{1}{6}$):

$$H = \log_2 6 \approx 2.58 \text{ bits}$$

**Biased die** (e.g. $p_6 = \frac{1}{2}$, three faces at $\frac{1}{10}$):

$$H \approx 2.16 \text{ bits} < 2.58 \text{ bits}$$

Bias **reduces entropy** → more compression is possible.

**Biased coin** with heads probability $p$:

$$H(p) = -p\log_2 p - (1-p)\log_2(1-p)$$

- **Maximum** at $p = 0.5$ → $H = 1$ bit (maximum uncertainty)
- $H$ is **concave** with a single peak at $p=0.5$

---

### The Toffoli Gate — Reversible Classical Computing

Classical gates (AND, OR, XOR) are **irreversible**: outputs do not uniquely determine inputs. Quantum gates must be **unitary** and therefore **reversible**.

The **Toffoli gate** (controlled-controlled-NOT, CCNOT):

- Inputs: $A$, $B$, $C$
- Outputs: $A$, $B$, $C \oplus (A \land B)$

The third bit is flipped **only if both** $A=1$ and $B=1$; otherwise all outputs equal their inputs.

#### Truth Table

| $A$ | $B$ | $C$ | Out $A$ | Out $B$ | Out $C$ |
|-----|-----|-----|---------|---------|---------|
| 0 | 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 | 0 | 1 |
| 0 | 1 | 0 | 0 | 1 | 0 |
| 0 | 1 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 0 | 0 |
| 1 | 0 | 1 | 1 | 0 | 1 |
| 1 | 1 | 0 | 1 | 1 | **1** |
| 1 | 1 | 1 | 1 | 1 | **0** |

Applying the gate **twice** recovers the original inputs → fully reversible.

---

### Key Definitions

| Term | Definition |
|------|------------|
| Shannon's Noiseless Coding Theorem | Minimum average bits per symbol for lossless encoding = $H(X)$ |
| AEP | For large $N$, typical sequences each have probability $\approx 2^{-NH(X)}$ |
| Toffoli Gate | Reversible 3-bit gate: flips $C$ iff $A=B=1$ |
| Reversible Gate | Output uniquely determines input; information is preserved |

---

### Summary Insights

- **Entropy sets the fundamental compression limit** — no lossless scheme can go below $H(X)$ bits per symbol.
- **Variable-length prefix codes exploit probability skew** to approach the entropy bound.
- **Biased distributions allow greater compression** than uniform ones.
- **The Toffoli gate** is the classical bridge toward quantum computation: it is reversible and can simulate any classical Boolean function.
- Lecture 16 begins **quantum information theory**.

---

*Keywords: Density matrix, Liouville–von Neumann equation, Bloch sphere, Shannon entropy, Information content, AEP, Noiseless coding theorem, Data compression, Prefix codes, Toffoli gate, Reversible computation.*
