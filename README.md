# config_stats
Code to read in .csv files of the (x,y) coordinates of the point cloud and the adjacency matrix of a network metamaterial and compute various statistics, namely entropies and the effective resistance from the top left corner to the bottom right corner of the network.

## Network_Computation 

A folder containing Network_Statistics.ipynb and Entropy_Metrics.py. If one places the data folder containing the point cloud and adjancency matrix files into a local copy of Network_Computation, one can replicate the entropy analysis in _Electrical Transport in Tunably-Disordered Metamaterials_ by running Network_Statistics.ipynb.

### Entropy_Metrics.py
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


### Network_Statistics.ipynb
Computes the entropies and resistances across the network and produces plots. Additionally, it outputs the Network_Data and Network_Statistics data files used for plotining in graphing_script.ipynb

## Figure_Generator
Figure_Generator is a folder which contains graphing_script.ipynb and the Network_Statistics data set which allows one to recreate the figures in Entropy_Statistics.ipynb without analysis. The data used for this is contained within the Network_Statistics data file. 

### Network_Statistics

Network_Statistics is a data file containing the mean and standard deviation of the resistance, degree, and conductance entropy per iteraion of Lloyd's algorithm. Used to create the figures made by graphing_script.ipynb. Network_Statistics is a dictionary with structure detailed in the last cell of Network_Statistics.ipynb and procedures on reading it can be seen in the example provided in graphing_script.ipynb.

### graphing_script.ipynb 

graphing_script.ipynb is a jupyter notebook which produces the figures in Network_Statistics.ipynb without analysis by referencing the Network_Statistics data file

## Network_Data
Network_Data is a data file which contains the resistance and entropies of each network for sizes N=100, N=200, and N=300. The original data files that were used to calculate these values are not stored or referenced in this file. Network_Data is a dictionary and its structure is detailed in the last cell of Network_Statistics.ipynb. The three keys distinguish by network size, followed by subkeys distingishing the desired metric. A matrix of variable rows and 101 columns is under each subkey. The columns notate what iteration of Llody's algorithm the network has gone through with the first column starting from 0. The rows notate what ensemble the network belongs to. Two networks are part of the same ensemble if they both Lloyd's iterations of a single parent point distrobution. 
