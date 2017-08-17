---
title: Polymer Input Parameters
folder: user_guide
permalink: polymer_input_parameters.html
---

## Polymer Input Parameters

These parameters define necessary information for polymer runs.

*   **Npol_comp**(int): The number of polymer components in the mixture of interest.
*   **Nblock**[Npol_comp](int vector): The number of distinct blocks in each of the polymer components.
*   **Block**[Npol_comp][Nblock[ipol_comp]](int array): The number of individual polymer segments in each block on each different polymer species.
*   **Block_type**[Npol_comp][Nblock[ipol_comp]](int array): The type of each block of segments. These are indexed starting with zero and should correspond with the physical parameters entered to described interaction potentials.
*   **Grafted**[Npol_comp](int array): An array of integers (0=FALSE, 1=TRUE) to indicate if the given polymer with polymer number Npol_comp is grafted to a surface. Polymers may only be grafted to planar surfaces with normals in the x-direction. Additionally, this option is only available for the CMS (Poly_type=0) and WJDC3 (Poly_type=5) functionals.
*   **Graft_wall**[Npol_comp](int array): An array specifying which wall number polymer Npol_comp is grafted to.
*   **Rho_g**[Npol_comp](int array): The chain grafting density on the wall, in units of chains/area. Note that this is distinct from Rho_b, which for the grafted chain case is used in the initial guess for the density profiles but is not part of the underlying theory.
*   **Type_poly_arch**(int): Directive for construction of a polymer chain. Options are:
    1.  0: POLY_ARCH_FILE: read in polymer structure from a file (see poly_file below). This is required for any branched chain system.
    2.  1: LIN_POLY: automatically set up a linear chain polymer.
    3.  2: LIN_POLY_SYM: automatically set up a linear chain polymer taking advantage of symmetry in the bonds (for homopolymers only).
*   **poly_file**(string): The file that contains polymer connectivity and bond symmetries if applicable.
*   **NCrfiles**(int): The number of direct correlation function files to be read in. Up to 4 are allowed, but most often this will be 1\. This is to facilitate careful continuation (or interpolation) between disparate direct correlation functions for CMS polymer functionals.
*   **Crfac**: A factor by which the first direct correlation function will be multiplied (for CMS polymers only). This should be between 0 and 1\. The second c(r) will then be multiplied by (1-Crfac), and the two direct correlation functions will be mixed. Note that this definition should be checked in the source code before computing as the desired mixing may be problem dependent.
*   **Cr_file1, Cr_file2, Cr_file3, Cr_file4**(strings): The file names that contain direct correlation function data to be used in CMS polymer calculations. Interpolation between the various files will be problem dependent and may require source code modification.
*   **Cr_break**[i=0 to NCr_files-2](real vector): A parameter to be used to set breakpoints between different c(r) files when automated continuation is performed on CMS polymer functionals. This parameter is problem dependent, and will require source code modification.
*   **Cr_rad**(real): The range of the direct correlation function in units of the segment size, Sigma_ff. CMS polymer DFT only.
    
***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a> 