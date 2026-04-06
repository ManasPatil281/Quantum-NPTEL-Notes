# Quantum Information Theory — Lecture Notes
## Bell State Analyser · Experimental Protocols · Cryptography · RSA · Quantum Fourier Transform

---

## Lecture 31 — Beam Splitters and Bell State Analysis

### Beam Splitter as a Hadamard Gate

A **50/50 beam splitter** with input modes $a$, $b$ and output modes $c$, $d$ obeys:

$$R^2 + T^2 = 1 \qquad \text{(energy conservation)}$$

Reflection introduces a phase shift of $\pi$. The beam splitter acts as a **Hadamard transform** on spatial modes:

$$H|a\rangle = \frac{1}{\sqrt{2}}(|c\rangle + |d\rangle), \qquad H|b\rangle = \frac{1}{\sqrt{2}}(|c\rangle - |d\rangle)$$

Output field relations:

$$E_3^+ = R\,E_1^+ + T\,E_2^+, \qquad E_4^+ = T\,E_1^+ - R\,E_2^+$$

---

### Symmetric and Antisymmetric Two-Photon States

| State | Form |
|-------|------|
| Symmetric spatial | $|\psi^+\rangle = \frac{1}{\sqrt{2}}(|a_1 b_2\rangle + |b_1 a_2\rangle)$ |
| Antisymmetric spatial | $|\psi^-\rangle = \frac{1}{\sqrt{2}}(|a_1 b_2\rangle - |b_1 a_2\rangle)$ |

The antisymmetric state is an **eigenstate of $H\otimes H$**:

$$H\otimes H\left(\frac{|a_1 b_2\rangle - |b_1 a_2\rangle}{\sqrt{2}}\right) = \frac{|c_1 d_2\rangle - |d_1 c_2\rangle}{\sqrt{2}}$$

The antisymmetric character is **preserved** — photons exit at **different** output ports.

---

### Photon Bunching vs Anti-Bunching

Photons are **bosons** → total wavefunction must be symmetric.

| Bell State | Spin Symmetry | Spatial Symmetry | Beam Splitter Behaviour |
|-----------|--------------|-----------------|------------------------|
| $|\Phi^+\rangle$, $|\Phi^-\rangle$, $|\Psi^+\rangle$ | Symmetric | Symmetric | **Bunching** — both photons same port |
| $|\Psi^-\rangle$ (singlet) | Antisymmetric | Antisymmetric | **Anti-bunching** — photons different ports |

> The **singlet $|\Psi^-\rangle$ is uniquely identifiable** by coincidence detection (simultaneous clicks at separate detectors). The other three Bell states bunch — they cannot be distinguished from each other by a simple beam splitter.

---

### Polarising Beam Splitter (PBS)

A PBS separates photons by polarisation (H vs V). For the singlet (antisymmetric spin), the same anti-bunching logic applies in polarisation space: photons exit **different output ports**, enabling direct identification via coincidence detection.

---

### Key Definitions

| Term | Definition |
|------|------------|
| Bunching | Photons exit same output port (symmetric states) |
| Anti-bunching | Photons exit different ports (antisymmetric state) |
| Coincidence detection | Simultaneous clicks at two detectors — identifies singlet |
| PBS | Splits photons by H/V polarisation |

---

---

## Lecture 32 — Experimental Dense Coding and Quantum Teleportation

### Experimental Setup (SPDC)

Entangled photon pairs are generated via **type-II spontaneous parametric down-conversion (SPDC)** in a **BBO crystal**:

$$\omega_p = \omega_1 + \omega_2, \qquad \mathbf{k}_p = \mathbf{k}_1 + \mathbf{k}_2$$

| Component | Role |
|-----------|------|
| Pulsed UV laser (400 nm) | Pump source |
| BBO crystal (type-II) | Generates orthogonally polarised entangled pairs (~800 nm) |
| $\lambda/2$, $\lambda/4$ wave plates | Rotate polarisation / adjust relative phase $\phi$ |
| Compensator crystal | Fine-tunes phase to select Bell state |
| Beam splitters / PBS | Route photons and enable Bell measurement |
| Delay lines | Synchronise photon arrival at beam splitter |
| Coincidence detector | Confirms entangled state / teleportation success |

The two-photon state from SPDC:

$$|\psi\rangle = \frac{1}{\sqrt{2}}\!\left(|H\rangle_1|V\rangle_2 + e^{i\phi}|V\rangle_1|H\rangle_2\right)$$

Phase $\phi$ is controlled by the compensator crystal; all four Bell states are accessible via wave plates.

---

### Dense Coding (Experimental)

Alice's operations on her qubit of a shared $|\beta_{00}\rangle$ pair:

| Bits | Alice's Operation | Bell State | Detection |
|------|-------------------|-----------|-----------|
| 00 | $I$ | $|\Phi^+\rangle$ | Bunching |
| 01 | $\sigma_z$ | $|\Phi^-\rangle$ | Bunching |
| 10 | $\sigma_x$ | $|\Psi^+\rangle$ | Bunching |
| 11 | $i\sigma_y$ | $|\Psi^-\rangle$ | **Anti-bunching / coincidence** |

Bell measurement: CNOT + Hadamard → computational basis measurement.

---

### Quantum Teleportation (Experimental)

Requires two entangled pairs: photons (1,4) and (2,3).

| Step | Action |
|------|--------|
| 1 | Alice holds unknown qubit (1) and one half of pair (2); Bob holds (3); auxiliary (4) |
| 2 | Alice performs Bell measurement on (1,2) |
| 3 | Alice sends 2-bit result classically to Bob |
| 4 | Bob applies $I$, $\sigma_x$, $\sigma_z$, or $i\sigma_y$ on (3) to recover $|\psi\rangle$ |

Experimentally verified by **three- or four-fold coincidence counting**. Varying the delay line (path length) confirms that zero delay maximises teleportation fidelity — photons must arrive **simultaneously** at the beam splitter.

---

---

## Lecture 33 — Classical Cryptography and RSA Introduction

### Context: Quantum Algorithms Ahead

| Algorithm | Quantum Resource Used |
|-----------|----------------------|
| Deutsch's algorithm | Superposition (quantum parallelism) |
| Grover's search | Superposition |
| Shor's factoring | Superposition + entanglement + QFT |

---

### The Factorisation Problem

Find primes $p$, $q$ such that $n = p \times q$. Example: $15 = 3 \times 5$.

RSA security rests on the **computational hardness** of factorising large $n$.

---

### Classical Period-Finding Algorithm

| Step | Action |
|------|--------|
| 1 | Choose $a < n$ |
| 2 | Compute $a^x \bmod n$ for $x = 0, 1, 2, \ldots$ |
| 3 | Find period $f$: smallest integer with $a^f \equiv 1 \pmod{n}$ |
| 4 | If $f$ is odd, choose different $a$ and repeat |
| 5 | Compute $\gcd(a^{f/2}-1,\, n)$ and $\gcd(a^{f/2}+1,\, n)$ |

#### Example: $n = 15$, $a = 2$

| $x$ | $2^x$ | $2^x \bmod 15$ |
|-----|-------|----------------|
| 0 | 1 | 1 |
| 1 | 2 | 2 |
| 2 | 4 | 4 |
| 3 | 8 | 8 |
| 4 | 16 | **1** (period $f=4$) |

Period $f = 4$ (even). Factors:

$$\gcd(2^2-1,\,15) = \gcd(3,15) = 3$$
$$\gcd(2^2+1,\,15) = \gcd(5,15) = 5$$

---

### RSA Protocol

Developed 1977 (Rivest, Shamir, Adleman).

| Step | Actor | Action |
|------|-------|--------|
| 1 | Bob | Choose primes $p$, $q$; compute $N = p \times q$ (public) |
| 2 | Bob | Compute totient $M = (p-1)(q-1)$ |
| 3 | Bob | Choose $c$ with $\gcd(c, M) = 1$; compute $d \equiv c^{-1} \pmod{M}$ |
| 4 | Bob | Publish public key $(N, c)$; keep private key $(N, d)$ |
| 5 | Alice | Encrypt: $e = m^c \bmod N$; send $e$ |
| 6 | Bob | Decrypt: $m = e^d \bmod N$ |

---

### Classical vs Quantum Factorisation Time

| Number Size | Classical (100 workstations) | Quantum Computer |
|------------|------------------------------|-----------------|
| 130-digit | ~1 month | ~1 month |
| 400-digit | ~10 billion years | ~3 years |

> Quantum algorithms **exponentially accelerate** factorisation, threatening RSA.

---

---

## Lecture 34 — RSA Numerical Example and Quantum Factorisation Setup

### RSA Numerical Example

| Parameter | Value | Explanation |
|-----------|-------|-------------|
| $p$ | 3 | Prime |
| $q$ | 7 | Prime |
| $N$ | 21 | Public modulus |
| $M$ | 12 | Totient $(2\times 6)$ |
| $c$ | 5 | Encryption exponent (coprime to 12) |
| $d$ | 5 | Decryption exponent ($5\times 5=25\equiv 1\pmod{12}$) |
| $m$ | 4 | Plaintext |
| $e$ | 16 | Ciphertext ($4^5\bmod 21 = 1024\bmod 21$) |

**Verification:** $16^5 \bmod 21 = 4$ ✓

An eavesdropper who factors $N=21$ into $p=3$, $q=7$ can compute $M$ and $d$, breaking the encryption.

---

### Quantum RSA: Period Finding with Registers

Two quantum registers $A$ and $B$:

$$|x\rangle|0\rangle \xrightarrow{\text{oracle}} |x\rangle|a^x\bmod N\rangle$$

#### Example: $N=15$, $a=7$

| $x$ | $7^x\bmod 15$ |
|-----|---------------|
| 1 | 7 |
| 2 | 4 |
| 3 | 13 |
| 4 | **1** (period $f=4$) |
| 5 | 7 |
| $\vdots$ | $\vdots$ |

$$\gcd(7^2-1,\,15) = \gcd(48,15) = 3, \qquad \gcd(7^2+1,\,15) = \gcd(50,15) = 5$$

**Register size:** must satisfy $2^c \geq N$ (e.g. 4 bits for $N=15$).

---

### Quantum Oracle

The oracle entangles the two registers:

$$\frac{1}{\sqrt{2^c}}\sum_{x=0}^{2^c-1}|x\rangle|0\rangle \xrightarrow{\text{oracle}} \frac{1}{\sqrt{2^c}}\sum_{x=0}^{2^c-1}|x\rangle|a^x\bmod N\rangle$$

After **measuring register $B$** (e.g. outcome $= 7$), register $A$ collapses to a superposition of all $x$ consistent with that outcome — spaced by period $f$. The QFT then extracts $f$.

---

---

## Lecture 35 — Quantum Fourier Transform (QFT)

### Classical Discrete Fourier Transform (DFT)

For a dataset $\{x_j\}_{j=0}^{n-1}$:

$$y_k = \frac{1}{n}\sum_{j=0}^{n-1} x_j\,e^{2\pi i\frac{jk}{n}}, \qquad k = 0,1,\ldots,n-1$$

Example ($n=2$, $x_0=x_1=2$): $y_0 = 2$, $y_1 = 0$.

---

### Quantum Fourier Transform

The QFT is a **unitary, linear** operator — a change of basis from the computational basis to the Fourier basis.

For a state $|\psi\rangle = \sum_{j=0}^{N-1} c_j|j\rangle$:

$$\mathrm{QFT}|\psi\rangle = \sum_{k=0}^{N-1}\tilde{c}_k|k\rangle$$

where $\tilde{c}_k = \frac{1}{\sqrt{N}}\sum_{j=0}^{N-1} c_j\,e^{2\pi i\frac{jk}{N}}$.

Action on a basis state:

$$\boxed{\mathrm{QFT}|j\rangle = \frac{1}{\sqrt{N}}\sum_{k=0}^{N-1} e^{2\pi i\frac{jk}{N}}|k\rangle}$$

---

### Role in Shor's Algorithm

After measuring register $B$, register $A$ holds a **periodic superposition** with spacing $f$. The QFT converts this periodicity into a **frequency peak** — measuring register $A$ after QFT reveals $f$.

---

### DFT vs QFT Comparison

| Aspect | Classical DFT | Quantum QFT |
|--------|--------------|-------------|
| Input | Discrete data $x_j$ | Quantum state amplitudes $c_j$ |
| Output | Complex coefficients $y_k$ | Quantum state in Fourier basis |
| Linearity | Yes | Yes (unitary) |
| Norm preservation | No | Yes ($\mathrm{QFT}^\dagger\mathrm{QFT} = I$) |
| Mathematical form | $y_k = \frac{1}{n}\sum x_j e^{2\pi i jk/n}$ | $\mathrm{QFT}|j\rangle = \frac{1}{\sqrt{N}}\sum_k e^{2\pi i jk/N}|k\rangle$ |
| Application | Signal processing | Period finding, Shor's algorithm |

---

### Shor's Algorithm: Full Flow

```
1. Initialise: register A in uniform superposition, register B = |0⟩
2. Oracle: entangle A and B via |x⟩|0⟩ → |x⟩|aˣ mod N⟩
3. Measure B: collapses A to periodic superposition (period f)
4. Apply QFT to A: converts period → frequency peak
5. Measure A: extract f
6. Compute gcd(a^(f/2) ± 1, N) → prime factors
```

---

### Key Takeaways

- **RSA security** rests on the classical hardness of factorisation; quantum algorithms threaten it.
- The **quantum oracle** encodes modular exponentiation into entangled registers.
- **QFT is the heart of Shor's algorithm** — it efficiently extracts periodicity from a quantum superposition.
- QFT is unitary, norm-preserving, and operates as a change of basis — directly analogous to the classical DFT but acting on quantum amplitudes.
- The **no-cloning theorem** motivates quantum cryptography as an alternative to RSA.

---

*Keywords: Bell state analyser, Beam splitter, Bunching, Anti-bunching, SPDC, BBO crystal, Dense coding, Quantum teleportation, Coincidence detection, RSA encryption, Modular arithmetic, GCD, Period finding, Quantum oracle, Quantum Fourier Transform, Shor's algorithm.*
