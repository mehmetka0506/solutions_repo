# Problem 2
#  Dynamics of a Forced Damped Pendulum: A Computational Exploration
 
---
 
##  Motivation

The forced damped pendulum is a key system in nonlinear dynamics. When damping and external periodic forces act on a pendulum, its behavior ranges from predictable oscillations to complex and chaotic motion. This diversity reflects many real-world systems — from electronics to biomechanics.
 
By tuning parameters like the damping factor and the strength and frequency of the driving force, we observe phenomena such as resonance, quasiperiodicity, and transitions to chaos. These insights are fundamental in understanding oscillatory systems in engineering, physics, and nature.
 
---
 
## 1.  Mathematical Framework
 
###  Differential Equation
 
The system is modeled by the second-order nonlinear ODE:
 
$$
\frac{d^2\theta}{dt^2} + b\frac{d\theta}{dt} + \frac{g}{L}\sin\theta = A\cos(\omega t)
$$
 
Where:
- $\theta$: angular displacement  
- $b$: damping coefficient  
- $g$: gravitational acceleration  
- $L$: length of pendulum  
- $A$: external driving amplitude  
- $\omega$: angular frequency of the driving force
 
---
 
###  Linear Approximation (Small Angle)
 
For small angular displacements:
 
$$
\sin\theta \approx \theta
$$
 
Reducing the equation to:
 
$$
\frac{d^2\theta}{dt^2} + b\frac{d\theta}{dt} + \frac{g}{L}\theta = A\cos(\omega t)
$$
 
This linear form simplifies simulation and helps analyze regular behavior before chaos emerges.
 
---
 
## 2.  Parameter-Based Behavior Analysis
 
We analyze system behavior by varying:
 
- Damping coefficient $b$
- Driving amplitude $A$
- Driving frequency $\omega$
 
This helps reveal:
- Transition from underdamped to overdamped behavior
- Resonance and amplification
- Onset of chaotic regimes
 
---
 
## 3.  Real-World Relevance
 
This model describes:
- Suspension systems in vehicles  
- Oscillating electrical circuits (e.g., RLC)  
- Structures under periodic stress  
- Biological movement patterns (gait dynamics)
 
---
 
## 4.  Python Modeling
 
Below is a simulation using `solve_ivp` from `scipy.integrate` to model pendulum behavior for different conditions.
 
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp
 
def dynamics(t, y, b, g, L, A, omega):
    theta, omega_ = y
    return [omega_, -b * omega_ - (g / L) * np.sin(theta) + A * np.cos(omega * t)]
 
# Setup
y0 = [0.15, 0.0]
t_range = (0, 60)
t_eval = np.linspace(*t_range, 1500)
 
cases = [
    {"label": "Light Damping", "b": 0.1, "A": 0.8, "omega": 1.0, "color": "royalblue"},
    {"label": "Critical Damping", "b": 0.6, "A": 0.8, "omega": 1.0, "color": "firebrick"},
    {"label": "High Drive", "b": 0.3, "A": 1.8, "omega": 3.0, "color": "darkgreen"},
]
 
g = 9.8
L = 1.0
 
fig, axes = plt.subplots(len(cases), 2, figsize=(12, 11))
 
for i, c in enumerate(cases):
    sol = solve_ivp(
        dynamics,
        t_range,
        y0,
        args=(c["b"], g, L, c["A"], c["omega"]),
        t_eval=t_eval
    )
    theta, omega_ = sol.y
 
    axes[i, 0].plot(sol.t, theta, color=c["color"])
    axes[i, 0].set_title(f'{c["label"]} - θ(t)')
    axes[i, 0].set_xlabel("Time (s)")
    axes[i, 0].set_ylabel("θ (rad)")
    axes[i, 0].grid()
 
    axes[i, 1].plot(theta, omega_, color=c["color"])
    axes[i, 1].set_title(f'{c["label"]} - Phase Diagram')
    axes[i, 1].set_xlabel("θ (rad)")
    axes[i, 1].set_ylabel("ω (rad/s)")
    axes[i, 1].grid()
 
plt.tight_layout()
plt.show()
```
![image](https://github.com/user-attachments/assets/7c49c8ad-31f7-47f3-8431-5cf4a0b96882)
![image](https://github.com/user-attachments/assets/21f9dd1c-4d9a-4452-800a-206e8719a3af)

 
---
 
## 5.  Simulation Outcomes
 
**Light Damping**  
- Oscillations persist  
- Phase plot shows large elliptical orbits
 
**Critical Damping**  
- Motion stabilizes quickly  
- System returns to equilibrium smoothly
 
**High Drive**  
- Complex motion develops  
- Phase space suggests early chaos
 
---
 
## 6.  Summary and Future Work
 
This experiment demonstrates how driven damped pendulums can show both stability and complexity, depending on parameters.
 
**Possible extensions:**
- Generate bifurcation diagrams for varying $\omega$
- Add nonlinear damping
- Analyze long-term chaos with Poincaré maps
 
These tools help bridge theory with systems seen in engineering, nature, and modern physics.
