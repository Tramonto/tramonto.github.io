---
title: State Point Parameters
folder: user_guide
permalink: state_point_parameters.html
---

## State Point Parameters

This section defines the type of system to be studied, and sets the appropriate bulk state point(s). Note that Tramonto currently uses bulk fluid densities rather than chemical potentials to define the bulk state points. However, it is possible to perform arc-length continuation studies varying chemical potential if desired.

*   **Type_interface**(int): Indicates the type of interface problem that is being considered. For a study of an equilibrium single phase system, only one state point will be required (bulk density) as input. For either a two phase interface (e.g. liquid-vapor interface with bulk liquid on one side of the domain and bulk vapor on the other side of the domain) or for a diffusing system where the chemical potentials on the two sides of the domain are different, two boundary conditions are required as input. Note that CMS polymers can only be studied as homogeneous problems because an explict calculation of the chemical potential is never done. Specific options for all other fluids are:
    *   0: Homogeneous system - only one bulk density is required.
    *   1: Diffusing system - two bulk densities are required as boundary conditions.
    *   2: Two phase interfacial system - two bulk densities are required as boundary conditions.
*   **Grad_dim**(int): When Type_interface=1 or 2, this parameter indicates the orientation of the inhomogeneous density boundary conditions. For example, to study diffusion with a chemical potential gradient in the z direction, set Grad_dim to 2\.
*   **Lconstrain_interface** : Logical (0=FALSE, 1=TRUE). This parameter can be used to pin the location of an interface (for example a liquid-vapor interface) at a particular place in the computational doman in order to prevent numerical instabilities associated with movement of the interface.
*   **Rho_b_0**[Ncomp](real array) or **Rho_b_0**[Npol_comp](real array): The bulk number density for each fluid component in the system. For polymers, enter the density of each polymer component; the code will automatically determine the density per segment type. Note that if Type_interface=1 or 2, Rho_b_0 is mapped to Rho_LBB (left(x) bottom(y) or back(z) of domain depending on Grad_dim).
*   **Rho_b_1**[Ncomp](real array) or **Rho_b_1**[Npol_comp](real array): The bulk number density for each fluid component in the system. For polymers, enter the density of each polymer component; the code will automatically determine the density per segment type. Note that if Type_interface=1 or 2, Rho_b_1 is mapped to Rho_RTF (right(x) top(y) or front(z) of domain depending on Grad_dim). If Type_interface=0 then this parameter is not used.
*   **Elec_pot_LBB**[Ncomp](vector real): The bulk electrostatic potential on the left (x0), bottom (x1), or back (x2) of the computational domain depending on the direction Grad_dim. Note this only applies when electrostatics are turned on and Type_interface=1 or 2; otherwise for bulk equilibrium systems with homogeneous boundary conditions, the bulk electrostatic potential is set to zero.
*   **Elec_pot_RTF**[Ncomp](vector real): The bulk electrostatic potential on the right (x0), top (x1), or front (x2) of the computational domain depending on the direction Grad_dim. Note this only applies when electrostatics are turned on and Type_interface=1 or 2; otherwise for bulk equilibrium systems with homogeneous boundary conditions, the bulk electrostatic potential is set to zero.
*   **x_const_mu**(real): A distance in the Grad_dim dimension measured from the edges of the computational domain where the densities and chemical potentials are held constant. This parameter is used in two contexts. First, for a diffusion study (Type_interface=1), this parameter is used to set up a region of constant density and chemical potential on either side of the domain that will be held constant through the solve. Second, if a linear density profile initial guess is desired in the center of the computational domain (perhaps near a liquid-vapor interface), this parameter sets the width of the two bulk regions outside the area where the linear profile has been set up. Note that in this case, there are no constraints to maintain the bulk region during the solve.

***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a> 