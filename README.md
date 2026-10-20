# Black-hole-simulator
A Python black hole particle simulator with numerical validation, interactive visualization, and a relativistic extension.
# 🌌 EVENT HORIZON — Black Hole Simulator

## Overview

EVENT HORIZON is a Python-based educational simulation that explores how particles move around a massive central object under the influence of gravity.

The project combines orbital mechanics, numerical integration, and scientific visualization to create an animated black hole-inspired environment with particle trajectories and a glowing accretion-disk effect.

It runs in Google Colab using free Python libraries, without paid APIs or specialized hardware.

## Features

- Simulates particle motion under Newtonian gravitational acceleration.
- Initializes particles with approximately circular orbital velocities.
- Calculates particle trajectories using the fourth-order Runge–Kutta (RK4) numerical integration method.
- Visualizes particle orbits and an animated accretion-disk-inspired environment.
- Calculates the Schwarzschild radius as a reference for the central black hole.
- Uses a simplified particle-capture boundary.
- Tests numerical accuracy through a circular-orbit energy-conservation experiment.

## Technology Stack

- Python
- NumPy
- Matplotlib
- IPython
- Google Colab
- Git and GitHub

All core dependencies are available free of charge.

---

## Scientific Laws and Mathematical Equations

This project uses classical mechanics and numerical methods to calculate particle motion. It also uses a relativistic black hole equation to establish the Schwarzschild radius.

### 1. Newton's Law of Universal Gravitation

Newton's law describes the gravitational attraction between two masses.

**Equation:**

$$
F = \frac{GMm}{r^2}
$$

Where:

- \(F\) = gravitational force
- \(G\) = universal gravitational constant
- \(M\) = mass of the central object
- \(m\) = mass of the particle
- \(r\) = distance between their centers

**Explanation:**

The gravitational force increases as the distance between objects decreases. This attraction causes particles to change their direction and speed as they move around the central mass.

**Application in the project:**

The simulation calculates gravitational acceleration from the particle's current position at every integration step.

### 2. Newton's Second Law of Motion

Newton's second law relates force to mass and acceleration.

**Equation:**

$$
F = ma
$$

Where:

- \(F\) = net force
- \(m\) = particle mass
- \(a\) = particle acceleration

Combining Newton's second law with the law of universal gravitation gives the acceleration of a particle due to the central mass.

**Vector equation used in the simulation:**

$$
\mathbf{a} = -\frac{GM}{r^3}\mathbf{r}
$$

Where:

- \(\mathbf{a}\) = gravitational acceleration vector
- \(\mathbf{r}\) = position vector relative to the central mass
- \(r = |\mathbf{r}|\) = distance from the center

The negative sign indicates that the acceleration points toward the central object.

**Application in the project:**

This equation is the foundation of the gravity engine. It determines how the velocity and position of every active particle change over time.

### 3. Circular Orbital Velocity

For a particle in a circular Newtonian orbit, gravitational acceleration supplies the required centripetal acceleration.

**Equation:**

$$
\frac{GM}{r^2} = \frac{v^2}{r}
$$

Rearranging gives the circular orbital velocity:

$$
v = \sqrt{\frac{GM}{r}}
$$

Where:

- \(v\) = orbital speed
- \(G\) = gravitational constant
- \(M\) = central mass
- \(r\) = orbital radius

**Explanation:**

A particle needs an appropriate tangential velocity to maintain a circular orbit. In the Newtonian model, particles closer to the central mass require higher circular orbital speeds.

**Application in the project:**

This equation initializes the particles with approximately circular velocities before the simulation begins. Small velocity variations create a range of orbital behaviors.

### 4. Schwarzschild Radius

The Schwarzschild radius is the event-horizon radius of an idealized, non-rotating, uncharged black hole, according to general relativity.

**Equation:**

$$
r_s = \frac{2GM}{c^2}
$$

Where:

- \(r_s\) = Schwarzschild radius
- \(G\) = gravitational constant
- \(M\) = black hole mass
- \(c\) = speed of light

**Explanation:**

The Schwarzschild radius defines the boundary of the event horizon in the idealized Schwarzschild solution. Once an object crosses the event horizon inward, it cannot send a signal back out to a distant observer.

**Application in the project:**

The program calculates the Schwarzschild radius and uses it as a reference for the central black hole's visual boundary.

**Important limitation:** The current particle trajectories are calculated using Newtonian gravity, not the full equations of general relativity. The Schwarzschild radius is therefore a relativistic reference scale rather than proof that the simulated motion is relativistically accurate.

### 5. Conservation of Mechanical Energy

For a particle moving under Newtonian gravity without non-conservative forces, its total mechanical energy remains constant.

The specific mechanical energy, measured per unit mass, is:

$$
E = \frac{v^2}{2} - \frac{GM}{r}
$$

Where:

- \(E\) = specific mechanical energy
- \(v\) = particle speed
- \(G\) = gravitational constant
- \(M\) = central mass
- \(r\) = distance from the central mass

The first term represents kinetic energy per unit mass, while the second represents gravitational potential energy per unit mass.

For a circular Newtonian orbit:

$$
E = -\frac{GM}{2r}
$$

**Explanation:**

As a particle moves through an ideal gravitational orbit, its kinetic and potential energies can change while their sum remains constant.

**Application in the project:**

The simulation runs an independent circular-orbit test and measures how much the calculated energy changes during numerical integration. This helps evaluate the accuracy of the integration method.

The validation test returned:

- Initial specific energy: approximately \(-0.08333333\)
- Maximum relative energy error: approximately \(7.161 \times 10^{-15}\)

These results indicate excellent energy conservation for the tested orbit and timestep. They do not establish the physical accuracy of every aspect of the black hole visualization.

### 6. Fourth-Order Runge–Kutta Method (RK4)

RK4 is a numerical integration method used to approximate solutions to differential equations. It is not a physical law.

For a differential equation

$$
\frac{dy}{dt} = f(t,y)
$$

the classical RK4 method calculates four intermediate slope estimates:

$$
k_1 = f(t_n,y_n)
$$

$$
k_2 = f\left(t_n+\frac{h}{2},
y_n+\frac{hk_1}{2}\right)
$$

$$
k_3 = f\left(t_n+\frac{h}{2},
y_n+\frac{hk_2}{2}\right)
$$

$$
k_4 = f(t_n+h,y_n+hk_3)
$$

It then updates the solution using:

$$
y_{n+1}=y_n+\frac{h}{6}
(k_1+2k_2+2k_3+k_4)
$$

Where:

- \(y_n\) = current state
- \(h\) = timestep
- \(k_1,k_2,k_3,k_4\) = intermediate derivative estimates
- \(y_{n+1}\) = estimated next state

**Explanation:**

Instead of using only one estimate of the particle's motion, RK4 evaluates four intermediate slopes and combines them to calculate the next state more accurately.

**Application in the project:**

RK4 advances particle positions and velocities through time using the gravitational acceleration calculated by the physics engine.

### 7. Numerical Error and Validation

Numerical simulations approximate continuous motion using finite timesteps. Consequently, small numerical errors can occur.

The relative energy error used in the validation test is:

$$
\epsilon =
\frac{\max_t |E(t)-E(0)|}{|E(0)|}
$$

Where:

- \(\epsilon\) = maximum relative energy deviation
- \(E(t)\) = calculated specific energy at time \(t\)
- \(E(0)\) = initial specific energy

**Explanation:**

This metric measures the largest deviation from the initial energy during the test. A smaller value indicates better energy conservation over the tested interval.

**Application in the project:**

The validation experiment checks whether the RK4 implementation reproduces the expected behavior of a circular Newtonian orbit.

This is a numerical accuracy check, not an independent physical law.

---

## Model Assumptions and Limitations

EVENT HORIZON is an educational Newtonian particle simulation inspired by black hole astrophysics. It is not a complete relativistic black hole model.

- Particle motion is calculated using Newtonian gravity.
- The Schwarzschild radius is calculated using a general-relativistic equation.
- A simplified capture boundary is used to remove particles that cross the chosen threshold.
- The accretion-disk glow is a visual effect rather than a radiative-transfer calculation.
- The simulation does not currently solve Einstein's field equations.
- It does not simulate realistic accretion-disk fluid dynamics, magnetic fields, or relativistic gravitational lensing.
- Numerical accuracy depends on the timestep, initial conditions, and integration method.

These assumptions make the simulation easier to understand, run, and extend while keeping the distinction between visualization and physical realism clear.

## How to Run

1. Open the notebook in Google Colab.
2. Execute the notebook cells in order.
3. Observe the calculated particle trajectories and animated visualization.
4. Run the circular-orbit validation test to inspect numerical energy error.

## References and Further Reading

1. **NASA — Anatomy of a Black Hole**  
   https://science.nasa.gov/universe/black-holes/anatomy/  
   Background on event horizons, black hole structure, and accretion disks.

2. **NASA — Gravity and Mechanics**  
   https://science.nasa.gov/learn/basics-of-space-flight/chapter3-2/  
   Background on gravitational forces and orbital mechanics.

3. **NIST Digital Library of Mathematical Functions — Numerical Methods**  
   https://dlmf.nist.gov/3.7  
   Mathematical reference for numerical solution methods.

4. **SciPy — Numerical Integration Documentation**  
   https://docs.scipy.org/doc/scipy/reference/generated/scipy.integrate.solve_ivp.html  
   Documentation for numerical integration of ordinary differential equations.

## Future Improvements

- Interactive controls for black hole mass and particle initial conditions.
- Improved accretion-disk rendering and particle trails.
- More extensive numerical convergence tests.
- More physically realistic relativistic particle trajectories.
- Approximate gravitational lensing and a more advanced scientific visualization.
- Additional automated tests and performance measurements.

## Project Information

- **Project:** EVENT HORIZON
- **Language:** Python
- **Environment:** Google Colab
- **Libraries:** NumPy, Matplotlib, IPython
- **Cost:** Free core toolchain
- **Purpose:** Educational simulation, numerical physics, and scientific visualization
