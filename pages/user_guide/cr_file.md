---
title: Defining bulk liquid state behavior for CMS polymer functionals
folder: user_guide
permalink: cr_file.html
---

## Cr_file.dat: defining bulk liquid state behavior for CMS polymer functionals

When using the CMS polymer functionals, an input of the direct correlation function (DCF) is required. 
The name (Cr_file) of the DCF file is defined by the user in dft_input.dat in the [polymer input section](UG_sect7.html). 
This input could come from PRISM theory calculations, from simulations, or from experiments. Note that the DCF does not need to be defined on the same mesh as the rest of the DFT problem, so for example, the spacing between r values might be 0.04, while the mesh size in the DFT calculation could be anything, e.g. 0.05 or 0.1, or 0.2. As of the v2.1 release, Tramonto currently takes the DCF for a repulsive chain with the same bond patterns as the polymer of interest to the DFT calculations. 
Attractions are added using the random phase approximation by assuming c(r)=-u_att(r) when r>d. 
See the [functional control parameter section](UG_sect3.html) for further information on the Type_poly and Type_attr settings. 
See examples of direct correlation functions files generated from PRISM theory in several of the Tramonto/Examples/POLY* directories.

***

[Privacy and Security](http://www.sandia.gov/general/privacy-security/index.html)
[Andrew Salinger](mailto:agsalin@sandia.gov) or [Laura Frink](mailto:ljfrink@colderinsights.com) - Site Contacts 