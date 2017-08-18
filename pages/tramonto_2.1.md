---
title: Tramonto 2.1 
permalink: tramonto_2.1.html
---

## Tramonto-2.1

Tramonto is a real space matrix based code that solves the integral equations of certain implemented density functional theories (DFTs) as described under _Physics Capabilities_ below. We have included original citations related to the various functionals. The specifics of our implementations can be found in papers on our [Publication](publications.html) list. The numerical methods used in Tramonto are based on a real space finite element approach discretized on a cartesian grid using Newton's method along with a variety of solver and numerical analysis tools found in the Trilinos software package. Certain features of the numerical methods that are particularly helpful in efficient calculation of large systems are listed here under _Solvers and Numerical Methods_. Finally we note that Tramonto can als be compiled as a library and coupled with the [Towhee](http://towhee.sourceforge.net/) configurational bias Monte-Carlo (CBMC) code for use as an implicit solvent. Please vist the [People/Developers](snl_team.html) page for points of contact for the Tramonto software.

### PHYSICS CAPABILITIES

#### Hard-Sphere Atomistic Fluids

*   Hard-Sphere fluids: Rosenfeld's Original Fundamental Measures Theory.  
    _(Y. Rosenfeld, Free-energy model for the inhomogeneous hard-sphere fluid mixture and density-functional theory of freezing. Phys. Rev. Lett., 63:980, 1989.)_ .
*   Hard-Sphere fluids: a FMT with correct zero-dimensional crossover behavior.  
    _(Y. Rosenfeld, M. Schmidt, H. Lowen, and P. Tarazona. Fundamental-measure free-energy density functional for hard spheres: Dimensional crossover and freezing. Phys. Rev. E, 55:4245, 1997.)_ .
*   Hard-Sphere fluids: a FMT with Carnahan-Starling high pressure behavior.  
    _(R. Roth, R. Evans, A. Lang, and G. Kahl. Fundamental measure theory for hard-sphere mixtures revisited: the white bear version. J. Phys. Condens. Matter, 14:12063, 2002.)_ .

#### Extended NonCoulombic Potentials

*   12-6 Lennard Jones Fluids: attractions in a Weeks-Chandler-Anderson strict mean field perturbation approach. One of the hard-sphere FMT functionals must be chosen as a reference fluid.
*   12-6 Lennard Jones Fluids: Barker-Henderson corrections to soft repulsive core in a strict mean field perturbation approach. One of the hard-sphere FMT functionals must be chosen as a reference fluid.

#### Bonded Systems

*   Freely-jointed linear polymers using functional expansion truncated at second order (Chandler-McCoy-Singer (CMS) DFT). This implementation is based on the direct correlation function (DCF) for a bulk fluid at the bulk density of interest. The DCF can be obtained either from a molecular simulation or from PRISM theory. Another option is to generate a DCF for a suitable repulsive system (e.g. a hard-chain) and add extended potentials (e.g. dispersion attractions) in a strict mean field approach in the Tramonto code (see the [Users Guide](users_guides.html) for more information). Attractions are treated as a perturbation to the hard chains in the Tramonto implementation.  
    _(D. Chandler, J. D. McCoy, and S. J. Singer. J. Chem. Phys., 85:5971, 1986.)_  
    _(D. Chandler, J. D. McCoy, and S. J. Singer. J. Chem. Phys., 85:5977, 1986.)_  
    _(J. P. Donley, J. J. Rajasekaran, J. D. McCoy, and J. D. Curro. Microscopic approach to inhomogeneous polymeric liquids. J. Chem. Phys., 103(12):5061, 1995.)_
*   Freely-jointed branched polymers for CMS DFT  
    _unpublished extension_
*   Polymer chains based on Wertheim's theory implemented as a perturbation to atomistic hard spheres. One of the hard-sphere FMT functionals listed above must be chosen as a reference fluid.  
    _(S. Tripathi and W. G. Chapman. Microstructure and thermodynamics of inhomogeneous polymer blends and solutions. Phys. Rev. Lett., 94:087801, 2005.)_  
    _(S. Tripathi and W. G. Chapman. Microstructure of inhomogeneous polyatomic mixtures from a density functonal formalism for atomic mixtures. J. Chem. Phys., 122:094506, 2005.)_

#### Charged Systems

*   Electrolytes in a Poisson-Boltzmann approximation (point charges).
*   Electrolytes as a point charge perturbation to atomistic FMT based .
*   Restricted Primimitive Model Electrolytes: second order direct correlation function based correction to embedded point charges

#### Transport

*   Diffusion coupled DFT at steady state (spatially varying chemical potential field).  
    _(L.J.D. Frink, A. Thompson, and A.G. Salinger, Applying molecular theory to steady-state diffusing systems. J. Chem. Phys., 112: 7564-7571, 2000)._

### SOLVERS AND NUMERICAL METHODS

#### Discretization refinements

*   **Geometric Mesh Coarseneing**: Coarsen the mesh in powers of two at user specified distances from a surface. Since most of the complex solvation structure is resolved in a short distance this coarsening can speed up the computations significantly.
*   **Coarseneing of Jacobian Integration Stencils**: Implementation of an approximate Jacobian as specified by the user where the integration stencils used in computation of the Jacobian are more coarse than the integration stencils used in computation of the residual equations.
*   **Bulk fluid zone**: Regions in the domain a set distance from all surfaces in the system may be flagged as bulk regions. In these regions, the DFT equations are replaced by a simple set of equations enforcing uniform bulk conditions.
*   **Poisson-Boltzmann zone**: Regions in the domain a set distance all surfaces where the full DFT equations are replaced by a simple Poisson-Boltzmann approximation. This approximation is meant to capture electrostatic decay and short range solvation structure at a reduced cost. Note that this approximation is not fully debugged and tested.
*   **Reduced Dimension (Ndim=1) zone**: Regions in the domain where the solution is expected to vary only in 1 dimension even though the calculation is being done in higher dimensions. Note that the remaining variable dimension must be x so the system geomentry must be set up appropriately.

#### Solvers

*   **Krylov space iterative solvers**: The solver used in the Trilinos/Aztecoo package. These solvers were written for PDE applications. While they are not optimized for the integral equations found in DFTS, they are robust and usually work for solution of DFTS. The Aztecoo package has a variety of preconditioners that can be used for enhanced stability.
*   **Schur complement based linear solvers**: A solver strategy that has been optimized for the DFTs found in Tramonto. These solver strategies could likely be applied profitably in a more general context of integral equtions of finite range.

#### Continuation Algorithms

*   **Arc-length continuation**: A feature of the LOCA library. Allows for continuation of any continuous parameter. continuation around turning points is possible so metastable and unstable branches may be explicitly computed.
*   **Domain size continuation**: A feature of the Tramonto code not available for Arc-length continuation. Useful for generating surfaces forces information (force vs. separation of surfaces).

#### Algorithms for Phase Diagrams

*   **Turning point tracking**: A feature of the LOCA library that allows for tracing spinodals.
*   **Binodal tracking**: A feature of the LOCA library unique to the Tramonto implementation that allows for rapid enumeration of phase diagrams by enforcing two phase coexistence while varying the thermodynamic state point.

***

[Privacy and Security](http://www.sandia.gov/general/privacy-security/index.html)  