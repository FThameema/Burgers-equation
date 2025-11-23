# Burger's Equation Simulation

## Project Overview
As a physics student, I built this project to understand **nonlinear physics** through the Burger's equation - a simplified version of the complex Navier-Stokes equation that captures essential fluid dynamics phenomena.

## Physics concept background
### from Navier-Stokes to Burgers equation.
The full Navier-Stokes equation:

$$\frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \nabla)\mathbf{v} = -\frac{\nabla p}{\rho} + \nu\nabla^2\mathbf{v} + \mathbf{F}$$

Burgers equation simplifies this by removing:
1) **pressure term** $(-\nabla p/\rho)$ - the velocity-pressure coupling.
2) **3D complexity** - Reduced to 1D for easiness and clarity.
3) **Body forces** $(F)$ - No external forces.

And keeping the interesting parts:
1) **Nonlinear convection** $(u \frac{\partial u}{\partial x})$ - self-interaction and wave steepening
2) **Viscous diffusion** $(\nu \frac{\partial^2 u}{\partial x^2})$ - smoothing and energy dissipation

So we have Burgers equation like this:

$$\frac{\partial u}{\partial t} + u \frac{\partial u}{\partial x} = \nu \frac{\partial^2 u}{\partial x^2}$$

### Physical Interpretation
- **$u \frac{\partial u}{\partial x} > 0$**: Acceleration - faster fluid catches slower fluid
- **$u \frac{\partial u}{\partial x} < 0$**: Deceleration - slower fluid holds back faster fluid 
- **This nonlinearity creates shocks** - waves that steepen until they "break"

## What my code actually does

### Numerical Method
I implemented an **upwind finite difference scheme**:

```python
# Nonlinear convection - upwind scheme
if u[i] >= 0:
    conv = u[i] * (u[i] - u[i-1]) / dx  # Wave moving right
else:
    conv = u[i] * (u[i+1] - u[i]) / dx  # Wave moving left

# Viscous diffusion
diff = (u[i+1] - 2*u[i] + u[i-1]) / (dx**2)

# Time evolution
u_new[i] = u[i] - dt * conv + dt * nu * diff
```

## key features in my implementation
1. **Periodic boundary conditions**: $u(0,t) = u(L,t)$ - like a circular domain
2. **CFL stability condition**: $\Delta t/\Delta x < 1$ to prevent numerical explosions
3. **Real-time animation**: Watch shocks form and evolve
4. **Parameter exploration**: study how viscosity changes the behaviour

## What i discovered through coding
### Shock formation visualised 
Starting with a simple sine wave $u = \sin(2\pi x/L)$, I observed:
- **Wave steepening**: The sine wave front gets steeper over time
- **Shock development**: A discontinuity tries to form
- **Viscous balancing**: Diffusion prevents infinite slopes
- **Energy dissipation**: The wave amplitude decreases over time

### The viscosity effects:
- **Low viscosity** $(\nu = 0.001)$: Sharp shocks form quickly
- **High viscosity** $(\nu = 0.1)$: Smooth evolution, no shocks
- **Medium viscosity** $(\nu = 0.01)$: Balanced - you can see both effects

## How to Run the code
```bash
cd src/1d
python 1d_burgers_equation.py
```
 
## the code will:
1) Solve the Burgers equation numerically
2) Show an animation of shock formation
3) Display initial vs final state comparison
4) Let you explore different parameters interactively.

### Interactive Exploration
My code includes sliders to change:
- **viscosity** $(\nu)$: From smooth diffusion to sharp shocks
- **Initial amplitude**: How strong the initial wave is.
- **Simulation time**: Watch short-term vs long-term behavior.

## sample results
From my simulations:
- Initial smooth sine wave → develops steep front in ~0.5 seconds
- Maximum gradient increases from ~3 to over 15 (shock strength).
- Energy decays exponentially due to viscosity.

## future extensions
as I learn more, I plan to:
- Add different initial conditions (square waves, Gaussian pulses)
- Implement spectral methods for higher accuracy
- Study the inviscid limit $(\nu \to 0)$ and shock theory
- Extend to 2D Burgers equation

This project taught me that coding isn't just about programming - it's a new way to do physics experiments and develop intuition about complex systems.
Which I can learn by visualizing and changing the parameters my own to see the different results.
