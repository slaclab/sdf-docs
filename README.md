Welcome to the SLAC Shared Scientific Data Facility (S3DF). The S3DF
is a compute, storage and network architecture designed to support
massive scale analytics required by all SLAC experimental facilities
and programs, including LCLS/LCLS-II, UED, cryo-EM, the accelerator,
and the Rubin observatory. The S3DF infrastructure is optimized for
data analytics and is characterized by large, massive throughput, high
concurrency storage systems.

****Scheduled Maintenance Notice: Slurm Upgrade on December 3rd
On Tuesday December 3rd between 13:00 and 14:00 PDT, we will perform a mandatory upgrade of the slurm controller, the database, and the client components on all batch nodes, kubernetes nodes, and interactive nodes. After the upgrade, all slurm commands should continue to run as expected. We shall be introducing support for pmix with this release, but generally this should be considered a patch release.
Impact on Users: All job submissions (sbatch/srun/squeue) and slurm database queries (sacct) /during/ the upgrade window will fail. Any jobs that are running before the upgrade window will continue to run. Completed jobs during the window will be accounted for after the system is back up.
We recommend planning your work accordingly to minimize disruption. If you have any questions or concerns, please contact s3df-help@slac.stanford.edu.****


## Quick Reference

| Access 	| Address | 
| :--- | :--- |
| SSH 	|  s3dflogin.slac.stanford.edu|
| NoMachine |  s3dfnx.slac.stanford.edu|
| OnDemand 	| [https://s3df.slac.stanford.edu/ondemand](/ondemand ':ignore') |	
| Globus Endpoint 	| slac#s3df_globus5|
| Documentation | [This!](/ ':ignore')|
| Help (slack channel) | [slac.slack.com#comp-sdf](https://app.slack.com/client/T1X4J8FJ8/C01965DTG91)|
| Help (email) | s3df-help@slac.stanford.edu|
| Banking & Accounting | https://s3df.slac.stanford.edu/coact|
| S3DF Dashboard & Monitoring | https://grafana.slac.stanford.edu|


![SRCF-II](assets/srcf-ii.png)
