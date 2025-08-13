# S3DF General Workflow Guide

This guide provides a clear step-by-step workflow for using the S3DF system. Follow these instructions to efficiently connect to the S3DF environment and run your desired software.

# Step-by-Step Workflow

## Connect to a Login Node

### 1. Use SSH or NoMachine to connect to a login node. This is your initial access point to the system.

- Use SSH or NoMachine to connect to a login node. This is your initial access point to the system
- Example command for SSH:

                ssh username@login-node-address

### 2. Connect to a Pool Node

- After successfully connecting to the login node, establish a second connection to a pool node using SSH.
- Example command:

              ssh username@pool-node-address

### 3. Run Desired Software

- You can run your desired software interactively. For instance, if you need to use HFSS, launch it from the pool node.
- Alternatively, if you're configuring input files for other software, such as ACE3P, proceed to the next step.

### 4. Configure Input Files

- Prepare and configure the necessary input files for the software you intend to use. Ensure all files are correctly set up for your simulations.

### 5. Submit Jobs to a Compute Node

- Use the sbatch command to submit your jobs to a compute node for execution.
- Example command:

            sbatch your-job-script.sbatch

### 6. Check Status of Running Jobs (Optional)

- To monitor the status of your submitted jobs, use the following command:
  
            squeue -u username

### 7. View Data Output

 - Once your jobs have completed, you can view the data output directly on the pool node to ensure results are as expected.

### 8. Transfer Data (if necessary)

- If you need to transfer data, connect to a data transfer node to facilitate the movement of your files.
- Use appropriate file transfer commands (e.g., scp, rsync) to move your data to the desired location.

## Conclusion
By following this workflow, you can effectively utilize the S3DF system for your computational needs. 
Ensure you have all necessary software and dependencies installed before starting, 
and refer to additional documentation for specific software setup if needed.

For further assistance, see S3DF document
