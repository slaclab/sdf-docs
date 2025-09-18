# Beginner's Guide

Welcome to S3DF! This guide presents three different methods of accessing S3DF. We aim to provide a straightforward, 
step-by-step workflow suitable for all users, especially those with limited computing experience. Within this document, you will find guidance on how to:

- Log in to the S3DF system
- Navigate directories and storage spaces
- Access supported applications
- Prepare and submit a job script
Follow these instructions to efficiently connect to the S3DF environment and run your desired software. Let's get started!
  

## Access to S3DF Through SSH

This example provides a clear, step-by-step workflow for running software, ACE3P (Advanced Computational Electromagnetics 3D Parallel), on S3DF throgh SSH. 

- Connect to a Login Node
To start, connect to the login node using the following command:

                  ssh username@s3dflogin.slac.stanford.edu

- Connect to a Pool Node
After successfully connecting to the login node, establish a second connection to a pool node using SSH. For example:

                  ssh iana
     
-  Set Up the Running Environment
To set up the running environment, create a bash file containing all necessary commands, and then execute the bash file.

-  Configure an [SLURM](batch-compute.md#)slurm Job Script
Here is an example SLURM job script named run.sbatch:


                   #!/bin/bash
                  #SBATCH --partition=milano
                  #SBATCH --account=rfar
                  #SBATCH --job-name=test
                  #SBATCH --output=output-%j.txt
                  #SBATCH --error=error-%j.txt
                  #SBATCH --nodes=1
                  #SBATCH --ntasks-per-node=16
                  #SBATCH --time=0-00:10:00
                  mpirun /sdf/group/rfar/ace3p/bin/omega3p pillbox.omega3p


 -  Submit Jobs to a Compute Node
Use the sbatch command to submit your job to a compute node for execution:

                  sbatch run.sbatch

 -  Check the Status of Running Jobs (Optional)
To monitor the status of your submitted jobs, run the following command:

                  squeue -u username

-  View Data Output
Once your jobs have completed, you can view the data output directly on the pool node to verify that the results are as expected.

-  Transfer Data (If Necessary)
If you need to transfer data, connect to a data transfer node to facilitate the movement of your files. Use appropriate file transfer commands (e.g., scp, rsync) to move your data to the desired location.

## Access to S3DF Through NoMachine
 - NoMachine offers a specialized remote desktop solution that enhances the performance of X11 graphics over slow connections, compared to SSH.
 - A key feature of NoMachine is its ability to maintain the state of your desktop across multiple sessions, even if your internet connection is unexpectedly lost.
 - To access NoMachine, use the login pool at s3dfnx.slac.stanford.edu.
 - For additional information about this access method, please refer to the [NoMachine](reference.md#nomachine) documentation.

## Access to S3DF Through OnDemand
 - Users can also access S3DF through [Open OnDemand](interactive-compute.md#ondemand) via any (modern) browser.
 - This solution is recommended for users who want to run Jupyter notebooks, or don't want to learn SLURM, or don't want to download a terminal or the NoMachine remote desktop on their system.
 - After login, you can select which Jupyter image to run and which hardware resources to use (partition name and number of hours/cpu-cores/memory/gpu-cores).
 - The partition can be the name of an interactive pool or the name of a SLURM partition.
 - You can choose an interactive pool as partition if you want a long-running session requiring sporadic resources; otherwise slect a SLURM partition.
 - Note that no GPUs are currently available on the interactive pools.
