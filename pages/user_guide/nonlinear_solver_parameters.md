---
title: Nonlinear Solver Control Parameters
folder: user_guide
permalink: nonlinear_solver_control_parameters.html
---

## Nonlinear Solver Control Parameters

These parameters control the nonlinear solver used in the calculation. Load balancing options are also included here.

*   **NL_Solver**(int): The type of nonlinear solver to use in the calculation. Options are:
    *   0: Built-In Newton Method: Often the method of choice; update damping is linked to physics in dft_newton.c.
    *   1: NOX Newton Method: library based Newton solver with numerical updates.
    *   2: Built-In Picard Method: simple successive substitution.
    *   3: NOX Picard Method: also simple successive substitution using some NOX routines.
    *   4: Built-In Picard/NOX method. This option runs a Picard method for Max_NL_iter iterations and then switches to the Built-In Newton Method. This can help if convergence from a simple initial guess is difficult.
*   **Max_NL_Iter**(int): The maximum number of nonlinear iterations the code will peform before exiting.
*   **Physics_Scaling**(int): Options for physics scaling in the WJDC code. This scaling can improve poor numerical performance that results from the term e<sup>μ</sup> that appears in the WJDC theory where μ is the chain chemical potential. Options are:
    *   0: Turn off physics scaling.
    *   1: Turn on automated physics scaling.
    *   2: Set physics scaling parameters manually.
*   **ATTInA22Block**(int): Logical (0=FALSE; 1=TRUE) for including attractions in A22 superblock of Schur complement system. FALSE is preferred, but sometimes preconditioning attractions can be helpful. For unstable systems, try setting to TRUE.
*   **Analyt_WJDC_JAC**(int): Logical (0=FALSE; 1=TRUE) to switch between approximate and analytic Jacobian options for WJDC functionals TRUE is preferred.
*   **Scale_fac_WJDC**[Npol_comp][Ncomp](real 2dvector): Manual entry of Scaling factors for WJDC cases.
*   **NL_rel_tol**(real): Relative convergence tolerance for the nonlinear Newton solver.
*   **NL_abs_tol**(real): Absolute convergence tolerance for the nonlinear Newton solver.
*   **NL_update_scalingParam**(real): During the nonlinear solve, the code will mix some fraction of the new solution in with the old solution at each iteration. In the case of Newton steps, this parameter is the minimum step size the code will take; however, updates are adaptive and as the solution is approached, full updates are usually reached. In the case of picard iterations, a very slow mixing of old and new solutions is usually needed. At this time, the Picard update fraction is not adaptive. For Newton solves we recommend setting the parameter between 0.1 and 1.0 (starting with 1.0). For Picard solves, typical values are 0.001 to 0.01\. When performing a mixed Picard/Nox solve set this parameter to about 0.2, and Tramonto will use a mixing parameter 100x smaller for the Picard steps.
*   **NL_rel_tol_picard**(real): Relative convergence tolerance for the nonlinear Picard solver.
*   **NL_abs_tol_picard**(real): Absolute convergence tolerance for the nonlinear Picard solver.
*   **Load_Bal_Flag**(int): Seclect option for load balancing the Tramonto problem. Options are:
    *   0: LB_LINEAR - This results in a linear partitioning of the matrix, but a recursive bisection partitioning of the matrix fill.
    *   1: LB_BOX - This results in a recursive bisection partitioning of the matrix fill and the matrix solve.
    *   2: LB_WEIGHTS - This results in a weighted recursive bisection partitioning of the matrix fill and the matrix solve where some nodes with simple residuals equations (i.e. density=zero in a surface) are given lesser weights than the remaining fluid nodes.
    
***

[Privacy and Security](http://www.sandia.gov/general/privacy-security/index.html)
[Andrew Salinger](mailto:agsalin@sandia.gov) or [Laura Frink](mailto:ljfrink@colderinsights.com) - Site Contacts 