# Getting Started

## Access Information

| Access 	| Address 	|  	
|-	|-	|
| SSH 	|  sdf-login.slac.stanford.edu |  	
| Ondemand 	| [https://sdf.slac.stanford.edu/pun/sys/dashboard](/pun/sys/dashboard ':ignore') 	|  	
| Globus Endpoint 	| slac#sdf 	|  	
| Documentation | [this!](/ ':ignore') |
| Scheduler | [slurm](https://slurm.schedmd.com/) |
| Help | [slac.slack.com #comp-sdf](https://app.slack.com/client/T1X4J8FJ8/C01965DTG91) |


## Accounts

!> SDF uses a different authentication method compared to our previous Unix services. You will need a [SLAC Windows AD account](accounts-and-access.md) if you don't already have one to use SDF.


## Compute Environment

### Basics

!> __TODO__ This page will describe the compute environment of SDF

SDF is a typical high performance batch cluster as shown below:

```
                                      ________
                                     (________) 
                                     | Shared |
                                     | File   | 
                                     | System |
                                     (________)
                                       |    |
                              _________|    |_________________
                              |                              |
                        ,,,,,,,,,,,,,,               ,,,,,,,,,,,,,,,,,,,             
                   -->  , Login Node ,               ,, Compute Nodes ,,              
                   |    ,,,,,,,,,,,,,,               ,,,,,,,,,,,,,,,,,,,              
                   SSH        |                ,////   /////   /////   /////       
                   Web     sbatch             ,*****  ,*****  ,*****  ,*****      
                   |        srun      |---->  ,*****  ,*****  ,*****  ,*****      
                   |          |       |       ,*****  ,*****  ,*****  ,*****      
     ,-#%#%-%#%.   |      ---------   |       ,*****  ,*****  ,*****  ,*****      
    # Internet %---|      | Queue |---|       ,*****  ,*****  ,*****  ,*****      
     "%#%__%#%#,          ---------                                            

```

Users would typically use SSH or a web portal to 'log in' a Login Node that provides tools to interact with a Batch scheduler or queuing system where a compute job (a long running program) will wait for requested resources to become available on one or more of the available Compute Nodes. All Nodes and Shared File Systems  are inter-connected using a very fast low latency network to benefit scalable compute and fast access to data.

The Login Nodes are a shared resource and what you do on these nodes may affect other users who are also logged into the Login Node. Therefore the Login Node should NOT be used for computational jobs but rather to find and organise files/data on the Shared File System and to submit jobs to the batch scheduler. Once you job starts running on one or many Compute Nodes, they shall run solely on the machine (and or a specified fraction of the machine).

Our Login Nodes for SDF are

|   |   |
|---|---|
| SSH | sdf-login.slac.stanford.edu |
| Web | sdf.slac.stanford.edu |

We have numerous types of [Compute Nodes](resources-and-allocations.md#compute) - both CPU and GPU and a high speed [Shared File System](resources-and-allocations.md#storage) as part of SDF.

We make use of the environment module system in order for users to quickly identify scientific applications that are available for immediate use on the Compute Nodes.

?> __TODO__ more about module avail etc.

We also provide common compilation tools...

?> __TODO__ describe compilation tools etc.


## Storage

### Disk

We have 4 kinds of on disk immediate access storage available; each have their limitations which are described below:

| File System  | Description | Snapshots  | Backup  | Purging  | Access | Retention | Speed |
|---|---|---|---|---|---|---|---|
| [$HOME](#home) | General user level configuration files | no | yes * | no | user | Forever | Fast |
| [$LSCRATCH](#lscratch) | Local (to compute node) temporary storage | no | no | yes | user | Per Job | Fastest |
| [$SCRATCH](#scratch) | Global (to cluster) temporary storage | no | no | yes | group | 31 days* | Fast |
| [$GROUP](#scratch) | Group space for shared data and programs | no | no | no | group | Forever | Fast |

#### $HOME Storage :id=home

Permanent, relative small storage space for things like source code, shell scripts, etc. Our current file system will place small files (<1MB) SSD and also spread larger files across multiple hard drives in order to improve performance and scalability.

#### $LSCRATCH Storage :id=lscratch

It may be beneficial to bulk move data from somewhere else onto the local compute node to guarantee the quickest and fastest access to that data - especially if a lot of random input/output is performed on that data. The limitatations of using this method are that you will be constrained by the amonut of storage available on the Compute Node and that clustered software (eg MPI jobs) may need to be especially programmed to take advantage of this. In addition, any data stored under $LSCRATCH will be automatically deleted after each job. This is therefore ideal for intermediate data or very read heavy data.

#### $SCRATCH Storage :id=scratch

We provide a small shared $SCRATCH space that is globally shared on all Compute Nodes. This is similar to $LSCRATCH but is not just locally bound to a single node. It is also not purged after each job, but upon a schedule whereby any data which has not been read/modified over 31 days will be automatically deleted. If you wish to keep the data for longer, then we recommend moving the data into [$GROUP storage](#group). Due to the nature of the performance edge of this storage, we also enforce a quota. $SCRATCH is especially useful for temporary data such as checkpoints and application input and output.
Dedicated storage for each SDF user had been created at /scratch/<first_username_letter>/<username>/ (so user "radmer" would use "/scratch/r/radmer/", for example).  For each user we plan to set $SCRATCH to point to this area, but the schedule for this change is not yet determined.

?> __TODO__ what is quota? what conditions is it enforced?

#### $GROUP Storage :id=group

?> How do we define what a group is?

For long term storage of data, we recommend that users keep data under $GROUP storage. This is tuned for large datasets and shared colloration efforts where it may be necessary to share data within a group of researchers. Due to the volume of data we expect, we enforce a [quota] on the group space. Users may be members of numerous different groups/experiments and therefore have access to numerous different junctions/paths for different groups/experiments.

When you [purchase extra storage](resources-and-allocations?id=storage-1) you will primarily be adding space to $GROUP.




### Archive


### Managing Your Files

#### Navigating the Shared File Systems


#### Moving data around
Traditional secure copies (scp) will work and SDF is a secure [Globus](https://www.globus.org/how-it-works) endpoint. 

#### Help! I've lost some files! What can I do?
Some directories are periodically backed up. [Contact us](contact-us.md) to retrieve the last back up. 

## Running Jobs
Depending on your application, you can run jobs in a variety ways:   
* through a traditional terminal (and SSH)
* a broswer terminal, opened from the [SDF login page](https://sdf.slac.stanford.edu/public/doc/#/)
* in a jupyter notebook

Jobs are submitted using the batch scheduler software called Slurm. 
More information on Slurm, submission scripts, and commands can be found on the [Batch Compute page. ](batch-compute.md)

### Example
A basic Slurm example [can be found here](batch-compute.md#slurmexample) on the Batch Compute page.  
Submission scripts can be submitted using the sbatch command on the command line: `sbatch filename.sh` 

### Running Jupyter
Please see [Jupyter](interactive-compute.md#jupyter)


### Software
SDF uses the module system. Currently installed modules can be viewed with this command: `module avail`


To load a specific module (and use the software), use the `module load module-name-you-want` command.

```

----------------------------------------------------------------------------------------- /usr/share/Modules/modulefiles -----------------------------------------------------------------------------------------
dot         module-git  module-info modules     null        use.own

------------------------------------------------------------------------------------------------ /etc/modulefiles ------------------------------------------------------------------------------------------------
slurm

---------------------------------------------------------------------------------------------- /sdf/sw/modulefiles -----------------------------------------------------------------------------------------------
atlas-jupyter/20200502               exo200_offline/v01_g4                google-sdk/292.0.0-alpine            matlab/R2020b                        rh-python36
cuda/10.2.89                         fftw2/2.1.5-openmpi-4.0.4-gcc-4.8.5  hdf5/1.12.0-openmpi-4.0.4-gcc-4.8.5  openmpi/4.0.4-gcc-4.8.5              slac-ml/20190712.2
cudnn/cudnn-10.2-linux-x64-v7.6.5.32 fftw3/3.3.8-openmpi-4.0.4-gcc-4.8.5  imagemagick/6.8.9                    pytorch/1.4                          slac-ml/20200211.0
devtoolset/7                         gcc/4.8.5                            lsst/r18_1_0                         rclone/1.44                          slac-ml/20200227.0
devtoolset/8                         gcc/9.3.1                            lsst/r19_0_0                         rclone/1.51                          slurm
devtoolset/9                         git/2.13.0                           matlab/R2020a                        rclone/1.52.2                        xfce/ubuntu18.04

--------------------------------------------------------------------------------------- /sdf/group/cryoem/sw/modulefiles/ ----------------------------------------------------------------------------------------
amira/6.7.0             cryosparc/2.13.2        emClarity/1.0.0         imod/4.9.11             motioncor2/1.2.3-intpix protomo/2.4.2           relion/ver3.1           topaz/0.2.2
chimera/1.13.1          cryosparc/2.14.2        fah/7.5.1               imod/4.9.12             motioncor2/1.2.6        pymol/2.1.1             resmap/1.95             topaz/0.2.4
cryodrgn/0.2.1          ctffind/4.1.10          icon-gpu/1.2.9          jax/0.1.64              motioncor2/1.3.0        pymol/2.2               rosetta/2018.48         xds/20190315
cryodrgn/0.3.1          ctffind/4.1.13          imod/4.10.38            motioncor2/1.2.1        motioncor2/1.3.2        relion/3.0.2            rosetta/3.10
cryolo/1.5.4            eman2/20200922          imod/4.10.42            motioncor2/1.2.2        openmbir/2.3.5          relion/3.0.8            scipion/1.2.1
cryosparc/2.12.4        eman2/20200925          imod/4.9.10             motioncor2/1.2.3        phenix/1.14-3260        relion/3.1.0            tem-simulator/1.3

```

Anything not installed via the module system will need to be installed locally by you (in $HOME or project directories) or globally by sytem admins. [Contact us](contact-us.md) if you would like something installed system wide. Note, $HOME storage is limited, so we do not recommend installing large software packages there. 

## Compiling Software
When compiling, avoid placing large amounts of software in your $HOME area, as space is limited there.

## Requesting Software
[Contact us!](contact-us.md)

## Monitoring





!> __TODO__

## Do's and Don'ts

- Do [talk to us](contact-us.md) about your requirements!

- Don't perform any compute or disk intensive tasks on the Login Nodes!

- Do be respectful of other's jobs - you shall be sharing a limited set of nodes with many many other users. Please consider the type, size and quantity of jobs that you submit so that you do not starve others of compute resources. We do implement [fair sharing] to limit the impact upon others, however there are ways to game the system ;)

- Don't run interactive sessiosn for a long time - do not treat the Compute Nodes as your private remote terminal. Opening an interactive session (using `srun --pty bash`) and not actually running any heavy processes is very wasteful of resources and could potentially be preventing others from dong their work. Consider using [Jupyter] of just using the Login Nodes for light tasks.

?> where should we compile code?

- Don't run your jobs from your `$HOME` directory (does this actually matter due to our SDF architecture?)

- Avoid keeping many (hundreds) of files in a single directory if possible - file systems typically do a lot better when you use a small number of large files.

- Do keep an eye on your file system [quotas] - your jobs will likely fail if it cannot write to disk due to a full quota. You can either choose a different file system to write to, or request a [quota increase]

- Limit I/O intensive sessions where your jobs reads or writes a lot of data, or performs intensive meta data operations such as stat'ing many files or directories and opening and closing files in quick succession.

- Do launch test jobs requesting a smaller resource before launching many (potentially hundreds) of jobs.

- Do request only the resources that you need. If you ask for more time or more CPU's or GPU's than you can actually use in your job, then not only will you be reducing your fairshare so that your later jobs may be de-prioritised, but it also prevents others from using potentially idle resources.



- 
- 
