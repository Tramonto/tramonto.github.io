---
title: LOCA Continuation Parameters
folder: user_guide
permalink: loca_continuation_parameters.html
---

## LOCA Continuation Parameters

These parameters define how LOCA continuation capabiliites will be used in a Tramonto calcualtion. Note that the [LOCA documentation](https://trilinos.github.io/nox_and_loca_doxygen.html) provides more details on the library, and its integration with the NOX nonlinear solvers. While NOX is not the default nonlinear solver for Tramonto as of the v4.0 release, it may be accessed if Tramonto is configured using the option --with-nox-loca.

*   **Continuation Method**(int): Several types of continuation may be performed using LOCA. The options available to Tramonto are:
    *   -1: None.
    *   0: 0th order continuation using a constant step (non-adaptive).
    *   1: 1st order continuation.
    *   2: 2nd order, i.e. arc-length, continuation.
    *   3: Track spinodal (turning) points. If restarting, this requires two density files as input (dft_dens.dat and dft_dens2.dat).
    *   4: Track binodal points. In this case two different density solutions have the same free energy at the same state point. Use this capability to track phase transitions as continuous variables change. If restarting, this option requires two density files (dft_dens.dat and dft_dens2.dat) as input. These files should contain different density profiles of the two different morphologies at or near a state point where the free energies of the two branches cross.
*   **Continuation_Type**(int): This variable selects which of the continuous parameters of the system will be varied. Several basic types are available using the options listed in dft_input.dat. These include temperature, density, chemical potential, interaction energy parameters, electrostatic parameters, and the characteristics of semipermeable surfaces. However, continuation is possible with any combination of continuous variables (e.g. vary two densities simultaneously while holding the total bulk density constant). These user defined routines can be easily implemented in dft_plugin_user_continue.c. Indexing for user defined continuation capabilities must be 200<=Continuation_type<300\. IDs 0-100 are reserved for generic continuaion types, IDs 100-199 are reserved for archived but special purpose continuation types (found in dft_plugin_archived_continue.c).
*   **NID_Cont**: Indicates the number of IDs needed to identify which parameter will be varied. This is 0 in the case of temperature, 1 in the case of densities (e.g. Rho_b[icomp]), and 2 in the case of some interaction energy parameters (e.g. Eps_ff[icomp][jcomp]).
*   **ID1,ID2**: These are the ids associated with the parameter(s) that will be varied. Provide as many IDs as were indicated by NID_Cont.
*   **Step_size**(real): Initial value for the change in the parameter with continuation. This step size will be adjusted by the algorithm as continuation proceeds unless 0th order continuation is used. Large values will sometimes fail to converge, while small values can lead to very small step sizes along a continuation curve.
*   **N_steps**(int): The number of continuation steps to perform.
*   **Agressiveness**(real): A measure of how fast the algorithm will step along the continuation curve.
*   **Continuation_Type2, NID_Cont, ID1, ID2**(int): For binodal calculations (method 4), this is the second parameter that is varied in order to keep the two systems at the same free energy. It can be any of the implemented continuation parameters in the code. For example, one might have a phase transition at a given chemical potential (Rho_b) and temperature, and the goal is to track the transition as a function of temperature. Then the temperature should be the first continuation variable, that will be increased or decreased as specified by the Step_size parameter. The chemical potential variable will be the second parameter, and it will be adjusted by the code as necessary in order to maintain the system at the phase transition.
_One further note on continuation: It is possible to do mesh continuation in a binodal calculation. In that case, the N_steps parameter in this section should be set to 0, and mesh continuation will be handled in an outer loop outside the LOCA routines. This allows for some improved efficiency when generating phase transitions with mesh size as one of the parameters._

***

[Privacy and Security](http://www.sandia.gov/general/privacy-security/index.html)
[Andrew Salinger](mailto:agsalin@sandia.gov) or [Laura Frink](mailto:ljfrink@colderinsights.com) - Site Contacts
