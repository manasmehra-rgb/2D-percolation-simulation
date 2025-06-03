# 2D-percolation-simulation

What happens when liquid tries to seep through a sponge, or electricity flows through a network of wires but some parts are randomly blocked? That’s what percolation theory tries to answer.

This project simulates that process on a square grid using Python. It shows how clusters of connected open spaces form and whether they create a path from one side of the grid to the other. The project also estimates the percolation threshold, a key concept in physics, probability, and network science.

This notebook answers a simple question
  *If we randomly block some parts of a grid, what’s the chance that a path still exists from one   side to the other?*

To answer this, the code does the following:

1. Creates a 2D grid (a.k.a lattice) where each square (a.k.a site) is either open or blocked.

2. Labels connected groups of open squares using an algorithm.

3. Checks if a connected group goes from the left side to the right side.

4. Repeat the experiment thousand of times for different probabilities.

5. Finds the tipping point (a.k.a percolation threshold) where the system almost always connects.



## Key Concepts

### 1. Lattice (Grid) Generation
The code creates an L x L square grid where each cell is
1. Open (1) with probability p
2. Blocked (0) with probability 1 - p
   
This simulates a porous material or a network where only some paths are active.

### 2. Cluster Labeling
Using a basic depth-first search (DFS) algorithm, the code finds and labels each connected region of open sites. Each "cluster" gets a unique label so we can track it.

The figure below shows a 6×6 lattice where we check for **horizontal percolation** i.e, whether there exists a continuous path of connected open sites from the **leftmost column** to the **rightmost column**.

- The **left plot** is the raw lattice: yellow = open site, purple = blocked site.
- The **right plot** shows labeled clusters: each connected group of open sites is colored differently.

![Percolation Check](https://github.com/user-attachments/assets/dfa55146-5304-4cf1-a4c3-9ec049d966e6)


### 3. Percolation Detection
We then check *does any cluster stretch from the left edge to the right edge?*
If yes -> the grid percolates.

### 4. Monte Carlo Simulation
Monte Carlo simulation is a technique that uses repeated random sampling to estimate outcomes in complex, uncertain systems. I tried hundreds of random grids for each value of p (like p = 0.5, 0.6, 0.7, etc.) and recorded how often percolation happens.

This helped estimate the chance of percolation for each p.


### 5. Percolation Probability vs. Site Occupancy (3×3 Lattice)

The plot below shows the estimated probability of percolation for a 3×3 lattice as the site occupation probability p varies from 0 to 1.

- The **blue line** represents the results of a Monte Carlo simulation: for each value of p, I generated 100 random lattices and recorded the fraction that successfully percolated.
- The **orange line** shows a theoretical percolation probability curve derived from exact calculations for small grids.

As expected, the chance of percolation increases as p rises. The blue line approximates the theoretical model, though with some variance due to the small lattice size and randomness of sampling.

![Plot](https://github.com/user-attachments/assets/b9c1ccb8-d388-406e-a33c-5bf163f91d2a)

### 6. Percolation Threshold

As p increases, we see a sharp jump in the percolation probability i.e, *a phase transition*.
This tipping point is called the percolation threshold or the minimum probability where large scale connectivity becomes likely.



