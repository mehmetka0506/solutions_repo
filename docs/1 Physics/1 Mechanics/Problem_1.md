# Problem 1
# Investigating the Range as a Function of the Angle of Projection
## Motivation
Projectile motion, though seemingly simple, presents a deep and rich structure when examined thoroughly. By studying how the range of a projectile depends on the launch angle, we reveal fundamental principles of kinematics and dynamics. Variables like initial velocity, gravitational acceleration, and launch height provide a broad variety of solutions, applicable to real-world situations such as sports, engineering, and space science.

## Theoretical Foundation
Starting from the basic laws of motion, we can derive the projectile equations. Assume no air resistance and flat terrain.

Let:

$v_0$ = Initial velocity

$\theta$ = Angle of projection

$g$ = Gravitational acceleration

The equations of motion are:

𝑑
2
𝑥
𝑑
𝑡
2
=
0
⇒
𝑑
𝑥
𝑑
𝑡
=
𝑣
0
cos
⁡
(
𝜃
)
dt 
2
 
d 
2
 x
​
 =0⇒ 
dt
dx
​
 =v 
0
​
 cos(θ)
𝑑
2
𝑦
𝑑
𝑡
2
=
−
𝑔
⇒
𝑑
𝑦
𝑑
𝑡
=
𝑣
0
sin
⁡
(
𝜃
)
−
𝑔
𝑡
dt 
2
 
d 
2
 y
​
 =−g⇒ 
dt
dy
​
 =v 
0
​
 sin(θ)−gt
Integrating these:

𝑥
(
𝑡
)
=
𝑣
0
cos
⁡
(
𝜃
)
𝑡
x(t)=v 
0
​
 cos(θ)t
𝑦
(
𝑡
)
=
𝑣
0
sin
⁡
(
𝜃
)
𝑡
−
1
2
𝑔
𝑡
2
y(t)=v 0
​
 sin(θ)t− 
2
1
​
 gt 
2
 
Time of Flight
Setting $y=0$ at landing:

0
=
𝑣
0
sin
⁡
(
𝜃
)
𝑇
−
1
2
𝑔
𝑇
2
0=v 
0
​
 sin(θ)T− 
2
1
​
 gT 
2
 
Solving
𝑇=
2
𝑣
0
sin
⁡
(
𝜃
)
𝑔
T= 
g
2v 
0
​
 sin(θ)
​
 
Range
Horizontal distance covered:

𝑅=
𝑣
0
cos
⁡
(
𝜃
)
𝑇
=
𝑣
0
2
sin
⁡
(
2
𝜃
)
𝑔
R=v 
0
​
 cos(θ)T= 
g
v 
0
2
​
 sin(2θ)
​
 
Maximum Height

𝐻 =
𝑣
0
2
sin
⁡
2
(
𝜃
)
2
𝑔
H= 
2g
v 
0
2
​
 sin 
2
 (θ)
​
 
Analysis of the Range
From the range formula:

𝑅 =
𝑣
0
2
sin
⁡
(
2
𝜃
)
𝑔
R= 
g
v 
0
2
​
 sin(2θ)
​
 
## Observations
Maximum range occurs when $\sin(2\theta) = 1$, that is, $\theta = 45^\circ$

Symmetry: $R(\theta) = R(90^\circ - \theta)$

Effects of parameters
$v_0$: Range increases quadratically with initial velocity.

$g$: Range decreases inversely with gravitational acceleration.

Launch height: Would modify the symmetry and the optimal angle if included.

Practical Applications
Sports: Finding the best launch angles for throws, shots, or kicks.

Engineering: Ballistics calculations.

Astrophysics: Launching satellites or projectiles from planetary surfaces.

Including air resistance, wind, or launching from non-level terrain are real-world complications addressed with numerical methods.

## Implementation
Below are Python scripts simulating projectile motion under the given scenarios.
![alt text](image-4.png)
Scenario 1: 45° angle, different velocities (30, 40, 50 m/s)
python

import numpy as np
import matplotlib.pyplot as plt

def projectile(v0, angle_deg, g=9.81):
    angle_rad = np.radians(angle_deg)
    t_flight = 2 * v0 * np.sin(angle_rad) / g
    t = np.linspace(0, t_flight, num=500)
    x = v0 * np.cos(angle_rad) * t
    y = v0 * np.sin(angle_rad) * t - 0.5 * g * t**2
    return x, y

velocities = [30, 40, 50]
angle = 45

plt.figure(figsize=(10,6))
for v0 in velocities:
    x, y = projectile(v0, angle)
    plt.plot(x, y, label=f'$v_0$ = {v0} m/s')

plt.title("Projectile Motion at 45° with Different Velocities")
plt.xlabel("Horizontal Distance (m)")
plt.ylabel("Vertical Distance (m)")
plt.grid(True)
plt.legend()
plt.show()
Scenario 2: 50 m/s, different angles (15°, 45°, 75°)
python

angles = [15, 45, 75]
v0 = 50

plt.figure(figsize=(10,6))
for angle in angles:
    x, y = projectile(v0, angle)
    plt.plot(x, y, label=f'$\\theta$ = {angle}°')

plt.title("Projectile Motion at 50 m/s with Different Angles")
plt.xlabel("Horizontal Distance (m)")
plt.ylabel("Vertical Distance (m)")
plt.grid(True)
plt.legend()
plt.show()
Graphical Representations
In the first plot, as initial velocity increases, range increases significantly.
![alt text](image-3.png)
In the second plot, $45^\circ$ provides the maximum range, while $15^\circ$ and $75^\circ$ give the same (shorter) range.

## Limitations and Extensions
Limitations
No air resistance considered.

Flat launch and landing height assumed.

Extensions
Include air resistance: drag force proportional to velocity.

Launch from or land on elevated platforms.

Add wind effects.

## Summary
Analyzing projectile motion illustrates fundamental physics while also introducing opportunities for deeper exploration using computational methods. Studying range as a function of launch angle helps us understand both idealized and real-world trajectories.

## Colab Link
Colab - [Problem 1 Simulation](https://colab.research.google.com/drive/1yZDVYnCJ0oDE6Qy4iyeiyP3jnYpd3z0q?usp=sharing)