---
title: Tramonto 3.0/3.1 
permalink: tramonto_3.0-3.1.html
---

## Tramonto-3.0/3.1

Tramonto is a real space matrix based code that solves the integral equations of certain implemented density functional theories (DFTs) as described under _Physics Capabilities_ below. We have included original citations related to the various functionals. The specifics of our implementations can be found in papers on our [Publication](publications.html) list. The numerical methods used in Tramonto are based on a real space finite element approach discretized on a cartesian grid using Newton's method along with a variety of solver and numerical analysis tools found in the Trilinos software package. Certain features of the numerical methods that are particularly helpful for efficient calculation of large systems are listed here under _Solvers and Numerical Methods_. Finally we note that Tramonto can als be compiled as a library and coupled with the [Towhee](http://towhee.sourceforge.net/) configurational bias Monte-Carlo (CBMC) code for use as an implicit solvent. Please vist the [People/Developers](snl_team.html) page for points of contact for the Tramonto software.

### TYPES OF CALCULATIONS THAT CAN BE DONE WITH TRAMONTO-3.0/3.1

Density functional theories can be used in a wide variety of contexts. This list captures several categories of problems that are currently represented in the Tramonto 3.0/3.1 test harness which has more than 80 Example problems.

*   Pure bulk fluids - state parameters.
*   Fluid mixtures - state parameters.
*   Phase equilibria for bulk fluids and mixtures. For example: Liquid-vapor equilibia, Pxy diagrams, and partitioning.
*   Self-assembled systems. Interface structures and competing phases.
*   Two phase interfaces (one phase on left side of domain another phase on right side of domain).
*   Fluid structure near surfaces.
*   Diffusing fluid systems at steady state.
*   Intefacial fluid phase transitions.
*   atomistic and bonded fluid models.
*   neutral and charged systems.
*   Surfaces that are combinations of simple geometric shapes.
*   Surfaces based on of collections of atomic coordinates.

### ALGORITHMS FOR RAPID INVESTIGATION OF STATE SPACE WITH TRAMONTO

The algorithms listed here are particularly helpful for rapid investigation of phase diagrams and state space. They are available to the Tramonto application by linking with the LOCA library found in the the Trilinos solver package.

#### Continuation Algorithms

*   Arc-length continuation: A feature of the LOCA library. Allows for continuation of any continuous parameter. continuation around turning points is possible so metastable and unstable branches may be explicitly computed.
*   Domain size continuation: A feature of the Tramonto code that is useful for generating surfaces forces information (force vs. separation of surfaces). As a discontinous parameter it is not available for Arc-length continuation, but may be used in conjunction with Binodal tracking (see below) to compute phase diagrams of confined fluids.

#### Algorithms for Phase Diagrams

*   Turning point tracking: A feature of the LOCA library that allows for tracing numerical spinodals.
*   Binodal tracking: A feature of the LOCA library that allows for rapid enumeration of phase diagrams by enforcing two phase coexistence while varying the thermodynamic state point.

### PHYSICS CAPABILITIES

#### Hard-Sphere Atomistic Fluids

*   Hard-Sphere fluids (FMT1): Rosenfeld's Original Fundamental Measures Theory.  
    _(Y. Rosenfeld, Free-energy model for the inhomogeneous hard-sphere fluid mixture and density-functional theory of freezing. Phys. Rev. Lett., 63:980, 1989.)_ .
*   Hard-Sphere fluids (FMT2): a FMT with correct zero-dimensional crossover behavior.  
    _(Y. Rosenfeld, M. Schmidt, H. Lowen, and P. Tarazona. Fundamental-measure free-energy density functional for hard spheres: Dimensional crossover and freezing. Phys. Rev. E, 55:4245, 1997.)_ .
*   Hard-Sphere fluids (FMT3): a FMT with Carnahan-Starling high pressure behavior.  
    _(R. Roth, R. Evans, A. Lang, and G. Kahl. Fundamental measure theory for hard-sphere mixtures revisited: the white bear version. J. Phys. Condens. Matter, 14:12063, 2002.)_ .
*   NOTE: Barker-Henderson diameters may be used if there is an extended non-Coulombic Potential in the problem. Otherwise particle diameters are used in calculation of the hard sphere terms.

#### Extended NonCoulombic Potentials

*   12-6 Lennard Jones Fluids: attractions in a Weeks-Chandler-Anderson strict mean field perturbation approach. One of the hard-sphere FMT functionals must be chosen as a reference fluid.
*   Yukawa Fluids: exponentially decaying attractive or repulsive interactions often used to model colloidal systems.  
    _S.A. Egorov. Effect of repulsive and attractive interactions on depletion forces in colloidal suspensions: A density functional theory treatment. Phys Rev E, V. 70, 031401, 2004\._

#### Bonded Systems

*   CMS-DFT (Chanlder-McCoy-Singer): Freely-jointed linear polymers using functional expansion truncated at second order. This implementation is based on the direct correlation function (DCF) for a bulk fluid at the bulk density of interest. The DCF can be obtained either from a molecular simulation or from PRISM theory.  
    Another option is to generate a DCF for a suitable repulsive system (e.g. a hard-chain) and add extended potentials (e.g. dispersion attractions) in a strict mean field approach in the Tramonto code. Attractions are treated as a perturbation to the hard chains in the Tramonto implementation.  
    _(D. Chandler, J. D. McCoy, and S. J. Singer. J. Chem. Phys., 85:5971, 1986.)_  
    _(D. Chandler, J. D. McCoy, and S. J. Singer. J. Chem. Phys., 85:5977, 1986.)_  
    _(J. P. Donley, J. J. Rajasekaran, J. D. McCoy, and J. D. Curro. Microscopic approach to inhomogeneous polymeric liquids. J. Chem. Phys., 103(12):5061, 1995.)_
*   CMS-DFT for branched (freely jointed) polymers.  
    _unpublished extension available in Tramonto._
*   iSAFT, or WTC-DFT (Wertheim, Tripathi, Chapmn): theory for bonded systems. This implementation treats bonded systems as a perturbation to hard spheres using a Wertheim's theory based approach. One of the hard-sphere FMT functionals listed above must be chosen as a reference fluid.  
    _(S. Tripathi and W. G. Chapman. Microstructure and thermodynamics of inhomogeneous polymer blends and solutions. Phys. Rev. Lett., 94:087801, 2005.)_  
    _(S. Tripathi and W. G. Chapman. Microstructure of inhomogeneous polyatomic mixtures from a density functonal formalism for atomic mixtures. J. Chem. Phys., 122:094506, 2005.)_
*   modified iSAFT, or WJDC-DFT (Werthim, Jain, Dominik, and Chapman) theory for bonded systems. This theory improves on the WTC theory in capturing stoichiometry constraints inherant to bonded systems. Like the WTC functional, this approach treats bonded systems as a perturbation to hard sphere fluids. _(S. Jain, A. Dominik, and W.G. Chapman. Modified interfacial statistical associating fluid theory: A perturbation density functional theory for inhomogeneous complex fluids. J. Chem. Phys., 127:244904, 2007.)_
*   WJDC-DFT (modified iSAFT) for branched chain systems. Tramonto 3.0 includes the extension of the WJDC approach to branched systems. _(S. Jain and W.G. Chapman. Modiﬁed Interfacial Statistical Associating Fluid Theory: Extension to inhomogenous branched polymers, Shekhar Jain and Walter G. Chapman, in preparation for J. Chem. Phys., 2009.). We would like to thank Shekhar Jain and Walter Chapman for providing results on branched chains in advance of publication._
*   Tethered (grafted) polymers: Polymers can be grafted to planar walls with normals in the x-direction, in 1D systems. This functionality is available for the CMS and WJDC3 functionals. The treatment follows that described in the paper by Jain et al. listed here.  
    _(S. Jain, P. Jog, J. Weinhold, R. Srivastava, and W. G. Chapman. Modified interfacial statistical associating fluid theory: Application to tethered polymer chains. J. Chem. Phys., 128:154910, 2008\. We thank Shekhar Jain for assistance.)_

#### Charged Systems

*   Electrolytes in a Poisson-Boltzmann approximation (point charges).
*   Electrolytes as a point charge perturbation to atomistic FMT based model (note: non-Coulombic effects may alos be included in th model.  
    _(Z. Tang, L. Mier-y-Teran, H.T. Davis, L.E. Scriven, and H.S. White. Non-local free energy density functional theory applied to the electrical double layer. Molecular Physics, 71:369-392, 1990)._
*   Restricted Primimitive Model Electrolytes: second order direct correlation function based correction to embedded point charges.  
    _(Z. Tang, L.E. Scriven, and H.T. Davis. Interactions between primitive electrical double layers. J. Chem. Phys., 97:9258, 1992.)_
*   Electrolytes where both the ions and the solvent have finite size, but dielectric constant is still treated as a continuum parameter.  
    _(Z. Tang, L.E. Scriven, and H.T. Davis. A three-component model of the electrical double layer. J. Chem. Phys., 97:494, 1992.)_

_

#### Transport

*   Diffusion coupled DFT at steady state (spatially varying chemical potential field).  
    _(L.J.D. Frink, A. Thompson, and A.G. Salinger, Applying molecular theory to steady-state diffusing systems. J. Chem. Phys., 112: 7564-7571, 2000)._

_

_

### SOLVERS AND NUMERICAL METHODS

#### Discretization refinements

*   **Geometric Mesh Coarseneing**: Coarsen the mesh in powers of two at user specified distances from a surface. Since most of the complex solvation structure is resolved in a short distance this coarsening can speed up the computations significantly.
*   **Coarseneing of Jacobian Integration Stencils**: Implementation of an approximate Jacobian as specified by the user where the integration stencils used in computation of the Jacobian are more coarse than the integration stencils used in computation of the residual equations.
*   **Bulk fluid zone**: Regions in the domain a set distance from all surfaces in the system may be flagged as bulk regions. In these regions, the DFT equations are replaced by a simple set of equations enforcing uniform bulk conditions.
*   **Poisson-Boltzmann zone**: Regions in the domain a set distance all surfaces where the full DFT equations are replaced by a simple Poisson-Boltzmann approximation. This approximation is meant to capture electrostatic decay and short range solvation structure at a reduced cost. Note that this approximation is not fully debugged and tested.
*   **Reduced Dimension (Ndim=1) zone**: Regions in the domain where the solution is expected to vary only in 1 dimension even though the calculation is being done in higher dimensions. Note that the remaining variable dimension must be x so the system geomentry must be set up appropriately.

#### Non-Linear Solvers

*   **Newton Method solvers** : These solvers include both density and other fields (nonlocal densities, chain propagator equations etc) as explicit fields in the solve. They exhibit quadratic convergence and good stability with a good initial guess. Both NOX solvers and locally developed solvers are available. Often the solution is obtained in O(20) or less nonlinear iterations.
*   **Picard solvers** : These solvers are based on successive substitution of the density residual equation with updates of other fields. Small fractional updates (perhaps 0.2% updates)may be required for convergence. The solution may require O(1000) or more nonlinear iterations. These solvers require much less memory than the Newton solvers. They can be more stable in the case of a poorly conditioned system where it is difficult to converge without a very good initial guess. Again, both NOX and built-in capabilities are available.
*   **Mixed Picard/Newton solvers**: In this case, Picard iterations are used for a preset iteration count to relax an initial guess slowly before attempting Newton solves. Both NOX and built-in capabilities are available.

#### Linear Solvers

*   **Krylov space iterative solvers**: The solver used in the Trilinos/Aztecoo package. These solvers were written for PDE applications. While they are not optimized for the integral equations found in DFTS, they are robust and usually work for solution of DFTS. The Aztecoo package has a variety of preconditioners that can be used for enhanced stability.
*   **Schur complement based linear solvers**: A solver strategy that has been optimized for the DFTs found in Tramonto. These solver strategies could likely be applied profitably in a more general context of integral equtions of finite range.

***

[Privacy and Security](http://www.sandia.gov/general/privacy-security/index.html)  