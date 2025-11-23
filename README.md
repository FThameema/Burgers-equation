# 🌀 Burger's Equation Simulation

## 📌 Project Overview
As a physics student, I built this project to understand **nonlinear physics** using the **Burgers equation** — a simplified version of the Navier–Stokes equation that still captures essential fluid-dynamics behavior such as **shock formation** and **viscous dissipation**.

---

## 🔬 Physics Background  
### From Navier–Stokes to Burgers Equation

The full Navier–Stokes equation is:

\\[
\\frac{\\partial \\mathbf{v}}{\\partial t} + (\\mathbf{v} \\cdot \\nabla)\\mathbf{v} = -\\frac{1}{\\rho} \\nabla p + \\nu \\nabla^2 \\mathbf{v} + \\mathbf{F}
\\]

Burgers equation simplifies this by removing:
1. **Pressure term** \\( -\\frac{1}{\\rho} \\nabla p \\) → removes velocity–pressure coupling  
2. **3D complexity** → reduced to **1D** for clarity  
3. **External body forces** \\( \\mathbf{F} \\)

Keeping the interesting nonlinear physics:
- **Nonlinear convection:** \\( u \\frac{\\partial u}{\\partial x} \\)
- **Viscous diffusion:** \\( \\nu \\frac{\\partial^2 u}{\\partial x^2} \\)

The resulting **1D viscous Burgers equation**:

\\[
\\frac{\\partial u}{\\partial t} + u \\frac{\\partial u}{\\partial x} = \\nu \\frac{\\partial^2 u}{\\partial x^2}
\\]

---

### 🧠 Physical Interpretation
- \\( u \\frac{\\partial u}{\\partial x} > 0 \\) → **acceleration** (fast fluid catches slower fluid)
- \\( u \\frac{\\partial u}{\\partial x} < 0 \\) → **deceleration** (slow fluid holds faster fluid back)
- The **nonlinearity creates shock waves** → steep fronts that form over time

---

## 💻 What the Code Does

### Numerical Method
I implemented an **upwind finite difference scheme** for convection and a centered scheme for diffusion.

**Nonlinear convection — upwind selection:**
\\[
\\text{if } u_i \\ge 0: \\quad \\text{conv} = u_i \\frac{u_i - u_{i-1}}{dx}
\\]
\\[
\\text{else}: \\quad \\text{conv} = u_i \\frac{u_{i+1} - u_i}{dx}
\\]

**Viscous diffusion:**
\\[
\\text{diff} = \\frac{u_{i+1} - 2u_i + u_{i-1}}{dx^2}
\\]

**Time evolution:**
\\[
u_i^{\\text{new}} = u_i - dt \\cdot \\text{conv} + dt \\cdot \\nu \\cdot \\text{diff}
\\]

---

### 🔑 Key Features
- **Periodic boundary conditions:** \\( u(0, t) = u(L, t) \\)
- **CFL stability condition enforced:** \\( \\frac{dt}{dx} < 1 \\)
- **Real-time animation of shock formation**
- **Interactive parameter exploration**

---

## 🔍 What I Observed
Starting with the initial condition:

\\[
u(x,0) = \\sin\\left(\\frac{2\\pi x}{L}\\right)
\\]

I observed:
- **Wave steepening** → sine wave develops a sharp front  
- **Shock development** (in low viscosity)  
- **Viscous smoothing** prevents infinite gradients  
- **Energy decays over time due to viscosity**

Viscosity effects:
| Viscosity \\(\\nu\\) | Behavior |
|---|---|
| 0.001 | Sharp shocks form rapidly |
| 0.01 | Balanced competition — shock + dissipation |
| 0.1 | Fully smooth diffusion, no shocks |

---

## ▶️ How to Run
```bash
cd src/1d
python 1d_burgers_equation.py
```
