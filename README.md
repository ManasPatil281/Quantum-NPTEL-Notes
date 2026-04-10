# QUANTUM COMPUTING & INFORMATION THEORY

## NPTEL Course — Complete Story-Driven Notes

### Weeks 2 – 12 | Lectures 6 – 60

> *Every formula. Every definition. Every idea — told as one continuous story.*

---

# PROLOGUE: THE STORY OF THIS COURSE

Imagine you are a particle — a humble electron. You have a spin. Sometimes it points up. Sometimes down. But until someone looks, it might point in both directions at once. This course is the story of how humanity learned to harness that mysterious "both directions at once" to build computers, send information, crack codes — and in doing so, discovered that the universe is far stranger than Newton ever imagined.

The journey begins in Week 2 with rotations — the mathematics of turning things in space. It passes through density matrices and quantum uncertainty, through the shocking weirdness of entanglement, through the elegant economics of data compression, all the way to the grand algorithmic ambition of Shor's algorithm, and finally lands in the noisy, real world of quantum decoherence. Every chapter builds on the last. Nothing is disconnected. Let us begin.

---

# WEEK 2: ROTATIONS, THE BLOCH SPHERE & DENSITY MATRICES

Before we can talk about quantum computation, we must talk about geometry. Quantum states of a single qubit live on a beautiful object called the **Bloch sphere** — a perfect globe where every point on the surface is a possible quantum state. To understand how quantum gates manipulate qubits, we need to understand how to *rotate* points on that sphere. This week lays down the geometric machinery.

---

## Passive vs Active Rotations

Think of turning a map versus turning yourself. When you rotate the map while standing still, that is a **passive rotation** — your body (the "system") hasn't changed; only the reference frame has. When you spin yourself in a chair, that is an **active rotation** — your body actually moves while the room stays fixed. Both give you the same relative orientation, but the mathematics differs by a sign.

- **Active Rotation:** The physical object (vector or quantum state) is rotated; the coordinate axes stay fixed.
- **Passive Rotation:** The coordinate axes are rotated; the object stays put.

In quantum mechanics, we usually think in terms of **passive** rotations when changing basis, and **active** rotations when applying gates. The rotation matrix about the Z-axis by angle φ is:

$$
R_Z(\phi) = \begin{pmatrix}
\cos\phi & -\sin\phi & 0 \\
\sin\phi & \cos\phi & 0 \\
0 & 0 & 1
\end{pmatrix}
$$
---

## Angular Momentum as the Generator of Rotations

Here is a beautiful idea: what is the "engine" that produces a rotation? For orbital motion, the answer is **angular momentum**. Specifically, the z-component of angular momentum, $L_z = x·p_y − y·p_x$, is the generator of rotations about the Z-axis.



> [!TIP]
> **Analogy:** Think of angular momentum as the "instruction manual" for rotation — it tells space how to spin. Just as linear momentum generates translations ("move 5 metres in the x direction"), angular momentum generates rotations ("spin 30 degrees about the z-axis").

Mathematically, if you rotate a wave function ψ by an infinitesimal angle δφ about Z:

$$
ψ'(r) = ψ(r) − δφ·(y·∂/∂x − x·∂/∂y)·ψ(r) = (1 − i·δφ·L_z / ℏ)·ψ
$$
Stacking infinitesimal rotations into a finite one (like building a staircase out of tiny steps):

$$
ψ' = exp(−i·φ·L_z / ℏ) · ψ
$$


> [!IMPORTANT]
> **Key Idea:** L_z is the generator of rotations about the Z-axis. Rotating a state is equivalent to exponentiating −i times the angular momentum operator.

---

## Spin and the Bloch Sphere

For a spin-½ particle (a qubit), angular momentum L_z is replaced by the spin operator $S_z = (ℏ/2)σ_z$. The rotation operators on the Bloch sphere are therefore:

$$
R_Z(φ) = exp(−i·φ·σ_z / 2)
R_X(φ) = exp(−i·φ·σ_x / 2)
R_Y(φ) = exp(−i·φ·σ_y / 2)
$$
For a general unit vector n̂ = (nₓ, nᵧ, n_z), the rotation by angle α about n̂ is:

$$
R_{n̂}(α) = exp(−i·α·(n̂·σ⃗)/2) = cos(α/2)·I − i·sin(α/2)·(n̂·σ⃗)
$$
This beautiful formula (derived using $(n̂·σ⃗)² = I$ for any unit vector) is the **fundamental rotation formula** on the Bloch sphere.

- **Bloch Sphere:** A unit sphere in 3D space where any point on the surface represents a pure qubit state $|ψ⟩ = cos(θ/2)|0⟩ + e^(iφ)sin(θ/2)|1⟩$, and interior points represent mixed states.

---

## The Hadamard Gate — A Rotation in Disguise

The famous Hadamard gate H, which turns |0⟩ into a superposition (|0⟩+|1⟩)/√2, is actually a rotation on the Bloch sphere:

$$
H = R_X(\pi)\,R_Y(\pi/2) = \frac{1}{\sqrt{2}}\begin{pmatrix}1 & 1 \\ 1 & -1\end{pmatrix}
$$
R_Y(π/2) tilts the state from the north pole of the Bloch sphere (|0⟩, along Z) to the equator (along X). R_X(π) then flips it to produce the correct Hadamard output. The overall phase is physically irrelevant.

---

## Euler Decomposition

Just as any rotation in 3D space can be broken into three simple rotations (like describing how a top spins, precesses, and nutates), any single-qubit rotation can be decomposed into rotations about just Y and Z:

$$
R_{n̂}(α) = R_Z(φ) · R_Y(θ) · R_Z(α) · R_Y(−θ) · R_Z(−φ)
$$


> [!IMPORTANT]
> **Key Idea:** Any quantum gate on a single qubit can be built using only Z-rotations and Y-rotations. This is critical for physical hardware where you can only turn knobs in fixed directions.

---

## The Density Matrix — Describing Impure Knowledge

So far we have described quantum states as vectors |ψ⟩. But what if you only know the quantum state *probabilistically*? For example, you know your electron is spin-up with 60% probability and spin-down with 40%, but you don't know which it actually is. This is not a superposition — it is genuine *ignorance*. To handle this, we introduce the **density matrix**.



> [!TIP]
> **Analogy:** A pure state is like knowing exactly where a ball is in a box. A mixed state is like knowing it could be in one of several places with certain probabilities — your knowledge is impure.

- **Density Matrix (Pure State):** $\rho = |\psi\rangle\langle\psi|$. For a qubit $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$: $\rho = \begin{pmatrix}|\alpha|^2 & \alpha\beta^* \\ \alpha^*\beta & |\beta|^2\end{pmatrix}$
- **Density Matrix (Mixed State):** $ρ = Σᵢ pᵢ |ψᵢ⟩⟨ψᵢ|$, a probability-weighted sum over pure states.

The key properties of any valid density matrix are:

- $Tr(ρ) = 1$ — total probability = 1
- $ρ = ρ†$ — Hermitian (all eigenvalues are real and non-negative)
- $Tr(ρ²) = 1$ for a pure state; $Tr(ρ²) < 1$ for a mixed state
- $ρ² = ρ$ for a pure state (it is a projector)

The **diagonal elements** ρᵢᵢ are called **populations** — they give the probability of measuring the system in state |i⟩. The **off-diagonal elements** are called **coherences** — they encode the quantum phase relationships between states.

On the Bloch sphere, pure states sit on the surface (|α⃗| = 1), mixed states live inside (|α⃗| < 1), and the **maximally mixed state** ρ = I/2 sits at the very centre — the most uncertain state possible.

- **Bloch Vector Representation:** $ρ = (1/2)(I + α⃗·σ⃗)$, where α⃗ = (α₁,α₂,α₃) is the Bloch vector with $αᵢ = Tr(ρ·σᵢ)$.
- **Expectation Value via Density Matrix:** $⟨O⟩ = Tr(ρ·Ô)$. For pure states, this reduces to the familiar $⟨ψ|Ô|ψ⟩$.

> *→ We now know how to represent and rotate quantum states. Next, we ask: how do these states change over time, and how does information fit into the quantum picture?*

---

# WEEK 3: TIME EVOLUTION, CLASSICAL INFORMATION THEORY & REVERSIBLE GATES

With the density matrix in hand, we have a complete description of any quantum state — pure or mixed. Now we ask the physicist's favourite question: *what happens next?* And then, in a surprising twist, we take a detour into the classical world of information theory. The reason will become clear — quantum information is built on top of classical information, so we must understand the classical foundation before constructing the quantum edifice.

---

## How Quantum States Evolve Over Time

For a closed quantum system (one that doesn't interact with anything outside), evolution is always **unitary** — meaning it preserves the total probability and is perfectly reversible. The state at time t is:

$$
ρ(t) = U(t) · ρ(0) · U†(t),     where U(t) = exp(−iHt/ℏ)
$$
Here H is the Hamiltonian — the total energy operator of the system. Differentiating this gives the celebrated **Liouville–von Neumann equation**:

$$
dρ/dt = (1/iℏ)[H, ρ]
$$


> [!TIP]
> **Analogy:** This is the quantum version of Newton's second law. Just as F = ma tells you how position and momentum evolve, the Liouville equation tells you how the density matrix (the quantum state) evolves. The commutator [H, ρ] = Hρ − ρH plays the role of the force.



> [!IMPORTANT]
> **Key Idea:** The commutator [H, ρ] is to quantum mechanics what the Poisson bracket {H, ρ} is to classical mechanics — the fundamental bracket that generates time evolution.

On the Bloch sphere, the Bloch vector α⃗ precesses around the axis defined by H — exactly like a magnetic compass needle precessing around a magnetic field. This precession is **perfect rotation**, never shrinking the Bloch vector. Decoherence (studied in Week 10) is what makes it shrink.

---

## Information: What Does It Mean to Know Something?

Now we pivot to classical information theory, created by Claude Shannon in 1948. Shannon asked a simple but profound question: **how much information does a message contain?** His genius was to connect information to *surprise*. If I tell you the sun rose this morning, you learn nothing — you already knew. But if I tell you it rained in the Sahara today, that's genuinely informative, because it was unexpected.

- **Information Content (Hartley/Shannon):** $I(p) = −log₂(p)$ bits, where p is the probability of the event. Unlikely events (small p) carry high information; certain events (p = 1) carry zero information.



> [!TIP]
> **Analogy:** Information is like surprise. Hearing that a common word appears in a sentence ("the") tells you almost nothing. Hearing that a rare word appears ("syzygy") tells you a lot. The rarer the event, the more information it carries.

To encode m possible messages, you need at least n bits where $2ⁿ ≥ m$, so $n = log₂(m)$ bits. This is Hartley's formula (1927) — the first mathematical connection between messages and bits.

For independent events, information is **additive**: $I(A and B) = I(A) + I(B)$. This makes sense: learning two independent facts gives you the sum of their individual surprises.

---

## Shannon Entropy — The Average Surprise

But a source doesn't send one fixed event — it sends a stream of events drawn from a probability distribution. The natural measure of "how informative is this source on average?" is the **Shannon entropy**:

$$
H(P) = −Σᵢ pᵢ log₂(pᵢ)
$$
Shannon entropy has four beautiful properties that uniquely characterise it:

- **Continuity:** small changes in probabilities → small changes in H
- **Non-negativity:** H ≥ 0, with H = 0 only when the outcome is certain
- **Maximum at uniform distribution:** H ≤ log₂(N) for N outcomes
- **Additivity:** H(P·Q) = H(P) + H(Q) for independent sources

These four axioms together *uniquely determine* the Shannon entropy formula. No other function satisfies all four — a remarkable result.

- **Boltzmann Analogy:** Shannon entropy is mathematically identical to Boltzmann entropy S = k·ln(Ω), with k replaced by 1 and Ω by the number of equally likely messages. Information and thermodynamics are deeply linked.

---

## The Asymptotic Equipartition Property (AEP) — The Magic of Large Numbers

Here is one of the most counterintuitive ideas in information theory. Suppose your source emits N symbols, each chosen randomly from a distribution. For large N, a remarkable thing happens: **almost all sequences become equally likely**, each with probability approximately $2^(−N·H(X))$.

$$
P(X₁, ..., Xₙ) ≈ 2^(−N·H(X))
$$
The number of such "typical sequences" is about $2^(N·H(X))$, which is exponentially smaller than the total number of possible sequences. This is why compression works!



> [!TIP]
> **Analogy:** Imagine shaking a bag containing 100 biased coins (75% heads). If you tip them out and record the sequence, almost every sequence you see will have roughly 75 heads and 25 tails — the "typical" sequences. There are about $2^(N·H(0.75))$ such sequences, vastly fewer than $2^100$ total possibilities. You only need to encode those.

---

## Shannon's Noiseless Coding Theorem

This theorem is the crown jewel of classical information theory: **you cannot losslessly compress a source below H(X) bits per symbol, but you can get arbitrarily close to H(X).** The entropy is the ultimate compression limit.

Practically, this is achieved with **prefix-free codes** (like Huffman coding): give short codewords to frequent symbols and long codewords to rare ones. For a source with probabilities (½, ¼, ⅛, ⅛), the optimal code uses codewords of lengths (1, 2, 3, 3), achieving average length 1.75 bits — exactly H(X).

---

## The Toffoli Gate — The Bridge Between Classical and Quantum

We end this week with a key observation: classical logic gates like AND and OR are **irreversible** — you cannot uniquely reconstruct the inputs from the outputs (two different input pairs can give the same output). But quantum gates must be **unitary**, which means **reversible**. How do we build reversible classical logic?

The answer is the **Toffoli gate** (also called CCNOT — controlled-controlled-NOT):

- **Toffoli Gate:** A 3-bit gate with inputs (A, B, C) and outputs (A, B, C ⊕ (A∧B)). The third bit is flipped if and only if both A=1 AND B=1; otherwise all bits pass through unchanged.

Crucially, applying the Toffoli gate *twice* recovers the original inputs — it is its own inverse. This makes it reversible.



> [!IMPORTANT]
> **Key Idea:** Every quantum gate must be reversible (unitary). The Toffoli gate proves that reversible classical computation is possible — quantum computers can simulate classical computers without wasting information.

> *→ We have now mastered classical information. It is time to go quantum. Starting from Shannon entropy, we build its quantum cousin — and discover that entropy becomes entangled with entanglement itself.*

---

# WEEK 4: VON NEUMANN ENTROPY, ENTANGLEMENT & REDUCED DENSITY MATRICES

Classical information lives in bits — definite 0s and 1s with a probability distribution. Quantum information lives in *amplitudes* — complex numbers whose squares are probabilities. The natural quantum generalisation of Shannon entropy replaces probability distributions with density matrices. This week, we discover that quantum uncertainty is richer than classical uncertainty, and that when two quantum systems share their fate — a phenomenon called **entanglement** — information becomes irreducibly non-local.

---

## Von Neumann Entropy — Quantum Uncertainty

Shannon entropy was $H = −Σ pᵢ log pᵢ$. The **von Neumann entropy** replaces the probability distribution with the density matrix:

$$
S(ρ) = −Tr(ρ log ρ)
$$
To compute this, diagonalise ρ (always possible since ρ is Hermitian). Then:

$$
S(ρ) = −Σᵢ λᵢ log λᵢ
$$
where λᵢ are the eigenvalues of ρ. This is exactly Shannon entropy applied to the eigenvalue spectrum.



> [!TIP]
> **Analogy:** Think of von Neumann entropy as "how mixed is this state?" A pure state (one eigenvalue = 1, rest = 0) has S = 0 — perfect certainty. A maximally mixed state (all eigenvalues = 1/n) has S = log n — maximum uncertainty. Entropy measures how far we are from knowing exactly what state we're in.

For a qubit: S = 0 for any pure state, and S = 1 bit for ρ = I/2 (the maximally mixed state). The von Neumann entropy is zero for pure states even if they are in superposition — **superposition is not uncertainty!**

---

## Two-Qubit Systems and the Tensor Product

When we bring two qubits together, the Hilbert space becomes a **tensor product**: H = H_A ⊗ H_B, with dimension 2×2 = 4. The computational basis consists of four states: |00⟩, |01⟩, |10⟩, |11⟩.

- **Separable State:** $|ψ_AB⟩ = |ψ_A⟩ ⊗ |ψ_B⟩$ — a state that can be factored into independent parts. The two qubits are completely independent.
- **Entangled State:** A state that *cannot* be written as $|ψ_A⟩ ⊗ |ψ_B⟩$ for any single-qubit states. The two qubits are correlated in a way with no classical analogue.



> [!TIP]
> **Analogy:** A separable state is like two people who each roll their own die. The outcomes are independent. An entangled state is like two people sharing a single mysterious coin: whenever Alice sees heads, Bob sees tails, no matter how far apart they are — and this correlation was "baked in" at the moment of entanglement, not by any signal between them.

---

## Bell States — The Four Maximally Entangled States

The four Bell states are the maximally entangled two-qubit states, forming an orthonormal basis:

$$
|Φ⁺⟩ = (1/√2)(|00⟩ + |11⟩)    [both same]
|Φ⁻⟩ = (1/√2)(|00⟩ − |11⟩)    [both same, phase flip]
|Ψ⁺⟩ = (1/√2)(|01⟩ + |10⟩)    [both different]
|Ψ⁻⟩ = (1/√2)(|01⟩ − |10⟩)    [singlet]
$$
None of these can be written as a product of two single-qubit states. They are the most entangled states possible.

---

## Partial Trace — Peeking at One Half of an Entangled Pair

When we have a bipartite system AB and want to describe only subsystem A (ignoring B), we use the **partial trace** over B:

$$
ρ_A = Tr_B(ρ_AB) = Σ_b (I_A ⊗ ⟨b|) · ρ_AB · (I_A ⊗ |b⟩)
$$
For the Bell state |Φ⁺⟩:

$$
\rho_A = \mathrm{Tr}_B(\rho_{AB}) = \frac{1}{2}I = \begin{pmatrix}\frac{1}{2} & 0 \\ 0 & \frac{1}{2}\end{pmatrix}
$$
The reduced density matrix of A is the **maximally mixed state** — even though the joint state is pure! This is the signature of entanglement.



> [!IMPORTANT]
> **Key Idea:** A pure entangled state → mixed reduced state (after partial trace). S(ρ_A) > 0 signals entanglement. The more entangled, the more mixed the subsystem.

- **Entanglement Criterion (Pure Bipartite States):** |ψ_AB⟩ is entangled if and only if ρ_A = Tr_B(ρ_AB) is mixed, i.e., S(ρ_A) > 0.

This result was confirmed experimentally by Aspect, Clauser, and Zeilinger — the **2022 Nobel Prize in Physics**.

---

## Schmidt Decomposition — The Natural Language of Bipartite States

Every pure bipartite state can be written in a special "diagonal" form called the **Schmidt decomposition**:

$$
|ψ_AB⟩ = Σᵢ αᵢ |uᵢ⟩_A ⊗ |vᵢ⟩_B
$$
where {|uᵢ⟩} and {|vᵢ⟩} are orthonormal bases for A and B respectively, and αᵢ ≥ 0 are the **Schmidt coefficients**.

- **Schmidt Rank:** The number of non-zero Schmidt coefficients. Rank 1 → separable. Rank > 1 → entangled.

The entanglement entropy is:

$$
S(ρ_A) = −Σᵢ αᵢ² log αᵢ² = S(ρ_B)
$$


> [!IMPORTANT]
> **Key Idea:** S(ρ_A) = S(ρ_B) always — the entanglement entropy is the same for both subsystems. Entanglement is symmetric.

> *→ We know entanglement exists. But can we test it experimentally against classical explanations? The story now leads to one of the deepest questions in physics: is quantum mechanics complete, or is something hidden?*

---

# WEEK 5: EPR PARADOX, BELL'S INEQUALITY & THE QUANTUM REVOLUTION

Einstein never accepted quantum mechanics as a complete theory. He felt that something was missing — hidden variables behind the scenes that would restore determinism and locality. In 1935, with Podolsky and Rosen, he published a famous thought experiment (the EPR paradox) arguing that quantum mechanics must be incomplete. For 30 years, no one knew how to test it. Then Bell showed how. Then experimentalists proved Einstein wrong. This week tells that story.

---

## The Singlet State and Perfect Anti-Correlation

The EPR pair is the singlet Bell state — the quantum state of two spin-½ particles with total spin zero:

$$
|Ψ⁻⟩ = (1/√2)(|↑⟩_A|↓⟩_B − |↓⟩_A|↑⟩_B)
$$
This state is **rotationally invariant** — it looks the same in any measurement basis. It exhibits **perfect anti-correlation**: if Alice measures spin-up along any axis, Bob's particle *instantly* collapses to spin-down along that same axis, no matter how far apart they are.



> [!TIP]
> **Analogy:** Imagine a factory that makes pairs of gloves — one left, one right — and ships them to Alice and Bob in separate boxes. When Alice opens her box and sees a left glove, she instantly knows Bob has a right glove. Is that spooky? No — the information was in the glove all along. EPR argued: maybe quantum particles are like gloves — their properties were pre-determined, we just haven't found the "label" yet.

---

## The EPR Argument — Local Realism

Einstein's argument rested on two principles:

- **Locality Principle:** A measurement on system A cannot instantaneously affect a causally disconnected system B.
- **Reality Principle:** If the value of a physical quantity can be predicted with certainty without disturbing the system, then it corresponds to an "element of physical reality" — something that exists independently.

EPR concluded: since measuring Alice's spin along Z predicts Bob's spin along Z with certainty (without touching Bob), Bob's spin-Z must be a pre-existing "element of reality". There must be **hidden variables** filling in the missing details.

There's a problem: spin along X and spin along Z do not commute: $[S_z, S_x] ≠ 0$. Quantum mechanics says they cannot simultaneously have definite values. Hidden variable theories must assign definite values to both simultaneously. Bell showed this leads to testable contradictions.

---

## Bell's Inequality — Turning Philosophy into Physics

John Bell (1964) found a way to test local realism:

$$
Bell-Wigner Inequality: P(A⁺B⁺) ≤ P(A⁺C⁺) + P(C⁺B⁺)
$$


> [!IMPORTANT]
> **Key Idea:** Bell's inequality is a constraint that *any* locally realistic theory must satisfy. If experiments violate it, local realism is ruled out — the universe is fundamentally non-local, or non-real, or both.

---

## Quantum Mechanics Violates Bell's Inequality

For the singlet state, when Alice measures axis A and gets +1, the probability that Bob gets +1 along axis B (separated by angle θ_AB) is:

$$
P(A⁺B⁺) = (1/2)·sin²(θ_AB/2)
$$
At θ = 60°: LHS = sin²(60°) = 3/4, RHS = 2·sin²(30°) = 1/2. Since **3/4 > 1/2**, quantum mechanics **violates Bell's inequality**.

Aspect, Clauser, and Zeilinger performed these experiments and confirmed the quantum prediction. For this, they shared the **2022 Nobel Prize in Physics**. The universe is not locally realistic.

> *→ We now know that entanglement is real, non-local, and certified by Bell tests. It is time to put this powerful resource to work.*

---

# WEEK 6: CNOT GATE, DENSE CODING, TELEPORTATION & ENTANGLED PHOTONS

We have established that entanglement is real and powerful. Now we harness it. This week introduces three of the most beautiful protocols in quantum information science.

---

## The CNOT Gate — Creating Entanglement

The Controlled-NOT (CNOT) gate is *the* two-qubit gate. It flips the **target** qubit if and only if the **control** qubit is |1⟩:

$$
CNOT|00⟩ = |00⟩      CNOT|01⟩ = |01⟩
CNOT|10⟩ = |11⟩      CNOT|11⟩ = |10⟩
$$
The magic of CNOT: applying it after a Hadamard gate creates Bell states from computational basis states:

$$
|00⟩ → |Φ⁺⟩ = (1/√2)(|00⟩+|11⟩)
|01⟩ → |Ψ⁺⟩ = (1/√2)(|01⟩+|10⟩)
|10⟩ → |Φ⁻⟩ = (1/√2)(|00⟩−|11⟩)
|11⟩ → |Ψ⁻⟩ = (1/√2)(|01⟩−|10⟩)
$$
---

## Dense Coding — 2 Classical Bits via 1 Qubit

Alice wants to send Bob 2 classical bits of information. She has only 1 qubit. Classically, 1 bit per transmission is the limit. With entanglement, she can send **2 bits per qubit!**

**Protocol:** Alice and Bob share |Φ⁺⟩. Alice holds qubit 1, Bob holds qubit 2.

- To send "00": Alice applies I (identity) → state stays |Φ⁺⟩
- To send "01": Alice applies σ_x → state becomes |Ψ⁺⟩
- To send "10": Alice applies σ_z → state becomes |Φ⁻⟩
- To send "11": Alice applies iσ_y → state becomes |Ψ⁻⟩

Alice sends her qubit to Bob. Bob performs a Bell measurement and recovers the 2 bits.



> [!IMPORTANT]
> **Key Idea:** Dense coding doubles classical communication capacity using pre-shared entanglement.

---

## Quantum Teleportation — Transmitting Quantum States Classically

Teleportation is the reverse of dense coding. Alice has an **unknown qubit** |ψ⟩ = α|0⟩ + β|1⟩. She cannot measure it (destroys superposition). She cannot clone it (no-cloning theorem). But she can **teleport** it:

**Step 1:** Write the total 3-qubit state:
$$
|Total⟩ = |ψ⟩₁ ⊗ |Φ⁺⟩₂₃
$$
**Step 2:** Rewrite in Alice's Bell basis for qubits 1,2:
$$
|Total⟩ = (1/2)[|Φ⁺⟩₁₂(α|0⟩+β|1⟩)₃ + |Φ⁻⟩₁₂(α|0⟩−β|1⟩)₃
         + |Ψ⁺⟩₁₂(α|1⟩+β|0⟩)₃ + |Ψ⁻⟩₁₂(−α|1⟩+β|0⟩)₃]
$$
**Step 3:** Alice measures in the Bell basis → Bob's qubit collapses to a known rotation of |ψ⟩.

**Step 4:** Alice sends 2 classical bits to Bob.

**Step 5:** Bob applies the correction (I, σ_z, σ_x, or iσ_y) and recovers |ψ⟩ exactly.



> [!IMPORTANT]
> **Key Idea:** No physical qubit was transmitted — only 2 classical bits. Alice's qubit is destroyed in the measurement, respecting no-cloning.

---

## Generating Entangled Photons in the Lab

The standard technique is **Parametric Down-Conversion (PDC)** in a nonlinear optical crystal (e.g., BBO — beta barium borate). One high-energy pump photon (400 nm UV) splits into two daughter photons (~800 nm each) with orthogonal polarisations:

$$
ω_pump = ω₁ + ω₂,    k_pump = k₁ + k₂    (energy and momentum conservation)
$$
The resulting entangled state:
$$
|ψ⟩ = (1/√2)(|H⟩₁|V⟩₂ + e^(iφ)|V⟩₁|H⟩₂)
$$
> *→ We can now create, manipulate, and communicate with entanglement. Next: how do we detect Bell states, and can we break classical cryptography?*

---

# WEEK 7: BELL STATE ANALYSIS, RSA CRYPTOGRAPHY & THE QFT

This week ties together the physical world of photon experiments with the mathematical world of cryptography.

---

## Beam Splitters as Hadamard Gates

A 50/50 beam splitter is the optical analogue of the Hadamard gate:
$$
H|a⟩ = (1/√2)(|c⟩ + |d⟩),     H|b⟩ = (1/√2)(|c⟩ − |d⟩)
$$
---

## Photon Bunching and the Singlet's Unique Identity

Photons are **bosons** — the total wavefunction must be symmetric under exchange.

- For |Φ⁺⟩, |Φ⁻⟩, |Ψ⁺⟩ (symmetric spin): both photons exit the *same* output port → **photon bunching**
- For the singlet |Ψ⁻⟩ (antisymmetric spin): photons exit *different* ports → **coincidence detection**



> [!IMPORTANT]
> **Key Idea:** The singlet |Ψ⁻⟩ is the only Bell state identifiable with a single beam splitter via coincidence detection.

---

## RSA Cryptography — Classical Security and Its Quantum Threat

RSA security rests on a simple fact: multiplying two large primes is easy, but finding those primes from their product is computationally hard.

**RSA Key Generation:**
- Bob chooses large primes p, q and computes N = p×q (public) and M = (p−1)(q−1) (private)
- Bob chooses e with gcd(e, M) = 1, computes d ≡ e⁻¹ (mod M). Public key: (N, e). Private key: (N, d).
- Alice encrypts: ciphertext = m^e mod N
- Bob decrypts: m = (m^e)^d mod N

An eavesdropper who factors N can break the encryption. **Quantum computers change this.**

---

## The Quantum Fourier Transform — The Heart of Shor's Algorithm

The **Quantum Fourier Transform (QFT)** transforms quantum state amplitudes:

$$
QFT|j⟩ = (1/√N) · Σₖ exp(2πi·jk/N) · |k⟩      where N = 2ⁿ
$$


> [!IMPORTANT]
> **Key Idea:** The QFT converts periodicity in the computational basis into a clear frequency peak. If the input has period r, the output has amplitude concentrated at multiples of N/r.

> *→ We now know WHY the QFT is powerful. Next week, we learn HOW to build it.*

---

# WEEK 8: THE QFT CIRCUIT — BUILDING THE QUANTUM FOURIER TRANSFORM

The QFT output state factorises into a **tensor product** over individual qubits:

$$
QFT|x⟩ = ⊗ₖ₌₁ⁿ  (|0⟩ + exp(2πi·x/2^k)|1⟩) / √2
$$
### Building Block Gates

- **Hadamard Gate H:** Creates superposition
- **Rotation Gate U_rot,k:** Matrix $\begin{pmatrix}1 & 0 \\ 0 & e^{2\pi i/2^k}\end{pmatrix}$
- **Controlled Rotation C-R_k:** Applies U_rot,k only if control is |1⟩
- **SWAP Gate:** Exchanges two qubit states

### Gate Count — The Exponential Advantage

- n Hadamard gates
- n(n−1)/2 controlled rotation gates
- ⌊n/2⌋ SWAP gates
- **Total: O(n²) gates**



> [!IMPORTANT]
> **Key Idea:** QFT uses O(n²) quantum gates vs O(n·2ⁿ) classical operations. For n=300 qubits: ~90,000 gates vs ~3×10^92 classical operations.

> *→ We have our Fourier engine. Now we assemble Shor's algorithm.*

---

# WEEK 9: SHOR'S ALGORITHM — QUANTUM FACTORING IN FULL DETAIL

This is arguably the most important quantum algorithm ever discovered — the one that would break every RSA-encrypted message on the internet.

---

## Algorithm Architecture: Two Registers

- **Register A (input):** C qubits, where 2^C > N². Holds superposition of inputs x.
- **Register B (output):** L = ⌈log₂N⌉ qubits. Stores f(x) = aˣ mod N.

## Step-by-Step Walkthrough

### Step 1: Initialise
$$
|ψ₀⟩ = |0⟩_A ⊗ |0⟩_B
$$
### Step 2: Create Superposition
$$
|ψ₁⟩ = (1/√2^C) · Σₓ |x⟩_A ⊗ |0⟩_B
$$
### Step 3: Modular Exponentiation Oracle
$$
|ψ₂⟩ = (1/√2^C) · Σₓ |x⟩_A ⊗ |aˣ mod N⟩_B
$$
### Step 4: Measure Register B
Collapses A to a periodic superposition with spacing r:
$$
|ψ₃⟩ = (1/√m) · Σⱼ |x₀ + j·r⟩_A ⊗ |y₀⟩_B
$$
### Step 5: Apply QFT to Register A
Constructive interference at $n ≈ l·2^C/r$. Measurement finds one of these peaks.

### Step 6: Extract r via Continued Fractions
Use the continued fraction algorithm to find the best rational approximation to n/2^C.

### Step 7: Classical Factorisation
$$
P = gcd(a^(r/2) − 1, N)      Q = gcd(a^(r/2) + 1, N)
$$
---

## Worked Example: Factoring N = 15 with a = 7

The sequence 7^x mod 15 has period r = 4:
- 7¹ mod 15 = 7
- 7² mod 15 = 4
- 7³ mod 15 = 13
- 7⁴ mod 15 = 1 ✓

After QFT, measuring n = 64: $n/2^C = 64/256 = 1/4 → r = 4$
$$
P = gcd(7² − 1, 15) = gcd(48, 15) = 3
Q = gcd(7² + 1, 15) = gcd(50, 15) = 5
N = 3 × 5 = 15  ✓
$$
### Complexity Comparison
- **Classical best:** ~10 billion years for 400-digit N
- **Shor's algorithm:** O(n³) — hours on a large quantum computer

> *→ Shor's algorithm assumes a perfect quantum computer. Reality is messier. Real qubits lose their quantum properties through decoherence.*

---

# WEEK 10: DECOHERENCE, OPEN QUANTUM SYSTEMS & THE KRAUS FORMALISM

A quantum computer operates like a delicate symphony — every qubit must maintain its precise phase. But the universe is not silent. Every qubit is surrounded by stray photons, vibrating atoms, fluctuating fields. These interactions gradually destroy the quantum information — **decoherence**.

---

## What Is Decoherence?

- **Decoherence:** The loss of off-diagonal elements in the density matrix, caused by entanglement of the system with its environment. Populations may be preserved even as coherences decay.
- **Dissipation:** The loss of energy from the system to the environment. Both populations AND coherences change.



> [!TIP]
> **Analogy:** Imagine writing a message in chalk on a blackboard. Dust and vibrations slowly blur the letters (decoherence). Eventually you can't read any message — that's the maximally mixed state.

---

## A Simple Model: CNOT as Decoherence

Model the environment as a single qubit starting in |0⟩:

$$
(α|0⟩ + β|1⟩) ⊗ |0⟩  →  α|0,0⟩ + β|1,1⟩
$$
Tracing out the environment:
$$
\rho_S = \begin{pmatrix}|\alpha|^2 & 0 \\ 0 & |\beta|^2\end{pmatrix}
$$
The off-diagonal elements have **completely vanished!** A single environmental interaction destroyed all coherence.

---

## Kraus Operators — The Mathematics of Open Evolution

The most general description of open quantum system dynamics:

$$
ρ_S(t) = Σₖ Eₖ · ρ_S(0) · Eₖ†
$$
- **Completeness Condition:** $Σₖ Eₖ†Eₖ = I$ — guarantees probability is preserved
- **CPTP Map:** Completely Positive Trace-Preserving map — the mathematical definition of any valid quantum channel



> [!IMPORTANT]
> **Key Idea:** Every physical evolution of an open quantum system can be written as $ρ → Σₖ Eₖ ρ Eₖ†$, with $Σₖ Eₖ†Eₖ = I$.

---

## The Depolarising Channel

The most symmetric noise model for a single qubit:
$$
E₀ = √(1−3p/4)·I,    E₁ = √(p/4)·σₓ,    E₂ = √(p/4)·σᵧ,    E₃ = √(p/4)·σ_z
$$
Effect: The Bloch sphere **shrinks uniformly** by factor (1−p). At p = 1, ρ' = I/2.

---

## Unitary Dilation



> [!IMPORTANT]
> **Key Idea:** Every open quantum system evolution is, in an extended picture, a perfectly unitary rotation on a larger Hilbert space. Decoherence is just our limited view of a larger unitary universe.

> *→ We have the formalism for noise. Now we apply it to specific physical channels.*

---

# WEEK 11: QUANTUM NOISE CHANNELS, LINDBLAD EQUATION & SPONTANEOUS EMISSION

---

## The Bit Flip Channel
$$
E₀ = √(1−p)·I,    E₁ = √p·σₓ
$$
Bloch sphere: compressed into an oblate ellipsoid — squashed along y and z.

## The Phase Flip Channel
$$
E₀ = √(1−p)·I,    E₁ = √p·σ_z
$$
Bloch sphere: compressed along x and y — this is **T₂ dephasing** in NMR.

## The Amplitude Damping Channel — Spontaneous Emission
$$
E_0 = \begin{pmatrix}1 & 0 \\ 0 & \sqrt{1-p}\end{pmatrix},\quad
E_1 = \begin{pmatrix}0 & \sqrt{p} \\ 0 & 0\end{pmatrix}
$$
Bloch sphere: shrinks non-uniformly AND shifts toward the north pole (|0⟩). At p = 1, the qubit has completely relaxed to the ground state.

---

## The Lindblad Master Equation

The most general Markovian quantum master equation for continuous-time dissipative evolution:

$$
dρ_S/dt = −(i/ℏ)[H, ρ_S] + Σₖ(Lₖ·ρ_S·Lₖ† − (1/2){Lₖ†Lₖ, ρ_S})
$$
The three terms:
- $−(i/ℏ)[H, ρ_S]$: coherent (Hamiltonian) evolution
- $Σₖ Lₖρ_S Lₖ†$: "quantum jump" term — transitions caused by the environment
- $−(1/2)Σₖ{Lₖ†Lₖ, ρ_S}$: "no-jump" term — ensures Tr(ρ) = 1



> [!IMPORTANT]
> **Key Idea:** The Lindblad equation is to open quantum systems what Newton's equation is to classical mechanics — the universal law of motion for quantum systems in contact with an environment.

---

## Spontaneous Emission — A Complete Solution

For a two-level atom with energy splitting ℏω and decay rate γ:

$$
dρ₁₁/dt = −γ·ρ₁₁          →  ρ₁₁(t) = ρ₁₁(0)·e^(−γt)
dρ₀₀/dt = +γ·ρ₁₁          →  ρ₀₀(t) = 1 − ρ₁₁(0)·e^(−γt)
dρ₀₁/dt = (iω − γ/2)·ρ₀₁  →  ρ₀₁(t) = ρ₀₁(0)·e^((iω−γ/2)t)
$$
- **T₁ = 1/γ:** Population decay time — how fast the excited state decays
- **T₂ = 2/γ = 2T₁:** Coherence decay time — coherences decay TWICE as slowly as populations



> [!TIP]
> **Analogy:** T₁ is like the time for a spinning top to fall over (energy loss). T₂ is the time for the top to wobble chaotically while falling — the phase gets randomised before the energy is fully lost.

> *→ One final chapter remains — measuring entanglement in mixed states.*

---

# WEEK 12: POVM MEASUREMENTS, ENTANGLEMENT IN MIXED STATES & CONCURRENCE

In our final week, we address three interrelated questions. How do we generalise quantum measurement beyond the simple projective measurements we have used so far? How do we detect and quantify entanglement in *mixed* states — states that are already partially noisy? And what happens to entanglement as temperature rises? The answers introduce POVMs, the Peres-Horodecki criterion, and concurrence.

---

## Lindblad Equation in NMR/ESR — Full Treatment

In magnetic resonance (NMR/ESR), three Lindblad operators govern the dynamics of a spin-1/2 system in a magnetic field $H = -(\omega/2)\sigma_z$:

$$
L_+ = \sqrt{\gamma_+}\begin{pmatrix}0 & 1 \\ 0 & 0\end{pmatrix}\quad \text{(emission: }|1\rangle\to|0\rangle\text{)}
L_- = \sqrt{\gamma_-}\begin{pmatrix}0 & 0 \\ 1 & 0\end{pmatrix}\quad \text{(absorption: }|0\rangle\to|1\rangle\text{)}
L_z = \sqrt{\gamma_z}\,\sigma_z\quad \text{(dephasing: no energy exchange)}
$$
The relaxation times are given by:

$$
1/T1 = γ+ + γ-              (amplitude/population decay)
1/T2 = (γ+ + γ-)/2 + 2γz    (phase/coherence decay)
$$
At thermal equilibrium, the populations satisfy the Boltzmann distribution:

$$
ρ11/ρ00 = γ-/γ+ = exp(−ℏω/kBT)
$$
This thermal relation connects quantum open-system dynamics to statistical mechanics — a direct bridge between microscopic quantum jumps and macroscopic thermodynamics.

---

## Generalised Quantum Measurement — POVMs

So far, quantum measurement has meant projective measurements (PVMs): measuring in an orthonormal basis $\{|e_i\rangle\}$, with projectors $\Pi_i = |e_i\rangle\langle e_i|$. But this is not the most general measurement allowed by quantum mechanics.

A **generalised measurement** is described by a set of measurement operators $\{M_i\}$:

- **Completeness:** $\sum_i M_i^\dagger M_i = I$ (ensures probabilities sum to 1)
- **Measurement probability:** $p_i = \langle\psi|M_i^\dagger M_i|\psi\rangle = \mathrm{Tr}(\rho M_i^\dagger M_i)$
- **Post-measurement state:** $|\psi_i'\rangle = M_i|\psi\rangle/\sqrt{p_i}$
- **POVM element:** $F_i = M_i^\dagger M_i$; the collection $\{F_i\}$ with $\sum_i F_i = I$ is a Positive Operator-Valued Measure



> [!TIP]
> **Analogy:** A PVM is like a clear yes/no detector: either the photon is found in a basis state or not. A POVM is like a richer detector with multiple outcomes, including possible "inconclusive" outcomes. This allows tasks like distinguishing non-orthogonal states with controlled failure probability.

Key comparison:

- **PVM:** orthogonal projectors, outcomes <= Hilbert-space dimension, sharp collapse
- **POVM:** positive operators (not necessarily projectors), can have more outcomes than dimension, supports inconclusive outcomes

Connection to environment: a POVM can always be realised as a projective measurement on a larger system. If

$$
U|ψ⟩|e0⟩ = Σi Mi|ψ⟩|ei⟩,
$$
then measuring the environment basis $\{|e_i\rangle\}$ corresponds to applying POVM $\{M_i\}$ to the system.

---

## Entanglement in Mixed States — The Heisenberg Chain

For pure bipartite states, entanglement detection is straightforward: take a partial trace and check whether the reduced state is mixed. For **mixed states**, the problem is subtler. A state can look mixed locally yet still be separable globally.

- **Separable mixed state:**

$$
ρ = Σi pi ρA(i) ⊗ ρB(i)
$$
A separable state can be prepared by local operations plus shared classical randomness; no entanglement resource is required.

As a physical model, consider two spin-1/2 particles with Heisenberg interaction:

$$
H = (J/4)(σx⊗σx + σy⊗σy + σz⊗σz)
$$
The thermal state at temperature $T$ is:

$$
ρ(T) = (1/Z) Σi exp(−βEi)|Ei⟩⟨Ei|,     β = 1/kBT
$$
At $T \to 0$, the system approaches the singlet ground state (maximally entangled). At $T \to \infty$, $\rho \to I/4$ (maximally mixed, separable). Temperature destroys entanglement, and there is a critical temperature above which the state becomes separable.

---

## Convexity and the Structure of Quantum States

- **Convex combination:** $\sum_i p_i V_i$ where $p_i \ge 0$ and $\sum_i p_i = 1$
- **Convex set:** a set $S$ where $\lambda A + (1-\lambda)B \in S$ for any $A,B \in S$ and $\lambda \in [0,1]$

The set of all density matrices is convex. The set of separable states is a convex subset. Entangled states lie outside that subset. In geometric language, entanglement detection asks whether a given state lies inside or outside the separable body.

---

## The Peres-Horodecki Criterion — Partial Transpose Test

For $2\otimes2$ (two-qubit) and $2\otimes3$ (qubit-qutrit) systems, there is a necessary and sufficient condition for separability: the **partial transpose (PPT) criterion**.

- **Partial transpose on B:** for matrix elements $\rho_{ij,kl}$, map $\rho_{ij,kl} \to \rho_{ij,lk}$
- **All eigenvalues of $\rho^{T_B}$ >= 0:** state is **separable**
- **At least one negative eigenvalue of $\rho^{T_B}$:** state is **entangled**



> [!IMPORTANT]
> **Key Idea:** For two-qubit and qubit-qutrit systems, entanglement shows up as negativity under partial transpose.

Example — **Werner state**:

$$
ρW = (1−p)·I/4 + p·|Ψ⁻⟩⟨Ψ⁻|
$$
It is entangled iff $p > 1/3$.

---

## Concurrence — Quantifying Two-Qubit Entanglement

The Peres-Horodecki test answers *whether* a state is entangled. **Concurrence** answers *how much* entanglement it has.

- **Spin-flip operation:** $|\tilde\psi\rangle = (\sigma_y\otimes\sigma_y)|\psi^*\rangle$
- **Pure-state concurrence:**

$$
C(|ψ⟩) = |⟨ψ~|ψ⟩|
$$
For mixed state $\rho$, define

$$
R~ = (σy⊗σy)ρ*(σy⊗σy),   R = ρR~
$$
Let $\lambda_1 \ge \lambda_2 \ge \lambda_3 \ge \lambda_4$ be square roots of eigenvalues of $R$:

$$
C(ρ) = max(0, λ1 − λ2 − λ3 − λ4)
$$
For the Werner state:

$$
C(ρW) = max(0, (3p−1)/2)
$$
So $C=0$ for $p \le 1/3$, and $C\to1$ at $p=1$ (pure singlet).

- **Entanglement of formation:**

$$
E(ρ) = h((1+√(1−C²))/2)
$$
where $h(x) = -x\log x -(1-x)\log(1-x)$ is binary entropy.

---

# EPILOGUE: THE STORY CONTINUES

We began as a humble electron, spinning in some unknown direction. Over twelve weeks, we learned:

- That quantum states live on a Bloch sphere, manipulated by rotations generated by angular momentum.
- That density matrices are the right language for uncertainty — both quantum and classical.
- That information has a fundamental unit (the bit) and a fundamental limit (Shannon entropy).
- That entanglement is real, non-local, and experimentally confirmed to violate Bell inequalities.
- That entanglement can be used to teleport quantum states and double classical communication capacity.
- That the Quantum Fourier Transform enables Shor's algorithm to factor numbers exponentially faster than any classical computer.
- That real quantum systems lose their quantumness through decoherence, described by Kraus operators and the Lindblad equation.
- That entanglement in mixed states can be detected (Peres-Horodecki) and quantified (concurrence).

The story of quantum information is not finished. Quantum error correction, fault-tolerant computing, quantum key distribution, topological quantum computing — these are the chapters still being written. But with this foundation, you are now prepared to read them.

---

***— End of Course Notes —***
