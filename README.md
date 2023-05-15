# Traffic_Simulation
Implement several models of one- dimensional traffic flow on a freeway.

# Project Description
Let the system be described by the state variables,
* $ρ = ρ(x, t)$ be the density of cars at position x and time t, having
units of, say, number of vehicles per km;
* $v = v(x, t)$ be the velocity of a car at position x and time t, in units of km/h; and
* $f = f(x,t)$ be the flow of cars at position x and time t, in units of number of vehicles per hour.
These are interrelated by $f = ρv$, which is consistent with the units. Suppose the initial conditions $ρ(x, 0) ≡ ρ0(x), v(x, 0) ≡ v0(x)$ are given. Furthermore, assume that vehicles cannot travel faster than $v_{\ max}$, and that maximum density of vehicles at any point on the road is $ρ_{\ max}$. The general Lighthill-Whitham-Richards(LWR) model says the state of the system evolves in time and space according to the partial differential equation (PDE),
```math
\begin{align}
\frac{∂ρ}{∂t}= −\frac{∂f}{∂x}
\end{align}
```

Made two additional simplifying assumptions. First, assume that the flow $f$ is an explicit function of $ρ$ only, i.e., $f = f(ρ)$. When imposing this assumption on
eq. (1), the resulting model is sometimes called the shallow-water equation or transport equation, and it is an instance of a nonlinear hyperbolic PDE.

Second, assume f has the form of a logistic function,
```math 
\begin{align}
f(ρ) = v_{max} \cdot ρ \left( 1 - \frac{ρ}{ρ_{max}} \right)
\end{align}
```
Substituting eq. (2) into eq. (1) yields
```math 
\begin{align}
\frac{∂ρ}{∂t} = − \frac{∂f}{∂x}
\end{align}
```
```math 
\begin{align}
= -\left( \frac{df}{dρ} \right) \frac{∂ρ}{∂x}
\end{align}
```
```math 
\begin{align}
= -\left( \frac{df}{dρ} \right) \frac{∂ρ}{∂x}
\end{align}
```
```math 
\begin{align}
= −v_{max} \left( 1 − 2 \frac{ρ}{ρ_{max}} \right) \frac{∂ρ}{∂x}
\end{align}
```
## 1. Initial Condition
> Assume that there is an initial shock. Suppose the maximum density $ρ_{\ max}$ is 160 cars per km. Traffic enters from the left ($x=−5$ km) at 80 cars per km, half the maximum density. This density is fixed until $x=−0.25$ km, where a “shock” occurs, meaning traffic suddently hits the maximum density. This shock extends until $x=0$ km. To the right of that point, the density is zero.
<img src="https://github.com/lsh4205/Traffic_Simulation/assets/63761734/19043e5a-47ba-4155-ad59-35533984a49d" width="80%" height="80%">

> Simulate with 2 minutes of logical time with a time step of $0.1s$(one-tenth of a second). Therefore, your simulation loop will evaluate $1,200$ time steps in total.

> A spatial step will be size of 0.01 km (10 m). Therefore, your grid will have about $1,000$ points.

### 2. Simulate with Upwind scheme and Lax-Friedrichs scheme
#### Lax-Friedrichs Scheme
* Space is discretized at the points $x_1$, $x_2$, $x_3$, . . ., $x_i$, . . ., with step
size $x_{i+1} − x_i ≡ s$.
* Time is discreteized at the points $t_1$, $t_2$, $t_3$, . . ., $t_j$, . . ., with step size
$t_{j+1} − t_j ≡ h$.
* The approximate density at point $x_i$ and time $t_j$ is $ρ_{i,j}$.
* The approximate flow at $x_i$ and $t_j$ is $f(i\ ,\ j) = f (ρ_i,j)$. Then the Lax-Friedrichs update formula is given by

```math
ρ_{i\ , j+1} = \frac{ρ_{i+1\ ,j} + ρ_{i−1\ ,j}}{2} − \frac{h}{s} \frac{ f_{i+1\ ,j} − f{i−1\ ,j} }{2}
```

* (a) Upwind Scheme (with $0.05s$ time-step)
* (b) Lax-Friedrichs Scheme (with $0.05s$ time-step) 
* (c) Lax-Friedrichs Scheme (with $0.1s$ time-step)
* (d) Lax-Friedrichs Scheme (with $0.2s$ time-step)

<img src="https://github.com/lsh4205/Traffic_Simulation/assets/63761734/41fda534-2795-4154-9f39-8af7642e7c0f" width="90%" height="90%">
<img src="https://github.com/lsh4205/Traffic_Simulation/assets/63761734/593f6009-9495-47ab-b0cb-2c8ae7015e65" width="90%" height="90%">
<img src="https://github.com/lsh4205/Traffic_Simulation/assets/63761734/fc8a516f-3275-454d-ac1d-75b17d9ceaf6" width="90%" height="90%">
<img src="https://github.com/lsh4205/Traffic_Simulation/assets/63761734/a5ad9b6a-b505-429e-bfe7-048c31e38e0b" width="90%" height="90%">

### 3. Simulate with CA-Based Model
The rule of CA-based model.
* Update for vehicle *$i$* :
>1. **Accelerate:** $v_i := min \left( v_i + 1, v_{max} \right)$
>2. **Decelerate:** $v_i := d\ (i, i+1), \ if \ v_i > d \ (i, i+1)$
>3. **Move:** vehicle $i$ moves $v_i$ cells forward

<img src="https://github.com/lsh4205/Traffic_Simulation/assets/63761734/aa8ca38a-736d-4822-a3b1-4e25d9fddb33" width="100%" height="100%">

# Conclusion
Please find the following code details in my code.
