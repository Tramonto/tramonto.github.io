---
title: Output Format Parameters
folder: user_guide
permalink: output_format_parameters.html
---

## Output Format Parameters

These parameters control how some output will be printed in various files.

*   **Lper_area**(int): Logical (0=FALSE, 1=TRUE) to indicate whether Adsorption, Free Energy, Charge in the fluid, and Force are normalized per unit area before printing in dft_output.dat. If FALSE, the code prints the extensive quantity. If TRUE, the code divides by the total exposed surface area.
*   **Lcount_reflect**(int): Logical (0=FALSE, 1=TRUE) to indicate whether Adsorption, Free Energy, Charge in the fluid, and Force should be printed for the computational domain only (FALSE) or for the domain plus reflected domains (TRUE).
*   **Lprint_gofr**(int): Logical (0=FALSE, 1=TRUE) to indicate whether a radial distribution function should be printed. The code will print a file dft_gofr.dat where the first column will be the distance r measured relative to the center of the surface, and the other columns will be the rho(r)/rho_bulk for each fluid component.
*   **Lprint_uww**(int): Logical (0=FALSE, 1=TRUE) to indicate whether the surface-surface interactions should be printed in dft_output.dat along with the surface free energy. The direct interactions are needed to compute the complete potential of mean force between a pair of particles immersed in a solvent.
*   **Print_rho_type**(int): This switch determines how the files that contain density output will be named. Options include:
    *   0: Put all density output in the default files: dft_dens.dat, dft_dens2.dat (if performing binodal tracking), and dft_dens.datg (if performing CMS or WJDC polymer calculation).
    *   1: Put output in unique numbered files (i.e. dft_dens.0, dft_dens.1, dft_dens.2...). This allows a copy of every density profile solution to be saved during the course of the continuation run. The numbering scheme also makes it relatively easy to locate a profile at a particular point in the continuation solution.
*   **Print_rho_switch**(int): This switch determines the kind of bulk density information that will be printed to dft_output.dat. Options include:
    *   0: Print densities as ρ<sub>b</sub>σ<sup>3</sup>.
    *   1: Include the value of p/p_sat where p_sat is the saturation pressure of the fluid at the given temperature (disabled at v2.1 release).
    *   2: Include the Debye screening length. This is applicable to electrolytes.
    *   3: Include the chemical potentials.
*   **Print_mesh_switch**(int): This switch sets how the mesh will be represented in the file dft_output.dat when doing mesh continuation runs. The options are:
    *   0: print the surface separations between all pairs of surfaces in the domain.
    *   1: print the surface positions at the center of each surface.
*   **Iwrite**(int): This switch controls how much output will be printed. Options are:
    *   0: minimal output - no density profiles.
    *   1: minimal output - with density profiles.
    *   2: extended output - density profiles, segment profiles, dft_dens.datg, and attractive potentials.
    *   3: verbose debugging output.
    *   4: no screen output at all (use when Tramonto calculation is embedded in another simulation).

***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a> 