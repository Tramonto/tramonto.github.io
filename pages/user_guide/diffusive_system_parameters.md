---
title: Diffusive System Parameters
folder: user_guide
permalink: disffusive_system_parameters.html
---

## Diffusive System Parameters

These parameters set up cases where steady state diffusion is present in the physical problem. Note these are steady state calculations only. A time-dependent DFT is not implement as of the v2.1 release of Tramonto.

### Define general transport parameters

*   **D_coeff**[Ncomp](vector real): The diffusion coefficient for each species (or polymer chain) in the problem of interest. Given the assumptions of ideal diffusion and steady state, these constants are only used in post processing a flux: they are not needed in the calculation of density or chemical potential profiles.
*   **Velocity**(real): A constant that accounts for center of mass motion in steady state transport.

### Parameters for transport through a pore - treated as a 1-dimensional problem

Transport through a nanopore can be treated as a 1D problem as has been done for studies of ion channel proteins. Several parameters are needed to set up these kinds of problems depending on if the pore has a constant radius or varies in size down the length of the pore. The parameters are as follows:

*   **Geom_Flag**(int): This flag indicates whether we are doing a nanopore calculation in this way and whether the area of the pore varies in the Grad_dim dimension. Options are:
    *   0: unit area - not performing nanopore calculation
    *   1: cylindrical pore - uniform area finite length
    *   2: pore composed of a sequence of tapered segments*   **Nseg**(int): This constant sets how many pore segments of different geometry there are for a given pore. For example a cylindrical pore with tapered ends might have be three segments.*   **Radius_L**[Nseg](vector real): Stores the radius of the left side of each pore segment (use when Geom_Flag=2).*   **Radius_R**[Nseg](vector real): Stores the radius of the right side of each pore segment (use when Geom_Flag=2).*   **Length**[Nseg](vector real): Stores the length of each pore segment (use when Geom_Flag=1 or 2).

***

[Privacy and Security](http://www.sandia.gov/general/privacy-security/index.html)
[Andrew Salinger](mailto:agsalin@sandia.gov) or [Laura Frink](mailto:ljfrink@colderinsights.com) - Site Contacts 