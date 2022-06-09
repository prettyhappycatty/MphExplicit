# Copyight
```
//================================================================================================//
//------------------------------------------------------------------------------------------------//
//    MPH-WC : Moving Particle Hydrodynamics for Weakly Compressible  (explicit calculation)      //
//------------------------------------------------------------------------------------------------//
//    Developed by    : Masahiro Kondo                                                            //
//    Distributed in  : 2022                                                                      //
//    Lisence         : GPLv3                                                                     //
//    For instruction : see README                                                                //
//    For theory      : see the following references                                              //
//     [1] CPM 8 (2021) 69-86,       https://doi.org/10.1007/s40571-020-00313-w                   //
//     [2] JSCES Paper No.20210006,  https://doi.org/10.11421/jsces.2021.20210006                 //
//     [3] CPM 9 (2022) 265-276,     https://doi.org/10.1007/s40571-021-00408-y                   //
//     [4] CMAME 385 (2021) 114072,  https://doi.org/10.1016/j.cma.2021.114072                    //
//     [5] JSCES Paper No.20210016,  https://doi.org/10.11421/jsces.2021.20210016                 //
//    Copyright (c) 2022                                                                          //
//    Masahiro Kondo & National Institute of Advanced Industrial Science and Technology (AIST)    //
//================================================================================================//

This program is for conducting particle based fluid simulation
using MPH-WC (Moving Particle Hydrodynamics for Weakly Compressible) method. 
```

------ Directories ------
The directories in the repository is as follows:  

MphExplicit ---- generator
            |--- results
            |--- source
           

# How to execute samples
(1)"generator" is for pre-process. To compile it, run
> make 
in generator directory. (g++ is to be installed)

(2)"results" contains sample cases for the calculation. 
In a case directory, execute
> ./generate.sh
The generator will be launched and particles will be generated
reading cubolid file (*.boid).

(3)"source" contains the main solver for MPH-WC calculations. 
To complie it, run
> make 
in the source directory. 

(4)Then, back to the case directory, and launch
> ./execute.sh
The solver starts with reading parameter file (*.data) 
and particle file (*.grid). 
The series of calculation results (*.vtk) are output,  
and they can be visualized with a viewer like ParaView. 
(https://www.paraview.org/)


# Using openMP and openACC
In compling with openMP or openACC, edit make file to switch the compliers
and its options. 
For using openMP apply
 CC = g++
 CFLAGS  = -O3 -fopenmp 
For using openACC apply
 CC = pgc++
 CFLAGS    =  -acc -O3 -Minfo=accel 
The solver program has only been tested with 
   g++ 7.5.0.   and   NVIDIA HPC-SDK 20.9
So, they are recomended though compatible versions may work. 


# Generating particles
Initial particle disturiburion in combination of cuboids 
can be generated by editting the cuboid file (*.boid) and using the generator. 
For distribution including shape other than cuboid, particles 
are to be generated in other way such as making a new program for it.   
  
In the main solver, the particle types are defined as
 0: fluid 
 1: fluid
 2: wall
 3: wall
Therefore, 2 fluid types and 2 wall types can be used in the solver. 
To change tne number of types, the main solver is to be modified. 


# Changing physical properties
The physical properties and calculation conditions are given in 
the parameter file (*.data). By editting the file, the physical 
properties can be changed. 


# For 3D calculation
Particle distribution in 3D can be generated only by editing the 
cuboid file (*.boid). No modification in the generator program is needed. 
For the main solver, the macro TWO_DIMENSIONAL in main.cpp is to be
commented out and the program has to be re-compiled. 
After re-compiling, the solver can be executed in the same way as the 2D samples.  





