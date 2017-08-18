---
title: Charged Systems - Dielectric Constant Parameters
folder: user_guide
permalink: charged_systems_dielectric_constant_parameters.html
---

## Charged Systems: Dielectric Constant Parameters

These parameters detail the treatment of the dielectric constant parameters when Type_coul is turned on, and Poisson's equation is to be solved.

*   **Type_dielec**(int): Flag for the treatment of dielectric constants. Options are:
    *   0: uniform dielectric constant everywhere in the domain.
    *   1: set different dielectric constants for fluid regions and surface regions in the computational domain.
    *   2: set different dielectric constants for bulk fluid, restricted fluid (i.e. in a pore), and surface regions in the computational domain.
    *   3: set a constant dielectric constant in a surface, but allow variation with density in the fluid (for use with Type_coul=3 option).
*   **Sigma_Angstroms_plasma**(real): The particle diameter d, in angstroms, used in calculating the reduced temperature T<sub>elec</sub> = 4πkTκε<sub>0</sub>d/e<sup>2</sup> (in MKS units). A physical value for d is needed here, since it's possible in the code to use a dimensionless value for σ<sub>ref</sub>. The parameter T<sub>elec</sub> appears in the dimensionless form of Poisson's equation (see the [Reduced Units](userguide_4.0/UG_dft_units.html) web page). It is related to the Debye length; also note that the Bjerrum length is l<sub>B</sub> = d/T<sub>elec</sub>.
*   **Temp_K_plasma**(real): The temperature T in Kelvin used in calculating T<sub>elec</sub>.
*   **DielecConst_plasma**(real): The dielectric constant κ used in calculating T<sub>elec</sub>.
*   **Dielec_bulk**(real): The dielectric constant of the bulk fluid. If Dielec_ref<0, enter the ratio κ/78.5\. If Dielec_ref>0, enter the dielectric constant κ.
*   **Dielec_pore**(real): The dielectric constant for a "restricted" fluid (e.g. a fluid confined in a pore or near a surface). Again enter the ratio κ<sub>pore</sub>/78.5 if Dielec_ref<0 otherwise enter κ<sub>pore</sub>.
*   **Dielec_X**(real): The distance from the surfaces where the fluid will be considered to be restricted by a surface, and where Dielec_pore will be used.
*   **Dielec_wall[Nwall_type]**(real vector): The dielectric constant to be used inside the surfaces in the system (where ρ=0). Note that different surface types may be assigned different dielectric constants. Again enter the ratio κ<sub>surf</sub>/78.5 if Dielec_ref<0 otherwise enter κ<sub>surf</sub>.

***

[Privacy and Security](http://www.sandia.gov/general/privacy-security/index.html)
[Andrew Salinger](mailto:agsalin@sandia.gov) or [Laura Frink](mailto:ljfrink@colderinsights.com) - Site Contacts