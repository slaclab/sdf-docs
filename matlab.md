
# MatLab

This section describes how to run Matab in the S3DF Parallel Computing
environment.  You can bring up matlab interactively on your
desktop/laptop with nomachine or in an interactive slurm session with srun,
submit jobs from within matlab, or submit jobs using sbatch from a job submission node.
If you are going to use slurm, you will need to configure matlab for your account
following instructions included below.


## Using NoMachine

Install and configure nomachine on your system:
```
https://s3df.slac.stanford.edu/public/doc/#/reference?id=nomachine
https://confluence.slac.stanford.edu/display/SCSPub/NoMachine

Bring up nomachine, ssh to a  submission host and issue:

module load matlab
matlab
```

## Interactively using srun
```
ssh -X <batch submission host>
srun --x11 -A <account> -p <partition> -n 1 --pty /bin/bash
module load matlab
matlab
```


## How to set up your matlab configuration for slurm job submission

You will need to have access
to a slurm account and a partition in order to submit jobs.  Bring up
matlab,
```
module load matlab
matlab
```

Once in the matlab environment run the following commands:
```
configCluster
c = parcluster
c.AdditionalProperties.AccountName = '<name of account>'
c.AdditionalProperties.QueueName = '<name of partition>'
c.saveProfile
```
These steps will create a .matlab/3p_cluster_jobs directory under your account with
our site¿s configuration and you can submit jobs which will run on the
partition and account specified.


## Submitting matlab jobs with sbatch

You will need access to an account and a partition to
submit matlab jobs with slurm, and you will have to
configure matlab as described above.  Below are two
examples of batch submission scripts to run matlab.

### Example sbatch single node submission

```
#!/bin/sh

#SBATCH --partition=roma
#SBATCH --account=rubin
#SBATCH -n 1                            # 1 instance of MATLAB
#SBATCH --cpus-per-task=8               # 8 cores per instance
#SBATCH --mem-per-cpu=4gb               # 4 GB RAM per core
#SBATCH --time=00:30:00                 # 10 minutes

# Add MATLAB to system path
module load matlab

# Run code 
matlab -batch calc_pi
```

This is the sample calc_pi.m matlab job used in the above submission:

```
function calc_pi

c = parcluster('local');

% Query for available cores (assume either Slurm or PBS)
sz = str2num([getenv('SLURM_CPUS_PER_TASK') getenv('PBS_NP')]); %#ok<ST2NM>
if isempty(sz), sz = maxNumCompThreads; end

if isempty(gcp('nocreate')), c.parpool(sz); end

spmd
    a = (labindex - 1)/numlabs;
    b = labindex/numlabs;
    fprintf('Subinterval: [%-4g, %-4g]\n', a, b)

    myIntegral = integral(@quadpi, a, b);
    fprintf('Subinterval: [%-4g, %-4g]   Integral: %4g\n', a, b, myIntegral)

    piApprox = gplus(myIntegral);
end

approx1 = piApprox{1};  % 1st element holds value on worker 1
fprintf('pi           : %.18f\n', pi)
fprintf('Approximation: %.18f\n', approx1)
fprintf('Error        : %g\n',    abs(pi - approx1))


function y = quadpi(x)
%QUADPI Return data to approximate pi.

% Derivative of 4*atan(x)
y = 4./(1 + x.^2);
```

The job would look like this in the slurm queue:
```
[renata@sdfrome001 examples]$ squeue -u renata
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
           1155746      roma matlab-s   renata  R       0:10      1 sdfrome027
```

and the output should look like:
```
Starting parallel pool (parpool) using the 'Processes' profile ...
Connected to the parallel pool (number of workers: 8).
Worker 1: 
  Subinterval: [0   , 0.125]
  Subinterval: [0   , 0.125]   Integral: 0.49742
Worker 2: 
  Subinterval: [0.125, 0.25]
  Subinterval: [0.125, 0.25]   Integral: 0.482495
Worker 3: 
  Subinterval: [0.25, 0.375]
  Subinterval: [0.25, 0.375]   Integral: 0.455168
Worker 4: 
  Subinterval: [0.375, 0.5 ]
  Subinterval: [0.375, 0.5 ]   Integral: 0.419508
Worker 5: 
  Subinterval: [0.5 , 0.625]
  Subinterval: [0.5 , 0.625]   Integral: 0.379807
Worker 6: 
  Subinterval: [0.625, 0.75]
  Subinterval: [0.625, 0.75]   Integral: 0.339607
Worker 7: 
  Subinterval: [0.75, 0.875]
  Subinterval: [0.75, 0.875]   Integral: 0.301316
Worker 8: 
  Subinterval: [0.875, 1   ]
  Subinterval: [0.875, 1   ]   Integral: 0.266273
pi           : 3.141592653589793116
Approximation: 3.141592653589792672
Error        : 4.44089e-16
```


### Example sbatch multi-node  submission
In this case you would
see 2 slurm jobs, one just to bring up matlab and the other to run the job:
```
[renata@sdfrome001 examples]$ squeue -u renata
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
           1156422      roma    Job15   renata  R       0:12      1 sdfrome028
           1156401      roma matlab-m   renata  R       0:49      1 sdfrome028
```
This is the slurm submission job:
```
#!/bin/sh

#SBATCH --partition=roma
#SBATCH --account=rubin
#SBATCH -n 1                            # 1 instance of MATLAB
#SBATCH --cpus-per-task=1               # 1 core per instance
#SBATCH --mem-per-cpu=4gb               # 4 GB RAM per core
#SBATCH --time=00:20:00                 # 20 minutes

# Add MATLAB to system path
module load matlab

# Run code 
matlab -batch calc_pi_multi_node
```

And this is the matlab job, calc_pi_multi_node.m used in the above script:
```
function calc_pi_multi_node

c = parcluster;

% Required fields
c.AdditionalProperties.WallTime = '00:20:00';


if isempty(gcp('nocreate')), c.parpool(20); end

spmd
    a = (labindex - 1)/numlabs;
    b = labindex/numlabs;
    fprintf('Subinterval: [%-4g, %-4g]\n', a, b)

    myIntegral = integral(@quadpi, a, b);
    fprintf('Subinterval: [%-4g, %-4g]   Integral: %4g\n', a, b, myIntegral)

    piApprox = gplus(myIntegral);
end

approx1 = piApprox{1};  % 1st element holds value on worker 1
fprintf('pi           : %.18f\n', pi)
fprintf('Approximation: %.18f\n', approx1)
fprintf('Error        : %g\n',    abs(pi - approx1))


function y = quadpi(x)
%QUADPI Return data to approximate pi.

% Derivative of 4*atan(x)
y = 4./(1 + x.^2);
```

The output should look like:
```
Starting parallel pool (parpool) using the 's3df R2022b' profile ...

additionalSubmitArgs =

    '--ntasks=20 --cpus-per-task=1 --ntasks-per-core=1 -A rubin --mem-per-cpu=4gb -p roma -t 00:20:00'

Connected to the parallel pool (number of workers: 20).
Worker  1: 
  Subinterval: [0   , 0.05]
  Subinterval: [0   , 0.05]   Integral: 0.199834
Worker  2: 
  Subinterval: [0.05, 0.1 ]
  Subinterval: [0.05, 0.1 ]   Integral: 0.198841
Worker  3: 
  Subinterval: [0.1 , 0.15]
  Subinterval: [0.1 , 0.15]   Integral: 0.196885
Worker  4: 
  Subinterval: [0.15, 0.2 ]
  Subinterval: [0.15, 0.2 ]   Integral: 0.194022
Worker  5: 
  Subinterval: [0.2 , 0.25]
  Subinterval: [0.2 , 0.25]   Integral: 0.190332
Worker  6: 
  Subinterval: [0.25, 0.3 ]
  Subinterval: [0.25, 0.3 ]   Integral: 0.185913
Worker  7: 
  Subinterval: [0.3 , 0.35]
  Subinterval: [0.3 , 0.35]   Integral: 0.180872
Worker  8: 
  Subinterval: [0.35, 0.4 ]
  Subinterval: [0.35, 0.4 ]   Integral: 0.175326
Worker  9: 
  Subinterval: [0.4 , 0.45]
  Subinterval: [0.4 , 0.45]   Integral: 0.16939
Worker 10: 
  Subinterval: [0.45, 0.5 ]
  Subinterval: [0.45, 0.5 ]   Integral: 0.163175
Worker 11: 
  Subinterval: [0.5 , 0.55]
  Subinterval: [0.5 , 0.55]   Integral: 0.156782
Worker 12: 
  Subinterval: [0.55, 0.6 ]
  Subinterval: [0.55, 0.6 ]   Integral: 0.150305
Worker 13: 
  Subinterval: [0.6 , 0.65]
  Subinterval: [0.6 , 0.65]   Integral: 0.143823
Worker 14: 
  Subinterval: [0.65, 0.7 ]
  Subinterval: [0.65, 0.7 ]   Integral: 0.137403
Worker 15: 
  Subinterval: [0.7 , 0.75]
  Subinterval: [0.7 , 0.75]   Integral: 0.131101
Worker 16: 
  Subinterval: [0.75, 0.8 ]
  Subinterval: [0.75, 0.8 ]   Integral: 0.124959
Worker 17: 
  Subinterval: [0.8 , 0.85]
  Subinterval: [0.8 , 0.85]   Integral: 0.119012
Worker 18: 
  Subinterval: [0.85, 0.9 ]
  Subinterval: [0.85, 0.9 ]   Integral: 0.113284
Worker 19: 
  Subinterval: [0.9 , 0.95]
  Subinterval: [0.9 , 0.95]   Integral: 0.107791
Worker 20: 
  Subinterval: [0.95, 1   ]
  Subinterval: [0.95, 1   ]   Integral: 0.102542
pi           : 3.141592653589793116
Approximation: 3.141592653589793116
Error        : 0
```

## Submitting slurm jobs from inside matlab

You will need to have done the configuration steps shown above and
have access to an account and partition in slurm in order to be able
to submit jobs from within a matlab session.  Following is a log of
a session that runs the example batch script "j=batch(c,@pwd,1,{})"
from within a matlab interactive session:

```

[renata@sdfrome001 ~]$ module load matlab
[renata@sdfrome001 ~]$ matlab
MATLAB is selecting SOFTWARE OPENGL rendering.

                                                           < M A T L A B (R) >
                                                 Copyright 1984-2022 The MathWorks, Inc.
                                            R2022b Update 1 (9.13.0.2080170) 64-bit (glnxa64)
                                                            September 28, 2022

 
To get started, type doc.
For product information, visit www.mathworks.com.
 
>> c = parcluster

c = 

 Generic Cluster

    Properties: 

                   Profile: s3df R2022b
                  Modified: false
                      Host: sdfrome001.sdf.slac.stanford.edu
                NumWorkers: 100000
                NumThreads: 1

        JobStorageLocation: /sdf/home/r/renata/.matlab/3p_cluster_jobs/s3df/R2022b/shared
         ClusterMatlabRoot: /sdf/sw/matlab/R2022b
           OperatingSystem: unix

   RequiresOnlineLicensing: false
     PluginScriptsLocation: /sdf/sw/matlab/R2022b/toolbox/local/IntegrationScripts/s3df
      AdditionalProperties: List properties

    Associated Jobs: 

            Number Pending: 0
             Number Queued: 0
            Number Running: 9
           Number Finished: 3

>> c.AdditionalProperties

ans = 

  AdditionalProperties with properties:

             AccountName: 'rubin'
    AdditionalSubmitArgs: ''
              Constraint: ''
            EmailAddress: ''
             EnableDebug: 0
                MemUsage: '4gb'
            ProcsPerNode: 0
               QueueName: 'roma'
    RequireExclusiveNode: 0
             Reservation: ''
                 UseSmpd: 0
                WallTime: ''

>>  
>> 
>> j=batch(c,@pwd,1,{}) 

additionalSubmitArgs =

    '--ntasks=1 --cpus-per-task=1 --ntasks-per-core=1 -A rubin --mem-per-cpu=4gb -p roma'


j = 

 Job

    Properties: 

                   ID: 16
                 Type: independent
             Username: renata
                State: queued
       SubmitDateTime: 23-Nov-2022 07:25:43
        StartDateTime: 
      RunningDuration: 0 days 0h 0m 0s
           NumThreads: 1

      AutoAttachFiles: true
  Auto Attached Files: {}
        AttachedFiles: {}
    AutoAddClientPath: true
      AdditionalPaths: /sdf/home/r/renata/matlab
            FileStore: [1x1 parallel.FileStore]
           ValueStore: [1x1 parallel.ValueStore]
 EnvironmentVariables: {}

    Associated Tasks: 

       Number Pending: 1
       Number Running: 0
      Number Finished: 0
    Task ID of Errors: []
  Task ID of Warnings: []
   Task Scheduler IDs: 1184718

>> 
>> 
>> j.fetchOutputs

ans =

  1x1 cell array

    {'/sdf/home/r/renata'}

```



## Links to more information about MATLAB

Parallel computing documentation:
https://www.mathworks.com/help/parallel-computing/index.html

Parallel computing coding examples:
https://www.mathworks.com/products/parallel-computing.html

Parallel computing tutorials:
https://www.mathworks.com/videos/series/parallel-and-gpu-computing-tutorials-97719.html

Parallel computing videos:
https://www.mathworks.com/videos/search.html?q=&fq[]=product:DM&page=1

Parallel computing webinars:
https://www.mathworks.com/videos/search.html?q=&fq[]=product:DM&fq[]=video-external-category:recwebinar&page=1

