# Data and Storage

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




## Directory Structure

To promote long term consistency, the S3DF directory structure provides immutable paths, independent from the underlying file system organization and technology:

* `/sdf`: Root mount point.  Not a file system (use local directory to help avoid I/O hangs).

* `/sdf/home/<u>/<username>`: Home directories.  Disk & inode quotas imposed for all users.

* `/sdf/sw/<package>/<version>`: For general purpose software not installed on each node, e.g., EPICS, matlab, matplotlib, GEANT4, etc.  Not meant for SW that is used by only one group.

* `/sdf/group/<organization>/<groupname>` or `/sdf/group/<groupname>`: For group/project specific software (e.g., lcls/psdm, ad/hla, etc.)

* `/sdf/data/<facility>/…`: For science data (as opposed to code, documents, etc), including raw, calibrated data, and results. Some examples:
  - LCLS experimental: `/sdf/data/lcls/<instrument>/<experiment>`
  - LCLS accelerator: `/sdf/data/lcls/accel/<bld|bsa|ca|...>`
  - FACET experimental: `/sdf/data/facet/<instrument>/<experiment>`
  - FACET accelerator: `/sdf/data/facet/accel/`
  - CryoEM: `/sdf/data/cryoem/<YYYYMM>/<experiment>`

* `/sdf/scratch/<facility>/…`: 3 months retention on a best effort basis (actual retention can be shorter or longer depending on actual usage)

### Notes:

- Everything under `/sdf/{home, sw, group}` will be backed-up. The backup mechanism will be the same for all folders: snapshots will be taken at regular intervals (e.g., a few times a day) and will be accessible by the users through the file system itself, with no intervention from the system administrators. A subset of the snapshots will be copied to tape at a lower rate (e.g., once a day).

- Home directories permissions will be delegated to each user. By default, home folders will not be readable. Everyone will be able to list `/sdf/home/<u>`.

- General purpose software will go under sw. We'll need to define what general purpose means - as SCS may end up supporting everything under sw, there may be some push back. Group specific software will go under `/sdf/group` and will be maintained by each group.

- Files/objects under `/sdf/data` will be archived according to a data retention policy defined by the facility. Facilities will be responsible for covering the media costs and overhead required by their policy. Dedicated scratch spaces will not be archived. Derived data (results) may be backed up, or archived, or somewhere in between - TBD.

- Some groups may decide to logically hold all their information under `/sdf/group/<groupname>`. Such a structure may be implemented by each group via symlinks. The actual mount points and relative backup and archive policies will be based on the structure shown above. 

- A subset of users in each group will be able to access the command line interface to HPSS for the purpose of archiving/restoring to/from tape. Differently from backup, which will be automatically performed by the storage team within SCS, archiving will be the responsibility of each group (POC within SCS is OK).




### Archive


### Managing Your Files

#### Navigating the Shared File Systems


#### Moving data around
Traditional secure copies (scp) will work and SDF is a secure [Globus](https://www.globus.org/how-it-works) endpoint. 

#### Help! I've lost some files! What can I do?
Some directories are periodically backed up. [Contact us](contact-us.md) to retrieve the last back up. 


## Data Management Policy

SLAC provides a means to storage, manage and share their data. The SDF is specifically tuned to provide a variety of storage technologies that enable researchers to conduct their research through the entire data lifecycle such that users and delegates are able to manage, protect and control their data.

### User Responsibilities


### Group Leader Responsibilities


## Data Retention Policies


## Data Confidentiality and Access Control



