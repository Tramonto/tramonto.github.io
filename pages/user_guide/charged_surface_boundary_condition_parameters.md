---
title: Charged Surfaces - Boundary Condition Parameters
folder: user_guide
permalink: charged_surface_boundary_condition_parameters.html
---

## Charged Surfaces: Boundary Condition Parameters

These parameters detail the treatment of fixed charges or charged boundary conditions in the system.

*   **Type_bc_elec**[Nwall_type](int vector): A vector that stores the type of boundary condition to be applied at each type of surface. Note that the actual value of the charge per area, surface potential, or atomic surface charge is read in the dft_surfaces.dat file. Options for Type_bc_elec are:
    *   0: No charge.
    *   1: Constant surface potential (applied at the surface-fluid boundary).
    *   2: Constant surface charge (smeared over surface elements).
    *   3: Atom of constant charge (point charge in center of atom surfaces).
*   **Nlocal_charge**(int): The number of local volumetric charges that exist within the computational domain. These charges may or may not be located within boundaries of surfaces from which solvent is precluded. They result in source terms in Poission's equation that are independent from the fluid density terms. Setting Nlocal_charge$=-1$ is a special case that puts two charges at two specified locations in the domain and then generates a linear distribution of charge between them. Note that most often this parameter is set to zero (0).
*   **Charge_loc**[Nlocal_charge](real vector): Vector stores the total charge associated with source terms set by Nlocal_charge>0.
*   **Charge_diam**[Nlocal_charge](real vector): Vector stores the diameter over which a given local charge should be spread. If Charge_diam=0.0, then Charge_loc is all put in one element of the domain.
*   **Charge_x**[Nlocal_charge][Ndim](real array): Array that contains the position of the center of each of the local source terms set byt Nlocal_charge>0.0\.
*   **Charge_type_atoms**(int): Indicates how atomic charges (Type_bc_elec=3) should be treated. Options are:
    *   0 : Smear the charges over the diameter Sigma_ww.
    *   1: Approximate point charges by putting all the charge in one element at the center of the atom (defined by WallPos array).
*   **Charge_type_local**(int): Indicates how local source term charges (Nlocal_charge>0) should be treated. Options are:
    *   0 : Smear the charges over the diameter Charge_diam.
    *   1: Approximate point charges by putting all the charge in one element at the center of the atom (defined by Charge_x array).
    *   2: Smear charge over every element in the domain for a uniform background charge.
    
***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a> 