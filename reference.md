# Reference

## Common Tools



## FAQ :faq

### How do I check current status of storage quotas? :id=storagequota

You might want to know how much of your quota is used; reaching the
limit might be the cause of error messages whose reason is not
obvious. To do so for your home, simply type `df -h ~/` in a terminal
window. More in general type `df -h <folder>` to determine the quota
for any folder.


### How do I access AFS/GPFS/Lustre? :id=legacyfs

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


### How are my files backed up? :id=backup

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


### May I Contribute to the S3DF Documentation? :id=docsify

Please feel free to send us suggestions and modifications to this documentation! The content is hosted on [github](https://github.com/slaclab/sdf-docs) and as long as you have a github account, you can send us [pull request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request) where we can review your changes and merge them into this site.

?> __TIP__ At the top of each page, there is also a 'Edit Page' button that will send you directly to the page on github to be edited

The documentation uses [docsify.js](https://docsify.js.org/) to render [markdown](https://www.markdownguide.org/) documents into a static website using only javascript. Whilst not necessary to submit changes, you may want to view the webpage locally for development purposes. Once you have cloned this document repository, you can start a local web server to preview all changes. Please see [docsify](https://docsify.js.org/#/quickstart) for more details.


## Presentations :Presentations

### Town Hall Meetings

#### Scientific Computing Town Hall 11/30/22

[Slide Deck](https://docs.google.com/presentation/d/1255ekxq8dscz7vvOAbgQ_tI4o13lOO-IMPMLm2A7gtg/edit?usp=sharing)

[Zoom meeting recording](https://stanford.zoom.us/rec/share/jLaKasYYRubW4qt9KOcOL0_-qLqwc7CpRUwVniYe2VCUsmkpL9lsagU1ILSg9Xtz.Bgy1KyefVpqW2zvg)

## S3DF Acknowledgement in Publications

Please acknowledge the role that the use of S3DF resources at SLAC had in your publications. We would also appreciate letting us know when your work is published or presented - this will allow us to highlight your work as well.

If your work uses resources that were made available as a result of explicit contributions from your project to S3DF, you may use the following suggested acknowledgement:

***"This work used the resources of the SLAC Shared Science Data Facility (S3DF) at SLAC National Accelerator Laboratory, funded by `[Your Funding Source]` under contract `[your contract number]`. S3DF is a shared High-Performance Computing facility that supports the scientific and data-intensive computing needs of all experimental facilities and programs of the SLAC National Accelerator Laboratory. SLAC is operated by Stanford University for the U.S. Department of Energy’s Office of Science."***

If your work used generally available resources on S3DF without explicit contributions to S3DF, you may use the following suggested acknowledgement:

***"This work used the resources of the SLAC Shared Science Data Facility (S3DF) at SLAC National Accelerator Laboratory. S3DF is a shared High-Performance Computing facility, operated by SLAC, that supports the scientific and data-intensive computing needs of all experimental facilities and programs of the SLAC National Accelerator Laboratory. SLAC is operated by Stanford University for the U.S. Department of Energy’s Office of Science."***

We appreciate your cooperation in the acknowledgment and publication notifications. This will help the S3DF in communicating  the importance of its role in science to SLAC and our funding agencies and help assure the continued availability of this valuable resource.
