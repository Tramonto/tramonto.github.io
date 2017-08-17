---
title: Dimension Control Parameters
folder: user_guide
permalink: dimension_control_parameters.html
---

## Functional Control Parameters

These are switches that control the density functional equations being studied for a given case. The functional switches are separated into hard sphere, attractive, Coulombic, and polymer functionals.

*   **Type_func**(int): Hard sphere functional type (for HS perturbation calculations). Options are:
    *   -1: NONE: no hard sphere functionals. Set this for ideal gases, Poisson-Boltzman electrolytes, or CMS polymers.
    *   0: FMT1: original FMT functional developed by Rosenfeld (Phys Rev Lett, v.63, p.980, 1989).
    *   1: FMT2: FMT with corrected zero dimensional crossover behavior (Rosenfeld et.al., Phys. Rev. E., v.55, p.4245, 1997 and Rosenfeld et.al., J. Phys. Cond. Matt., v.8, p.L577, 1996).
    *   2: FMT3: White Bear functional (Roth et.al., J. Phys. Cond. Matt., v.14, p.12063, 2002)
    *   3: FMT4: White Bear functional, corrected for zero dimensional crossover behavior (Oleksy and Hansen, Mol. Phys., v. 104, p. 2871, 2006.)
*   **Type_hsdiam**(int): Type of hard sphere diameter to be used in FMT functional. Options are:
    *   0: use Sigma_ff parameters as the hard sphere diameter in FMT functionals.
    *   1: use Barker-Henderson approach to set hard sphere diameters in FMT functionals. This is a specific optimized approach for a Weeks-Chandler-Andersen type approach for Lennard-Jones fluids. Use with care in other circumstances.
    *   2: manual input of hard sphere diameters FMT functionals. This allows the hard sphere diameter to be separated from the characteristic size, σ, of the longer range mean field potentials. It can be useful in studying nonadditive potentials for example.
*   **Type_attr**(int): Define how to treat the core region when longer range (often but not always attractive) interactions are included as a strict mean field contribution to the free energy functional. if Type_attr> -1, then Type_pairPot must be defined. Options are:
    *   -1: NONE: no long range pair interactions (or Coulomb only to be treated with Poisson's equation).
    *   0: MFPAIR_RMIN_UMIN: Weeks-Chandler-Andersen approach. Identify distance where minimum in potential is found, r<sub>min</sub>. Then set potentential to that constant value (u=u<sub>min</sub>) for r < r<sub>min</sub>.
    *   1: MFPAIR_SIGMA_ZERO: Set potentential to u=0 for r<=σ\.
    *   2: MFPAIR_SIGMA_USIGMA: Set potentential to u=u(σ) for r<=σ\.
    *   3: MFPAIR_SIGTOUMIN_UMIN: Set potentential to u=0 for r<=σ but set u=u<sub>min</sub> if σ<=r<=r<sub>min</sub>.
    *   4: MFPAIR_RCSZERO_ZERO: Identify the distance, r<sub>zero</sub>, where the potential crosses zero. Set potentential to u=0 for r<=r<sub>zero</sub>.
*   **Type_pairPot**(int): Type of pair potential to be used for fluid-fluid interactions based on the strict mean field approximation. The implementation of each type of potential can be found in Tramonto/src/dft_pairPot_potID.c, where potID depends on the potential of interest. The potential parameters, σ<sub>ij</sub>, ε<sub>ij</sub>, z<sub>i</sub>, ε<sub>ij</sub><sup>Y</sup>, K<sub>ij</sub><sup>Y</sup>, N<sub>ij</sub><sup>POW</sup>, and r<sub>ij</sub><sup>cut</sup> are discussed further in Section 6: [Interaction Potential Physical Parameters](userguide_4.0/UG_sect6.html).
    *   -1: **PAIR_HARD**: No extended pair interactions.

        u<sub>ij</sub>(r)=∞ if r < σ<sub>ij</sub>. Else u<sub>ij</sub>(r)=0.

    *   0: **PAIR_LJ12_6_CS**: Cut and shifted 12-6 Lennard-Jones potential.

        u<sub>ij</sub><sup>CS</sup>(r)= u<sub>ij</sub>(r)- u<sub>ij</sub>(r<sub>ij</sub><sup>cut</sup>). With:

        u<sub>ij</sub>(r)=4ε<sub>ij</sub>[(σ<sub>ij</sub>/r)<sup>12</sup>-(σ<sub>ij</sub>/r)<sup>6</sup>].

    *   1: **PAIR_COULOMB_CS**: Cut and shifted Coulomb potential<sup>*</sup>

        u<sub>ij</sub><sup>CS</sup>(r)= u<sub>ij</sub>(r)- u<sub>ij</sub>(r<sub>ij</sub><sup>cut</sup>). With:

        u<sub>ij</sub>(r)=(1/T<sub>elec</sub>)(z<sub>i</sub>z<sub>j</sub>/r), where T<sub>elec</sub>=4πk<sub>B</sub>Tκε<sub>0</sub>σ<sub>ref</sub>/e<sup>2</sup>.

        The various constants are:

        *   k<sub>B</sub>=1.3807e-23 J/K (the Boltzmann constant).
        *   ε<sub>0</sub>=8.85419e-12 C<sup>2</sup>/(Jm) (the permittivity of free space).
        *   e=1.60219e-19 (the unit charge).
    *   2: **PAIR_COULOMB**: Coulomb potential (Cut not shifted)<sup>*</sup>.

        u<sub>ij</sub><sup>C</sup>(r)= u<sub>ij</sub>(r) if r≤r<sub>ij</sub><sup>cut</sup>. Otherwise u<sub>ij</sub><sup>C</sup>(r)=0\. Once again:

        u<sub>ij</sub>(r)=(1/T<sub>elec</sub>)(z<sub>i</sub>z<sub>j</sub>/r), where T<sub>elec</sub>=4πk<sub>B</sub>Tκε<sub>0</sub>σ<sub>ref</sub>/e<sup>2</sup>.

        <sup>*</sup>Treating Coulomb potentials as mean field contributions with explicit cut or cut and shifted pair potentials is not an optimal treatment of electrostatics. This approach will and will become less accurate as the Debye length in the system increases. Alternatively, only treat short range potentials with the strict mean field term and instead turn on the Type_coul parameter to couple a Possion solve with the Euler-Lagrange equation. That approach preserves charge neutrality.

    *   3: **PAIR_YUKAWA_CS**: Cut and shifted Yukawa potential (as in Egorov, Phys.Rev.E., v.70, p.031402, 2004).

        u<sub>ij</sub><sup>CS</sup>(r)= u<sub>ij</sub>(r)- u<sub>ij</sub>(r<sub>ij</sub><sup>cut</sup>). With:

        u<sub>ij</sub>(r)=ε<sub>ij</sub><sup>Y</sup>exp[-α<sub>ij</sub>(r/σ<sub>ij</sub>-1.)]/(r/σ<sub>ij</sub>) where α<sub>ij</sub>=K<sub>ij</sub><sup>Y</sup>σ<sub>ij</sub>

    *   4: **PAIR_EXP_CS**: Cut and shifted exponential potential.

        u<sub>ij</sub><sup>CS</sup>(r)= u<sub>ij</sub>(r)- u<sub>ij</sub>(r<sub>ij</sub><sup>cut</sup>). With:

        u<sub>ij</sub>(r)=-ε<sub>ij</sub>exp[-(r-σ<sub>ij</sub>)/α<sub>ij</sub>] where α<sub>ij</sub>=K<sub>ij</sub><sup>Y</sup>.

    *   5: **PAIR_SW**: Square well interaction potential.

        u<sub>ij</sub>(r)= -ε<sub>ij</sub> if r≤r<sub>ij</sub><sup>cut</sup>. Otherwise u<sub>ij</sub>(r)=0\.

    *   6: **PAIR_LJandYUKAWA_CS**: Cut and shifted summed Yukawa and Lennard-Jones potential.

        u<sub>ij</sub><sup>CS</sup>(r)= u<sub>ij</sub>(r)- u<sub>ij</sub>(r<sub>ij</sub><sup>cut</sup>). With:

        u<sub>ij</sub>(r)=4ε<sub>ij</sub>[(σ<sub>ij</sub>/r)<sup>12</sup>-(σ<sub>ij</sub>/r)<sup>6</sup>] + (ε<sub>ij</sub><sup>Y</sup>exp[-α<sub>ij</sub>(r/σ<sub>ij</sub>-1.)])/(r/σ<sub>ij</sub>) where α<sub>ij</sub>=K<sub>ij</sub><sup>Y</sup>σ<sub>ij</sub>

    *   7: **PAIR_r12andYUKAWA_CS**: Cut and shifted summed Yukawa and r<sup>12</sup> repulsive potential.

        u<sub>ij</sub><sup>CS</sup>(r)= u<sub>ij</sub>(r)- u<sub>ij</sub>(r<sub>ij</sub><sup>cut</sup>). With:

        u<sub>ij</sub>(r)=4ε<sub>ij</sub>(σ<sub>ij</sub>/r)<sup>12</sup> + ε<sub>ij</sub><sup>Y</sup>exp[-α<sub>ij</sub>(r/σ<sub>ij</sub>-1.)]/(r/σ<sub>ij</sub>) where α<sub>ij</sub>=K<sub>ij</sub><sup>Y</sup>σ<sub>ij</sub>

    *   8: **PAIR_r18andYUKAWA_CS**: Cut and shifted summed Yukawa and r<sup>18</sup> repulsive potential.

        u<sub>ij</sub><sup>CS</sup>(r)= u<sub>ij</sub>(r)- u<sub>ij</sub>(r<sub>ij</sub><sup>cut</sup>). With:

        u<sub>ij</sub>(r)=4ε<sub>ij</sub>[(σ<sub>ij</sub>/r)<sup>18</sup>] + ε<sub>ij</sub><sup>Y</sup>exp[-α<sub>ij</sub>(r/σ<sub>ij</sub>-1.)]/(r/σ<sub>ij</sub>) where α<sub>ij</sub>=K<sub>ij</sub><sup>Y</sup>σ<sub>ij</sub>

    *   9: **PAIR_rNandYUKAWA_CS**: Cut and shifted summed Yukawa and r<sup>n</sup> repulsive potential where _n_ is variable.

        u<sub>ij</sub><sup>CS</sup>(r)= u<sub>ij</sub>(r)- u<sub>ij</sub>(r<sub>ij</sub><sup>cut</sup>). With:

        u<sub>ij</sub>(r)=4ε<sub>ij</sub>[(σ<sub>ij</sub>/r)<sup>N<sub>ij</sub><sup>POW</sup></sup>] + ε<sub>ij</sub><sup>Y</sup>exp[-α<sub>ij</sub>(r/σ<sub>ij</sub>-1.)]/(r/σ<sub>ij</sub>) where α<sub>ij</sub>=K<sub>ij</sub><sup>Y</sup>σ<sub>ij</sub>

*   **Type_coul**(int): Type of potential to be used to treat electrostatics for cases where the electrostatic potential is introduced into the system of equations, and Poisson's equation is solved simultaneously with the DFT Euler-Lagrange equations. Options are:
    *   -1: NONE: turn off Poisson terms. Do this for neutral systems or for Type_pairPot=1 or 2.
    *   0: BARE: Mean field electrostatics based on point charges only (no other correlations included).
    *   1: DELTAC: Mean field electrostatics for point charges plus a 2nd order correction based on an analytical solution for the RPM using the mean spherical approximation (MSA) for the special case of a restricted primitive model (RPM) where all charged species have identical size. (see Tang and Davis, J. Chem. Phys., 97:9258, 1992).
    *   2: DELTAC_GENERAL: Extension of the mean field electrostatics with 2nd order correction generalizing to arbitrary particle sizes (see Oleksy and Hansen, Mol. Phys., v. 104, p. 2871, 2006).
    *   3: POLARIZE: Electrostatics for a polarizeable fluid. (Preliminary 1D implementation only in Tramonto-2.1/3.0/4.0)
*   **Type_poly**(int): The type of functional to be used to describe bonded systems. Note that long range interactions and electrostatics can be turned on in conjunction with bonded systems by turning on Type_attr and/or Type_coul as described above. Furthermore note that the WTC and WJDC polymers (options 2-5) also require a selection for the reference hard sphere fluid type using Type_func above. Options for Type_poly are:
    *   -1: NONE: No polymer functionals. No bonds.
    *   0: CMS: Chandler-McCoy-Singer DFT (J.Chem.Phys., v.85, p. 5971, 1986; v.85, p.5977, 1986; v. 87, p.4853, 1987) based on freely-jointed chains where the single chain part of the functional is evaluated numerically (see Donley et al., J. Chem. Phys., v.103, p.5061, 1995; and Frischknecht et al., J. Chem. Phys., v. 117, 10385, 2002).
    *   1: CMS_SCFT: This option simplifies the CMS theory to reproduce polymer Self-Consistent Field Theory. Note that the algorithms in Tramonto are not optimal for SCFT. Rather this approach serves as a test and a point of comparison with work in the SCFT community. (This option is not yet fully implemented.)
    *   2: WTC: iSAFT (interfacial statistical associating fluid theory) DFT by Tripathi and Chapman; functionals based on Wertheim's TPT1 theory, in the limit of infinitely strong associations (see Tripathi and Chapman, Phys. Rev. Lett., v.94, p. 087801, 2005 and J. Chem. Phys., v.122, p.094506, 2005).
    *   3: WJDC: the modified iSAFT functional of Jain, Dominik, and Chapman (see J. Chem. Phys., 127:244904, 2007). This implementation treats both the densities and the effective fields as segment based variables explicitly. It may be used in conjunction with Schur solvers.
    *   4: WJDC2: variation of WJDC functional. This implementation treats the densities segment based variable but the effective field as a component (segment type) based variable. It may NOT be used in conjunction with Schur solvers.
    *   5: WJDC3: variation of WJDC functional. This implementation treats both the densities and the effective fields as component (segment type) based variables. It may be used in conjunction with Schur solvers, and is considered the optimal implementation of the WJDC functional from a performance perspective.
    
***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a>     