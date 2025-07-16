# Storage

## Directory Structure

To promote long term consistency, the S3DF directory structure provides immutable paths, independent from the underlying file system organization and technology. This means the /sdf paths below will remain the same even as upgrades happen in the future.

* `/sdf`: Root mount point.

* `/sdf/home/<u>/<username>`: Home directories.  Quotas are enabled for all users.

* `/sdf/sw/<package>/<version>`: For general purpose software not installed on each node, e.g., EPICS, Matlab, matplotlib, GEANT4, etc.  Not meant for software that is used by only one group.

* `/sdf/group/<organization>/<groupname>` or `/sdf/group/<groupname>`: For group/project specific software (e.g., lcls/psdm, ad/hla, etc). Quotas are enabled for all groups.

* `/sdf/data/<facility>/…`: For science data (as opposed to code, documents, etc), including raw, calibrated data, and results. Quotas are enabled for all data directories. Some examples:
  - LCLS experimental: `/sdf/data/lcls/<instrument>/<experiment>`
  - LCLS accelerator: `/sdf/data/lcls/accel/<bld|bsa|ca|...>`
  - FACET experimental: `/sdf/data/facet/<instrument>/<experiment>`
  - FACET accelerator: `/sdf/data/facet/accel/`
  - CryoEM: `/sdf/data/cryoem/<YYYYMM>/<experiment>`

* `/sdf/scratch/<facility>/…`: 3 months retention on a best effort basis. Actual retention can be shorter or longer depending on space availability. Quotas are enabled for all scratch directories. NOTE: as of June 2025, the auto-purge policy is not in effect, but could be enabled at any time. Protect your data accordingly. 

?> Access to AFS, GPFS, and SDF Lustre from S3DF is described in this
[reference section on legacy file systems](reference.md#legacyfs).

## Quotas

Most directories have some kind of quota assigned to them. Use the `df <directory>` command to check a directory quota. The current default quota limits are:

* `/sdf/home`: 30 GB (provided to users by SLAC)
* `/sdf/group`: 10 TB (provided to groups or facilities by SLAC)
* `/sdf/sw`: varies (specific software repositories only, provided by SLAC)
* `/sdf/data`: varies according to how much a group or facility purchased
* `/sdf/scratch/users`: 100 GB (short term space, provided by SLAC)
* `/sdf/scratch/<group>`: varies according to how much a group or facility purchased; short term space, up to 5 TB provided by SLAC

## Policies

- Home directory permissions will be delegated to each user. By default, home folders will be readable by everyone, though you can change that by changing UNIX permissions on one or more of your folders. Everyone will be able to list `/sdf/home/<u>`.

- General purpose software will go under sw. Group specific software will go under `/sdf/group` and will be maintained by each group.

- Some groups may decide to logically hold all their information under `/sdf/group/<groupname>`. Such a structure may be implemented by each group via symlinks. The actual mount points and relative backup and archive policies will be based on the structure shown above. 

?> __TODO__ Desktop/endpoint access to S3DF file systems will likely be via authenticated NFS v4.  This is currently a topic of investigation as we wait for an updated WekaFS release.


## Backup and Archiving

- Everything under `/sdf/{home, sw, group}` will be backed up. We currently use snapshots taken at regular intervals (e.g., a few times a day) that users can access with no intervention from system administrators. A subset of the snapshots will be copied to tape at a lower rate (e.g., once a day). Snapshots for\
`/sdf/{home, sw, group}/<folder>`\
can be found at\
`/sdf/{home, sw, group}/.snapshots/<GMT_time>/<folder>`

- Files/objects under `/sdf/data` will be backed up or archived according to a data retention policy defined by the facility. Facilities will be responsible for covering the media costs and overhead required by their policy. Similar to the /sdf/home area, you can also check in /sdf/data/\<facility\>/.snapshots to see if snapshots are enabled for self-service restores.

- The scratch spaces under `/sdf/scratch` and all directories named "nobackup" (located *anywhere* in an /sdf path) will not be backed up or archived. Please use as many "nobackup" subdirectory locations as required for any files that do not need backup.  That can save significant tape and processing resources.

- A subset of users in some groups will be able to access the command line interface to HPSS for the purpose of archiving/retrieving data to/from tape. Unlike backups, which will be automatically performed by the storage team within SCS, archiving will be the responsibility of each group (contact SCS for assistance).

?> The current and target backup and archiving policies are summarized in this [reference section on data backup](reference.md#backup).

## Change to AFS Tape Backup Retention Policy
March 31, 2025

Summary: due to the upcoming retirement of a legacy tape library, the tape backup retention policy for the legacy AFS file system will be reduced from one year to one month (31 days), effective May 14, 2025 (the deadline date). This policy change means any request to restore accidentally deleted files must be created within one month (rather than one year) of the deletion event. In addition, if a user deleted an AFS file more than one month prior to the deadline date and needs it restored, they have until the deadline date to create a restore request via email to s3df-help@slac.stanford.edu.

Details: the AFS file system used for legacy Unix home directory and group file storage originally started with a one-year tape backup retention policy. This meant that the tape backup system used to store backup copies of files had the ability to go back approximately one year and restore files that were accidentally deleted.

The legacy AFS file system will be retired before the end of 2025. Since a restore request for an AFS file requires the AFS file system itself to be online, the current retention policy would require the AFS file system to remain running for one year beyond its public retirement date just to satisfy restore requests. Since that will not be possible, the tape backup retention policy for legacy AFS files is being reduced from one year to one month (defined as 31 days) effective May 14, 2025 (the deadline date).

This policy change means any request to restore accidentally deleted files must be created within one month (rather than one year) of the deletion event. In addition, if a user deleted an AFS file more than one month prior to the deadline date and needs it restored, they have until the deadline date to create a restore request via email to s3df-help@slac.stanford.edu. After the deadline date, the backup system will be able to restore an AFS file only if it was deleted within the last one month.
