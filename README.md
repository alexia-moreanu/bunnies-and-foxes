# 🐰🦊 Predator–Prey Ecosystem Simulation  

---

## 📌 Overview

This project implements and analyzes a spatial predator–prey ecosystem using a 2D grid-based simulation. The model captures:

- Nonlinear population dynamics  
- Spatial diffusion  
- Stochastic extinction events  
- Phase transitions (extinction ↔ coexistence)  
- Oscillatory dynamics  

The project combines:

- Mathematical modeling  
- Numerical simulation  
- Parameter sweeps & empirical analysis  
- Mean-field theoretical derivation  
- Data visualization & reproducible experimentation  

---

## 🧠 Model Description

The system models two species on an \( N \times N \) grid:

- **Bunnies (prey)**
- **Foxes (predators)**

Each grid cell stores local population density.

At each timestep, the model applies:

### 1️⃣ Logistic Bunny Growth

\[
B_{t+1} = B_t (1 + g_b (1 - B_t / k_b))
\]

Prevents unbounded growth by incorporating carrying capacity.

---

### 2️⃣ Diffusion (4-neighbor, periodic boundaries)

A fraction of the population redistributes to neighboring cells using vectorized `np.roll`.

Both species use the **same diffusion rule** to isolate the effect of relative mobility rather than asymmetric movement mechanisms.

---

### 3️⃣ Predation

\[
b_{\text{hunted}} = \min(B, c_f F)
\]

Fox survival depends on food availability.

---

### 4️⃣ Fox Reproduction + Stochastic Mortality

- Growth proportional to food intake  
- Cell-level wipeout with probability \( m_f \)

This introduces stochastic extinction near critical thresholds.

---

## 💻 Technical Implementation

### Tools Used

- **Python**
- **NumPy** (fully vectorized grid updates)
- **Matplotlib** (plots + animation)
- Reproducible random seeds

### Design Choices

- No nested loops — fully vectorized updates
- Periodic boundaries via `np.roll`
- Clear separation of:
  - Transient phase
  - Stationary window
- Automated parameter sweeps
- Replicate runs for statistical robustness

---

## 📊 Empirical Analysis (Task 2)

### 1️⃣ System Viability — Fox Growth Rate \( g_f \)

- Swept \( g_f \)
- Computed stationary means after removing transients
- Averaged across replicates
- Estimated survival probability

**Key Result:**  
There exists a critical extinction threshold.  
Below a critical \( g_f \), foxes cannot compensate for mortality → extinction.  
Above it, coexistence emerges.

---

### 2️⃣ Pattern Formation — Diffusion Ratio \( d_b / d_f \)

- Varied relative mobility
- Compared stationary densities and spatial snapshots

**Key Result:**  
Relative diffusion shapes spatial structure:

- Balanced diffusion → patch formation  
- High asymmetry → spatial mismatch  
- Strong mobility differences weaken clustering  

Behavior resembles reaction–diffusion systems discussed in class.

---

### 3️⃣ Stability — Bunny Growth Rate \( g_b \)

- Swept \( g_b \)
- Measured stationary means
- Quantified oscillation strength (standard deviation)

**Key Result:**  
Increasing prey growth amplifies nonlinear feedback:

- Larger oscillations  
- Stronger predator–prey cycles  
- No sharp extinction transition  

---

## 📐 Theoretical Analysis (Task 3)

Using a mean-field approximation (spatially homogeneous assumption), I derived a predicted extinction threshold:

\[
(1 - m_f)(1 + g_f) = 1
\]

\[
g_f = \frac{m_f}{1 - m_f}
\]

Simulation results show a higher threshold due to:

- Spatial clustering  
- Diffusion-induced predator–prey mismatch  
- Stochastic local wipeouts  

This demonstrates limitations of mean-field models in spatial stochastic systems.

---

## 🎥 Outputs Included

- Grid snapshots under multiple diffusion regimes  
- Validation time-series plots  
- Parameter sweep figures  
- Survival probability curves  
- Oscillation strength analysis  
- Theory vs simulation comparison  
- Animated GIF of ecosystem dynamics  
- Full PDF report with derivations  

---

## 🧩 Skills Demonstrated

- Dynamical systems modeling  
- Grid-based simulation design  
- Vectorized numerical computation  
- Parameter sweep automation  
- Statistical estimation (stationary windows, replicates)  
- Visualization & interpretation  
- Debugging & performance optimization  
- Bridging theory and empirical results  

---

## 🔁 Reproducibility

All experiments:

- Use fixed random seeds  
- Separate transient vs stationary phases  
- Compute replicate averages when appropriate  

Ensures statistically meaningful and reproducible results.

---

## 🚀 Key Takeaway

Simple local nonlinear rules combined with diffusion and stochasticity generate:

- Phase transitions  
- Spatial self-organization  
- Oscillatory dynamics  
- Deviations from theoretical mean-field predictions  

This project demonstrates how mathematical theory, simulation, and data analysis work together to understand complex systems.

---
