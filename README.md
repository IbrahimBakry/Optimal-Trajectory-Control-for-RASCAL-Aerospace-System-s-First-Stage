# 🚀 **Optimal Trajectory Control for RASCAL Aerospace System’s First Stage**  

## **📌 Project Overview**  
**Objective**: Develop **optimal and nominal control programs** for the **first stage** of the RASCAL aerospace system during its **passive altitude climb phase**, ensuring maximum final velocity while meeting flight constraints.  

**Key Achievements**:  
✅ **Two control strategies** tested: *Nominal (step-based)* and *Optimal* (Pontryagin’s Maximum Principle + Interior-Point Method).  
✅ **MATLAB simulations** validated trajectories for a **26.8 km → 63.15 km climb** at Mach 3.8.  
✅ **Published research** on hypersonic dynamics and control optimization.  

---

## **🔧 Tools & Methods**  
| **Category**       | **Tools/Techniques**                     | **Purpose** |
|--------------------|------------------------------------------|-------------|
| **Modeling**       | 6-DOF equations, Standard Atmosphere (GOST 4401-81) | Flight dynamics, aerodynamics |
| **Optimization**   | Pontryagin’s Maximum Principle, Interior-Point NLP (MATLAB `fmincon`) | Trajectory optimization |
| **Numerical Methods** | Runge-Kutta ODE solver, Finite-difference collocation | Equation discretization |
| **Visualization**  | MATLAB Plotting                          | Trajectory and parameter graphs |

---

## **📐 Modeling & Numerical Solutions**  

### **1. 🛩️ Flight Dynamics Model**  
- **Equations of Motion**: Simplified 3-DOF system in trajectory coordinates:  
  - **Velocity (V)**: Affected by drag (`C_xa`) and gravity.  
  - **Flight Path Angle (θ)**: Controlled via lift (`C_ya`).  
  - **Altitude (h)**: Coupled with `V` and `θ`.  
- **Aerodynamics**:  
  - Parabolic drag polar: `C_xa = C_xa0(M) + A(M)·C_ya²`.  
  - Lift/drag coefficients interpolated from Mach-dependent data (Fig. 1.3).  

### **2. ⚙️ Control Strategies**  
#### **🔹 Nominal Control (Step Program)**  
- **Two-phase angle-of-attack (α) profile**:  
  - **Phase 1**: α = 10° (max lift for climb).  
  - **Phase 2**: α = 0° (min drag for speed).  
- **Results**: Achieved target altitude (63.15 km) and θ = 20° but **suboptimal final velocity** (Fig. 2.3–2.5).  

#### **🔹 Optimal Control (Pontryagin’s Principle)**  
- **Hamiltonian Minimization**:  
  - Costate variables (`ψ_V, ψ_θ, ψ_h`) for sensitivity analysis.  
  - Optimal `C_ya(t)` derived from `dH/dC_ya = 0` (Eq. 3.12).  
- **Constraints**: α ∈ [0°, 20°], `C_ya` bounds (Mach-dependent).  
- **Implementation**: Solved via **shooting method** with MATLAB ODE45.  

#### **🔹 Interior-Point Method (NLP)**  
- **Reformulated Problem**:  
  - Minimize `-V(t_f)` subject to dynamics + path constraints.  
  - Slack variables for inequality bounds (Eq. 3.3–3.4).  
- **Convergence**: Achieved in **<50 iterations** with adaptive μ-tuning.  

---

## **📊 Results & Validation**  
### **Optimal vs. Nominal Performance**  
| **Metric**          | **Nominal Control** | **Optimal Control** |  
|----------------------|---------------------|---------------------|  
| Final Velocity (m/s) | ~650                | **680** (target)    |  
| Fuel Efficiency      | Lower               | **Maximized**       |  
| Control Smoothness   | Step-discontinuous  | Continuous `C_ya(t)`|  

**Key Plots**:  
- Fig. 3.1: Optimal `α(t)` smoothly transitions to minimize drag.  
- Fig. 3.5: Costates (`ψ_V, ψ_θ, ψ_h`) validate optimality conditions.  

---

## **🎯 Key Insights**  
- **Optimal Control Advantage**: **5% higher final velocity** vs. nominal.  
- **Numerical Challenges**:  
  - **Stiff ODEs**: Addressed with adaptive step-sizing.  
  - **Initial Guess Sensitivity**: Mitigated via hybrid shooting-collocation.  
- **Future Work**: Real-time adaptive control for turbulence.  

---

## **📜 Publications**  
1. **"Optimization of Transatmospheric Flight Using Pontryagin’s Principle"** (Samara University Aerospace Journal, 2020).  

---

### **🚀 Why this project**  
This work bridges **theoretical optimal control** and **practical aerospace engineering**, enabling **fuel-efficient high-altitude climbs**—critical for reusable launch systems like RASCAL!  

