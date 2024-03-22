# AxiSEM3D-Modified

This is a custom version of AxiSEM3D. The original version can be found [here](https://github.com/AxiSEMunity/AxiSEM3D). Please also see instructions there regarding installation and general usage. 

The modifications consist the following:

1. Output of deformed undulated geometry.

Input mesh for AxiSEM 3D are all regular, with no undulations. Currently, it's not possible to display quantities in the deformed mesh, no matter for defined quantities (velocities etc.) or computed quantities (wavefield). The current modification provides a means to visualize these quantities in the deformed mesh, through outputting quantities from the main code as well as using provided post-processing script in a Jupyter Notebook. 

This modification allows correct visualization of wavefield without distorting it by plotting on the regular mesh, and also enables checking if your desired, undulated model, has been represented correctly by AxiSEM3D. 

An example with the provided example2_3dcrust is provided.

2. Intensive I/O leveraging locally-connected but volatile storage (i.e. local_scratch)

AxiSEM3D by default dumps all outputs to a single location. When multiple MPI ranks try to do this, this usually causes I/O taking more time than computing and in the worst case could cause filesystem faliures resulting in failed simulations. This can be avoided if the HPC system you are using has local_scratch, i.e. physically-connected hard drives to each computing node usually through the high-throughput infiniband. These storage only persist during run-time, so it's essential to copy the files back to a persistent storage as the last step of your job. For large simulations, this set up can significantly increase simulation speed. 

In addition, post-processing scripts for filtering the entire wavefield and making a movie (in the deformed mesh), using Dask distributed computing and leveraging loocal_scratch are also provided. Currently, to make ".vtk" files to use with Paraview, your Python version cannot be higher than 3.7. 

