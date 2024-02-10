!> **AS OF FRIDAY FEBRUARY 9TH 4:26PM PST:** Filesystems in S3DF mounted under `/sdf/data` are currently unavailable. We are troubleshooting a communication issue between the underlying NVMe and spinning disk subsystems. Please do not access pathnames under `/sdf/data`. Any type of job or task that attempts to access `/sdf/data` will fail. Existing data is safe and has not been lost. We will be posting periodic updates. Will post the next update tomorrow at 12:00PM PST. We are working hard to diagnose and fix the problem. Thanks for your patience.

Welcome to the SLAC Shared Scientific Data Facility (S3DF). The S3DF
is a compute, storage and network architecture designed to support
massive scale analytics required by all SLAC experimental facilities
and programs, including LCLS/LCLS-II, UED, cryo-EM, the accelerator,
and the Rubin observatory. The S3DF infrastructure is optimized for
data analytics and is characterized by large, massive throughput, high
concurrency storage systems.

## Quick Reference

| Access 	| Address | 
| :--- | :--- |
| SSH 	|  s3dflogin.slac.stanford.edu|
| NoMachine |  s3dfnx.slac.stanford.edu|
| OnDemand 	| [https://s3df.slac.stanford.edu/ondemand](/ondemand ':ignore') |	
| Globus Endpoint 	| slac_globus5_test|
| Documentation | [This!](/ ':ignore')|
| Help (slack channel) | [slac.slack.com#comp-sdf](https://app.slack.com/client/T1X4J8FJ8/C01965DTG91)|
| Help (email) | s3df-help@slac.stanford.edu|
| Banking & Accounting | https://s3df.slac.stanford.edu/coact|
| S3DF Dashboard & Monitoring | https://grafana.slac.stanford.edu|


![SRCF-II](assets/srcf-ii.png)
