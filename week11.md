# Quantum Information Theory — Lecture Notes
## Quantum Noise Channels · Lindblad Master Equation · Spontaneous Emission

---

## Lecture 51 — Depolarising Channel and Bit Flip Channel

### Depolarising Channel (Recap)

**Kraus operators:**

$$E_0 = \sqrt{1-\tfrac{3p}{4}}\,I, \quad E_1 = \sqrt{\tfrac{p}{4}}\,\sigma_x, \quad E_2 = \sqrt{\tfrac{p}{4}}\,\sigma_y, \quad E_3 = \sqrt{\tfrac{p}{4}}\,\sigma_z$$

**Superoperator action:**

$$\mathcal{E}(\rho) = \left(1-p\right)\rho + \frac{p}{2}I$$

**Bloch sphere:** uniform contraction by factor $(1-p)$ — $\vec{r}' = (1-p)\vec{r}$.

---

### Bit Flip Channel

**Physical model:** qubit flips $|0\rangle\leftrightarrow|1\rangle$ with probability $p$.

**Kraus operators:**

$$E_0 = \sqrt{1-p}\,I, \qquad E_1 = \sqrt{p}\,\sigma_x$$

**Superoperator:**

$$\mathcal{E}(\rho) = (1-p)\rho + p\,\sigma_x\rho\,\sigma_x$$

**Quantum circuit model:** inverted CNOT with environment in mixed state $\rho_E = (1-p)|0\rangle\langle 0| + p|1\rangle\langle 1|$, and system-environment unitary:

$$U = I\otimes|0\rangle\langle 0| + \sigma_x\otimes|1\rangle\langle 1|$$

**Bloch sphere:** $x$-component unchanged; $y$ and $z$ components shrink by factor $(1-2p)$.

---

### Channel Comparison

| Channel | Kraus Operators | Superoperator | Bloch Sphere Effect |
|---------|----------------|---------------|---------------------|
| Depolarising | $\sqrt{1-3p/4}\,I;\;\sqrt{p/4}\,\sigma_{x,y,z}$ | $(1-p)\rho + \frac{p}{2}I$ | Uniform shrinkage by $(1-p)$ |
| Bit Flip | $\sqrt{1-p}\,I;\;\sqrt{p}\,\sigma_x$ | $(1-p)\rho + p\,\sigma_x\rho\,\sigma_x$ | $y,z$ shrink by $(1-2p)$; $x$ unchanged |

---

---

## Lecture 52 — Bit Flip and Phase Flip Channels

### Bloch Vector Parametrisation

$$\rho_S = \frac{1}{2}\!\left(I + c_x\sigma_x + c_y\sigma_y + c_z\sigma_z\right), \qquad c_i = \mathrm{Tr}(\rho\,\sigma_i)$$

---

### Bit Flip Channel: Bloch Sphere Derivation

After applying $\mathcal{E}(\rho) = (1-p)\rho + p\,\sigma_x\rho\,\sigma_x$, using $\sigma_x\sigma_x = I$, $\sigma_x\sigma_y\sigma_x = -\sigma_y$, $\sigma_x\sigma_z\sigma_x = -\sigma_z$:

$$\mathcal{E}(\rho) = \frac{1}{2}\!\left[I + c_x\sigma_x + (1-2p)c_y\sigma_y + (1-2p)c_z\sigma_z\right]$$

| Component | After Channel |
|-----------|--------------|
| $c_x$ | $c_x$ (unchanged) |
| $c_y$ | $(1-2p)\,c_y$ |
| $c_z$ | $(1-2p)\,c_z$ |

**Bloch sphere:** compressed along $y$ and $z$; oblate deformation with $x$-axis intact.

---

### Phase Flip Channel

**Physical model:** phase of $|1\rangle$ flips ($|1\rangle\to-|1\rangle$) with probability $p$.

**Kraus operators:**

$$E_0 = \sqrt{1-p}\,I, \qquad E_1 = \sqrt{p}\,\sigma_z$$

**Superoperator:**

$$\mathcal{E}(\rho) = (1-p)\rho + p\,\sigma_z\rho\,\sigma_z$$

**Bloch sphere derivation:** using $\sigma_z\sigma_x\sigma_z = -\sigma_x$, $\sigma_z\sigma_y\sigma_z = -\sigma_y$, $\sigma_z\sigma_z\sigma_z = \sigma_z$:

$$\mathcal{E}(\rho) = \frac{1}{2}\!\left[I + (1-2p)c_x\sigma_x + (1-2p)c_y\sigma_y + c_z\sigma_z\right]$$

| Component | After Channel |
|-----------|--------------|
| $c_x$ | $(1-2p)\,c_x$ |
| $c_y$ | $(1-2p)\,c_y$ |
| $c_z$ | $c_z$ (unchanged) |

**Bloch sphere:** compressed along $x$ and $y$; $z$-axis (population) unchanged. Corresponds to **$T_2$ relaxation** (spin-spin, dephasing) in NMR.

---

---

## Lecture 53 — Phase Damping and Amplitude Damping Channels

### Phase Damping Channel

**Physical effect:** loss of phase coherence (dephasing) without energy exchange.

$$\mathcal{E}(\rho) = \frac{1}{2}\!\left(1+c_z\sigma_z\right) + \frac{1}{2}(1-2p)(c_x\sigma_x + c_y\sigma_y)$$

Off-diagonal elements of $\rho$ decay; populations (diagonal) preserved.

**Physical analogue:** **$T_2$ (spin-spin) relaxation** — spins precess around $z$ under a magnetic field and dephase. Some spins acquire phase shift $\pi$, reducing net transverse magnetisation.

---

### Amplitude Damping Channel

**Physical effect:** energy dissipation — excited state $|1\rangle$ decays to ground state $|0\rangle$ with probability $p$.

**Kraus operators:**

$$E_0 = \begin{pmatrix}1 & 0\\0 & \sqrt{1-p}\end{pmatrix}, \qquad E_1 = \begin{pmatrix}0 & \sqrt{p}\\0 & 0\end{pmatrix}$$

Completeness: $E_0^\dagger E_0 + E_1^\dagger E_1 = I$ ✓

**Effect on Bloch vector:**

$$c_x' = \sqrt{1-p}\,c_x, \quad c_y' = \sqrt{1-p}\,c_y, \quad c_z' = p + (1-p)\,c_z$$

**Bloch sphere:** shrinks non-uniformly and shifts centre toward north pole ($|0\rangle$).

**Physical analogue:** **$T_1$ (spin-lattice) relaxation** — energy exchange with lattice; analogous to spontaneous emission.

---

### All Channels: Bloch Sphere Summary

| Channel | $c_x'$ | $c_y'$ | $c_z'$ | Physical Process | NMR Notation |
|---------|--------|--------|--------|-----------------|-------------|
| Depolarising | $(1-p)c_x$ | $(1-p)c_y$ | $(1-p)c_z$ | Symmetric noise | — |
| Bit flip | $c_x$ | $(1-2p)c_y$ | $(1-2p)c_z$ | $x$-flip error | — |
| Phase flip | $(1-2p)c_x$ | $(1-2p)c_y$ | $c_z$ | Phase error | $T_2$ |
| Phase damping | $(1-2p)c_x$ | $(1-2p)c_y$ | $c_z$ | Dephasing | $T_2$ |
| Amplitude damping | $\sqrt{1-p}\,c_x$ | $\sqrt{1-p}\,c_y$ | $p+(1-p)c_z$ | Energy decay $|1\rangle\to|0\rangle$ | $T_1$ |

---

---

## Lecture 54 — Derivation of the Lindblad Master Equation

### Setup and Approximations

**Total Hamiltonian:**

$$H = H_S + H_E + H_{SE}$$

**Markov approximation:** evolution is memoryless — system's future depends only on current state; no information backflow from environment.

**Born approximation:** bath is large and unaffected; no feedback from bath to system.

---

### From Kraus Operators to Master Equation

For infinitesimal time step $\Delta t$, expand Kraus operators:

$$E_0 = I + \left(-\frac{i}{\hbar}H + K\right)\Delta t, \qquad E_k = L_k\sqrt{\Delta t} \quad (k=1,\ldots,m-1)$$

where $H$, $K$ are Hermitian and $L_k$ are **Lindblad operators**.

**Normalization** $\sum_k E_k^\dagger E_k = I$ requires:

$$K = -\frac{1}{2}\sum_k L_k^\dagger L_k$$

---

### Lindblad Master Equation

Substituting into the OSR $\rho_S(t+\Delta t) = \sum_k E_k\rho_S(t)E_k^\dagger$ and taking $\Delta t\to 0$:

$$\boxed{\frac{d\rho_S}{dt} = -\frac{i}{\hbar}[H,\rho_S] + \sum_k\!\left(L_k\rho_S L_k^\dagger - \frac{1}{2}\{L_k^\dagger L_k,\,\rho_S\}\right)}$$

where $\{A,B\} = AB + BA$ is the anticommutator.

---

### Interpretation of Each Term

| Term | Expression | Role |
|------|-----------|------|
| Unitary (Schrödinger) | $-\frac{i}{\hbar}[H,\rho_S]$ | Coherent evolution under system Hamiltonian |
| Quantum jump | $\sum_k L_k\rho_S L_k^\dagger$ | Transitions/dissipation induced by environment |
| Normalization | $-\frac{1}{2}\sum_k\{L_k^\dagger L_k,\rho_S\}$ | Ensures $\mathrm{Tr}(\rho_S) = 1$ when no jump occurs |

> The Lindblad master equation is the most general **Markovian, time-homogeneous** quantum master equation consistent with CPTP evolution.

---

### Key Equations Reference

| Description | Formula |
|-------------|---------|
| System evolution | $\rho_S(t) = \mathrm{Tr}_E[U(t)\rho(0)U^\dagger(t)]$ |
| Kraus at $\Delta t$ | $E_0 = I+(-\frac{i}{\hbar}H+K)\Delta t$; $E_k = L_k\sqrt{\Delta t}$ |
| $K$ from normalization | $K = -\frac{1}{2}\sum_k L_k^\dagger L_k$ |
| Lindblad equation | $\dot{\rho}_S = -\frac{i}{\hbar}[H,\rho_S] + \sum_k(L_k\rho_S L_k^\dagger - \frac{1}{2}\{L_k^\dagger L_k,\rho_S\})$ |

---

---

## Lecture 55 — Spontaneous Emission via the Lindblad Equation

### Model Setup

**System:** Two-level atom/spin-$\frac{1}{2}$ with Hamiltonian:

$$H = -\frac{\hbar\omega}{2}\sigma_z$$

**Single Lindblad operator** (amplitude damping / spontaneous emission):

$$L = \sqrt{\gamma}\begin{pmatrix}0&1\\0&0\end{pmatrix}, \qquad L^\dagger = \sqrt{\gamma}\begin{pmatrix}0&0\\1&0\end{pmatrix}$$

$$L^\dagger L = \gamma\begin{pmatrix}0&0\\0&1\end{pmatrix}, \qquad LL^\dagger = \gamma\begin{pmatrix}1&0\\0&0\end{pmatrix}$$

---

### Equations of Motion for Density Matrix Elements

Substituting into the Lindblad equation gives:

| Element | Equation | Solution |
|---------|----------|---------|
| $\dot{\rho}_{11}$ | $-\gamma\rho_{11}$ | $\rho_{11}(t) = \rho_{11}(0)\,e^{-\gamma t}$ |
| $\dot{\rho}_{00}$ | $+\gamma\rho_{11}$ | $\rho_{00}(t) = \rho_{00}(0) + \rho_{11}(0)(1-e^{-\gamma t})$ |
| $\dot{\rho}_{01}$ | $(i\omega - \frac{\gamma}{2})\rho_{01}$ | $\rho_{01}(t) = \rho_{01}(0)\,e^{(i\omega-\gamma/2)t}$ |
| $\dot{\rho}_{10}$ | $(-i\omega - \frac{\gamma}{2})\rho_{10}$ | $\rho_{10}(t) = \rho_{10}(0)\,e^{(-i\omega-\gamma/2)t}$ |

Trace conservation: $\rho_{00}(t)+\rho_{11}(t) = 1$ ✓

---

### Relaxation Times

$$\boxed{T_1 = \frac{1}{\gamma}} \qquad \text{(population / amplitude decay)}$$

$$\boxed{T_2 = \frac{2}{\gamma} = 2T_1} \qquad \text{(coherence / phase decay)}$$

Coherence decays **twice as slowly** as population — the off-diagonal decay rate is $\gamma/2$.

---

### Bloch Sphere Picture

- $\rho_{11}(t)\to 0$ as $t\to\infty$: Bloch vector relaxes from **north pole** ($|1\rangle$) to **south pole** ($|0\rangle$)
- Off-diagonal elements oscillate at frequency $\omega$ and decay with rate $\gamma/2$
- The system is fully characterised by two timescales: $T_1$ (amplitude) and $T_2 = 2T_1$ (phase)

---

### Key Takeaways

- **Lindblad equation unifies Hamiltonian and dissipative dynamics** in a single compact master equation.
- The **quantum jump operator $L$** captures the spontaneous emission mechanism.
- **Population and coherence decay at different rates** ($\gamma$ vs $\gamma/2$), a direct prediction of the formalism.
- For spontaneous emission (pure amplitude damping): $T_2 = 2T_1$ — this is an exact result, experimentally verifiable.
- The formalism applies to any open quantum system satisfying Born–Markov approximations: atoms, spins, quantum dots, superconducting qubits.

---

*Keywords: Depolarising channel, Bit flip channel, Phase flip channel, Phase damping, Amplitude damping, Kraus operators, Bloch sphere, $T_1$ relaxation, $T_2$ relaxation, NMR, Lindblad master equation, Lindblad operators, Quantum jump, Born approximation, Markov approximation, Spontaneous emission, Open quantum systems, Superoperator.*
