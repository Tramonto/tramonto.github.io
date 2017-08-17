---
title: Surface Interaction Potential Control Parameters
folder: user_guide
permalink: surface_interaction_potential_control_parameters.html
---

## Surface Interaction Potential Control Parameters

These switches control the type of wall-fluid and wall-wall interaction potential models that are to be used in the calculation.

*   **Ipot_wf_n**[Nwall_type](int array): An array to set the type of neutral interactions between the fluid particles and the surfaces. Each surface type must have an entry. Options are:
    *   0: VEXT_NONE: No interaction.
    *   1: VEXT_HARD: An infinitely hard wall. Vext=VEXT_MAX inside the surface geometry plus a shell of width 1/2 Sigma_wf.
    *   2: VEXT_DIST_SURFACE: Any Vext that is based on the distance to the edge of a surface.
    *   3: VEXT_DIST_CENTER: Any Vext that is based on the distance to the center of a surface.
    *   5: VEXT_INTEGRATED: Any Vext that is computed at every point in the fluid by a numerical integral over surface elements (a volume integral over a surface of arbitrary geometry). Example: This option allows an surface to be treated as a smeared out collection of atoms with a known density.
*   **Lhard_surfaces**(int): Logical (0=FALSE, 1=TRUE) that controls the application of integration stencils at the boundaries. If TRUE, a step function at the boundary is resolved carefully based on local elements that surround the boundary nodes. This can be FALSE for all soft potentials. It should be TRUE to obtain accurate density sum rules at hard surfaces. If any of the surfaces in the system are hard, set this parameter to TRUE.
*   **Type_vext[Nwall_type]**(int array): Select form for Vext potential for each wall type. Two options are available:

    *   0: Select Vext from the preset list of external fields defined by **Vext_PotentialID** below.
    *   1: Select Vext from the list of pair potential functions used to treat fluids. Those options are enumerated in Section 3: [Functional Control Parameters](userguide_4.0/UG_sect3.html) under the parameter **Type_pairPot**
*   **Vext_PotentialID[Nwall_type]**(int array): Array to specify the functional form of the external field for each surface type.
    *   For surfaces with **Type_vext**[iwall_type]=0, the options are listed below. The wall-fluid interaction parameters (ρ<sub>iw</sub>,σ<sub>iw,i</sub>, ε<sub>iw,i</sub>, ε<sub>iw,i</sub><sup>Y</sup>, K<sub>iw,i</sub><sup>Y</sup>, and r<sub>iw,i</sub><sup>cut</sup>) are discussed further in Section 6: [Interaction Potential Physical Parameters](userguide_4.0/UG_sect6.html)).
        *   **0: LJ9_3_CS**: Cut and shifted 9-3 Lennard-Jones potential.

            V<sub>iw,i</sub>(x)= V<sub>iw,i</sub><sup>ext</sup>(x)- V<sub>iw,i</sub><sup>ext</sup>(x<sub>iw,i</sub><sup>cut</sup>). With:

            V<sub>iw,i</sub><sup>ext</sup>(x)= (2π/3)(ε<sub>iw,i</sub>)ρ<sub>iw</sub>[(2/15)(σ<sub>iw,i</sub>/x)<sup>9</sup>-(σ<sub>iw,i</sub>/x)<sup>3</sup>].

        *   **1: LJ9_3_v2_CS**: Cut and shifted 9-3 Lennard-Jones potential of a slightly different form.

            V<sub>iw,i</sub>(x)= V<sub>iw,i</sub><sup>ext</sup>(x)- V<sub>iw,i</sub><sup>ext</sup>(x<sub>iw,i</sub><sup>cut</sup>). With:

            V<sub>iw,i</sub><sup>ext</sup>(x)= ε<sub>iw,i</sub>(ρ<sub>iw</sub>)[(2/15)(σ<sub>iw,i</sub>/x)<sup>9</sup>-(σ<sub>iw,i</sub>/x)<sup>3</sup>].

        *   **2: LJ9_3_noCS**: 9-3 Lennard-Jones potential (Cut but no shift).

            V<sub>iw,i</sub>(x)= (2π/3)(ε<sub>iw,i</sub>)ρ<sub>iw</sub>[(2/15)(σ<sub>iw,i</sub>/x)<sup>9</sup>-(σ<sub>iw,i</sub>/x)<sup>3</sup>] if x≤x<sub>iw,i</sub><sup>cut</sup>; else V<sub>iw,i</sub>(x)=0.

        *   **4: REPULSIVE9_noCS**: Pure repulsive potential (Cut but no shift).

            V<sub>iw,i</sub>(x)= (2π/3)(ε<sub>iw,i</sub>)ρ<sub>iw</sub>[(2/15)(σ<sub>iw,i</sub>/x)<sup>9</sup> if x≤x<sub>iw,i</sub><sup>cut</sup>; else V<sub>iw,i</sub>(x)=0.

        *   **5: EXP_ATT_noCS**: Pure exponential form for Vext (Cut but no shift).

            V<sub>iw,i</sub>(x)= -ε<sub>iw,i</sub>(ρ<sub>iw</sub>)exp[-x/σ<sub>iw,i</sub>] if x≤x<sub>iw,i</sub><sup>cut</sup>; else V<sub>iw,i</sub>(x)=0.

        *   **6: LINEAR_noCS**: Linear external field for charged systems. This is a special case for a single charged planar surface. See source code for implementation (dft_vext_1D.c).
        *   **7: R7_YUKAWA_SUM_CS**: Sum of a repulsive r^7 potential and a Yukawa term.

            V<sub>iw,i</sub>(x)= V<sub>iw,i</sub><sup>ext</sup>(x)- V<sub>iw,i</sub><sup>ext</sup>(x<sub>iw,i</sub><sup>cut</sup>). With:

            V<sub>iw,i</sub><sup>ext</sup>(x)= ε<sub>iw,i</sub>(ρ<sub>iw</sub>)(σ<sub>iw,i</sub>/x)<sup>7</sup> +(ε<sub>iw,i</sub><sup>Y</sup>) exp[-α<sub>iw,i</sub>(r/σ<sub>iw,i</sub>-1)]/(r/σ<sub>iw,i</sub>) where α<sub>iw,i</sub>=K<sub>iw,i</sub><sup>Y</sup>σ<sub>iw,i</sub>.

    *   For surfaces with **Type_vext**[iwall_type]=1, the options for **Vext_PotentialID** are identical to the options for Type_pairPot (See precise definitions in Section 3: [Functional Control Parameters](userguide_4.0/UG_sect3.html)). However, the the wall-fluid interaction parameters (σ<sub>iw,i</sub>, ε<sub>iw,i</sub>, ε<sub>iw,i</sub><sup>Y</sup>, K<sub>iw,i</sub><sup>Y</sup>, and r<sub>iw,i</sub><sup>cut</sup>) are used in the calculation of external field. The options are:
        *   0: **PAIR_LJ12_6_CS**: Cut and shifted 12-6 Lennard-Jones potential.

            V<sub>iw,i</sub><sup>CS</sup>(r)= V<sub>iw,i</sub>(r)- V<sub>iw,i</sub>(r<sub>iw,i</sub><sup>cut</sup>). With:

            V<sub>iw,i</sub>(r)=4ε<sub>iw,i</sub>[(σ<sub>iw,i</sub>/r)<sup>12</sup>-(σ<sub>iw,i</sub>/r)<sup>6</sup>].

        *   1: **PAIR_COULOMB_CS**: Cut and shifted Coulomb potential.

            V<sub>iw,i</sub><sup>CS</sup>(r)= V<sub>iw,i</sub>(r)- V<sub>iw,i</sub>(r<sub>iw,i</sub><sup>cut</sup>). With:

            V<sub>iw,i</sub>(r)=(1/T<sub>elec</sub>)(z<sub>wi</sub>z<sub>i</sub>/r), where T<sub>elec</sub>=4πk<sub>B</sub>Tκε<sub>0</sub>σ<sub>ref</sub>/e<sup>2</sup>. The charge of the wall is denoted by z<sub>wi</sub>, while z<sub>i</sub> is the valence of the fluid species, i.

            The various constants are:

            *   k<sub>B</sub>=1.3807e-23 J/K (the Boltzmann constant).
            *   ε<sub>0</sub>=8.85419e-12 C<sup>2</sup>/(Jm) (the permittivity of free space).
            *   e=1.60219e-19 (the unit charge).
        *   2: **PAIR_COULOMB**: Coulomb potential (Cut not shifted).

            V<sub>iw,i</sub><sup>C</sup>(r)= V<sub>iw,i</sub>(r) if r≤r<sub>iw,i</sub><sup>cut</sup>. Otherwise V<sub>iw,i</sub><sup>C</sup>(r)=0\. Once again:

            V<sub>iw,i</sub>(r)=(1/T<sub>elec</sub>)(z<sub>iw</sub>z<sub>i</sub>/r), where T<sub>elec</sub>=4πk<sub>B</sub>Tκε<sub>0</sub>σ<sub>ref</sub>/e<sup>2</sup>. The charge of the wall is denoted by z<sub>wi</sub>, while z<sub>i</sub> is the valence of the fluid species, i.

        *   3: **PAIR_YUKAWA_CS**: Cut and shifted Yukawa potential (as in Egorov, Phys.Rev.E., v.70, p.031402, 2004).

            V<sub>iw,i</sub><sup>CS</sup>(r)= V<sub>iw,i</sub>(r)- V<sub>iw,i</sub>(r<sub>iw,i</sub><sup>cut</sup>). With:

            V<sub>iw,i</sub>(r)=ε<sub>iw,i</sub><sup>Y</sup>exp[-α<sub>iw,i</sub>(r/σ<sub>iw,i</sub>-1.)]/(r/σ<sub>iw,i</sub>) where α<sub>iw,i</sub>=K<sub>iw,i</sub><sup>Y</sup>σ<sub>iw,i</sub>

        *   4: **PAIR_EXP_CS**: Cut and shifted exponential potential.

            V<sub>iw,i</sub><sup>CS</sup>(r)= V<sub>iw,i</sub>(r)- V<sub>iw,i</sub>(r<sub>iw,i</sub><sup>cut</sup>). With:

            V<sub>iw,i</sub>(r)=-ε<sub>iw,i</sub>exp[-(r-σ<sub>iw,i</sub>)/α<sub>iw,i</sub>] where α<sub>iw,i</sub>=K<sub>iw,i</sub><sup>Y</sup>.

        *   5: **PAIR_SW**: Square well interaction potential.

            V<sub>iw,i</sub>(r)= -ε<sub>iw,i</sub> if r≤r<sub>iw,i</sub><sup>cut</sup>. Otherwise V<sub>iw,i</sub>(r)=0\.

        *   6: **PAIR_LJandYUKAWA_CS**: Cut and shifted summed Yukawa and Lennard-Jones potential.

            V<sub>iw,i</sub><sup>CS</sup>(r)= V<sub>iw,i</sub>(r)- V<sub>iw,i</sub>(r<sub>iw,i</sub><sup>cut</sup>). With:

            V<sub>iw,i</sub>(r)=4ε<sub>iw,i</sub>[(σ<sub>iw,i</sub>/r)<sup>12</sup>-(σ<sub>iw,i</sub>/r)<sup>6</sup>] + (ε<sub>iw,i</sub><sup>Y</sup>exp[-α<sub>iw,i</sub>(r/σ<sub>iw,i</sub>-1.)])/(r/σ<sub>iw,i</sub>) where α<sub>iw,i</sub>=K<sub>iw,i</sub><sup>Y</sup>σ<sub>iw,i</sub>

        *   7: **PAIR_r12andYUKAWA_CS**: Cut and shifted summed Yukawa and r<sup>12</sup> repulsive potential.

            V<sub>iw,i</sub><sup>CS</sup>(r)= V<sub>iw,i</sub>(r)- V<sub>iw,i</sub>(r<sub>iw,i</sub><sup>cut</sup>). With:

            V<sub>iw,i</sub>(r)=4ε<sub>iw,i</sub>(σ<sub>iw,i</sub>/r)<sup>12</sup> + ε<sub>iw,i</sub><sup>Y</sup>exp[-α<sub>iw,i</sub>(r/σ<sub>iw,i</sub>-1.)]/(r/σ<sub>iw,i</sub>) where α<sub>iw,i</sub>=K<sub>iw,i</sub><sup>Y</sup>σ<sub>iw,i</sub>

        *   8: **PAIR_r18andYUKAWA_CS**: Cut and shifted summed Yukawa and r<sup>18</sup> repulsive potential.

            V<sub>iw,i</sub><sup>CS</sup>(r)= V<sub>iw,i</sub>(r)- V<sub>iw,i</sub>(r<sub>iw,i</sub><sup>cut</sup>). With:

            V<sub>iw,i</sub>(r)=4ε<sub>iw,i</sub>[(σ<sub>iw,i</sub>/r)<sup>18</sup>] + ε<sub>iw,i</sub><sup>Y</sup>exp[-α<sub>iw,i</sub>(r/σ<sub>iw,i</sub>-1.)]/(r/σ<sub>iw,i</sub>) where α<sub>iw,i</sub>=K<sub>iw,i</sub><sup>Y</sup>σ<sub>iw,i</sub>

        *   9: **PAIR_rNandYUKAWA_CS**: Cut and shifted summed Yukawa and r<sup>n</sup> repulsive potential where _n_ is variable.

            V<sub>iw,i</sub><sup>CS</sup>(r)= V<sub>iw,i</sub>(r)- V<sub>iw,i</sub>(r<sub>iw,i</sub><sup>cut</sup>). With:

            V<sub>iw,i</sub>(r)=4ε<sub>iw,i</sub>[(σ<sub>iw,i</sub>/r)<sup>N<sub>iw,i</sub><sup>POW</sup></sup>] + ε<sub>iw,i</sub><sup>Y</sup>exp[-α<sub>iw,i</sub>(r/σ<sub>iw,i</sub>-1.)]/(r/σ<sub>iw,i</sub>) where α<sub>iw,i</sub>=K<sub>iw,i</sub><sup>Y</sup>σ<sub>iw,i</sub>

*   **Ipot_ww_n**[Nwall_type][Nwall_type](int array): An array of switches indicating whether Tramonto should compute the type of neutral interactions between pairs of surface types in the system (only available for atomic surfaces). Often these terms are ignored; however, they may be needed in some cases. One example is the calculation of the potential of mean force between two solvated atoms, molecules, colloidal particles, or surfaces requires the direct interaction between a pair of explicit surfaces. Entries should be: O=FALSE, 1=TRUE; however, the parameters can be set more rapidly using the following convention:
    *   -2 in first entry of array turns off these terms for entire array (don't compute any uww).
    *   -1 in first entry of array turns on these terms for entire array (compute uww for all surface pairs).
*   **Type_uwwPot**(int): Select form for 3D surface-surface interaction potentials in the problem. Note that at the time of the v2.1 release this parameter is not dependent on the surface type, and all wall-wall potentials must have the same functional form. Choices are identical to Type_pairPot; however, the interaction potential parameters here are all based on wall-wall parameters, Sigma_ww, Epsilon_ww, etc. Options are:
    *   0: PAIR_LJ12_6_CS: Cut and shifted 12-6 Lennard-Jones potential.
    *   1: PAIR_COULOMB_CS: Cut and shifted Coulomb (note ... this is generally a bad idea - turn on Type_coul instead to preserve charge neutrality.
    *   2: PAIR_COULOMB: Full Coulomb potential used in forming integration stencils. (note ... this is still approximate and a bad idea - again turn on Type_coul instead to preserve charge neutrality.
    *   3: PAIR_YUKAWA_CS: Cut and shifted Yukawa potential (defined as in Egorov, Phys.Rev.E., v.70, p.031402, 2004).
    
***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a>     