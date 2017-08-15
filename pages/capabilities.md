---
title: Capabilities
permalink: capabilities.html
---

**Tramonto 4.x Summary of Capabilities**

***

This page contains information specific to Tramonto 4.0. 
Click the following links for capabilities of previous releases: [Capabilities: Tramonto v3.0/3.1](../Tramonto3.0_Web/tramonto3_0.html) or [Capabilities: Tramonto v2.1](../Tramonto2.1_Web/tramonto.html). 
For information on our previous work on FFT based DFT methods see the [FasTram](../FasTram_Web/fastram.html) page.

# Summary

Tramonto is a real space matrix based code that solves the integral equations of certain implemented density functional theories (DFTs) as described under _Physics Capabilities_ below. 
We have included original citations related to the various functionals. 
The specifics of our implementations can be found in papers on our [Publication](publications.html) list. 
The numerical methods used in Tramonto are based on a real space finite element approach discretized on a cartesian grid using Newton's method along with a variety of solver and numerical analysis tools found in the Trilinos software package. 
Certain features of the numerical methods that are particularly helpful for efficient calculation of large systems are listed here under _Solvers and Numerical Methods_. 
Tramonto can be compiled as a library and coupled with the [Towhee](http://towhee.sourceforge.net/) configurational bias Monte-Carlo (CBMC) code for use as an implicit solvent. 
Please visit the [People/Developers](snl_team.html) page for points of contact for the Tramonto software.

## WHAT'S NEW IN TRAMONTO 4.0

The Tramonto 4.0 release delivers a cmake based build that is compatible with trilinos v10.x. 
It delivers new physics capabilities in the areas of electrostatics, hard sphere models, mean-field interaction models, and greatly expanded capabilities for treating surface geometries and surface-fluid interactions. 
Schur solvers for charged polymers have been implemented, and automated output for bulk mode and sum-rule analysis have be added. 
There are more than 130 Example problems included in the Tramonto 4.0 release, with the largest number of new examples in the area of 2D and 3D surface geometries. 
A variety of bug fixes have been implemented including corrected energy calculations for electrostatics systems.

## TYPES OF CALCULATIONS THAT CAN BE DONE WITH TRAMONTO-4.0

Density functional theories can be used in a wide variety of contexts. 
This list captures many categories of problems that may be tackled using the Tramonto software.

*   Pure bulk fluids - state parameters.
*   Fluid mixtures - state parameters.
*   Phase equilibria for bulk fluids and mixtures. For example: Liquid-vapor equilibria, Pxy diagrams, and partitioning.
*   Self-assembled systems. Interface structures and competing phases.
*   Two phase interfaces (one phase on left side of domain, another phase on right side of domain).
*   Fluid structure near surfaces.
*   Diffusing fluid systems at steady state.
*   Interfacial fluid phase transitions.
*   Atomistic and bonded fluid models.
*   Neutral and charged systems.
*   Surfaces that are combinations of simple geometric shapes.
*   Surfaces based on collections of atomic coordinates.

## ALGORITHMS FOR RAPID INVESTIGATION OF STATE SPACE WITH TRAMONTO

The algorithms listed here are particularly helpful for rapid investigation of phase diagrams and state space. 
They are available to the Tramonto application by linking with the LOCA library found in the Trilinos solver package.

## Continuation Algorithms

*   Arc-length continuation: A feature of the LOCA library. Allows for continuation of any continuous parameter. 
Continuation around turning points is possible so that metastable and unstable branches may be explicitly computed.
*   Domain size continuation: A feature of the Tramonto code that is useful for generating surfaces forces information (force vs. separation of surfaces). 
As a discontinous parameter it is not available for Arc-length continuation, but may be used in conjunction with Binodal tracking (see below) to compute phase diagrams of confined fluids.

## Algorithms for Phase Diagrams

*   Turning point tracking: A feature of the LOCA library that allows for tracing numerical spinodals.
*   Binodal tracking: A feature of the LOCA library that allows for rapid enumeration of phase diagrams by enforcing two phase coexistence while varying the thermodynamic state point.

## PHYSICS CAPABILITIES

## Hard-Sphere Atomistic Fluids

*   Hard-Sphere fluids (FMT1): Rosenfeld's original Fundamental Measures Theory (FMT).  
    _(Y. Rosenfeld, Free-energy model for the inhomogeneous hard-sphere fluid mixture and density-functional theory of freezing. Phys. Rev. Lett., 63:980, 1989.)_
*   Hard-Sphere fluids (FMT2): a FMT with correct zero-dimensional crossover behavior.  
    _(Y. Rosenfeld, M. Schmidt, H. Lowen, and P. Tarazona. Fundamental-measure free-energy density functional for hard spheres: Dimensional crossover and freezing. Phys. Rev. E, 55:4245, 1997.)_
*   Hard-Sphere fluids (FMT3): a FMT based on the Mansoori-Carnahan-Starling-Leland (MCSL) equation of state (known as the "White Bear" FMT).  
    _(R. Roth, R. Evans, A. Lang, and G. Kahl. Fundamental measure theory for hard-sphere mixtures revisited: the white bear version. J. Phys. Condens. Matter, 14:12063, 2002.)_
*   Hard-Sphere fluids (FMT4): an extension of the White Bear FMT (FMT3), which accounts for correct "dimensional crossover" at high density, as in FMT2\.  
    _(A. Oleksy and J.-P. Hansen. Towards a microscopic theory of wetting by ionic solutions I. Surface properties of the semi-primitive model. Mol. Phys., 104:2871, 2006.)_
*   NOTE: Barker-Henderson diameters may be used if there is an extended non-Coulombic potential in the problem. Otherwise particle diameters are used in calculation of the hard sphere terms.

## Functional Forms for Mean-Field Pair Interactions

Pair interactions are included in the energy functional as a perturbation to the hard core interactions (defined by the FMT options above). 
In the strict mean field approach currently available in Tramonto, pair interactions are included in the energy functionals as F<sub>att</sub>=1/2∑<sub>i,j</sub>∫ ∫ ρ<sub>i</sub>(r)ρ<sub>j</sub>(r')u<sub>ij</sub>(r,r')dr dr'.

In performing the numerical integrals associated with F<sub>att</sub>, it is necessary to select a method for treating the inner core region of the pair potential. Both the range of the inner core region and the way it will be treated must be defined. Implementations in Tramonto 4.0 include:

*   Weeks-Chandler-Andersen (WCA) definition of the core potential. In this case u<sub>core</sub>=u<sub>min</sub>(r<sub>min</sub>), where the core potential is defined as a constant determined by the potential minimum. This classic approach is well suited to pair potentials with a short-range steep repulsion and a longer-range soft attraction such as a 12-6 Lennard-Jones potential. _(J. D. Weeks, D. Chandler, and H. C. Andersen. Role of repulsive forces in determining the equilibrium structure of simple liquids. J. Chem. Phys., 54:5237, 1971.)_
*   Zero core potential. In this case u<sub>core</sub>=0 for 0<=r<σ\. This option is suitable for cases where the pair potential of interest is purely repulsive or attractive so there is no u<sub>min</sub>.
*   Constant potential based on particle size, u<sub>core</sub>=u(r=σ). This option is suitable for cases where the pair potential of interest is purely repulsive or attractive so there is no u<sub>min</sub>. This may or may not be identical to the Zero core potential case.
*   Combination of zero core and WCA where u<sub>core</sub>=0 for (r<=σ) and u<sub>core</sub>=u<sub>min</sub> (for r<sub>min</sub> >=r>σ).
*   Alternate combination of zero core and WCA where u<sub>core</sub>=0 for (r<=r<sub>zero</sub>) and u<sub>core</sub>=u<sub>min</sub> (for r<sub>min</sub> >=r>σ). In this case, Tramonto locates the zero of the potential which may be different from σ and defines that distance as r<sub>zero</sub>.

## Extended Non-Coulombic Potentials for use with Strict Mean Field Attractions

<sub>ij</sub>

*   12-6 Lennard-Jones Fluids: attractions in a Weeks-Chandler-Anderson strict mean field perturbation approach.
*   Yukawa Fluids: exponentially decaying attractive or repulsive interactions often used to model colloidal systems.  
    _S.A. Egorov. Effect of repulsive and attractive interactions on depletion forces in colloidal suspensions: A density functional theory treatment. Phys Rev E, V. 70, 031401, 2004\._
*   Repulsive-Core combined with Yukawa in several forms:
    *   summed 12-6 Lennard-Jones and Yukawa potential
    *   summed r<sup>12</sup> and Yukawa potential
    *   summed r<sup>n</sup> and Yukawa (_variable n_) potential
*   Exponential potential, of the form u<sub>ij</sub> = -&epsilon<sub>ij</sub> exp[-(r-&sigma<sub>ij</sub>)/&alpha<sub>ij</sub>].
*   Square-Well potential.
*   Coulombic potentials can also be treated as pair interactions using a cut and shifted strict mean field approach. 
However, the coupled Poisson's approach is preferred for maintaining charge neutrality.

## Bonded Systems

*   CMS-DFT (Chanlder-McCoy-Singer): Freely-jointed linear polymers using functional expansion truncated at second order. This implementation is based on the direct correlation function (DCF) for a bulk fluid at the bulk density of interest. The DCF can be obtained either from a molecular simulation or from PRISM theory.  
    Another option is to generate a DCF for a suitable repulsive system (e.g. a hard-chain) and add extended potentials (e.g. dispersion attractions) in a strict mean field approach in the Tramonto code. Attractions are treated as a perturbation to the hard chains in the Tramonto implementation.  
    _(D. Chandler, J. D. McCoy, and S. J. Singer. J. Chem. Phys., 85:5971, 1986; ibid, 85:5977, 1986.)_  
    _(J. P. Donley, J. J. Rajasekaran, J. D. McCoy, and J. D. Curro. Microscopic approach to inhomogeneous polymeric liquids. J. Chem. Phys., 103(12):5061, 1995.)_  
    _(A. L. Frischknecht, J. D. Weinhold, A. G. Salinger, J. G. Curro, and L. J. D. Frink. Density functional theory for inhomogeneous polymer systems. I. Numerical methods. J. Chem. Phys., 117:10385, 2002.)_
*   CMS-DFT for branched (freely jointed) polymers.  
    _unpublished extension available in Tramonto._
*   iSAFT, or WTC-DFT (Wertheim, Tripathi, Chapmn): theory for bonded systems. This implementation treats bonded systems as a perturbation to hard spheres using a Wertheim's theory based approach. One of the hard-sphere FMT functionals listed above must be chosen as a reference fluid.  
    _(S. Tripathi and W. G. Chapman. Microstructure and thermodynamics of inhomogeneous polymer blends and solutions. Phys. Rev. Lett., 94:087801, 2005.)_  
    _(S. Tripathi and W. G. Chapman. Microstructure of inhomogeneous polyatomic mixtures from a density functonal formalism for atomic mixtures. J. Chem. Phys., 122:094506, 2005.)_
*   modified iSAFT, or WJDC-DFT (Werthim, Jain, Dominik, and Chapman) theory for bonded systems. This theory improves on the WTC theory in capturing stoichiometry constraints inherant to bonded systems. Like the WTC functional, this approach treats bonded systems as a perturbation to hard sphere fluids.  
    _(S. Jain, A. Dominik, and W.G. Chapman. Modified interfacial statistical associating fluid theory: A perturbation density functional theory for inhomogeneous complex fluids. J. Chem. Phys., 127:244904, 2007.)_
*   WJDC-DFT (modified iSAFT) for branched chain systems. Tramonto 3.0 and later include the extension of the WJDC approach to branched systems. _We would like to thank Shekhar Jain and Walter Chapman for providing results on branched chains in advance of publication._
*   Tethered (grafted) polymers: Polymers can be grafted to planar walls with normals in the x-direction, in 1D systems. This functionality is available for the CMS and WJDC3 functionals. The treatment follows that described in the paper by Jain et al. listed here.  
    _(S. Jain, P. Jog, J. Weinhold, R. Srivastava, and W. G. Chapman. Modified interfacial statistical associating fluid theory: Application to tethered polymer chains. J. Chem. Phys., 128:154910, 2008\. We thank Shekhar Jain for assistance.)_

## Charged Systems

*   Electrolytes in a Poisson-Boltzmann approximation (point charges; equivalent to the nonliner Poisson-Boltzmann equation).
*   Electrolytes as charged hard spheres, employing one of the FMT functionals and mean-field electrostatics (note: non-Coulombic effects may also be included in the model).  
    _(Z. Tang, L. Mier-y-Teran, H.T. Davis, L.E. Scriven, and H.S. White. Non-local free energy density functional theory applied to the electrical double layer. Molecular Physics, 71:369-392, 1990)._
*   Restricted Primitive Model Electrolytes: second order direct correlation function based correction to the free energy for symmetric charged hard spheres.  
    _(Z. Tang, L.E. Scriven, and H.T. Davis. A three-component model of the electrical double layer. J. Chem. Phys., 97:494, 1992.; Z. Tang, L.E. Scriven, and H.T. Davis. Interactions between primitive electrical double layers. J. Chem. Phys., 97:9258, 1992.)_
*   Semi-Primitive Model Electrolytes: extension that includes the second order direct correlation function term for mixtures of charged hard spheres with any size.  
    _(A. Oleksy and J.-P. Hansen. Towards a microscopic theory of wetting by ionic solutions I. Surface properties of the semi-primitive model. Mol. Phys., 104:2871, 2006.)_

## Transport

*   Diffusion coupled DFT at steady state (spatially varying chemical potential field).  
    _(L.J.D. Frink, A. Thompson, and A.G. Salinger, Applying molecular theory to steady-state diffusing systems. J. Chem. Phys., 112: 7564-7571, 2000)._

## SOLVERS AND NUMERICAL METHODS

## Discretization refinements

*   **Geometric Mesh Coarsening**: Coarsen the mesh in powers of two at user specified distances from a surface. Since most of the complex solvation structure is resolved in a short distance this coarsening can speed up the computations significantly.
*   **Coarsening of Jacobian Integration Stencils**: Implementation of an approximate Jacobian as specified by the user where the integration stencils used in computation of the Jacobian are more coarse than the integration stencils used in computation of the residual equations.
*   **Bulk fluid zone**: Regions in the domain a set distance from all surfaces in the system may be flagged as bulk regions. In these regions, the DFT equations are replaced by a simple set of equations enforcing uniform bulk conditions.
*   **Poisson-Boltzmann zone**: Regions in the domain a set distance from all surfaces where the full DFT equations are replaced by a simple Poisson-Boltzmann approximation. This approximation is meant to capture electrostatic decay and short range solvation structure at a reduced cost. Note that this approximation is not fully debugged and tested.
*   **Reduced Dimension (Ndim=1) zone**: Regions in the domain where the solution is expected to vary only in 1 dimension even though the calculation is being done in higher dimensions. Note that the remaining variable dimension must be x so the system geometry must be set up appropriately.

## Non-Linear Solvers

*   **Newton Method solvers** : These solvers include both density and other fields (nonlocal densities, chain propagator equations etc) as explicit fields in the solve. They exhibit quadratic convergence and good stability with a good initial guess. Both NOX solvers and locally developed solvers are available. Often the solution is obtained in O(20) or less nonlinear iterations.
*   **Picard solvers** : These solvers are based on successive substitution of the density residual equation with updates of other fields. Small fractional updates (perhaps 0.2% updates) may be required for convergence. The solution may require O(1000) or more nonlinear iterations. These solvers require much less memory than the Newton solvers. They can be more stable in the case of a poorly conditioned system where it is difficult to converge without a very good initial guess. Again, both NOX and built-in capabilities are available.
*   **Mixed Picard/Newton solvers**: In this case, Picard iterations are used for a preset iteration count to relax an initial guess slowly before attempting Newton solves. Both NOX and built-in capabilities are available.

## Linear Solvers

*   **Krylov space iterative solvers**: The solver used in the Trilinos/Aztecoo package. These solvers were written for PDE applications. While they are not optimized for the integral equations found in DFTS, they are robust and usually work for solution of DFTS. The Aztecoo package has a variety of preconditioners that can be used for enhanced stability.
*   **Schur complement based linear solvers**: A solver strategy that has been optimized for the DFTs found in Tramonto. These solver strategies could likely be applied profitably in a more general context of integral equations of finite range.  
    _(M. A. Heroux, A. G. Salinger, and L. J. D. Frink. Parallel segregated Schur complement methods for fluid density functional theories. SIAM J. Sci. Comput., 29:2059, 2007.)_
    
***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a>    