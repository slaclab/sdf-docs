# Compute Environment

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
| [$LSCRATCH](#lscratch | Local (to compute node) temporary storage | no | no | yes | user | Per Job | Fastest |
| [$SCRATCH](#scratch) | Global (to cluster) temporary storage | no | no | yes | group | 1 month* | Fast |
| [$GROUP](#scratch) | Group space for shared data and programs | no | no | no | group | Forever | Fast |

#### $HOME Storage :id=home

Permanent, relative small storage space for things like source code, shell scripts, etc. Our current file system will place small files (<1MB) SSD and also spread larger files across multiple hard drives in order to improve performance and scalability.

#### $LSCRATCH Storage :id=lscratch

It may be beneficial to bulk move data from somewhere else onto the local compute node to guarantee the quickest and fastest access to that data - especially if a lot of random input/output is performed on that data. The limitatations of using this method are that you will be constrained by the amonut of storage available on the Compute Node and that clustered software (eg MPI jobs) may need to be especially programmed to take advantage of this. In addition, any data stored under $LSCRATCH will be automatically deleted after each job. This is therefore ideal for intermediate data or very read heavy data.

#### $SCRATCH Storage :id=scratch

We provide a small shared $SCRATCH space that is globally shared on all Compute Nodes. This is similar to $LSCRATCH but is not just locally bound to a single node. It is also not purged after each job, but upon a schedule whereby any data which has not been read/modified over 1 month??? will be automatically deleted. If you wish to keep the data for longer, then we recommend moving the data into [$GROUP storage](#group). Due to the nature of the performance edge of this storage, we also enforce a quota. $SCRATCH is especially useful for temporary data such as checkpoints and application input and output.

?> __TODO__ what is quota? what conditions is it enforced?

#### $GROUP Storage :id=group

?> How do we define what a group is?

For long term storage of data, we recommend that users keep data under $GROUP storage. This is tuned for large datasets and shared colloration efforts where it may be necessary to share data within a group of researchers. Due to the volume of data we expect, we enforce a [quota] on the group space. Users may be members of numerous different groups/experiments and therefore have access to numerous different junctions/paths for different groups/experiments.

When you [purchase extra storage](resources-and-allocations?id=storage-1) you will primarily be adding space to $GROUP.




### Archive

!> __TODO__

## Do's and Don'ts

- Do [talk to us](contact-us.md) about your requirements!

- Don't perform any compute or disk intensive tasks on the Login Nodes!

- Do be respectful of other's jobs - you shall be sharing a limited set of nodes with many many other users. Please consider the type, size and quantity of jobs that you submit so that you do not starve others of compute resources. We do implement [fair sharing] to limit the impact upon others, however there are ways to game the system ;)

- Don't run interactive sessiosn for a long time - do not treat the Compute Nodes as your private remote terminal. Opening an interactive session (using `srun --tty`) and not actuallyl running any heavy processes is very wasteful of resources and could potentially be preventing others from dong their work. Consider using [Jupyter] of just using the Login Nodes for light tasks.

?> where should we compile code?

- Don't run your jobs from your `$HOME` directory (does this actually matter due to our SDF architecture?)

- Avoid keeping many (hundreds) of files in a single directory if possible - file systems typically do a lot better when you use a small number of large files.

- Do keep an eye on your file system [quotas] - your jobs will likely fail if it cannot write to disk due to a full quota. You can either choose a different file system to write to, or request a [quota increase]

- Limit I/O intensive sessions where your jobs reads or writes a lot of data, or performs intensive meta data operations such as stat'ing many files or directories and opening and closing files in quick succession.

- Do launch test jobs requesting a smaller resource before launching many (potentially hundreds) of jobs.

- Do request only the resources that you need. If you ask for more time or more CPU's or GPU's than you can actually use in your job, then not only will you be reducing your fairshare so that your later jobs may be de-prioritised, but it also prevents others from using potentially idle resources.



- 
- 
