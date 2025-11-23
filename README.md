
# Burger's Equation Simulation

# Project Overview
As a physics student, I built this project to understand **nonlinear physics** through the Burger's equation - a simplified version of the complex Navier-Stokes equation that captures essential fluid dynamics phenomena.
# Physics concept background
## from Navier-Stokes to Burgers equation.
The full Navier-Stokes equation:
∂v/∂t + (v·∇)v = -∇p/ρ + ν∇²v + F

Burgers equation simplifies this by removing:
1) **pressure term (-∇p/ρ)** - the velocity -pressure coupling.
2) **3D complexity** - Reduced to 1D for easiness and clarity.
3) **Body forces (F)** - No external forces .

And keeping the interesting parts:
1)** Nonlinear convection (u ∂u/∂x)** - self-interaction and wave steepening
2) **Viscous diffusion (ν ∂²u/∂x²)** - smoothing and energy dissipation
So we have Burgers equuation like this,
∂u/∂t + u ∂u/∂x = ν ∂²u/∂x²

### Physical Interpretation
- **u ∂u/∂x > 0**: Acceleration - faster fluid catches slower fluid
- **u ∂u/∂x < 0**: Deceleration - slower fluid holds back faster fluid 
-  **This nonlinearity creates shocks** - waves that steepen until they "break"

## What my code actually does

### Numerical Method
I implemented an **upwind finite difference scheme**:
 In python
#  Nonlinear convection - upwind scheme
if u[i] >= 0:
    conv = u[i] * (u[i] - u[i-1]) / dx  # Wave moving right
else:
    conv = u[i] * (u[i+1] - u[i]) / dx  # Wave moving left

Viscous diffusion
diff = (u[i+1] - 2*u[i] + u[i-1]) / (dx**2)
 Time evolution
u_new[i] = u[i] - dt * conv + dt * nu * diff
## key features in my implementation
1- Periodic boundary conditions:u(0,t) = u(L,t) - like a circular domain

CFL stability condition: Δt/Δx < 1 to prevent numerical explosions
Real-time animation: Watch shocks form and evolve
Parameter exploaration: study how viscosity changes the behaviour

## What i discovered through coding
Shock formation visualised 
Starting with a simple sine wave u = sin(2πx/L), I observed:
Wave steepening: The sine wave front gets steeper over time
Shock development: A discontinuity tries to form
Viscous balancing: Diffusion prevents infinite slopes
Energy dissipation: The wave amplitude decreases over time

The viscosity effects:
Low viscosity (ν = 0.001): Sharp shocks form quickly
High viscosity (ν = 0.1): Smooth evolution, no shocks
Medium viscosity (ν = 0.01): Balanced - you can see both effects

## How to Run the code
cd src/1d
python 1d_burgers_equation.py
 
## the code will:
1) Solve the Burgers equation numerically
2)Show an animation of shock formation
3)Display initial vs final state comparison
4) Let you explore different parameters interactively.

Interactive Exploration
 My code includes sliders to change:
viscosity(ν): From smooth diffusion to sharp shocks
Initial amplitude: How strong the initial wave is.
Simulation time: Watch short-term vs long-term behavior.

## sample results
From my simulations:
Initial smooth sine wave → develops steep front in ~0.5 seconds
Maximum gradient increases from ~3 to over 15 (shock strength).
Energy decays exponentially due to viscosity.

## time evolution series.
* smooth sine wave initial condition* ( t=0.0sec)
<img width="1000" height="600" alt="shock_formation_0 0sec" src="https://github.com/user-attachments/assets/69f8f425-7696-4c4f-a260-b2e7e4064cda" />

* wave begin to steepen *(early development t=0.5sec)
<img width="1000" height="600" alt="shock_formation_0 5sec" src="https://github.com/user-attachments/assets/ad91ae6a-c466-42d6-a4ef-980866d993c8" />

* clear shock front developing (shock formationt t=1.0sec)
<img width="1000" height="600" alt="shock_formation_1 0sec" src="https://github.com/user-attachments/assets/8c78e143-eee7-4e1a-944f-d57a6eb798b0" />

* mature shock with viscous balancing (fully developed t=2.0s)
<img width="1000" height="600" alt="shock_formation_2 0sec" src="https://github.com/user-attachments/assets/b9886bcf-26a8-490a-a5b1-22240a36e38c" />

* time evolution analysis
*Progression from initial sine wave to shock formation - showing wave steepening and viscous balancing over 2.0 seconds*
<img width="1189" height="490" alt="time_evolution" src="https://github.com/user-attachments/assets/cf814409-498f-45b8-bc98-52741dbd28ea" />

* Initial final comparison
 <img width="1189" height="390" alt="initial_final_comparison" src="https://github.com/user-attachments/assets/73cab568-300a-41fc-b527-24dcdac4c914" />
parison
  
  ## future extensions
as I learn more, I plan to;
Add different initial conditions (square waves, Gaussian pulses)
Implement spectral methods for higher accuracy
Study the inviscid limit (ν → 0) and shock theory
Extend to 2D Burgers equation

This project taught me that coding isn't just about programming - it's a new way to do physics experiments and develop intuition about complex systems.
Which I can learn by visualizing and changing the parameters my own to see the different results.


