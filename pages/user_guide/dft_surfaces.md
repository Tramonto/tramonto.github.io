---
title: Defining surface types, positions, and charge
folder: user_guide
permalink: dft_surfaces.html
---

## dft_surfaces.dat: Defining surface types, positions, and charge.

The second required input file for Tramonto is dft_surfaces.dat. This file is needed unless there are no surfaces in the calculation. This file contains the locations of the centers of the surfaces of interest. Each surface gets one line of entry in this file, and the parameters must be listed in the correct order (WalllType id, Link id, positions, Elec_param_w). These parameters are:

*   **WallType**[Nwall](int vector): Assigns a surface type (and all properties associated with that Nwall_type in dft_input.dat) to each surface in the problem. Begin indexing with zero (0).
*   **Link**[Nwall](int vector): Groups surfaces that should be treated as a linked collection (i.e. a molecule composed of individual atoms). Note that linking a surface allows computation of force on a single compound surface. Begin indexing with zero (0).
*   **WallPos**[Nwall][Ndim](real array): Enter Ndim positions on each line to locate the center of each surface. Note that the origin is defined to be in the center of the computational box so the positions should be in the range -Size_x[idim]/2 to +Size_x[idim]/2 in each direction. For easier visualization, the domain is shifted in the file dft_dens.dat such that the origin is moved to the lower, left, back corner of the domain. Nevertheless, even when restarting from an old profile, the positions in the dft_surfaces.dat file must assume the origin is at the center of the domain.
*   **Elec_param_w**[Nwall](real vector): Enter the charge parameter (potential, charge per unit area, atomic charge etc) associated with each surface. For a neutral system enter 0.0 for this variable on each line.

***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a> 