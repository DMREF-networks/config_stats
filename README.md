# config_stats
Code to read in .csv files of the (x,y) coordinates of the point cloud and the adjacency matrix of a network metamaterial and compute various statistics, namely entropies.

## Entropy_Metrics.py
Uses the built-in functions for computing entropy from scipy.stats.  Contains the following functions:

**weight_adj** return the adjacency matrix weighted by $1/R_{ij}$ where 
```math
R_{ij} = \frac{\rho}{a}\sqrt{(x_i-x_j)^2 + (y_i-y_j)^2} 
```
is the resistance of one edge, based on its length, resistivity of the material $\rho$, and the cross-sectional area of the edge beam $a$.

**degree_entropy** returns the Shannon entropy $S_k$ of the discrete degree distribution $p_k$
```math
S_k = -\sum_{k\in D} p_k\ln(p_k)
```

**edge_entropy** returns the differential entropy $S_e$ of the weights in the weighted adjacency matrix
```math
S_e = -\int_{\mathbb{R}} f(c)\ln(f(c))dc
```
where $c=1/\sqrt{(x_i-x_j)^2 + (y_i-y_j)^2}$ is proportional to the conductance of each edge.

**resistance** returns the effective resistance across the diagonal of the network from the 
upper left-most corner to the bottom right-most corner


## Compute_Entropy.ipynb
Computes the entropies and resistances across the network and produces plots
