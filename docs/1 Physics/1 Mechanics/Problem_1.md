# Problem 1
# Projectile Motion Analysis

import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # gravitational acceleration (m/s^2)

# Function to calculate range of projectile
def calculate_range(v0, theta_deg):
    theta_rad = np.radians(theta_deg)
    return (v0**2 * np.sin(2 * theta_rad)) / g

# Generate range vs angle plot
def plot_range_vs_angle(v0_values):
    angles = np.linspace(0, 90, 500)
    plt.figure(figsize=(10, 6))

    for v0 in v0_values:
        ranges = calculate_range(v0, angles)
        plt.plot(angles, ranges, label=f'v0 = {v0} m/s')

    plt.title('Range vs Angle of Projection')
    plt.xlabel('Angle (degrees)')
    plt.ylabel('Range (m)')
    plt.legend()
    plt.grid(True)
    plt.show()

# Example usage
v0_samples = [10, 20, 30]  # initial velocities in m/s
plot_range_vs_angle(v0_samples)

# Theoretical Analysis Description (Markdown style)
"""
## Theoretical Foundation

The motion of a projectile launched with initial velocity `v0` at an angle `theta` to the horizontal is governed by Newton's laws.

Decomposing the motion:
- Horizontal: x(t) = v0 * cos(theta) * t
- Vertical: y(t) = v0 * sin(theta) * t - (1/2) * g * t^2

Solving for time of flight T (when y = 0):
T = 2 * v0 * sin(theta) / g

Range R:
R = v0 * cos(theta) * T = (v0^2 * sin(2 * theta)) / g

This formula assumes flat ground and no air resistance.

## Analysis of Range

- The range is maximized at 45° for given `v0` and constant `g`.
- Increasing `v0` increases the range quadratically.
- On different planets (different `g`), the trajectory varies accordingly.

## Practical Applications

- Sports: optimizing angles for long throws or jumps.
- Military: artillery range prediction.
- Space: analyzing launch trajectories.

## Limitations & Extensions

- Ignores air resistance: can be modeled with differential equations including drag force.
- Assumes level ground: terrain elevation changes require numerical solutions.

## Future Improvements

- Include wind and drag.
- Model projectile launched from varying heights.
- Use Runge-Kutta methods for precise trajectory paths.
"""

