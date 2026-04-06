# Quantum Information Theory — Lecture Notes
## Shor's Algorithm: Full Derivation, QFT Circuit, and Worked Example

---

## Lecture 41 — QFT Circuit: Binary Fractions and Phase Accumulation

### Binary Fractional Notation

For an $n$-qubit register, the integer $x$ is written as:

$$x = \sum_{l=1}^n x_l\,2^{n-l}$$

The **binary fraction** notation used in phase calculations:

$$0.x_l x_{l+1}\cdots x_m = \frac{x_l}{2} + \frac{x_{l+1}}{2^2} + \cdots + \frac{x_m}{2^{m-l+1}}$$

This allows the QFT phase $e^{2\pi i x/2^k}$ to be written as a product over bits:

$$e^{2\pi i x/2^k} = \prod_{l=1}^n e^{2\pi i x_l 2^{n-l-k}}$$

When $n-l-k \geq 0$, the exponent is a multiple of $2\pi i$ and contributes factor $1$. Only the **fractional bits** (where $n-l-k < 0$) produce non-trivial phases — these are what the controlled rotation gates implement.

---

### QFT Gate Sequence

For input $|x_1 x_2\cdots x_n\rangle$, the circuit processes each qubit $x_k$ as:

1. **Hadamard** on $x_k$:
$$|x_k\rangle \to \frac{|0\rangle + e^{2\pi i\cdot 0.x_k}|1\rangle}{\sqrt{2}}$$

2. **Controlled $R_2$** (ctrl: $x_{k+1}$): adds phase $e^{2\pi i x_{k+1}/4}$
3. **Controlled $R_3$** (ctrl: $x_{k+2}$): adds phase $e^{2\pi i x_{k+2}/8}$
4. $\vdots$ continue through $R_{n-k+1}$ (ctrl: $x_n$)

After all gates on qubit $k$, its state carries phase $e^{2\pi i\cdot 0.x_k x_{k+1}\cdots x_n}$:

$$\frac{|0\rangle + e^{2\pi i\cdot 0.x_k x_{k+1}\cdots x_n}|1\rangle}{\sqrt{2}}$$

The rotation gate matrix:

$$R_m = \begin{pmatrix}1 & 0\\0 & e^{2\pi i/2^m}\end{pmatrix}$$

---

### Gate Summary

| Gate | Role | Matrix |
|------|------|--------|
| $H$ | Creates superposition on qubit $k$ | $\frac{1}{\sqrt{2}}\begin{pmatrix}1&1\\1&-1\end{pmatrix}$ |
| $C\text{-}R_k$ | Adds conditional phase $e^{2\pi i/2^k}$ | $\mathrm{diag}(1,1,1,e^{2\pi i/2^k})$ |
| SWAP | Reverses qubit order at output | Exchanges $|x_j\rangle \leftrightarrow |x_{n-j+1}\rangle$ |

---

---

## Lecture 42 — Shor's Algorithm: Setup and Oracle

### Problem Statement

**Goal:** Find prime factors $p$, $q$ of integer $N = p \times q$.

**Method:** Reduce factorisation to **period finding** of $f(x) = a^x \bmod N$, where $a$ is chosen coprime to $N$. The period $r$ satisfies $a^r \equiv 1 \pmod{N}$; then $\gcd(a^{r/2}\pm 1, N)$ gives the factors.

---

### Register Sizing

| Register | Label | Qubits | Size requirement |
|---------|-------|--------|-----------------|
| A (input) | $C$ qubits | $2^C > N$ | Typically $C = 2\lceil\log_2 N\rceil$ |
| B (output) | $L$ qubits | Stores $a^x\bmod N$ | $L = \lceil\log_2 N\rceil$ |

---

### Algorithm Steps 1–4

#### Step 1 — Initialise

$$|\psi_0\rangle = |0\rangle_A^{\otimes C} \otimes |0\rangle_B^{\otimes L}$$

#### Step 2 — Apply QFT to Register A

$$|\psi_1\rangle = \frac{1}{\sqrt{2^C}}\sum_{x=0}^{2^C-1}|x\rangle_A \otimes |0\rangle_B$$

QFT on $|0\rangle^{\otimes C}$ produces an **equal superposition** of all $2^C$ basis states.

#### Step 3 — Modular Exponentiation Oracle

The oracle entangles registers A and B:

$$|x\rangle_A|0\rangle_B \xrightarrow{\text{oracle}} |x\rangle_A|a^x\bmod N\rangle_B$$

$$\boxed{|\psi_2\rangle = \frac{1}{\sqrt{2^C}}\sum_{x=0}^{2^C-1}|x\rangle_A \otimes |a^x\bmod N\rangle_B}$$

#### Step 4 — Measure Register B

The function $f(x) = a^x\bmod N$ is **periodic with period $r$**: $f(x) = f(x+r)$.

Measuring B and obtaining value $y$ collapses A to a superposition of all $x$ consistent with $f(x) = y$, spaced by $r$:

$$|\psi_3\rangle = \frac{1}{\sqrt{m}}\sum_{j=0}^{m-1}|x_0 + jr\rangle_A \otimes |y\rangle_B$$

where $x_0$ is the smallest $x$ with $f(x_0) = y$ and $m = 2^C/r$.

Register B is now irrelevant; all information is in A.

---

### State Summary Table

| State | Expression | Description |
|-------|-----------|-------------|
| $|\psi_0\rangle$ | $|0\rangle_A|0\rangle_B$ | Initial state |
| $|\psi_1\rangle$ | $\frac{1}{\sqrt{2^C}}\sum_x|x\rangle_A|0\rangle_B$ | After QFT on A |
| $|\psi_2\rangle$ | $\frac{1}{\sqrt{2^C}}\sum_x|x\rangle_A|a^x\bmod N\rangle_B$ | After oracle (entangled) |
| $|\psi_3\rangle$ | $\frac{1}{\sqrt{m}}\sum_j|x_0+jr\rangle_A|y\rangle_B$ | After measuring B |
| $|\psi_4\rangle$ | QFT of $|\psi_3\rangle$ | Reveals period (next step) |

---

---

## Lecture 43 — Period Extraction via QFT and Interference

### Applying QFT to $|\psi_3\rangle$

$$|\psi_4\rangle = \mathrm{QFT}|\psi_3\rangle = \frac{1}{\sqrt{m\cdot 2^C}}\sum_{n=0}^{2^C-1}\left(\sum_{j=0}^{m-1}e^{2\pi i\frac{rn}{2^C}j}\right)e^{2\pi i\frac{x_0 n}{2^C}}|n\rangle$$

---

### Measurement Probability

The probability of observing $|n\rangle$ after QFT:

$$P(n) = \frac{1}{m\cdot 2^C}\left|\sum_{j=0}^{m-1}\left(e^{2\pi i\frac{rn}{2^C}}\right)^j\right|^2$$

Let $z_a = e^{2\pi i rn/2^C}$. This is a **geometric sum**:

- If $\frac{rn}{2^C} \approx l \in \mathbb{Z}$: $z_a \approx 1$ → sum $\approx m$ → $P(n) \approx \frac{m}{2^C} = \frac{1}{r}$ (**constructive interference**)
- If $\frac{rn}{2^C}$ far from integer: terms cancel → $P(n) \approx 0$ (**destructive interference**)

> **Key result:** Measurement outcomes cluster around values $n$ where $\frac{n}{2^C} \approx \frac{l}{r}$ for integer $l$.

---

### Extracting $r$: Continued Fractions

Since $n$ and $2^C$ are known after measurement:

$$\frac{n}{2^C} \approx \frac{l}{r}$$

Apply the **continued fraction algorithm** to $n/2^C$ to find rational approximants $\frac{L}{R_1}$ with $R_1 < N$:

$$R = a_0 + \cfrac{1}{a_1 + \cfrac{1}{a_2 + \cfrac{1}{\ddots + \cfrac{1}{a_N}}}}$$

**Example:** $R = \frac{15}{4} = 3 + \frac{1}{1 + \frac{1}{3}}$ → continued fraction $(3,\, 1,\, 3)$.

The denominator of a convergent gives a **candidate period** $R_1$. The true period may be $r = p \times R_1$ for small integer $p$.

---

---

## Lecture 44 — Classical Post-Processing and Factor Verification

### Full Post-Processing Pipeline

| Step | Action | Formula |
|------|--------|---------|
| 1 | Measure register A after QFT → get $n$ | — |
| 2 | Compute $n/2^C$ | Measured phase |
| 3 | Continued fraction expansion of $n/2^C$ | Find convergents $L/R_1$ |
| 4 | Test multiples: $r = p\cdot R_1$ for $p = 1, 2, \ldots$ | Check $a^r\bmod N = 1$ |
| 5 | Compute $P = \gcd(a^{r/2}-1,\,N)$ | Factor candidate |
| 6 | Compute $Q = \gcd(a^{r/2}+1,\,N)$ | Factor candidate |
| 7 | Verify $N = P\times Q$ | Confirm factorisation |

---

### Probability Summary

When $z_a \approx 1$:

$$P_n \approx \frac{m^2}{2^C m} = \frac{m}{2^C} = \frac{1}{r}$$

There are $r$ values of $l$ in $[0, r-1]$, each contributing probability $\sim 1/r$, so the total success probability is $O(1)$ — the algorithm succeeds with constant probability per run.

---

---

## Lecture 45 — Worked Example: Factoring $N = 15$ with $a = 7$

### Parameters

| Parameter | Value | Reason |
|-----------|-------|--------|
| $N$ | 15 | Number to factor |
| $a$ | 7 | Coprime to 15 |
| $L$ | 4 | $2^4 = 16 \approx N$ |
| $C$ | 8 | $C = 2L = 2\times 4$, ensures accuracy |
| $2^C$ | 256 | Size of register A state space |

---

### Step-by-Step Execution

#### Steps 1–2: Initialise and Create Superposition

$$|\psi_1\rangle = \frac{1}{\sqrt{256}}\sum_{x=0}^{255}|x\rangle_A|0\rangle_B$$

#### Step 3: Oracle — Modular Exponentiation

$$|\psi_2\rangle = \frac{1}{\sqrt{256}}\sum_{x=0}^{255}|x\rangle_A|7^x\bmod 15\rangle_B$$

$7^x\bmod 15$ has period $r = 4$:

| $x$ | $7^x\bmod 15$ |
|-----|---------------|
| 0 | 1 |
| 1 | 7 |
| 2 | 4 |
| 3 | 13 |
| 4 | **1** (repeats) |

#### Step 4: Measure Register B

Say outcome $= 7$. Register A collapses to $\{x : 7^x\bmod 15 = 7\} = \{1, 5, 9, \ldots\}$:

$$|\psi_3\rangle = \frac{1}{\sqrt{64}}\sum_{j=0}^{63}|1+4j\rangle_A$$

#### Step 5: QFT on Register A → Measure

Example outcome: $n = 127$.

Phase: $\frac{127}{256} \approx \frac{1}{2}$. Continued fraction: $\frac{127}{256} \approx \frac{1}{2}$ → $r = 2$ or try $r=4$.

Another likely outcome: $n = 64$. Phase: $\frac{64}{256} = \frac{1}{4}$ → $r = 4$ directly.

---

### Verification

With $r = 4$:

$$7^4\bmod 15 = 2401\bmod 15 = 1 \quad \checkmark$$

$$P = \gcd(7^2 - 1,\, 15) = \gcd(48,\, 15) = 3$$

$$Q = \gcd(7^2 + 1,\, 15) = \gcd(50,\, 15) = 5$$

$$N = P \times Q = 3 \times 5 = 15 \quad \checkmark$$

---

### Probability of Success

For $n = 127$: $P_{127} \approx 2.5\%$ per shot. Since there are $r = 4$ equally likely "peaks" ($n \approx 0, 64, 128, 192$), total success probability per run is $\sim r \times \frac{1}{r} = O(1)$.

---

### Complete Shor's Algorithm Summary

```
INPUT: N (integer to factor), a (coprime to N)

QUANTUM STEPS:
  1. Initialise: |0⟩_A ⊗ |0⟩_B
  2. QFT on A: equal superposition over 2^C states
  3. Oracle: |x⟩|0⟩ → |x⟩|aˣ mod N⟩
  4. Measure B: A collapses to periodic superposition (period r)
  5. QFT on A: interference peaks at n ≈ l·2^C/r

CLASSICAL STEPS:
  6. Compute n/2^C
  7. Continued fraction → candidate R₁
  8. Test r = p·R₁ until aʳ ≡ 1 (mod N)
  9. P = gcd(a^(r/2)−1, N),  Q = gcd(a^(r/2)+1, N)
  10. Verify N = P × Q

OUTPUT: prime factors P and Q
```

---

### Key Insights

- **Quantum parallelism** evaluates $a^x\bmod N$ for all $x$ simultaneously via superposition.
- **Entanglement** links register A (input) to register B (output), encoding periodicity.
- **QFT converts periodicity to frequency peaks** — measurement collapses to one peak probabilistically.
- **Continued fractions** bridge the quantum measurement and classical period extraction.
- **Exponential speedup**: classical best algorithms take $O(e^{n^{1/3}})$; Shor's runs in $O(n^3)$ on a quantum computer where $n = \log_2 N$.

---

*Keywords: Shor's algorithm, QFT circuit, Modular exponentiation, Oracle, Period finding, Quantum registers, Interference, Continued fractions, GCD, Factorisation, Binary fraction notation, Controlled rotation gates, Swap gates, Quantum parallelism.*
