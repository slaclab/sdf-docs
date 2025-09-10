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

## 3. Setup Running Environment

- S3DF uses the Lmod Module system to administrate common software packages
- There are default modules that are loaded into your environment upon logging in
- S3DF encourages experts from non-SCS to use Lmod to provide, support, maintain and share software tools they build.
- 
## 4. Slurm Job Script

- [Slurm](refernece.md#slurm-faq) is a batch scheduler that enables users to submit compute jobs of varying scope to our compute clusters. 
- It will queue up jobs such that the compute resources available in S3DF are fairly and efficiently shared and distributed for all users.
- Prepare a slurm job script

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

