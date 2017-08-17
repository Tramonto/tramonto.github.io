---
title: Surface Control Parameters
folder: user_guide
permalink: surface_control_parameters.html
---

## Surface Control Parameters

These parameters are used to set up the geometric parameters defining the surfaces of interest.

*   **Nwall_type**(int): Number of surface _types_ in the system (i.e. two surfaces may be identical).
*   **Nwall**(int): Number of surfaces in the system. (specify surface positions, types, and links in the file dft_surfaces.dat)
*   **Nlink**(int): Number of unique macrosurfaces (i.e. fixed atoms may be connected as molecules so Nlink may be small even though Nwall is large).
*   **Lauto_center**(int): Logical that signals whether the surfaces should be centered in the domain based on max and min coordinates (0=FALSE; 1=TRUE). Can be helpful with coupled DFT/Monte Carlo simulations (see Towhee code).
*   **Lauto_size**(int): Logical to have Tramonto choose the domain size based on the surface positions (0=FALSE; 1=TRUE). Can be helpful with coupled DFT/Monte Carlo simulations (see Towhee code).
*   **Xtest_reflect_TF**[Nlink][Ndim](int array): A logical array (0=FALSE: 1=TRUE). Only set an entry to True if there are reflective boundaries, a surface touches that reflective boundary, **and** if the surfaces in the next domain are to be treated as different surfaces than those in the computational domain. For example, consider a cylindrical surface with the long axis parallel to the z-coordinate of the system and assume all boundaries of the 3D domain are reflective. In the x and y directions, there are independent surfaces beyond the boundaries while in the z direction, the same cylinder is extended through the boundary. These parameters allow for differentiation between cases where that reflected cylinder should be treated as an independent surface (Xtest_reflect_TF[zdim]=TRUE) or where it should be treated as an extension of the surface in the computational domain (Xtest_reflect_TF[zdim]=FALSE).

### Definition of Basic Surface Geometries

*   **Surf_type**[Nwall_type](int vector):

    Vector to store surface geometries. Options are:

    *   0: Planar Wall of infinite extent in Ndim-1 dimensions.
    *   1: Planar Wall of finite extent in Ndim dimensions.
    *   2: Sphere (3D calculation) or Cylinder (2D calculation) ... use for studying colloidal systems.
    *   3: Atoms as surfaces (3D option only). Uses Sigma_w rather than WallParam to define size of spheres.
    *   4: One element surface (1D: thin membrane; 2D: thin rod, 3D: approximate point surface).
    *   5: Finite Length Cylinder (3D only)
    *   7: Pore defined by R only (infinite length cylindrical pore in 2D, spherical cavity in 3D)
    *   8: Pore of finite length (slit in 2D, cylindrical pore in 3D)
*   **Orientation**[Nwall_type](int vector):

    Vector to store the orientation of each surface type relative to the coordinate axis. This parameter does not have meaning for all of the surface types (e.g. atoms), and it is used only to indicate a direction for angle cutouts (see below) for other cases. Note that angle cutouts for 2D problems do not require this parameter because it the angle cutout is always based on the x-y plane. For surfaces where it does not have meaning enter 0 in the input file because an entry must be read for each surface type. The cases that require the orientation parameter are:

    *   0: Infinite Planar Wall: Indicates direction of surface normal if Ndim>1\. Also defines orientation of angle cutouts if Ndim=3\.
    *   1: Finite Planar Wall: Orientation only used to define angle cutouts.
    *   2: Cylindrical or Spherical Surface: Orientation only used to define angle cutouts.
    *   5: Finite Length Cylinder: Defines both direction of long axis of cylinder and orientation of angle cutouts if they are desired.
    *   7: Pore defined by R: Orientation only used to define angle cutouts.
    *   8: Pore of Finite Length: Defines both direction of Long axis of pore and orientation of angle cutouts if desired.
*   **WallParam**[Nwall_type](real vector):

    Vector to store a first parameter associated with the geometry of a given surface. Every surface type must have an entry in the input file. The meaning of WallParam in various cases is as follows:

    *   0: Infinite Planar Wall: Half-thickness (note this is often coupled with Type_bc=IN_WALL where the surface is placed on the boundary, and then this distance indicates a region where densities will be zero in the computational domain).
    *   1: Finite Planar Wall: Half-thickness in the x-dimension.
    *   2: Cylindrical or Spherical Surface: Radius.
    *   5: Finite Length Cylinder: Radius.
    *   7: Pore defined by R: Radius.
    *   8: Pore of Finite Length: Radius.
*   **WallParam2**[Nwall_type](real vector):

    Vector to store a second parameter associated with the geometry a given surface. Every surface type must have an entry in the input file. The meaning of WallParam2 in various cases is as follows:

    *   1: Finite Planar Wall: half thickness in the y-dimension (2D/3D).
    *   5: Finite Length Cylinder: half-length of the cylinder.
    *   8: Pore of Finite Length: half-length of the pore.
*   **WallParam3**[Nwall_type](real vector):

    Vector to store a third parameter associated with the geometry of a a given surface. Every surface type must have an entry in the input file. WallParam3 is only required in one case where:

    *   1: Finite Planar Wall: half thickness in the z-dimension (3D).

### Definition of Modifications to Basic Surface Geometries

*   **Lapply_offsets**[Ndim](int vector): Vector to store a logical (0=FALSE, 1=TRUE) to indicate if offsets (roughness or overlay functions defined below) should be applied to the various geometrical measures (WallParams). This switches can be used to apply offsets to part of a surface. Note that this is not a surface specific parameter as of Tramonto 4.0.

### _Surface Roughness Parameters_

*   **Lrough_surf**[Nwall_type](int vector):

    Vector to store a logical (0=FALSE, 1=TRUE) indicating if a surface should be roughened. This option is available for the following cases:

    *   0: Infinite Planar Wall: Only if Ndim>1
    *   1: Finite Planar Wall: Only if Ndim>1
    *   2: Cylindrical(2D) or Spherical(3D) Surfaces: Only if Ndim=2
    *   5: Finite Length Cylinder (3D only): Yes.
    *   7: Pore defined by R: Only if Ndim=2\.
    *   8: Pore of Finite Length: Yes
*   **Rough_param_max**[Nwall_type](real vector): Vector to specify the maximum magnitude, Δ<sub>max</sub> of the roughness. Tramonto uses this parameter combined with a random number generator to adjust geometry descriptors (e.g. WallParam +/- Δ) based on local coordinates.
*   **Rough_length**[Nwall_type](real vector): Vector to specify a length scale associated with surface roughness. Patches of the specified linear dimensions will have identical values of Δ.

    ### _Periodic Overlay Function Parameters_

*   **Nperiodic_overlay_fncs**[Nwall_type](int vector): Vector to specify the number of periodic functions to superimpose on the basic surface geometries. Up to 4 periodic functions can currently be applied. They are cosine functions that require as input an amplitude, period, orientation of the variation and an origin in the orientation direction. If more than 1 function is specified, the functions are summed. The function is applied to the base surface by setting [WallParamI= WallParamI+fnc(x-x<sub>O</sub>)] provided that Lapply_offsets[WallParamI]=TRUE. Periodic functions can be applied in the following cases:
    *   0: Infinite Planar Wall: If Ndim>1
    *   1: Finite Planar Wall: If Ndim>1
    *   5: Finite Length Cylinder: Yes.
    *   8: Pore of Finite Length: Yes
*   **OrientationPeriodicFnc**[Nwall_type][Nperiodic_overlay_fncs](int 2Dvector): Matrix to specify the direction (x,y,z) for applying all periodic overlay functions. Must have entries for entire matrix even if periodic functions will only be applied selectively.
*   **Amplitude**[Nwall_type][Nperiodic_overlay_fncs](double 2Dvector): Matrix to specify the amplitude for all periodic overlay functions. Must have entries for entire matrix even if periodic functions will only be applied selectively.
*   **Period**[Nwall_type][Nperiodic_overlay_fncs](double 2Dvector): Matrix to specify the distance associated with the period for all periodic overlay functions. Must have entries for entire matrix even if periodic functions will only be applied selectively.
*   **Origin**[Nwall_type][Nperiodic_overlay_fncs](double 2Dvector): Matrix to specify the origins for all periodic overlay functions. Note that the cosine function is at is maximum at the origin. Must have entries for entire matrix even if periodic functions will only be applied selectively.

### _Linear Overlay Function Parameters_

*   **Nlinear_overlay_fncs**[Nwall_type](int vector): Vector to specify the number of linear functions to superimpose on the basic surface geometries. Up to 4 linear functions can currently be applied. These linear functions are zero at a specified origin and are applied with a specified slope in a specified direction. An endpoint for the modification can also be specified. If more than 1 function is specified, the functions are summed. The functions are applied to the base surface by setting [WallParamI= WallParamI+fnc(x-x<sub>O</sub>)] provided that Lapply_offsets[WallParamI]=TRUE. Linear functions can be applied in the following cases:
    *   0: Infinite Planar Wall: If Ndim>1
    *   1: Finite Planar Wall: If Ndim>1
    *   5: Finite Length Cylinder: Yes.
    *   8: Pore of Finite Length: Yes
*   **OrientationLinearFnc**[Nwall_type][Nlinear_overlay_fncs](int 2Dvector): Vector to specify the direction (x,y,z) for applying all linear overlay functions. Must have entries for entire matrix even if periodic functions will only be applied selectively.
*   **Slope**[Nwall_type][Nlinear_overlay_fncs](double 2Dvector): Vector to specify the slope for all linear overlay functions. Must have entries for entire matrix even if periodic functions will only be applied selectively.
*   **Origin_linear**[Nwall_type][Nlinear_overlay_fncs](double 2Dvector): Vector to specify the origins for all linear overlay functions. Note that the linear function is zero at the origin. Must have entries for entire matrix even if periodic functions will only be applied selectively.
*   **Endpoint_linear**[Nwall_type][Nlinear_overlay_fncs](double 2Dvector): Vector to specify the endpoint for applying the linear overlay functions. Must have entries for entire matrix even if periodic functions will only be applied selectively.

### _Angle Cutout Parameters_

*   **LangleCutout_surf**[Nwall_type](int vector):

    Vector to store a logical (0=FALSE, 1=TRUE) indicating if a surface should be modified with an angle cutout. To apply this modification it is necessary to define the angles circumscribed by the surfaces. The wall positions (defined in dft_surfaces.dat) are taken as the origin for describing angles. The cutouts are based on a cylindrical coordinate system. In any 2-dimensional calculation, the z-direction is out of the plane of the calculation, and angles are computed relative to the positive x-axis from the surface based origin. In 3-dimensional problems, the _Orientation_ parameter defines the z-direction in the cylindrical coordinate system. If orientation=2, angles are measured from the positive x-axis, if orientation=1, angles are measured from the positive z-axis. If orientation=1, the angles are measured from the positive y-axis. This feature may be used to create surfaces with heterogeneous chemistry. This option is available for the following cases:

    *   0: Infinite Planar Wall: If Ndim>1
    *   1: Finite Planar Wall: If Ndim>1
    *   2: Cylindrical or Spherical Surfaces: Yes
    *   5: Finite Length Cylinder: Yes.
    *   7: Pore defined by R only: Yes
    *   8: Pore of Finite Length: Yes
*   **Angle_start**[Nwall_type](real vector): Vector to specify the angle (in degrees) from the appropriate origin where the surface should start. Must have entries for entire matrix even if ange cutouts will only be applied selectively.
*   **Angle_end**[Nwall_type](real vector): Vector to specify the angle (in degrees) from the appropriate origin where the surface should end. Must have entries for entire matrix even if angle cutouts will only be applied selectively.

***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a> 