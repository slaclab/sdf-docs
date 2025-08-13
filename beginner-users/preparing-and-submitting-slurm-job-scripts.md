# Running Jobs

S3DF provides two main ways to run jobs: 
- Interactive Jobs
- Batch Jobs.
This guide will help you understand how to use both methods effectively.

## 1. Interactive Jobs
Interactive jobs allow you to access compute resources for tasks such as building, debugging, running analyses, or submitting jobs to the batch system.

### Steps to Run an Interactive Job

#### 1. Log in to the Bastion Host:

Use an SSH terminal session (or NoMachine) to log into the bastion host:

  ssh s3dflogin.slac.stanford.edu

#### 2. Connect to an Interactive Pool:
After logging into the bastion host, SSH into an interactive pool:

    ssh <pool_name>

#### 3. Run Your Commands:
You can execute commands directly in the interactive session. For example:

    ./your_program

### Additional Notes:
- Ensure that you have sufficient resources for your tasks.
- When finished, simply type exit to end your interactive session.

## 2. Batch Jobs
Batch jobs in S3DF are managed through Slurm, a batch scheduler that allows users to submit compute jobs across clusters. This system ensures fair and efficient sharing of resources among all users.

### Why Use Batch Jobs?
 - Enhanced Resources: Batch jobs can utilize significantly more CPU, GPU, and memory than personal computers, enabling large computations and data processing tasks.
 - Efficient Processing: S3DF servers offer rapid access to centralized storage and have a variety of pre-installed software, facilitating quick and large-scale computation without impacting personal devices.
 - Slurm Transition: S3DF uses Slurm due to its compatibility with modern systems, including NVIDIA GPUs, improving scheduling efficiency and user experience compared to previous batch systems.

### Key Concepts in Batch Jobs
 - Batch Nodes: These are servers configured for running batch jobs.
 - Slurm Partition: A logical grouping of batch nodes with similar specifications (e.g., CPU types). Example partitions include roma and milano.
 - Resource Monitoring: Use the following command to check the status of nodes:

        sinfo --Node --format="%10N %.6D %10P %10T %20E %.4c %.8z %8O %.6m %10e %.6w %.60f"

### Submitting a Batch Job

#### 1. Create a Batch Script:
Write a script file (e.g., script.sh) with Slurm commands and the job commands you want to execute:

    #!/bin/bash
  
    #SBATCH --partition=milano
    #SBATCH --job-name=test
    #SBATCH --output=output-%j.txt
    #SBATCH --error=output-%j.txt
    #SBATCH --ntasks=1
    #SBATCH --cpus-per-task=12
    #SBATCH --mem-per-cpu=1g
    #SBATCH --time=0-00:10:00
    #SBATCH --gpus 1

    <commands here>

- Replace <commands here> with the specific commands for your job.
- The script will log output and error messages to output-%j.txt, where %j is replaced by the job ID.

#### 2. Submit the Job:
Use the sbatch command to submit your batch script:

    sbatch script.sh

#### 3. Monitor Your Job:
Check the status of your job using:

    scontrol show job <job_id>

### Submitting Jobs Without a Batch Script
Alternatively, you can submit jobs directly from the command line using the --wrap option:

    sbatch --wrap="your_command_here"

### Specifying Job Duration
It is crucial to set a meaningful duration for your job, allowing the Slurm scheduler to prioritize jobs effectively. Use the --time option with formats such as:

- M (minutes)
- H:M:S (hours, minutes, seconds)
- D-H (days, hours)
  
Jobs exceeding the specified time will terminate, potentially wasting computational resources.

This guide provides an overview of how to run both interactive and batch jobs in S3DF. Using these resources effectively can enhance your computational efficiency and overall experience on the system. If you have further questions, please refer to the S3DF documentation or reach out for support.
