# Investigating the Range as a Function of the Angle of Projection

# Motivation

Projectile motion, though often introduced early in physics education, reveals a rich and complex structure when explored deeply. Understanding how the range of a projectile depends on its angle of projection opens a gateway to mastering core physics principles—especially kinematics and dynamics.

The horizontal range is not only influenced by the angle but also by several key parameters such as initial velocity, gravitational acceleration, and launch height. These parameters provide flexibility for the model to apply in diverse real-world scenarios, ranging from sports trajectories to orbital launches.

# 1. Theoretical Foundation

## Governing Equations

We begin with the basic kinematic equations for projectile motion. Assuming no air resistance and a flat launch/landing surface:

Let:

: initial velocity

: angle of projection

: gravitational acceleration

The horizontal and vertical components of the initial velocity are:



The time of flight is:



The horizontal range  becomes:



Observations:

Range is maximized when 

For a fixed  and , different angles yield different ranges

The symmetry: 

# 2. Analysis of the Range

Using the range formula:



This function peaks at  and exhibits a parabolic relationship.

Influence of Other Parameters

Initial Velocity: Range increases quadratically with 

Gravity: Inverse relationship — greater  reduces the range

Launch Height: Introduces an asymmetry and increases max range, but breaks analytical simplicity

# 3. Practical Applications

The basic model assumes flat terrain and no air resistance. However, real-world adaptations include:

Launching projectiles from elevated platforms

Factoring in wind resistance or drag forces ()

Non-uniform gravitational fields (e.g., planetary launches)

Such complexities are addressed through numerical simulation methods or empirical correction models.

# 4. Implementation (Python Simulation)

Below is a Python script that simulates and plots the range as a function of angle for various initial velocities.

import numpy as np
import matplotlib.pyplot as plt

def projectile_range(v0, g=9.81):
    angles_deg = np.linspace(0, 90, 500)
    angles_rad = np.radians(angles_deg)
    ranges = (v0**2) * np.sin(2 * angles_rad) / g
    return angles_deg, ranges

# Simulation for different velocities
velocities = [10, 20, 30]
plt.figure(figsize=(10, 6))

for v0 in velocities:
    angles, ranges = projectile_range(v0)
    plt.plot(angles, ranges, label=f'v0 = {v0} m/s')

plt.title("Range vs. Projection Angle")
plt.xlabel("Angle (degrees)")
plt.ylabel("Range (meters)")
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

# 5. Graphical Interpretation

The graph shows a clear peak at  for each velocity.

Higher initial velocities stretch the curve upward proportionally.

The symmetry confirms the theoretical relation 

# 6. Limitations & Extensions

## Limitations:

Ignores air resistance, which becomes significant at higher velocities

Assumes flat terrain and level launch/landing height

## Suggested Extensions:

Implement drag force (e.g., Euler’s method for )

Incorporate different terrains and elevation changes

Add wind components to assess horizontal deflection

# Summary

Projectile motion, especially range analysis, offers a clear and accessible way to apply physics and computational tools. Starting from a simple closed-form solution, we extend understanding using numerical simulations and graphical interpretations.

This problem links core physics, programming, and real-world phenomena in a way that highlights both the power and limitations of idealized models.

