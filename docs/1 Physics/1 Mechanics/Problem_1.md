# Projectile Motion - Range vs Launch Angle
# -----------------------------------------

# 1. Libraries
import numpy as np
import matplotlib.pyplot as plt

# 2. Basic Physics Functions
def projectile_range(v0, angle_deg, g=9.81):
    """
    Calculate the range of a projectile launched with initial velocity v0 at angle (degrees).
    
    Parameters:
    - v0: Initial velocity (m/s)
    - angle_deg: Launch angle in degrees
    - g: Acceleration due to gravity (m/s²)
    
    Returns:
    - Horizontal range (meters)
    """
    angle_rad = np.radians(angle_deg)
    return (v0**2 * np.sin(2 * angle_rad)) / g

def projectile_range_with_height(v0, angle_deg, h, g=9.81):
    """
    Calculate range for projectile launched from height h.
    
    Parameters:
    - v0: Initial velocity (m/s)
    - angle_deg: Launch angle in degrees
    - h: Initial height (m)
    - g: Gravity (m/s²)
    
    Returns:
    - Range (m)
    """
    angle_rad = np.radians(angle_deg)
    t_flight = (v0 * np.sin(angle_rad) + 
                np.sqrt((v0 * np.sin(angle_rad))**2 + 2 * g * h)) / g
    return v0 * np.cos(angle_rad) * t_flight

# 3. Plotting Function
def plot_ranges(v0, h=0, g=9.81):
    """
    Plot range of projectile for different launch angles.
    
    Parameters:
    - v0: Initial velocity (m/s)
    - h: Launch height (m), default is 0
    - g: Gravity (m/s²)
    """
    angles = np.linspace(0, 90, 200)
    
    if h == 0:
        ranges = [projectile_range(v0, angle, g) for angle in angles]
        label = "Ground Launch"
    else:
        ranges = [projectile_range_with_height(v0, angle, h, g) for angle in angles]
        label = f"Launch from height {h} m"
        
    plt.figure(figsize=(10, 5))
    plt.plot(angles, ranges, label=f'{label}, v₀ = {v0} m/s', color='darkblue')
    plt.axvline(45, color='red', linestyle='--', label='θ = 45° (Max Range)')
    plt.xlabel("Launch Angle (degrees)")
    plt.ylabel("Range (meters)")
    plt.title("Projectile Range vs Launch Angle")
    plt.legend()
    plt.grid(True)
    plt.show()

# 4. Simulation Parameters
initial_velocity = 20   # m/s
launch_height = 0       # m (set to nonzero for elevated launch)

# 5. Run Plot
plot_ranges(initial_velocity, h=launch_height)
