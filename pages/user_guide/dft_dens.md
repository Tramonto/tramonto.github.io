---
title: Density fields...
folder: user_guide
permalink: dft_dens.html
---

## dft_dens.dat: density fields...

This file most often contains the solution vector fields as a function of the position in the mesh. The first three columns are $x$, $y$, and $z$. The following columns are the solution vector. The first few lines in the file summarize the variables that are printed by keywords. Depending on the calculation performed, these include the densities (for each fluid component), electrostatic field, chemical potentials, CMS-polymer mean fields, hard sphere nonlocal densities, cavity correlation functions for WTC polymer functionals, and bonding nonlocal densities for WTC polymer functionals.

There are a few variations to dft_dens.dat. For binodal tracking calculations where two solutions are solved simultaneously with a constraint of equal free energy, the second set of field variables is printed in dft_dens2.dat. Furthemore if one wants to save all density fields along a continuation curve, the output can be printed to sequentially numbered files (e.g. dft_dens.0, dft_dens.1, etc.) using the Print_rho_type parameter. Finally for the case of CMS polymers, the greens function propagator variables are printed in a file named dft_dens.datg (or dft_dens2.datg for binodal tracking, or dft_dens.0g for numbered printing).

Note that there is a change in Tramonto v3.0 compared to Tramonto v2.1\. For the CMS functional, the CMS field variable is now printed in dft_dens.dat in the form exp(-U), whereas in v2.1 it was printed as simply U. Restarts of old CMS results using the new code will therefore fail, unless the dft_dens.dat file is changed to reflect the new CMSFIELD variable.

***

[Privacy and Security](http://www.sandia.gov/general/privacy-security/index.html)
[Andrew Salinger](mailto:agsalin@sandia.gov) or [Laura Frink](mailto:ljfrink@colderinsights.com) - Site Contacts 