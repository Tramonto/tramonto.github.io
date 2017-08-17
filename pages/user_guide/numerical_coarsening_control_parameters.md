---
title: Numerical Coarsening Control Parameters
folder: user_guide
permalink: numerical_coarsening_control_parameters.html
---

## Numerical Coarsening Control Parameters

These parameters control how some output will be printed in various files.

*   **Nzone**(int): The number of mesh and/or Jacobian coarsening zones in the problem. Set to 1 for a uniform treatment of integration stencils in the domain. Additional zones are needed to coarsen the Jacobian and/or mesh away from the surfaces. In addition two zones are needed if a 1D region is to be applied (see description of [L1D_bc](UG_sect12.html) in section on diffusion parameters), if a bulk zone is to be specified (see below), or if a Poisson-Boltzmann limit is to be applied at some cutoff (see below). For mesh and Jacobian coarsing (see more information below), the coarsening will be based on powers of two changes in the mesh starting with the most refined zone (near the surfaces) set by Esize_x. For example if Esize_x=0.025 and Nzone=4, then integration stencils will be generated for mesh spacings of 0.025, 0.05, 0.1, and 0.2\.
*   **Rmax_zone**[Nzone-1](real vector): The distance from the surfaces associated with each zone.
*   **Mesh_coarsening**(int): This parameter selects the type of residual coarsening that will be done on the mes. The options are:
    *   0: No coarsening. Solve DFT equations on most resolved mesh as defined by [Esize_x[Ndim]](UG_sect2.html).
    *   1: Coarsen residual equation by position as defined by the Nzone and Rmax_zone parameters. In this case, the coarsening occurs in powers of two for each zone away from the surface. Field variables at nodes which are coarsened out of the system of equations are assumed to be linear averages of surrounding nodes. The integration stencils applied at remaining nodes (for example in the computation of Euler-Lagrange equations) are based on coarsened integration stencils that are smaller and less costly.
    *   2: BULK_ZONE. At a distance Rmax_zone[0] from the surfaces assume the fluid density is equal to the bulk fluid density [Rho_b[icomp]](UG_sect9.html).
    *   3: PB_ZONE. At a distance Rmax_zone[0] from the surfaces assume the fluid density is identical to a Poisson-Boltzmann fluid. Note this can result in discontinuities in the density profile and problems with charge neutrality. It should be used with caution.
*   **Coarser_jac**(int): This flag sets the type of Jacobian coarsening that will be performed for a given calculation. The options are:
    *   0: Jacobian coarsening matches residual coarsening. This results in an exact Jacobian for a coarsened system of residual equations. Note that if Nzone=1 and Mesh_coarsening=0, both residual and jacobian coarsening are turned off.
    *   1: Use integration stencils that are coarsened by a factor of two when computing Jacobian integrals in the zone nearest the surfaces (labeled zone 0). For example if Esize_x=0.025 and Nzone=4 as above, the jacobian coefficients in the four zones will be generated using integration stencils as follows: (zone 0: 0.05), (zone 1: 0.05), (zone 2: 0.1), and (zone 3: 0.2) resulting in an _approximate_ Jacobian.
    *   2: Use integration stencils that are coarsened by a factor of two when computing Jacobian integrals for all zones except the most coarse zone. For example if Esize_x=0.025 and Nzone=4 as above, the jacobian coefficients in the four zones will be generated using integration stencils as follows: (zone 0: 0.05), (zone 1: 0.1), (zone 2: 0.2), and (zone 3: 0.2) resulting in an _approximate_ Jacobian.
    *   3: Use integration stencils for the most coarse available stencil for all zones in the calculation. For example if Esize_x=0.025 and Nzone=4 as above, then integration stencils will be: (zone 0: 0.2), (zone 1: 0.2), (zone 2: 0.2), and (zone 3: 0.2) resulting in an _approximate_ Jacobian.
    *   4: Use the integration stencils for the second most coarse available stencil for all zones except the most coarse zone. For example if Esize_x=0.025 and Nzone=4 as above, then integration stencils will be: (zone 0: 0.1), (zone 1: 0.1), (zone 2: 0.1), and (zone 3: 0.2) resulting in an _approximate_ Jacobian.
    *   5: Use a constant mesh spacing defined by Esize_jacobian to define the integration stencils used for the Jacobian everywhere on the mesh. This again results in an _approximate_ Jacobian.
*   **Esize_jacobian**(real): The mesh spacing to be used for Jacobian integration stencils. For use with Coarser_jac=5.
*   **Ljac_cut**(int): A logical (0=FALSE; 1=TRUE) that indicates whether the Jacobian integrals will be cut off at some threshold value (see Jac_threshhold parameter below). This may be useful for attractive systems with rather long cutoffs, but again results in an _approximate_ Jacobian.
*   **Jac_threshhold**(real): The threshold value for whether or not to include a given point in the integration stencil. A value of 100 indicates that all points smaller the maximum value in the stencil divided by 100 will be rejected from the stencil.
*   **L1D_bc**(int): A logical (0=TRUE; 1=FALSE) that indicates if a 1D boundary conditions should be applied at some distance from th e ends of the boundary in the Grad_dim directions. This can be helpful in speeding up a 3D calculation where there is some region that becomes exactly or approximately 1D outside of a central 3D systems. This might occur in diffusion through a porous media of finite width.
*   **X_1D_bc**(real): The distance over which the 1D approximation should be applied. Only applies when L1D_bc=TRUE.

***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a> 