# config_stats
Will be public repository that computes statistics of either point clouds or networks

## Entropy_Metrics.py
Contains the following functions:

**weight_adj** return the adjacency matrix weighted by $1/R_{ij}$ where 
$$
R_{ij} = \frac{\rho}{a}\sqrt{(x_i-x_j)^2 + (y_i-y_j)^2} 
$$
is the resistance of one edge, based on its length, resistivity of the material $\rho$, and the cross-sectional area of the edge beam $a$.

**degree_entropy** returns the Shannon entropy $E_d$ of the discrete degree distribution $p_d$
$$
E_d = -\sum_{d\in D} p_d\ln(p_d)
$$

**edge_entropy** returns the differential entropy $E_e$ of the weights in the weighted adjacency matrix
$$
E_e = -\int_{\mathbb{R}} f_E(x)\log(f_E(x))dx
$$
Note the weights are the resistances, so they are proportional to 1/length.


##
