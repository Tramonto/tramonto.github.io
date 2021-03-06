---
title: Tramonto 3.x User Guide
permalink: tramonto_v3x_user_guide.html
---

## Quick start

After completing installation, the following steps are recommended for the new user.

*   1\. Proceed to the directory Tramonto/Examples in your local copy of the software.*   2\. Choose an example that is similar to a problem you are interested in. For help selecting a suitable example problem to study, see the short descriptions on the [Tabulated Examples](http://software.sandia.gov/tramonto/src_docs/files.html) web page. Note that each example listed on the web site corresponds to an identically named directory in Tramonto/Examples. Within that directory all of the input files needed to run that particular case can be found.*   3\. Run the example problem of your choice, and study the output files produced by Tramonto (use links below to intepret output files). Note that when compiled, the executable (called 'dft') is placed in the directory Tramonto/build_directory/src where the build_directory is specified by the user (see the [Installation Guide](installation_guides.html) for further instructions). The command needed to execute tramonto depends on the type of mpi libraries in use. A few possibilities are :
    *   mpirun -np 16 ~/path_to_Tramonto/Tramonto/build_directory/src/dft
    *   mpirun -np 16 ~/path_to_Tramonto/Tramonto/build_directory/src/dft your_input.dat (replace dft_input.dat with a file name of your choice)
    *   mpiexec -n 16 ~/path_to_Tramonto/Tramonto/build_directory/src/dft
    *   ~/path_to_Tramonto/Tramonto/build_directory/src/dft (single processor execute will work on most platforms)*   4\. Now you are ready to study the input files associated with your example problem using the links below that describe various files and parameters in detail.*   5\. Finally modify the input file as needed to set up a calculation for a system of interest to you. Note that depending on the complexity of your problem you may need to use arc-length continuation algorithms to establish a suitable initial guess for your studies.*   6\. If you need more information on the theories that have been implemented in the Tramonto software, please obtain a copy of the original references listed on the [Tramonto/capabilities](tramonto.html) page. If you are interested in algorithms under the hood of Tramonto or would like to know about previous applications studied using the code, visit the [Publications](publications.html) page.

## User's Guide: dft_input.dat

The default primary input file for Tramonto is dft_input.dat. Various parameters are described in this section. 
Other input files that may be needed are listed below. Note that in dft_input.dat, all lines containing data begin with an @ symbol signaling the code to begin reading data. 
Arbitrary numbers of blank lines or comments may be inserted following the data since everything after the needed data is treated as a comment. 
Numerous comments are included in the templates provided in the Tramonto/Examples/* directories. These comments are meant to assist the user in setting up the input file. 
Note that the input procedure for dft_input.dat is based on the variables being entered in a preset order. So, all lines must be present even if some variables are not needed. The input data is split into different logical categories described in the links here.

Note that the user guide has been updated to reflect source code changes in the v3.1 release of Tramonto

*   Section 1: [Dimension Control Parameters](dimension_control_parameters.html)
*   Section 2: [Mesh Parameters](mesh_parameters.html)
*   Section 3: [Functional Control Parameters](functional_control_parameters.html)
*   Section 4: [Surface Control Parameters](surface_control_parameters.html)
*   Section 5: [Surface Interaction Potential Control Parameters](surface_interaction_potential_control_parameters.html)
*   Section 6: [Interaction Potential Physical Parameters](interaction_potential_physical_parameters.html)
*   Section 7: [Polymer Input Parameters](polymer_input_parameters.html)
*   Section 8: [Semi-Permeable Surface Parameters](semi_permeable_surface_parameters.html)
*   Section 9: [State Point Parameters](state_point_parameters.html)
*   Section 10: [Charged Surfaces: Boundary Condition Parameters](charged_surface_boundary_condition_parameters.html)
*   Section 11: [Charged Systems: Dielectric Constant Parameters](charged_systems_dielectric_constant_parameters.html)
*   Section 12: [Diffusive System Parameters](disffusive_system_parameters.html)
*   Section 13: [Startup Control Parameters](startup_control_parameters.html)
*   Section 14: [Output Format Parameters](output_format_parameters.html)
*   Section 15: [Numerical Coarsening Control Parameters](numerical_coarsening_control_parameters.html)
*   Section 16: [Nonlinear Solver Control Parameters](nonlinear_solver_control_parameters.html)
*   Section 17: [Linear Solver Control Parameters](linear_solver_control_parameters.html)
*   Section 18: [Mesh Continuation Parameters](mesh_continuation_parameters.html)
*   Section 19: [LOCA Parameter Continuation (simple, arc-length, binodal)](loca_continuation_parameters.html)

## User's Guide: other input files

*   [dft_surfaces.dat](dft_surfaces.html): define surface types, positions, and charge.
*   [poly_file](poly_file.html): define polymer connectivity.
*   [Cr_file](cr_file.html): direct correlation function file for CMS DFT calculations.

## User's Guide: Tramonto output files (principle output)

A variety of files are generated by the Tramonto code. They can be split into two categories - principle output and debugging output. The latter are only printed when the code is operating in VERBOSE (see <a http="userguide_4.0/UG_sect14.html">Iwrite parameter</a>) mode for the purposes of debugging. The principle output files are dft_dens.dat, dft_output.dat, dft_out.lis, and dft_time.out. Various output files are described further below.

*   [dft_dens.dat (and dft_dens.datg)](dft_dens.html)
*   [dft_output.dat](dft_output.html)
*   [dft_out.lis](dft_out.html)
*   [Debugging output generated in VERBOSE mode](debugging_output.html)

***

[Privacy and Security](http://www.sandia.gov/general/privacy-security/index.html)    