---
title: Debugging output
folder: user_guide
permalink: debugging_output.html
---

## Debugging output

A variety of files may be printed by Tramonto in VERBOSE mode. Here is a quick reference for what can be found in those files.

*   dft_time.out: timing and parallel performance results for the run.
*   cr.out: For CMS polymers, this file prints back out the direct correlation function, as given by the Cr_file specified in dft_input.dat.
*   cr.lj.out: For CMS polymers, this file contains the direct correlation function after the LJ attractions have been added to it.
*   dens_iter.dat: Stores the solution vector as a function of position for each Newton iteration.
*   dft_freen_prof.dat: For cases where Ndim=1, this file contains the free energy density as a function of position. This is related to the surface tension profile of an interface with planar symmetry.
*   dft_vext.dat: This file contains the neutral part of the external field acting on each species as a function of position on the mesh.
*   dft_vext_c.dat: This file contains the Coulombic part of the external field acting on each species as a function of position on the mesh.
*   dft_zeroTF.dat: This file contains an array of 0s and 1s (FALSE and TRUE respectively) as a function of position on the mesh. When this array is TRUE, a given node is assumed to be inside a surface, and the Euler-Lagrange equations of the density functional theory are replaced with the simple condition density=0.
*   dft_zones.dat: This file contains the zone assignment of every node on the mesh (for mesh or Jacobian coarsenening purposes).
*   proc_mesh.dat: This file contains data on the node to processor map obtained by the load balancing process.
*   Resid2.dat: currently disabled (v2.1).
*   rho_init.dat (and rho_init.datg): echos initial guess for a given run (contains same parameters as would be found in dft_dens.dat and dft_dens.datg)
*   stencil.out: This file contains the integration stencils used for residual and jacobian calculations. The columns are an index, then the Ndim offsets, then the weight.

***

[Privacy and Security](http://www.sandia.gov/general/privacy-security/index.html)
[Andrew Salinger](mailto:agsalin@sandia.gov) or [Laura Frink](mailto:ljfrink@colderinsights.com) - Site Contacts