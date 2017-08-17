---
title: Dimension Control Parameters
folder: user_guide
permalink: dimension_control_parameters.html
---

## Dimension Control Parameters

These parameters define what kind of dimensions will be set in the input file. 
Note that if these values are set to any negative number, it is assumed that the input is all provided in dimensionless parameters. 
Otherwise the values entered here will be used to reduce all other parameters provided. 
For more information on the details of dimensionless parameters in Tramonto calculations, see the [Reduced Units](UG_dft_units.html) web page.

*   **Length_ref**(real): A reference length to use for making calculations dimensionless. Set as follows:
    *   -1.0 - indicates that all length parameters will be entered in reduced units (L/σ<sub>ref</sub>).
    *   >0.0 - to specify a characteristic size(σ<sub>ref</sub>) of one of the fluid species in some real units. All other variables with units of Length (e.g. Size of computational domain) must all be entered in the same real units. All length parameters are then reduced using Parameter/Length_ref.
*   **Density_ref**(real): A reference density to use for making calculations dimensionless. Set as follows:
    *   -1.0 - indicates that all density parameters will be entered in reduced units (ρσ<sup>3</sup><sub>ref</sub>).
    *   >0.0 - to specify a characteristic density (ρ<sub>ref</sub>σ<sup>3</sup><sub>ref</sub>). This reference density must provide an appropriate conversion factor between the real unit densities desired for entry in the input file (e.g. Molar) and the reduced densities in units of ρσ<sup>3</sup><sub>ref</sub>. Input densities are converted to reduced form densities using the formula (Density Parameter)/Density_ref.
*   **Temp**(real): Temperature reference parameter. Set as follows:
    *   -1 - indicates that all energy parameters will be entered in reduced units (ε/kT) where k is the Boltzmann constant.
    *   >0.0 - to specify the Temperature in Kelvin. All energy parameters must then entered as ε/k(also units of Kelvin). Reduced energies ε/kT will then be computed using the temperature provided.
*   **Dielec_ref**(real): Base value for dielectric constant for a charged system (κ).
    *   -1 - set to the default value of κ=78.5
    *   >0 - set some other value for κ in the bulk fluid.
*   **VEXT_MAX**(real): This parameter is always >0 and entered in kT units. This is the maximum external field, V<sub>ext</sub> where DFT equations will be solved. If V<sub>ext</sub>>VEXT_MAX then the fluid density is set strictly to zero. Note that in ideal systems, ρ(r)∝exp(-V<sub>ext</sub>(r)/kT). As a result, a large Vext value results in very small densities that can be difficult to resolve numerically. VEXT_MAX is typically between 10 and 20\.

***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a> 