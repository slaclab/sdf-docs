# Beginner's Guide

Welcome to S3DF! This guide provides a clear, step-by-step workflow for all users, particularly those with limited computing experience. In this document, we will walk you through how to:

- Log in to the S3DF system
- Navigate directories and storage spaces
- Access supported applications
- Prepare and submit a job script
Follow these instructions to efficiently connect to the S3DF environment and run your desired software. Let's get started!
  

## 1. Connect to a Login Node

- Use SSH or NoMachine to connect to a login node. This is your initial access point to the system.
- Example command for SSH:

                ssh username@login-node-address

## 2. Connect to a Pool Node

- After successfully connecting to the login node, establish a second connection to a pool node using SSH.
- Example command:

              ssh username@pool-node-address

## 3. Run Desired Software

- You can run your desired software interactively. For instance, if you need to use HFSS, launch it from the pool node.
- Alternatively, if you're configuring input files for other software, such as ACE3P, proceed to the next step.

## 4. Configure Input Files

- Prepare and configure the necessary input files for the software you intend to use. Ensure all files are correctly set up for your simulations.

## 5. Submit Jobs to a Compute Node

- Use the sbatch command to submit your jobs to a compute node for execution.
- Example command:

            sbatch your-job-script.sbatch

## 6. Check Status of Running Jobs (Optional)

- To monitor the status of your submitted jobs, use the following command:
  
            squeue -u username

## 7. View Data Output

 - Once your jobs have completed, you can view the data output directly on the pool node to ensure results are as expected.

## 8. Transfer Data (if necessary)

- If you need to transfer data, connect to a data transfer node to facilitate the movement of your files.
- Use appropriate file transfer commands (e.g., scp, rsync) to move your data to the desired location.


By following this workflow, you can effectively utilize the S3DF system for your computational needs. 
Ensure you have all necessary software and dependencies installed before starting, 
and refer to additional documentation for specific software setup if needed.

# Examples

## Logging In Through SSH

This example provides a clear, step-by-step workflow for running software, ACE3P (Advanced Computational Electromagnetics 3D Parallel), on S3DF throgh SSH. 

- 1. Connect to a Login Node
To start, connect to the login node using the following command:

        ssh username@s3dflogin.slac.stanford.edu

- 2. Connect to a Pool Node
After successfully connecting to the login node, establish a second connection to a pool node using SSH. For example:

        ssh iana
     
- 3. Set Up the Running Environment
To set up the running environment, create a bash file containing all necessary commands, and then execute the bash file.

- 4. Configure an SLURM Job Script
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


 - 5. Submit Jobs to a Compute Node
Use the sbatch command to submit your job to a compute node for execution:

        sbatch run.sbatch

 - 6. Check the Status of Running Jobs (Optional)
To monitor the status of your submitted jobs, run the following command:

        squeue -u username

- 7. View Data Output
Once your jobs have completed, you can view the data output directly on the pool node to verify that the results are as expected.

- 8. Transfer Data (If Necessary)
If you need to transfer data, connect to a data transfer node to facilitate the movement of your files. Use appropriate file transfer commands (e.g., scp, rsync) to move your data to the desired location.

