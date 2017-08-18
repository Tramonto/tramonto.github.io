---
title: Semi-Permeable Surface Parameters
folder: user_guide
permalink: semi_permeable_surface_parameters.html
---

## Semi-Permeable Surface Parameters

The parameters set up in this section allow some or all of the surfaces to be permeable to some or all of the fluid species in the system. Note that this parameter cannot be set up until all fluid and wall species are defined.

*   **Lsemiperm**[Nwall_type][Ncomp](int array): An array of integers (0=FALSE; 1=TRUE) that indicate if a given surface type should be treated as semipermeable with respect to a given fluid component. Note that if the first entry in the array is -2, the entire array will be set to FALSE. If the second entry in the array is -1, the entire array will be set to TRUE.
*   **Vext_membrane**[Nwall_type][Ncomp](real array): An array that sets the values of the external field (treated as a constant, noninfinite value) in a given surface for a specific component. If set to 0.0, the surface is invisible to the fluid. If set to a negative number, the fluid will preferentially accumulate in the surface. As Vext_membrane becomes larger and more positive, the fluid will be more strongly repelled from the core of the "surface". Note that this parameter is not used if Lsemiperm=FALSE (first entry of Lsemiperm=-2).

***

[Privacy and Security](http://www.sandia.gov/general/privacy-security/index.html)
[Andrew Salinger](mailto:agsalin@sandia.gov) or [Laura Frink](mailto:ljfrink@colderinsights.com) - Site Contacts 