
# S3DF FAQ :faq



## May I Contribute to the S3DF Documentation? :id=docsify

Please feel free to send us suggestions and modifications to this documentation! The content is hosted on [github](https://github.com/slaclab/sdf-docs) and as long as you have a github account, you can send us [pull request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request) where we can review your changes and merge them into this site.

?> __TIP__ At the top of each page, there is also a 'Edit Page' button that will send you directly to the page on github to be edited

The documentation uses [docsify.js](https://docsify.js.org/) to render [markdown](https://www.markdownguide.org/) documents into a static website using only javascript. Whilst not necessary to submit changes, you may want to view the webpage locally for development purposes. Once you have cloned this document repository, you can start a local web server to preview all changes. Please see [docsify](https://docsify.js.org/#/quickstart) for more details.



## Am I entitled to use the S3DF?

 If your computing tasks are associated with SLAC research or engineering, you should use the S3DF. It is fully supported by the lab. The first step is to identify the context of your work by selecting an S3DF ‘Facility’ - we use this term to describe an experiment, project or facility that has a user group and resource requirements. Every S3DF user is a member of a facility. Every facility has czars that act as gatekeepers and are authorized to manage any resources belonging to a facility.


## What is Coact?

[Coact](http://coact.slac.stanford.edu) is our portal for managing authorizations and tracking resource utilization. The czars control who gets access and how facility resources are distributed. Every new S3DF user must first login to coact (using their Unix account) and request S3DF access by specifying a facility. The facility czar must then approve the request before the user can login.

## What is the difference between Bastion hosts vs Interactive hosts

SSH login access to S3DF is via the ```s3dflogin.slac.stanford.edu``` pool. These systems are designed as externally-facing “bastion” login nodes. They mount only user home directories and run a limited number of commands. Once users have gained access via the login pool, they should then SSH into an [interactive pool](interactive-compute). Several facilities have their own dedicated interactive hosts, but all users can access the ‘iana’ pool. Use the interactive systems for interactive applications, compilation, slurm cluster commands, etc.

## Primary vs Legacy Filesystems

S3DF primary filesystems are mounted under ```/sdf``` on all S3DF interactive and compute hosts. This includes S3DF home directories, per-facility “group” space and multi-petabyte storage for the bulk of science data. These primary filesystems will eventually replace all legacy SLAC storage. The DDN Lustre storage from SDF “1.0” is also mounted across all S3DF interactive and compute hosts under ```/fs/ddn/sdf```. Several facilities invested in 5 years of DDN storage, and we will honor this investment. Legacy filesystems (GPFS, NFS) have already surpassed the 5 year lifecycle. To help migrate data off legacy storage, we have mounted a select number of GPFS filesystems on the interactive nodes. AFS is also mounted read-only on interactive nodes. See [data and storage](data-and-storage.md).


## How do I check current status of storage quotas? :id=storagequota

You might want to know how much of your quota is used; reaching the
limit might be the cause of error messages whose reason is not
obvious. To do so for your home, simply type `df -h ~/` in a terminal
window. More in general type `df -h <folder>` to determine the quota
for any folder.


## How do I access AFS/GPFS/Lustre? :id=legacyfs

The SLAC-wide legacy file systems AFS, GPFS, and SDF Lustre will be
mounted read-only, and only on the interactive pools, to enable the
migration of legacy data to S3DF storage:

- AFS: For now, AFS is available read-only at the standard /afs path. Once AFS is retired, the current plan is to make a portion of it available read-only at the /fs/afs path.

- GPFS: `/fs/gpfs` The current plan is to use NFS as the access
  method.  Affected systems: ACD, ATLAS, CryoEM, DES + DarkSky, Fermi,
  KIPAC, LSSTcam, MCC/EED, StaaS.

- Lustre: `/fs/ddn`  Although Lustre is currently operating in
  read-write mode, groups will likely benefit from moving data to S3DF
  storage as it becomes available to them.


## How are my files backed up? :id=backup

Current backup/archive situation

| File system | Snapshot | Tape backup (TSM) | Tape archive (HPSS) | Done by | Paid by |
| --- | --- | --- | --- | --- | --- |
| sdfhome | To flash | Yes | No | S3DF | SLAC |
| sdfscratch | No | No | No | - | - |
| sdfk8s | To flash | No | No | S3DF | SLAC |
| sdfdata | To tiering layer | On demand | Active, from files | S3DF | SLAC |
| sdfdata:/u | To tiering layer | On demand | No | S3DF | Group |
| S3 direct | No | No | No | No | No | 


Target backup/archive strategy

| File system | Snapshot | Tape backup (TSM-like) | Tape archive (HPSS-like) | Done by | Paid by |
| --- | --- | --- | --- | --- | --- |
| sdfhome | To S3 bucket | No | From S3 snapshots | S3DF | SLAC | 
| sdfscratch | No | No | No | - | - |
| sdfk8s | To S3 bucket | No | From S3 snapshots | S3DF | SLAC |
| sdfdata | To S3 bucket | No | Active, from files | Group | Group |
| sdfdata:/u | To S3 bucket | No | From S3 snapshots | S3DF | Group |
| S3 direct | No | No | From S3 | Group | Group | 

?> sdfdata:/u indicates folders that logically belong to sdfgroup but
are too large to be paid for by SLAC.

?> The target backup strategy is aspirational, we need to find the
right tools to copy from S3 to tape.

## What is the future of AFS?

AFS will be retired along with other RHEL6 infrastructure and other legacy platforms. Our goal is for S3DF native storage to be securely exported to test stands, control rooms, lab workstations, etc via authenticated NFS v4 where required. We want to migrate all user and group files off AFS by September 30th 2024. If you cannot meet this migration target, please contact s3df-help@slac.stanford.edu so we can discuss your requirement and seek an extension. Before we shutdown AFS, we will create a final copy of the entire ```/afs/slac``` directory tree and make select portions of it available read-only for a limited period of time. This will allow groups to copy data they may have forgotten to migrate earlier. However, we will no longer be able to perform tape restore requests (for files that were previously deleted) once AFS is shutdown; those requests must be made before AFS retirement.

## Who pays for S3DF Storage?

There is plenty of 'free' (lab-funded) S3DF space to cover AFS migration.

All S3DF users get a home directory with a 30GB quota. There is also S3DF group space ```/sdf/group``` with per-facility quotas. The group space is intended for that group's project-specific software, configuration files, etc. Typically, each facility has an ```/sdf/group``` quota of 10TB. Home directories and group space are stored on flash (NVMe SSDs) and are automatically backed up to tape daily. We also provided shared scratch space for free (limited lifetime and not backed up) with a quota of 100GB. The bulk of science data (petabyte scale) is funded directly by the facilities and located in ```/sdf/data```. We have a business model and the facility czars purchase their storage hardware and backups for science data.

## How to copy from AFS to S3DF

AFS is mounted read-only ```/afs/slac``` on the 'iana' interactive nodes. Command-line utilities like rsync and cp can be used to copy files and directories from AFS to S3DF. 

Login to S3DF and then login to the iana interactive pool:
```
ssh s3dflogin.slac.stanford.edu
ssh iana
```
Obtain an AFS Token. The kinit command will prompt you for your Unix password:
```
/usr/bin/kinit
/usr/bin/aklog
```
Verify the AFS Token:
```
/usr/bin/tokens
```
Create a destination subdirectory; we're using "afs" for this example and removing access permissions for everyone except the directory owner. We do not recommand that you copy the contents of your AFS home directory straight into your S3DF home directory since 1) some file names will conflict and 2) it will clutter your S3DF home directory with your old AFS files.
```
mkdir $HOME/afs
chmod og-rwx $HOME/afs
```
Use the rsync or cp command to transfer files; cp might be a little faster, but rsync is known to be quite robust. The examples below will copy your "workdir" subdirectory into the newly created afs subdirectory.  The -v option is for verbose output, which you can omit if you prefer. NOTE: if you do not know your /afs/slac home directory path, you can try the following command to find it: ls -ld /afs/slac/u/??/${USER}

rsync option: 
```
rsync -HaxSuv /afs/slac/u/<XX>/<userid>/workdir $HOME/afs
```
cp option:
```
cp -auv /afs/slac/u/<XX>/<userid>/workdir $HOME/afs
```
If the command gets interrupted part way through, you can run it again. The files that were already transferred shouldn't get copied again.

*Important: AFS ACLs (Access Control Lists) are not copied during this process! Be sure to protect the copied data with proper Unix permissions after the transfer!*

## Transferring files and data

S3DF has inherited the POSIX groups that are used for legacy storage permissions. This means S3DF users should have consistent file ownership and permissions, allowing them to copy over existing files from AFS, legacy Unix, and DDN Lustre storage to S3DF primary filesystems. If you are unable to copy your groups’ data because you lack the permissions, please contact s3df-help@slac.stanford.edu for assistance. [For external transfers over the internet, we provide a pool of Data Transfer Nodes](data-transfer.md#data-transfer).


## Compiling code for S3DF

The standard Linux distro for all S3DF machines is RHEL 8.6. We recommend you port your codes and applications to RHEL 8. You can compile on our interactive nodes or submit build jobs to our clusters. We are also looking at incorporating Rocky Linux 9 (a RHEL clone) into our environment.

## Where to find libraries and packages

We are keeping the quantity of locally installed packages (on a host’s local disk filesystem) to a minimum. Contact us if you are missing “core” HPC packages and we’ll consider installing RPMs from the default yum repos (Examples: BLAS, LAPACK, etc). A more flexible method of distributing software is to install it on our S3DF filesystems that are mounted on all hosts. We can install general packages under ```/sdf/sw``` . Facilities can keep their specific packages under ```/sdf/group/<facility>/```

## Exporting your software environment

S3DF uses the popular lmod module system for configuring shell environments. We can update modulefile search paths to include subdirectories under ```/sdf/sw/``` or ```/sdf/group/<facility>/``` . 

## Web applications and HTML content

We are hosting dynamic web applications and static content. Please see [service-compute.md#s3df-dynamic-sites-and-web-applications] . We are also discussing how to preserve existing AFS public_html directories that are accessed world-wide via ```https://www.slac.stanford.edu/~<username>``` . 

## Cron Jobs

We now have an [S3DF Cron Service](service-compute.md#?s3df-cron-tasks)

## Graphics and remote visualization

NoMachine is the recommended (supported) interface for displaying and interacting with graphics-based programs running on S3DF. The NoMachine "NX" protocol offers improved performance compared to X11 over SSH encryption.  It is located at s3dfnx.slac.stanford.edu.
