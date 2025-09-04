# A Beginner's Guide to using S3DF 

Welcome to S3DF! This guide provides a clear, step-by-step workflow for all users, particularly those with limited computing experience. In this document, we will walk you through how to:

- Log in to the S3DF system
- Navigate directories and storage spaces
- Access supported applications
- Prepare and submit a job script

These items illustrate a typical workflow for many S3DF users, particularly those utilizing our systems for extensive calculations. These calculations may encompass simulations of physical phenomena, data pre-processing or post-processing, and various forms of data generation or analysis.

Before we dive into the details, please remember that you can always reach out for [assistance](contact-us.md)

## 1. Connect to S3DF: there are three primary methods to [access](accounts-and-access.md#connect) S3DF 
   - **SSH** (Secure Shell):
      - You can connect Login Node using any SSH client

              ssh username@login-node-address

      - After successfully connecting to the Login Node, establish a second connection to a [Pool Node](interactive-compute.md#interactive-pools) using SSH to access S3DF batch compute resources and storage.  

              ssh username@pool-node-address
   - **NoMachine**: NoMachine offers a specialized remote desktop solution that enhances X11 graphics performance over slow connections compared to SSH[NoMachine reference](reference.md#nomachine)
   - **OnDemand**: you can access a web-based terminal via OnDemand [`https://s3df.slac.stanford.edu/ondemand`](https://s3df.slac.stanford.edu/ondemand). For further information on using OnDemand, please refer to the OnDemand reference documentation [OnDemand
reference](interactive-compute.md#ondemand).

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
