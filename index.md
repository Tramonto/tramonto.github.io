---
title: Tramonto Project
keywords: sample homepage
tags: [getting_started]
permalink: index.html
---

## Welcome to the Tramonto Home Page: Software for Nanostructured Fluids in Materials and Biology

***

### Project goals

This project is based at Sandia National Laboratories, and is focused on developing molecular theory based computational tools for predicting the structure and properties of fluids at the nanoscale near surfaces and macromolecules. At this length scale fluids are inhomogeneous and common approximations for bulk fluids such as incompressibility do not apply. The specific capabilities of Tramonto and the related FasTram software packages are detailed in the Capability links to the left. In both cases, the molecular theories treated by the codes are fluid density functional theories (F-DFTs). These theories compute fluid structure near surfaces or as a result of self-assembly in contrast to quantum density functional theories (Q-DFTs) which are widely used to compute electronic structure of materials.

### Applications of Fluids-DFTs

Fluids Density Functional Theory approaches have been used to study a wide range of physical systems. Some examples are: fluids at interfaces, surface forces, colloidal fluids, wetting, porous media, capillary condensation, interfacial phase transitions, nucleation phenomena, freezing, self-assembly, lipid bilayers, ion channel proteins, solvation of surfaces and molecules. The characteristic particle size in F-DFT models ranges from atoms (e.g Argon) to colloidal particles, proteins, or cells. Thus these F-DFT approaches provide a multiscale framework for studying the physcis of many complex fluid systems. Some of these applications are represented in the publication list on the left, others may be found in a very diverse literature. The Tramonto code does not capture all of the F-DFT approaches that have been developed to date, but can be extended to new theories and models.

### Scientific Computing Approach.

For many years, application of F-DFTs to problems in inhomogeneous fluids was limited to systems with two dimensions of symmetry. In these special cases (fluids near planar surfaces, fluids in infinite cylindrical pores, etc), it is possible to perform the F-DFT integrals analytically in two dimensions while computational methods are needed to solve the problem in only one dimension. These 1D computational problems can can be performed on single processer computers using algorithms of limited sophistication (e.g. Picard iterative schemes). However, solving F-DFTs in problems with two or three computational dimensions quickly become very costly due to integral nature of the systems of equations. Simple iterative schemes are less satisfactory in these cases. Tramonto addresses the challenges of 2D and 3D systems with a combination of parallel computing and specialized linear solver algorithms that are coupled with a Newton's method approach where quadratic convergence is obtained. By utilizing the tools in the [Trilinos](http://trilinos.sandia.gov) framework, the solve of the F-DFT system of equations can also be coupled to a variety of engineering analysis tools such as arc-length continuation and optimization. These algorithms expand the utility of the software for engineering purposes such as rapid generation of phase diagrams and optimization of coarse-grained molecular models.

### Citing Tramonto

Publications that refer to the Tramonto software or contain results computed from the Tramonto software should cite the URL for this web site as well appropriate original [publication(s)](publications.html).

### Status of the Software

Tramonto-4.0.1 was released in November 2011 under the Lesser Gnu Public Licence (click [here](http://www.gnu.org/copyleft/lgpl.html) for details). The complete release history of for the Tramonto software can be found [here](release_history.html), and a link to release notes is provided in the navigation bar. If a bug is found, or you require installation help contact the Tramonto development team at [tramonto-help@software.sandia.gov](mailto:tramonto-help@software.sandia.gov). General user inquiries should be directed to [tramonto-users@software.sandia.gov](mailto:tramonto-users@software.sandia.gov).

### Acknowledgements

The development of the Tramonto code has been funded by:

*   The [Applied Mathematics Program](http://www.sc.doe.gov/ascr/Research/AppliedMath.html) of the Advanced Scientific Computing Research ([ASCR](http://www.sc.doe.gov/ascr/home.html)) Office at the Department of Energy.
*   The Laboratory Directed Research and Development (LDRD) program at Sandia National Laboratories.

### Related Links

*   [Trilinos](http://trilinos.sandia.gov) parallel solver library.
*   [LOCA](http://trilinos.sandia.gov/packages/nox) arc-length continuation package.
*   [Sandia National Laboratories home page](http://www.sandia.gov/)

***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a>