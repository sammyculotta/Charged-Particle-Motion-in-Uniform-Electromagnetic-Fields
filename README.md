# Charged Particle Motion in Electromagnetic Fields

## Overview

This project simulates the motion of a charged particle in uniform electric and magnetic fields using the **velocity Verlet integration method**. The simulation numerically solves the classical equations of motion derived from the **Lorentz force law**, allowing one to study trajectories such as linear acceleration, circular motion, and helical motion depending on the applied fields.

The code is written in **Python** using **NumPy** and is designed to be modular, readable, and easily extensible to more general field configurations.

---

## Physics Background

The motion of a charged particle with charge \( q \) and mass \( m \) in electric and magnetic fields is governed by the **Lorentz force**:

\[
\mathbf{F} = q \left( \mathbf{E} + \mathbf{v} \times \mathbf{B} \right)
\]

Using Newton’s second law,

\[
\mathbf{a} = \frac{\mathbf{F}}{m} = \frac{q}{m} \left( \mathbf{E} + \mathbf{v} \times \mathbf{B} \right)
\]

### Key Physical Behaviors

- **Electric field acceleration**  
  A uniform electric field accelerates the particle along the field direction.

- **Magnetic field deflection**  
  A uniform magnetic field produces circular motion perpendicular to the field due to the velocity-dependent cross product.

- **Helical trajectories**  
  When the velocity has components both parallel and perpendicular to the magnetic field, the resulting motion is helical.

---

## Numerical Method: Velocity Verlet Integration

The equations of motion are integrated using the **velocity Verlet method**, a second-order, time-reversible algorithm commonly used in computational physics.

### Advantages of Velocity Verlet

- Second-order accuracy in time
- Good energy conservation properties
- Widely used in plasma physics and molecular dynamics

### Update Scheme

**Position update:**

\[
\mathbf{r}_{n+1} = \mathbf{r}_n + \mathbf{v}_n \Delta t + \frac{1}{2}\mathbf{a}_n \Delta t^2
\]

**Acceleration update:**

The new acceleration is computed using the updated position and velocity-dependent fields.

**Velocity update:**

\[
\mathbf{v}_{n+1} = \mathbf{v}_n + \frac{1}{2}\left( \mathbf{a}_n + \mathbf{a}_{n+1} \right)\Delta t
\]

---

## Code Structure

### Field Definitions

    def electric_field(t, r):
        return np.array([E0, 0.0, 0.0])

    def magnetic_field(t, r):
        return np.array([0.0, 0.0, B0])

These functions define uniform electric and magnetic fields and are written to allow easy replacement with time- or position-dependent field configurations.

---

### Particle Class

    class Particle:
        def __init__(self, q, m, r0, v0):
            ...

Encapsulates particle properties (charge, mass, position, velocity) and computes the acceleration using the Lorentz force.

---

### Integrator

    velocity_verlet(particle, E_func, B_func, dt, t)

Performs a single integration step using the velocity Verlet algorithm.

---

### Simulation Driver

    run_simulation(particle, dt, t_max)

Runs the time evolution loop and stores position and velocity histories for analysis and visualization.

---

## Key Takeaways

- Demonstrates how classical electromagnetism translates into computable equations of motion.
- Shows the practical implementation of a **symplectic integration method** used in plasma and particle simulations.
- Highlights the importance of numerical stability and time-stepping in long-term simulations.
- Provides a modular framework that can be extended to:
  - Non-uniform fields
  - Multiple particles
  - Relativistic corrections
  - Visualization and phase-space analysis

---

## Possible Extensions

- Replace uniform fields with spatially varying fields
- Add energy and momentum diagnostics
- Compare velocity Verlet with Boris or Runge–Kutta integrators
- Extend to many-body or plasma simulations
