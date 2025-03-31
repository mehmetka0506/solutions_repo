# Problem 1
# Investigating the Dynamics of a Forced Damped Pendulum
 
---
 
## 1.  Theoretical Background
 
A forced damped pendulum illustrates the dynamics of nonlinear oscillators. It models real systems where restoring forces, resistance (damping), and external periodic forces interact.
 
### Governing Equation
 
The general motion is described by:
 
$$
\frac{d^2\theta}{dt^2} + b\frac{d\theta}{dt} + \frac{g}{L} \sin(\theta) = A \cos(\omega t)
$$
 
Where:  
- $\theta$: angular position  
- $b$: damping constant  
- $g$: gravitational acceleration  
- $L$: pendulum length  
- $A$: driving force amplitude  
- $\omega$: driving force frequency  
 
---
 
### Full Derivation of the Equation
 
From Newton's second law for rotation:
 
$$
\sum \tau = I \cdot \alpha
$$
 
- $I = mL^2$ is the moment of inertia of the pendulum
- $\alpha = \frac{d^2\theta}{dt^2}$ is the angular acceleration
 
The torques are:
- Gravitational torque: $-mgL \sin(\theta)$  
- Damping torque: $-b \frac{d\theta}{dt}$  
- Driving torque: $A \cos(\omega t)$
 
Total torque:
 
$$
mL^2 \cdot \frac{d^2\theta}{dt^2} = -mgL \sin(\theta) - b \frac{d\theta}{dt} + A \cos(\omega t)
$$
 
Divide through by $mL^2$:
 
$$
\frac{d^2\theta}{dt^2} + \frac{b}{mL^2} \frac{d\theta}{dt} + \frac{g}{L} \sin(\theta) = \frac{A}{mL^2} \cos(\omega t)
$$
 
Let $b' = \frac{b}{mL^2}$ and $A' = \frac{A}{mL^2}$:
 
$$
\frac{d^2\theta}{dt^2} + b' \frac{d\theta}{dt} + \frac{g}{L} \sin(\theta) = A' \cos(\omega t)
$$
 
Or written in simplified form:
 
$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \sin(\theta) = A \cos(\omega t)
$$
 
---
 
### Linearized Approximation
 
Using the small-angle assumption ($\theta \approx 0$), the equation becomes:
 
$$
\frac{d^2\theta}{dt^2} + b\frac{d\theta}{dt} + \frac{g}{L} \theta = A \cos(\omega t)
$$
 
This approximation simplifies the problem to a linear, second-order non-homogeneous ODE, ideal for numerical simulation.
 
---
 
## 2.  Simulation in Python
 
We simulate three different pendulum conditions:
 
- A **frictionless simple pendulum**
- A **damped pendulum**
- A **driven pendulum with no damping**
 
### Python Code
 
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp
 
def pendulum_dynamics(t, y, b, g, L, A, omega):
    theta, omega_ = y
    dtheta_dt = omega_
    domega_dt = -b * omega_ - (g / L) * np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, domega_dt]
 
# Time setup
t_range = (0, 50)
t_points = np.linspace(*t_range, 1000)
initial_state = [0.2, 0.0]
 
# Pendulum setups
scenarios = [
    {"label": "1) Undamped", "b": 0.0, "A": 0.0, "color": "salmon"},
    {"label": "2) Damped", "b": 0.4, "A": 0.0, "color": "slateblue"},
    {"label": "3) Driven", "b": 0.0, "A": 1.0, "color": "mediumseagreen"},
]
 
# Constants
g = 9.8
L = 1.0
omega_drive = 2.0
 
# Plotting results
fig, axes = plt.subplots(len(scenarios), 2, figsize=(12, 10))
 
for i, scenario in enumerate(scenarios):
    sol = solve_ivp(
        pendulum_dynamics,
        t_range,
        initial_state,
        args=(scenario["b"], g, L, scenario["A"], omega_drive),
        t_eval=t_points
    )
    theta, omega_ = sol.y
    axes[i, 0].plot(sol.t, theta, color=scenario["color"])
    axes[i, 0].set_title(f'{scenario["label"]} - Time Evolution')
    axes[i, 0].set_xlabel("Time (s)")
    axes[i, 0].set_ylabel("Angle θ (rad)")
    axes[i, 0].grid(True)
 
    axes[i, 1].plot(theta, omega_, color=scenario["color"])
    axes[i, 1].set_title(f'{scenario["label"]} - Phase Space')
    axes[i, 1].set_xlabel("θ (rad)")
    axes[i, 1].set_ylabel("ω (rad/s)")
    axes[i, 1].grid(True)
 
plt.tight_layout()
plt.show()
```
 ![alt text](image.png)
 
---
 
## 3. Observations
 
**Undamped Case**  
- Angle oscillates periodically  
- Phase space shows perfect ellipses
 
**Damped Case**  
- Amplitude decays with time  
- Spiral phase plot confirms energy dissipation
 
**Driven Case**  
- Angle shows sustained oscillations  
- Phase diagram reveals complex periodic loops
 
---
 
## 4. Summary
 
This pendulum model shows how damping and external forces affect nonlinear oscillators. It lays the foundation for exploring chaos and resonance in later studies.
 
Possible extensions:
 
- Simulate chaotic regimes with stronger forcing  
- Visualize energy over time  
- Explore resonance phenomena and amplitude–frequency relationships

