# Modelling differentiation of cells in cell fate decisions in epigenetic landscape

###### Authors : Sairam Narendra Babu & Pratistha Saxena

#### Aim of the Project:

1. Construct the Waddington energy landscape of toy circuits that model cell differentiation in normal gene circuits.
  
2. Novel Exploration: Form the waddington energy landscape for a gene circuit, where cells dont differentiate, and continue residing within the cell cycle.
  

### Introduction

The concept of Waddington's epigenetic landscape serves as a visual and theoretical framework for understanding cell fate determination and differentiation. The valleys in this landscape symbolize stable cell states (attractors), while the ridges represent barriers that delineate distinct states. Based on deterministic quasi-potential landscapes, this study aims to explore and extend the computational modeling of such landscapes for gene regulatory networks.

By modeling the bistable and tristable models, this report demonstrates the ability of gene circuits to form multiple stable states through mutual inhibition and autoregulation. Furthermore, a novel system is introduced where one gene promotes the other while being inhibited in return. This system results in a unique potential landscape resembling simple harmonic motion (SHM), akin to a two-ball spring model, thereby highlighting its dynamic properties.

##### How does one construct the Waddington landscape for a general system

$$
\frac{dx_1}{dt}=F_1(x,y)
$$$$
\frac{dx_2}{dt} = F_2(x,y)
$$

Where $x_1,x_2$ are values representing thr concentration of proteins $x_1$ and $x_2$, and $F_1$ and $F_2$ are governing differential equations of these systems.

This can be generalized to a vector system:

$$
\frac{dS}{dt} = F(S)
$$

Where S represents a state vector of the system at some time point.

Now, for this system, we want to compute a potential energy landscape. A fundamental issue with that is the fact for larger systems, simply integrating would not be feasible, due to the fact that it would be a non-integrable "force" function.

So a way to bypass this is to compute a quasi-potential, for this system, to be more specific, a deviation in quasi-potential, and attempt to reconstruct the potential energy surface from that system.

$$
\begin{align}
\Delta V_q &= \frac{\partial V_q}{\partial x} \cdot \Delta x + \frac{\partial V_q}{\partial y} \cdot \Delta y \\
           &= -\frac{dx}{dt} \cdot \Delta x - \frac{dy}{dt} \cdot \Delta y \\
           &= -\bigg[ \bigg(\frac{dx}{dt} \bigg)^2 + \bigg(\frac{dy}{dt}\bigg)^2 \bigg] \Delta t
\end{align}


$$

This is obtained from the fact that, one could seperate the potentials in such a manner

$$
F = -F_c +  D^* \nabla V_q
$$

The approzimation is obtained from the fact that one could look at the system in a probabilistic manner, from which one could obtain a probability flux, and using an approximation, said quasi-potential formula could be obtained.

### Results

We simulated 3 systems :

$$
\begin{align*}
&\text{Case 1: } X \to Y, \quad Y \dashv X \\
&\text{Case 2: } X \dashv Y, \quad Y \dashv X \\
&\text{Case 3: } X \to X, \quad X \dashv Y, \quad Y \dashv X, \quad Y \to Y
\end{align*}

$$

Following were the waddington energy surfaces we obtained for these systems

### Case 3

This system is a tristable system, when solved analytically, the potential energy surface also has 3 valleys, and the differentiation to either state is seen in trajectories that passed through the middle basin, showing existence of a differentiating system.

![](file:///home/saigum/.config/marktext/images/2024-12-03-22-18-58-image.png?msec=1733244538712)

The middle basin is seen by where all the red points converge following which some red points, got to either valley on both side.

### Case 2

This case is a bistable system, with two major valleys, akin to a toggle switch, emulating systems that don't have pluripotent differentiations, where terminations occurs directly from each stem cell.

![](file:///home/saigum/.config/marktext/images/2024-12-03-22-21-08-image.png?msec=1733244668449)

One can see both stable states, with the set of blue trajectories, and the set of green trajectories.

### Case 1

This case is an oscillatory system, here the PES is akin to that of SHM. This biologically represents systems that are continually differentiating, akin to that of cancer-type cells.(Or stem cells).This PES is akin to that of an SHM system, with a single major fixed point, at the only minima in the system, which corresponds here to our waddington-energy landscape for this system, which shows basic proof of concept.

![](file:///home/saigum/.config/marktext/images/2024-12-03-22-22-47-image.png?msec=1733244767077)

# Methods

To simulate the above equations, we had to go through various trajectories, find the change in quasi-potential, and from this, we essentially obtain a quasi-potential surface,(considering the fact) that the quasi-potential surface is intially 0, for a completely inactive gene circuit.

So we had one major simulation, in order to obtain the quasi-potential values for each location on the plane covering possible protein concentrations for $X$ and $Y$, followed by a stochastic simulation of cells with initial conditions, for checking as to whether they reach the final basins.

For the stochastic simulations, we used a multiplicative noise, however the PES is obtained directly from the interpolations.For simulating the stochastic systems, one would need a correct set of initial configurations to reach one of the 3 basins(in the tri-stable system).

### Conclusions

From a broader perspective, the study enhances our understanding of the Waddington landscape as a powerful metaphor and computational tool. It showcases the flexibility of the landscape to represent both multistable and oscillatory systems, broadening its applicability beyond simple cell fate transitions to dynamic systems that may re-enter the cell cycle exhibit periodic behavior.

A few challenges an issues, since this is a quasi-potential, the system's initial conditions and parameters do matter a lot, we currently obtain the PES from interpolating the quasi-potential difference with the grid representing the concentrations of the protein.

One could use a regressor in order to obtain a functional form, for the Waddington energy surface, for example, if one wants to obtain it from a 1000 trajectories, one could use a gaussin processor regressor, to obtain a multivariate gaussian form, otherwise multivariate linear regression.

Another challenge is complexity of doing this for a large protein interaction system, you'd have to compute the quasi-potential along various trajectories, which would be a large number of variables. Similarly, pictorial depiction for the waddington energy landscape isn't feasible in 3 dimensions for a system with more than 2 variables, in order to overcome this, one would either have to go through dynamical systems reductions, or through some sort of component analysis based on threshold values for our system. In general however this framework, is generally applicable.

#### References

1. The potential landscape of genetic circuits imposes the arrow of time in stem cell
  differentiation.(Jin Wang, Li Xu, Erkang Wang, and Sui Huang).
  
2. Transition states and cell fate decisions in epigenetic landscapes.(Naomi Moris, Cristina Pina, Alfonso Martinez Arias).
  

### Roll numbers : 2022113004, 2022113008
