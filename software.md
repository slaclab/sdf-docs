# Software


## System Software

### Modules

SDF uses the module system. Currently installed modules can be viewed
with this command: `module avail`


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

[Contact us](contact-us.md) if you would like something installed
system wide.

### Singularity

For a detailed explanation of how to use Singularity on SDF, you can go through Yee-Ting Li's presentation [here](https://confluence.slac.stanford.edu/display/AI/AI+Seminar#AISeminar-Containers!Containers!Containers!) where you can find both the slides and the zoom recording.

#### Prerequisite

As pulling and building a new image can use quite a lot of disk space, we recommend that you set the appropriate cache paths for singularity to not use your $HOME directory. Therefore, before pulling or building an image, define the following environment variables:

```bash
export DIR=/scratch/${USER}/.singularity
mkdir $DIR -p
export SINGULARITY_LOCALCACHEDIR=$DIR
export SINGULARITY_CACHEDIR=$DIR
export SINGULARITY_TMPDIR=$DIR
```

#### Pulling images

To pull an image from DockerHub, do:
```bash
singularity pull docker://<user or organization>/<repository>:<tag>
```


### GCC Compiler

We offer various of GCC through (Redhat Software Collections](https://developers.redhat.com/products/softwarecollections/overview). These are wrapped up in [Environment Modules](#modulefiles) and are available with a `module load devtoolset/<version>`.

We also provide symlinks to the appropriate GCC version to the above `devtoolset` packages with `module load gcc/<version>`.


### Jupyter

We provide tunnel-less access to jupyter instances running on SDF via an easy to use web portal where you can 'bring-your-own' jupyter environments. See [Interactive Jupyter](interactive-compute.md#jupyter) for more information.

### MatLab

This ection describes how to run Matab in the S3DF Parallel Computing
environment.

#### Set up your matlab configuration

The first step is to set up matlab for your account.  These steps will
create a .matlab directory under your account with our site's configuration.  You only need to do this once per version of MATLAB.
```
ssh sdf-login
module load matlab
matlab
configCluster
exit
```

#### Submitting slurm jobs that run MATLAB

Slurm batch submissions of Matlab actually start up 2 jobs.  The
initial job is just to bring up matlab which, once successful, submits
a second job which runs your matlab code.

If you do not have access to a priority partition or you don't specify
a partition, your jobs will run in shared.  If you do have access and
want to run your jobs in a priority partition then you need to specify
the partition in both the sbatch script which launches matlab and as a
matlab setting in the matlab job.  You can set the partition for the
matlab job either in the matlab job itself which you will then need to
do everytime you submit.  For example, if you have access to the
spearx partition, your matlab code would begin:
```
c=parcluster;
c.AdditionalProperties.QueueName='spearx';
p=c.parpool(200);
```

or you can save the partition to your matlab
profile like so:
```
module load matlab
matlab
c=parcluster
c.AdditionalProperties.QueueName='spearx'
c.saveProfile
```
and then you won't need to specify it in any future matlab scripts.

You may need to increase the ulimit for processes in your .bashrc
depending on the size of the parpool you need.  The default is 4096
and too small for say a parpool of 100.  Include something like

ulimit -u 19200


#### Example

Following are an example sbatch and a test.m matlab file which can be used to test after you have
followed the steps to set up your environment.

Create the matlab job test.m:
```
c=parcluster;
p=c.parpool(100);
tic
n = 200;
A = 500;
a = zeros(1,n);
parfor i = 1:n
    a(i) = max(abs(eig(rand(A))));
end
rtime = toc;
fileID = fopen('readtime_out.txt','w');
fprintf(fileID,'%f',rtime);
fclose(fileID);
p.delete
```
Create the file testrun.sbatch and modify the "matlab -batch" line to
add the path to the directory containing your test.m file.  It is invoked
as just "test" without the ".m".  

```
#!/bin/sh
#SBATCH --partition=spearx
#SBATCH --job-name=test
#SBATCH --output=output-%j.txt
#SBATCH --error=error-%j.txt
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=2
#SBATCH --mem-per-cpu=4g
#SBATCH --time=5:00
source /usr/share/Modules/init/sh
module load matlab
matlab -batch "addpath ('/sdf/home/v/vanilla/matlab');test"
```
Note that this submission script only
needs to request enough resources to launch matlab.  Matlab will figure out
how many cores it needs from the parpool request, or you can give matlab
more specifics about nodes and processes as described in the next section.

Run the job:
```
[vanilla@sdf-login02]~% sbatch testrun.sbatch
Submitted batch job 722162
[vanilla@sdf-login02]~% 
[vanilla@sdf-login02]~% 
[vanilla@sdf-login02]~% 
[vanilla@sdf-login02]~% 
[vanilla@sdf-login02]~% squeue | grep vanilla
            722180    spearx     Job1  vanilla  R       0:14      2 rome[0244,0251] 
            722179    spearx     test  vanilla  R       0:42      1 rome0133 
```
In this example, jobid 722179 is the ntasks=1 job that starts up matlab and
722180 is the job that actually runs test.m.  You should end up with two
files in the location pointed to by addpath, the slurm output-jobid.txt file
with the details about the matlab submission, and the output file specified
in the matlab job that has the results of your computation:
```
-rw-r--r--  1 vanilla sf     591 Jun 29 11:27 output-722179.txt
-rw-r--r--  1 vanilla sf       8 Jun 29 11:27 readtime_out.txt
```
[vanilla@sdf-login02]~% cat output-722179.txt 
```
			Non-Degree Granting Education License -- for use at non-degree granting, nonprofit,
			educational organizations only.  Not for government, commercial, or other organizational use.

Starting parallel pool (parpool) using the 'sdf R2020b' profile ...

additionalSubmitArgs =

    '--ntasks=100 --cpus-per-task=1 --ntasks-per-core=1 -p spearx'

Connected to the parallel pool (number of workers: 100).
Parallel pool using the 'sdf R2020b' profile is shutting down.


[root@sdf-login01 ~vanilla]# cat readtime_out.txt
4.291791
```

#### Additional Parallel Server Job Considerations

You can manage the number of nodes when running your parallel server
jobs.  Our rome nodes have 128 cores.  If you don't tell matlab to use
some certain number of nodes it will spread the job out and use
whatever cores it finds available.  It may be preferrable to restrict
matlab jobs to fewer or even exclusive nodes and avoid any contention
that may come from other jobs.   

To restrict your matlab job which is requesting a parpool of 230 to 2
nodes, you would add this to your matlab job:

```
c.AdditionalProperties.NumNodes=2;
c.AdditionalProperties.ProcsPerNode = 116;
```
This tells matlab to run on 2 nodes, and the procspernode should be
the amount of the parpool, in this case 230, divided by the number of
nodes, and then add one, which in this case would be 230/2 and add one
115+1=116.

If you are running in a priority partition, and you want your jobs to
run exclusvely even if your parpool doesn't require all the cores, you
can add:

c.AdditionalProperties.AdditionalSubmitArgs = '--exclusive';

to your matlab job, but still keep the NumNodes and ProcsPerNode lines.



#### Links to more information about MATLAB

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


## User Software

Non-general purpose software should be installed locally by you under
$HOME or project directories. The latter is preferred as your home
space is limited and the project space offers better visibility to a
larger audience.

### Conda

It is not recommended to store your conda environments in your $HOME due to 1) quota limits, and 2) an inability to share conda environments across groups. We generally recommend that you install software into your $GROUP space (eg `/sdf/group/<group_name>/sw` - please see [$GROUP storage](getting-started.md#group)).

#### Install Miniconda

Download the latest version of Miniconda from the [conda](https://docs.conda.io/en/latest/miniconda.html) website and follow the [Instructions](https://conda.io/projects/conda/en/latest/user-guide/install/linux.html#installing-on-linux). Change the installion `prefix` to point to an appropriate [$GROUP directory](getting-started.md#group):

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/Miniconda3-latest-Linux-x86_64.sh
bash /tmp/Miniconda3-latest-Linux-x86_64.sh -p /sdf/group/<group_name>/sw/conda/
```

Replacing `<group_name>` appropriately.

We can also modify our [~/.condarc](https://conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html) file as follows;

```bash
channels:
  - defaults
  - anaconda
  - conda-forge
  - pytorch
envs_dirs:
  - /sdf/group/<group_name/sw/conda/envs
pkgs_dirs:
  - /sdf/group/<group_name/sw/conda/pkgs
auto_activate_base: false
```

#### Create a conda environment

Conda environments are a nice way of switching between different software versions/packages without multiple conda installs.

There is no unique way to create a conda environment, we illustrate here how to do so from a .yaml file (see the conda [documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file) for more details).

In order to create an environment called `mytest` with `python=3.6` and `numpy` and `pandas` in it, create `mytest-environment.yaml`:
```bash
name: mytest
dependencies:
  - python=3.6
  - numpy
  - pandas
```

Then run the following command: `conda env create -f mytest-environment.yaml`.

If successful, you should see `mytest` when listing your environments: `conda env list`. 

You can now activate your environment and use it: `conda activate test`. To double-check that you have the right packages, you can type `conda list` once in the environment and check that you see `numpy` and `pandas`.
