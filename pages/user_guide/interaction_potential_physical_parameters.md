---
title: Interaction Potential Physical Parameters
folder: user_guide
permalink: interaction_potential_physical_parameters.html
---

## Interaction Potential PhysicalParameters

These parameters define interaction potential parameters that define fluid-fluid, wall-fluid, and wall-wall interactions.

*   **Ncomp**[Nwall_type](int): The number of fluid components in the system. For polymer fluids, enter the total number of different block types in the system.
*   **Mix_type**(int): Type of mixing rules to be applied for a given problem. If Mix_type=0 then the Lorentz-Berthlot rules will be applied, and only the diagonal entries (i.e. Sigma_ff[0][0], Sigma_ff[1][1]) should be provided in the input file. If Mix_type is set to 1, then every element of the arrays must be manually entered. Note that depending on what types of fluid and surfaces are being studied many of these parameters may be irrelevent.

### Fluid Properties

*   **HS_diam**[Ncomp](real vector): Vector containing the hard sphere diameter of each fluid component. This is only used if Type_hsdiam=MANUAL ENTRY.
*   **Mass**[Ncomp](real vector): Vector containing the mass of each species. Used if one wants to include the deBroglie wavelength term in the chemical potential expressions. Otherwise set to 1.0\. Note that this functionality is currently disabled in the v2.1 release of Tramonto, but the input line is still required.
*   **Charge_f**[Ncomp](real vector): Vector containing the valence associated with each component. Charges are only relevant to charged fluids.
*   **Pol**[Ncomp](real vector): Vector containing the polarization parameter. Note that one must have Type_coul=3 for this vector to be used.
*   **Sigma_ff**[Ncomp][Ncomp](real array): Array containing characteristic sizes (often particle diameters) associated with interaction potentials. Set diagonal entries only if Mix_type=0 otherwise set up entire array. Components are listed in normal matrix order by row, e.g. Sigma_ff[0][0] Sigma_ff[0][1] ... Sigma_ff[0][Ncomp-1] Sigma_ff[1][0] ... Sigma_ff[1][Ncomp-1] ... Sigma_ff[Ncomp-1][0] ... Sigma_ff[Ncomp-1][Ncomp-1]. This same ordering is used for all 2D arrays of parameters.
*   **Eps_ff**[Ncomp][Ncomp](real array): Array containing energy parameters associated with interaction potentials. Set diagonal entries only if Mix_type=0 otherwise set up entire array.
*   **Cut_ff**[Ncomp][Ncomp](real array): Array containing cut-off distances associated with interaction potentials. Set diagonal entries only if Mix_type=0 otherwise set up entire array.
*   **Bond_ff**[Ncomp][Ncomp](real array): Array containing bond-lengths associated with segment pairs. Set diagonal entries only if Mix_type=0 otherwise set up entire array. Note that entries for nonbonded pairs are needed for the purposes of reading the array, but these values are never used.
*   **EpsYukawaK_ff**[Ncomp][Ncomp](real array): Array containing energy prefactor for exponential Yukawa potential terms in summed potentials with Lennard-Jones or repulsive terms.
*   **YukawaK_ff**[Ncomp][Ncomp](real array): Array containing exponential Yukawa parameter (i.e. the inverse Debroglie wavelength) associated with a given fluid-fluid interaction. Set diagonal entries only if Mix_type=0 otherwise set up entire array. Note that to model a mixture of colloids in an electrolyte, this number should most often be a constant independent of the species. However, the array is set up generally to allow for more flexibility in applying Yukawa based models.
*   **Npow_ff**[Ncomp][Ncomp](real array): Array containing the specific power to be applied to the repulsive contribution to a summed Yukawa-repulsive potential.

### Surface Properties

*   **Rho_w**[Nwall_type](real vector): Vector that contains the density of the solid surfaces of interest.
*   **Sigma_ww**[Nwall_type][Nwall_type](real array): Array containing interaction diameters of various surface types with one another. Set diagonal entries only if Mix_type=0 otherwise set up entire array.
*   **Eps_ww**[Nwall_type][Nwall_type](real array): Array containing interaction energy parameters of various surface types with one another. Set diagonal entries only if Mix_type=0 otherwise set up entire array.
*   **Cut_ww**[Nwall_type][Nwall_type](real array): Array containing cut-off distances for surface-surface interactions. Set diagonal entries only if Mix_type=0 otherwise set up entire array.
*   **EpsYukawaK_ww**[Nwall_type][Nwall_type](real array): Array containing energy prefactor for exponential Yukawa potential terms in summed potentials with Lennard-Jones or repulsive terms for wall-wall interactions.
*   **YukawaK_ww**[Nwall_type][Nwall_type](real array): Array containing exponential Yukawa parameter for surface-surface interactions. Set diagonal entries only if Mix_type=0 otherwise set up entire array.

### Fluid-Surface Interaction Properties

*   **Sigma_wf**[Ncomp][Nwall_type](real array): Array containing interaction diameters of various surface-fluid interactions. These parameters will be set automatically if Mix_type=0; otherwise set up entire array.
*   **Eps_wf**[Ncomp][Nwall_type](real array): Array containing interaction energy parameters of various surface-fluid interactions. These parameters will be set automatically if Mix_type=0; otherwise set up entire array.
*   **Cut_wf**[Ncomp][Nwall_type](real array): Array containing cut-off distances for surface-fluid interactions. These parameters will be set automatically if Mix_type=0; otherwise set up entire array.
*   **EpsYukawaK_wf**[Ncomp][Nwall_type](real array): Array containing energy prefactor for exponential Yukawa potential terms in summed potentials with Lennard-Jones or repulsive terms for wall-fluid interactions. These parameters will be set automatically if Mix_type=0; otherwise set up entire array.
*   **YukawaK_wf**[Ncomp][Nwall_type](real array): Array containing exponential Yukawa parameter for surface-fluid interactions. These parameters will be set automatically if Mix_type=0; otherwise set up entire array.

***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a>     