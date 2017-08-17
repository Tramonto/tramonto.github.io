---
title: Startup Control Parameters
folder: user_guide
permalink: startup_control_parameters.html
---

## Startup Control Parameters

These parameters determine how a given run will be started.

*   **Iguess**(int): This parameter sets the initial guess type for cases where there is no restart file. Note that the coexistence based options (-2,-1,1,2,5, and 6) are disabled at the time of the v2.1 release. Options are:
    *   0: CONST_RHO: a constant density set to Rho_b[icomp]
    *   1: EXP_RHO: an ideal density profile set to Rho_b[icomp]*exp(-Vext[icomp](r))
    *   2: STEP_PROFILE: a stepped density profile defined by the parameters Nsteps, Orientation_step, Xstep_start, Xstep_end, and Rho_step.
    *   3: CHOP_RHO: a chopped profile where an old density profile is read in, and then the profile is chopped off at a distance X_step_start[0] from the surface. The remainder of the profile is replaced with Rho_b[icomp].
    *   4: CHOP_RHO_STEP: same as CHOP_RHO except the remainder of the profile is replaced with Rho_step[0].
    *   5: LINEAR: set up a linear profile between Rho_LBB[icomp] and Rho_RTF[icomp] for diffusion problems.
*   **Iguess_fields**(int): This parameter determines how the non-density fields in the Tramonto calculation will be set up. These fields may include (nonlocal densities from FMT functionals, mean fields (CMS and WJDC functionals), nonlocal densities associated with cavity function (WTC and WJDC functionals), polymer chain equations (CMS and WJDC functionals), and mean field attractions (if designated as unique variable - see Type_attr definition). Options are:
    *   0: use bulk values for all fields as the initial guess.
    *   1: compute fields using the initial guess for the density field. Recommended for a run that restarts from an old density profile.
    *   2: compute nonlocal densitiy fields, but use bulk fields for chain equations and mean field variables (CMS/WJDC functionals). This option will be used infrequently.
    *   3: compute all fields except the mean field variables where the bulk value should be used (CMS/WJDC). This option will be used infrequently.
*   **Nsteps** (int): Used if Iguess=2\. Sets number of steps to start for initial density profile.
*   **Orientation[_istep_]**(ints): Array that indicates the orientation (x=0, y=1, z=2) of the density steps for the initial guess. Generally all will be the same.
*   **Xstart_step[_istep_]**(doubles): Array that indicates the distance parameter where each density step begins. Note that this parameter is also used if Iguess=3 or 4 with the understanding that Nsteps=1 and that for all x>Xstart_step, the indicated constant density (Rho_b[0] or Rho_step[0]) will be used as the density.
*   **Xstart_end[_istep_]**(doubles): Array that indicates the distance parameter where each density step ends.
*   **Rho_step[_icomp_][_istep_]**(doubles): Array the determines the density of each step in the initial guess profile. Note that this variable will also be used if Iguess=4 with the understanding that there is only Nsteps=1 in that case.
*   **Restart**(int): This switch controls how the run will start up. Options are:
    *   0: NORESTART: No restart file: construct an intital guess as indicated by Iguess and Iguess_fields parameters.
    *   1: RESTART_BASIC: Restart from default files. In all cases a file named dft_dens.dat (and dft_dens2.dat for the case of a binodal calculation) must be present to restart, and key words that signal which fields are available in the file must be present. However the behavior of the code will then depend on what particular data is supplied to Tramonto or what other settings have been selected. Here we summarize the possibilities:  

        *   **Density and all other field data supplied in dft_dens.dat and dft_dens.datg** : If Tramonto identifies that all necessary field variables are present in the files, it will use that data for the restart. If only some of the fields are present, the remainder will be calculated depending on the setting of Iguess_fields.
        *   **Only density data is supplied in dft_dens.dat** All other fields will be set by Tramonto depending on the setting of the Iguess_fields parameter.
        *   **Density data is supplied in dft_dens.dat, but it is of the wrong type.** If segment densities are supplied to Tramonto for a case where component densities are needed (i.e. results from WTC or WJDC1/2 are used to restart using the CMS or WJDC3 functional), Tramonto will automatically sum the segment densities. If component densities are provided, but segment densities are needed, Tramonto will assume that all segment densities of a given type are identical and generate a segment based initial density guess. Note that in this latter case, the restart will be approximate.
    *   2: RESTART_STEP: Restart from files, but step the profile as indicated by Iguess option 3 or 4.
    *   3: RESTART_DENSONLY: Restart density unknowns only regardless of other fields in dft_dens.dat. Reset those other fields based on Iguess_fields parameter.
    *   4: RESTART_FEWERCOMP: Restart from a density file that is incomplete with some parameters missing. In this case, density profiles in the file will be used for some parameters, and initial guesses for other components will be constructed based on the settings of Iguess and Iguess_fields parameters. Useful for starting some interface calculations. This restart requires specification of the parameter Nmissing_densities.
    *   5: RESTART_1DTOND: Use a 1-dimensional solution field as an initial guess for a 2 or 3 dimensional calculation. The 1-dimensional solution is simply replicated in the y and/or z directions.
*   **Nmissing_densities** (int): Only needed for Restart=4 (RESTART_FEWERCOMP). It is the number of density fields that are missing in the input file dft_dens.dat. For example in a 3 component calculation that is restarting from a solution file generated in a 2 component system, Nmissing_densities should be set to 1.
*   **Restart_Vext**(int): switch to select option for restart of external field. This may be used to use an external field generated elsewhere as input to a Tramonto calculation. Options are:
    *   0: Don't restart Vext from a file.
    *   1: Restart Vext from a file found in Vext_file1 (any name you like).
    *   2: Restart Vext by summing data in files Vext_file1 and Vext_file2.
    *   3: Follow same Vext restart procedure as option 2, but treate data in Vext2_file as static with respect to continuation of Vext parameters.
*   **Rho_max**(real): This is the maximum density allowed for continuation from an old profile. Note that very large densities can be difficult to converge, and is is sometimes better to disallow very high densities.

***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a> 