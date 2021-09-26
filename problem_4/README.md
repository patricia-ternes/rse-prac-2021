# Problem 4

You have been approached by a researcher who needs some help preparing a computational teaching exercise for an undergraduate module introducing Fluid Dynamics.

Your colleague wants to demonstrate a number of principles, including finite difference approaches and grid decomposition.

They would like a coding exercise to determine the flow pattern of a fluid in a cavity. For simplicity, the liquid is assumed to have zero viscosity which implies that there can be no vortices (i.e. no whirlpools) in the flow. The cavity is a square box with an inlet on one side and an outlet on another as shown below.

<p align='center'> <img src="cavity.png" alt="Cavity" height="250" id="cavity"> </p>

Describe how you would go about creating a programming exercise to solve this problem, the design decisions and assumptions that you need to let the undergraduates know about, and how you would test a solution. They may also need some pointers and reminders of the underpinning theory.

Provide a commented solution (in a language of your choice).

**Please provide both your code and your explanations in the response to this problem.**

## Solution

In the [cavity_flow](cavity_flow.ipynb) notebook you can find a simple solution for this problem. Please be aware that the algorithm in this notebook is written simply for comprehension purposes. The implemented code returns the following result:

<p align='center'> <img src="flow.png" alt="Cavity" height="300" id="cavity"> </p>

## Background

The flow pattern of a fluid can be obtained through velocity vectors at every point in space. However, the representation in terms of several vectors is complicated. An alternative is to use streamlines to represent the flow, where the streamline is a tangential curve to the velocity vector of the flow.

For a two-dimensional inviscid and incompressible flow in the given S region, the stream function satisfies:

<p align='center'> <img src="https://latex.codecogs.com/svg.image?\nabla^{2}&space;\Psi&space;=&space;\frac{\partial^{2}\Psi}{\partial&space;x^{2}}&space;&plus;&space;\frac{\partial^{2}\Psi}{\partial&space;y^{2}}&space;=&space;0&space;\text{&space;in&space;S}" title="\nabla^{2} \Psi = \frac{\partial^{2}\Psi}{\partial x^{2}} + \frac{\partial^{2}\Psi}{\partial y^{2}} = 0 \text{ in S}" /> </p>
