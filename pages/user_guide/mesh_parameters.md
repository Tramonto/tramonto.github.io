---
title: Mesh Parameters
folder: user_guide
permalink: mesh_parameters.html
---

## Mesh Parameters

These parameters set the size and mesh spacing of the computational domain. They also define boundary conditions.

*   **Ndim**(integer): The number of spatial dimensions to be solved numerically in the problem of interest. Note that as of the Tramonto 4.0 release only 3-dimensional functionals are implemented. So, reduced dimensions reflects symmetries in the problem of interest.
*   **Size_x**[idim](real vector): The size of the computational domain. There is one entry for each dimension.
*   **Esize_x**[idim](real vector): The mesh spacing. There is one entry for each dimension (they need not be the same). Note that the mesh spacing should be an integer divisor of the reference length (1σ).
*   **Type_bc**[0,1][idim](integer array): There are three lines of input associated with Type_bc. Each line should contain two integers. The different lines designate the boundary conditions in the different dimensions (some may not be used). The two entries on a given line specify boundary conditions for the two sides of the domain in a given dimension. The options are:
    *   -1: IN_WALL: semi-infinite surface : set ρ=0 for ghost nodes beyond computational boundary.
    *   0: IN_BULK: constant bulk fluid: set ρ=ρ<sub>bulk</sub> for ghost nodes beyond the computational boundary.
    *   1: PERIODIC: periodic boundary: beyond last computational node, N, set ρ<sub>N+k</sub>=ρ<sub>k</sub>. Periodic boundaries must be applied to both sides of the computational domain in the desired dimension(s).
    *   2: REFLECT: reflective boundary: beyond the last computational node, N, set ρ<sub>N+k</sub>=ρ<sub>N-k</sub>.
    *   3: LAST_NODE: continuation boundary: set ρ<sub>N+k</sub>=ρ<sub>N</sub>.
    *   4: LAST_NODE_RESTART: continuation boundary: set ρ<sub>N+k</sub>=ρ<sub>N</sub>, but use solution values obtained from a restart file for the last row. This can be useful for pinning a free interface.
    
***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a> 