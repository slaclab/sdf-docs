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



