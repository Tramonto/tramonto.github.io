---
title: Linear Solver Control Parameters
folder: user_guide
permalink: linear_solver_control_parameters.html
---

## Linear Solver Control Parameters

These parameters control the iterative linear solvers used to solve the linear system arising at each Newton step of the nonlinear solve. One may choose to solve a linear system with the Schur complement of the Jacobian (using the _Schur solver>_) or a linear system with the full Jacobian. The Schur solver is strongly recommended.

*   **L_Schur**(int): A logical (0=FALSE; 1=TRUE) to turn on segregated Schur solver approach of Heroux, Salinger and Frink (SIAM, 2007). This solver uses a preconditioned GMRES iteration to solve the Schur complement of the Jacobian at each Newton step of the nonlinear solve. This technique leverages the rich structure of the Schur complement of DFT problems for fast matrix-vector multiplications with the Schur complement matrix, as well as an efficient and scalable preconditioner for the Schur complement system. The reduced size and better conditioning of the Schur complement system makes it in general much faster than using the full Jacobian. <cr>**It is recommended that this parameter be set to TRUE (1).**</cr>
_The parameters below define how the iterative linear solves will be performed when solving linear systems using the full Jacobian at each Newton step (LSchur=FALSE). These parameters have no effect when using the Schur solver. Tramonto uses linear solver found in the Trilinos AztecOO package. More information on these parameters and additional options are available in the AztecOO solver package and can be found in the [AztecOO Users Guide](http://trilinos.sandia.gov/packages/aztecoo/documentation.html)._
*   **Solver**(int): The specific linear solver in AztecOO to be used. **The GMRES solver (option 0) is recommended**. Tramonto options are:
    *   0: GMRES (Generalized Minimum Residual). This solver is suitable for general (nonsymmetric) linear systems.
    *   1: CG (Conjugate Gradients). This solvers is suitable only for symmetric positive definite linear systems.
    *   2: TFQMR (Transpose Free Quasi-Minumum Residual). This solver is suitable for general (nonsymmetric) linear systems. It may be significantly faster than GMRES, may fail to converge for some problems.
    *   3: CG2 (Conjugate Gradient Squared). This solver is suitable for general (nonsymmetric) linear systems. It may be significantly faster than GMRES, but may fail to converge for some problems.
    *   4: BICGSTAB (Stabilized Biconjugate Gradients). This solver is suitable for general (nonsymmetric) linear systems. It may be significantly faster than GMRES, but may fail to converge for some problems. This solver is the most robust and popular alternative to GMRES.
*   **AZ_kspace**(int): Krylov subspace size for restarted GMRES. Typical range is 20-200\. If your iteration is not converging, try a larger value. Larger values of the restart parameter may lead to convergence in fewer iterations, but at increased cost.
*   **AZ_scaling**(int): Type of matrix scaling to use (see AzteccOO manual). Poorly scaled matrices may result in poor convergence.
    *   -1: None.
    *   0: Row Sum Scaling. After rescaling, the absolute value of the entries in each row sum to one.
    *   1: Jacobi scaling. Each row of the matrix is rescaled by its diagonal.
    *   2: Symmetric row sum scaling. This applies a row and column rescaling to the matrix, such that the rescaled matrix is symmetric if the original matrix was symmetric. i This option is most useful for symmetric positive definite linear systems used with the CG linear solver.
*   **Preconditioner**(int): Type of preconditioning to apply to solve (see AztecOO manual). A preconditioned matrix is in general easier to solve than a nonpreconditioned matrix, and the linear solver should converge in fewer iterations. However, preconditioners require some up-front cost to construct, and must be applied at each iteration, incurring additional cost. Note that these preconditioners behave differently on different numbers of processors. That is, when using these preconditioners, the number of linear solver iterations required for convergence will vary based on the number of processors used. Options are:
    *   -1: None
    *   0: ILU (Incomplete LU Factoriuzation) subdomain solves. An ILU factorization is formed and applied for each processors' submatrix.
    *   1: Jacobi. Applies three steps of a Jacobi iteration.
    *   2: Symmetric Gauss Seidel. Applies three steps of a symmetric Gauss-Seidel iteration.
    *   3: Third-degree Least-Squares Polynomial.
    *   4: ILUT (Threshold-based Incomplete LU Factorization). Use Saad's ILUT with a drop tolerance of zero and a level-of-fill specified by _level_, below.
*   **level**(int): Level-of-fill parameter when an ILUT preconditioner is used (see AztecOO manual).
*   **Max Iterations**(int): Maximum number of iterations allowed in linear solve (see AzteccOO manual). The linear solver will halt after this many iterations, even if the convergence tolerance is not met. Start with 500 and increase this value if convergence is not achieved.
*   **Convergence Tolerance**(real): Convergence tolerance for linear solve (see AztecOO manual). The solver will stop if the relative residual (the norm of the current residual vector divided by the norm of the initial residual vector) decreases below this value. For most cases, 1.0e-6 is a reasonable tolerance.
    
***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a> 