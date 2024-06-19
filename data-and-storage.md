# Storage

## Directory Structure

To promote long term consistency, the S3DF directory structure provides immutable paths, independent from the underlying file system organization and technology:

* `/sdf`: Root mount point.

* `/sdf/home/<u>/<username>`: Home directories.  Space quotas imposed for all users.

* `/sdf/sw/<package>/<version>`: For general purpose software not installed on each node, e.g., EPICS, Matlab, matplotlib, GEANT4, etc.  Not meant for software that is used by only one group.

* `/sdf/group/<organization>/<groupname>` or `/sdf/group/<groupname>`: For group/project specific software (e.g., lcls/psdm, ad/hla, etc.)

* `/sdf/data/<facility>/…`: For science data (as opposed to code, documents, etc), including raw, calibrated data, and results. Some examples:
  - LCLS experimental: `/sdf/data/lcls/<instrument>/<experiment>`
  - LCLS accelerator: `/sdf/data/lcls/accel/<bld|bsa|ca|...>`
  - FACET experimental: `/sdf/data/facet/<instrument>/<experiment>`
  - FACET accelerator: `/sdf/data/facet/accel/`
  - CryoEM: `/sdf/data/cryoem/<YYYYMM>/<experiment>`

* `/sdf/scratch/<facility>/…`: 3 months retention on a best effort basis (actual retention can be shorter or longer depending on actual usage)

?> Access to AFS, GPFS, and SDF Lustre from S3DF is described in this
[reference section on legacy file systems](reference.md#legacyfs).

## Policies

- Home directory permissions will be delegated to each user. By default, home folders will be readable by everyone, though you can change that by changing UNIX permissions on one or more of your folders. Everyone will be able to list `/sdf/home/<u>`.

- General purpose software will go under /sdf/sw. Group specific software can go under `/sdf/group/<groupname>` and will be maintained by each group.

- Some groups may decide to logically hold all their information under `/sdf/group/<groupname>`. Such a structure may be implemented by each group via symlinks to the actual file locations. However, the mount points and relative backup and archive policies will be based on the structure shown above. 

?> __TODO__ Desktop/endpoint access to S3DF file systems will likely be implemented via authenticated NFS v4.  This is currently a topic of investigation as we wait for an updated WekaFS release.

## Disk Quotas

Use df -h for basic quota information. Examples:
-  `df -h ${HOME}` (`${HOME}` is a shell variable representing your /sdf/home directory)
-  `df -h ${SCRATCH}` (`${SCRATCH}` is a shell variable representing your /sdf/scratch/users directory)
-  `df -h .` (the dot represents the current directory)

Default Quotas
-  /sdf/home = 25 GB per user (NOTE: as of 6/17/2024, df still reports 30GB instead of 25GB for the default quota. We are working on a fix for this.)
-  /sdf/scratch/users = 100 GB per user
-  /sdf/group = 10TB per group. It is possible to set subdirectory quotas within a group's directory. Please contact s3df-help@slac.stanford.edu since it currently requires root privileges to implement. 

## Backup and Archiving

- Everything under `/sdf/home, /sdf/sw, and /sdf/group` will be backed up. We currently provide snapshots taken at regular intervals so you can restore your own files with no intervention from system administrators. One snapshot will be copied to tape each night. Snapshots for /sdf/home, /sdf/sw, and /sdf/group subdirectories can be found at the parent directory level. For example, snapshots for /sdf/home are located at 
`/sdf/home/.snapshots/<gmttime>/<subdirectory>`. Select the GMT time period of your choice and then continue down the path to your home directory so you can restore your file. Note that the .snapshots directory is hidden and will not show up in an ls command.

- Files under `/sdf/data` will be backed up or archived to tape according to a data retention policy defined by the facility. Facilities will be responsible for covering the media costs and overhead required by their policy. Derived data (results) may be backed up, archived, or somewhere in between. Please contact s3df-help@slac.stanford.edu for assistance with /sdf/data backups or archives.

- All scratch areas under `/sdf/scratch` will not be backed up nor archived.

- Any directories named "nobackup" (located *anywhere* in _any_ /sdf path) will not be backed up nor archived. Please use as many "nobackup" subdirectory locations as required for any files that do not need backup.  That can save significant tape and processing resources.

- A subset of users in each group will be able to access the command line interface to HPSS for the purpose of archiving/retrieving data to/from tape. Unlike backups, which will be automatically performed by the storage team within SCS, archiving will be the responsibility of each group (contact SCS for assistance).


?> The current and target backup and archiving policies are summarized in this [reference section on data backup](reference.md#backup).

