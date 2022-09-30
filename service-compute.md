# Service Compute

[Contact us](contact-us.md) if you need resources for running
long-lived jobs, including dynamic websites, real-time and fast
feedback systems.

## S3DF Supported Sites

S3DF is currently supporting dynamic sites for several groups,
programs, and experiments. See the currently supported sites in the
table below.

| Access 	| Address | 
| :--- | :--- |
| Rubin RSP | https://usdf-rsp.slac.stanford.edu|
| LCLS | https://pswww.slac.stanford.edu|
| SuperCDMS | https://supercdms-dev.slac.stanford.edu|
| cryo-EM DAQ | https://cryoem-daq.slac.stanford.edu|
| cryo-EM Elog | https://cryoem-logbook.slac.stanford.edu|
| ARD Lume Project | https://ard-modeling-service.slac.stanford.edu|


## S3DF Public Access to User and Group Space 

S3DF can make static content from specific folders publicly available
through HTTP. If you need this service, send a request to
s3df-help. If you are the PoC of an S3DF facility, you may request
this service for your organization as a whole. See the table below for
the naming convention of how these user and group spaces will appear
on the S3DF file system and on the web. Any file or directory that you
want to make accessible via HTTP, need to be copied to the public_html
folder, links to other file system will not resolve. Note: eventually,
requests for these links will be managed via
[coact](https://s3df.slac.stanford.edu/coact).

| S3DF Folder | Public HTTP Address | 
| :--- | :--- |
| `/sdf/home/<u>/<username>/public_html` | https://s3df.slac.stanford.edu/people/&lt;username&gt;|
| `/sdf/data/<groupname>/public_html` | https://s3df.slac.stanford.edu/data/&lt;groupname&gt; |

