# Quantum Information & Open Systems — Lecture Summaries (56–60)

---

## Lecture 56: Lindblad Equation in NMR/ESR & Generalized Measurement

### Part 1: Lindblad Equation in NMR/ESR

- Hamiltonian:
  $$
  H = -\frac{\omega}{2} \sigma_z
  $$

- Lindblad operators:

  | Operator | Description | Form |
  |----------|------------|------|
  | $L_+$ | Emission | $\gamma_+ \begin{pmatrix}0 & 1 \\ 0 & 0\end{pmatrix}$ |
  | $L_-$ | Absorption | $\gamma_- \begin{pmatrix}0 & 0 \\ 1 & 0\end{pmatrix}$ |
  | $L_z$ | Dephasing | $\gamma_z \sigma_z$ |

- Master equation:
  $$
  \frac{d\rho}{dt} = -i[H,\rho] + \sum_k \left(L_k \rho L_k^\dagger - \frac{1}{2}\{L_k^\dagger L_k,\rho\}\right)
  $$

- Relaxation times:
  $$
  \frac{1}{T_1} = \gamma_+ + \gamma_-
  \quad , \quad
  \frac{1}{T_2} = \frac{\gamma_+ + \gamma_-}{2} + 2\gamma_z
  $$

- Thermal relation:
  $$
  \frac{\rho_{11}}{\rho_{00}} = \frac{\gamma_-}{\gamma_+} = e^{-\omega / k_B T}
  $$

---

### Part 2: Generalized Quantum Measurement

- Measurement operators:
  $$
  \sum_i M_i^\dagger M_i = I
  $$

- Probability:
  $$
  p_i = \langle \psi | M_i^\dagger M_i | \psi \rangle
  $$

- Post-measurement state:
  $$
  |\psi_i'\rangle = \frac{M_i |\psi\rangle}{\sqrt{p_i}}
  $$

- Connection to environment:
  $$
  U|\psi\rangle|e_0\rangle = \sum_i M_i|\psi\rangle|e_i\rangle
  $$

---

## Lecture 57: POVM & Generalized Measurements

### POVM Definition

- Operators:
  $$
  F_i = M_i^\dagger M_i, \quad \sum_i F_i = I
  $$

- Probability (mixed state):
  $$
  p_i = \text{Tr}(\rho F_i)
  $$

---

### PVM vs POVM

| Property | PVM | POVM |
|----------|-----|------|
| Operators | Projectors | Positive operators |
| Orthogonal | Yes | No |
| Outcomes | ≤ dimension | Can exceed dimension |

---

### Example: Non-Orthogonal State Discrimination

- POVM allows distinguishing states with **inconclusive outcomes**, unlike projective measurements.

---

## Lecture 58: Entanglement in Mixed States (Heisenberg Model)

### Hamiltonian

$$
H = \frac{J}{4}(\sigma_x \otimes \sigma_x + \sigma_y \otimes \sigma_y + \sigma_z \otimes \sigma_z)
$$

---

### Eigenstates

- **Singlet (entangled):**
  $$
  |\psi_-\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle)
  $$

- **Triplets (3 states)**

---

### Thermal State

$$
\rho = \frac{1}{Z} \sum_i e^{-\beta E_i} |E_i\rangle \langle E_i|
$$

---

### Temperature Effects

| Temperature | State |
|------------|------|
| $T \to 0$ | Pure entangled |
| $T \to \infty$ | Mixed separable |

---

### Separability

$$
\rho = \sum_i p_i \rho_A^{(i)} \otimes \rho_B^{(i)}
$$

---

## Lecture 59: Convexity & Peres-Horodecki Criterion

### Convexity

- Convex combination:
  $$
  \sum_i p_i V_i, \quad p_i \ge 0, \quad \sum p_i = 1
  $$

---

### Partial Transpose

$$
\rho_{ij,kl} \rightarrow \rho_{ij,lk}
$$

---

### Criterion

- If eigenvalues of $\rho^{T_B}$ are:
  - **Positive → separable**
  - **Negative → entangled**

---

### Werner State

$$
\rho_W = (1-p)\frac{I}{4} + p |\Psi^-\rangle \langle \Psi^-|
$$

- Entangled if:
  $$
  p > \frac{1}{3}
  $$

---

## Lecture 60: Concurrence

### Spin-Flip Operation

$$
|\tilde{\psi}\rangle = (\sigma_y \otimes \sigma_y)|\psi^*\rangle
$$

---

### Pure State Concurrence

$$
C(|\psi\rangle) = |\langle \tilde{\psi} | \psi \rangle|
$$

- 0 → separable  
- 1 → maximally entangled  

---

### Mixed State Concurrence

$$
C(\rho) = \max(0, \lambda_1 - \lambda_2 - \lambda_3 - \lambda_4)
$$

---

### Werner State Result

$$
C(\rho_W) = \max\left(0, \frac{3p - 1}{2}\right)
$$

---

## Key Takeaways

- Lindblad equation describes **open system dynamics**.
- $T_1$ vs $T_2$ distinguishes **relaxation vs dephasing**.
- POVMs generalize measurements beyond projectors.
- Entanglement depends on **temperature in mixed states**.
- Convexity defines **separability structure**.
- Partial transpose detects entanglement.
- Concurrence quantifies entanglement **numerically**.

---

## Keywords

- Lindblad equation  
- POVM / PVM  
- Density matrix  
- Entanglement  
- Werner state  
- Concurrence  
- Partial transpose  
- Convex sets  

---
