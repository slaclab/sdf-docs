# Status & Outages

## Support during Winter Shutdown

S3DF will remain operational over the Winter shutdown (Dec 21st 2024 to Jan 5th 2025). Staff will be taking time off as per SLAC guidelines. S3DF resources will continue to be managed remotely if there are interruptions to operations. Response times for issues will vary, depending on the criticality of the issue as detailed below.

**Contacting S3DF staff for issues:**
Users should email s3df-help@slac.stanford.edu for ALL issues (critical and non-critical) providing full details of the problem (including what resources were being used, the impact and other information that may be useful in resolving the issue).
We will update the #comp-sdf Slack channel for critical issues as they are being worked on with status updates.
[This S3DF status web-page](https://s3df.slac.stanford.edu/#/changelog) will also have any updates on current issues.
If critical issues are not responded to within 2 hours of reporting the issue please contact your [Facility Czar](https://s3df.slac.stanford.edu/#/contact-us) for escalation.

**Critical issues** will be responded to as we become aware of them, except for the period of Dec 24-25 and Jan 31-1, which will be handled as soon as possible depending on staff availability.
* Critical issues are defined as full (a system-wide) outages that impact:
  * Access to S3DF resources including
    * All SSH logins
    * All IANA interactive resources
    * B50 compute resources(*)
      * Bullet Cluster
  * Access to all of the S3DF storage
    * Home directories
    * Group, Data and Scratch filesystems
    * B50 Lustre, GPFS and NFS storage(*)
  * Batch system access to S3DF Compute resources
  * S3DF Kubernetes vClusters
  * VMware clusters
    * S3DF virtual machines
    * B50 virtual machines(*)
* Critical issues for other SCS-managed systems and services for Experimental system support will be managed in conjunction with the experiment as appropriate. This includes
  * LCLS workflows
  * Rubin USDF resources
  * CryoEM workflows
  * Fermi workflows
(*) B50 resources are also dependent on SLAC-IT resources being available.

**Non-critical issues** will be responded to in the order they were received in the ticketing system when normal operations resume after the Winter Shutdown. Non-critical issues include:
  * Individual node-outages in the compute or interactive pool
  * Variable or unexpected performance issues for compute, storage or networking resources.
  * Batch job errors (that do not impact overall batch system scheduling)
  * Tape restores and data transfer issues

## Outages

### Current

**January 3rd 9:35am PST: Today the team is working to address issues on the internal S3DF network. As a result, all S3DF services remain DOWN. Our next update will be at 3pm PST today.**

### Upcoming

### Past

|When	|Duration | What	|
| --- | --- | --- |
|Dec 26 2024| 1 days (unplanned)|One of our core networking switches in the data center failed and had to be replaced. The fall-out from this impacted other systems and services on S3DF. Staff worked through the night on stabilization of the network devices and connections as well as recovery of the storage subsystem.|
|Dec 10 2024|(unplanned)|StaaS GPFS disk array outage (partial /gpfs/slac/staas/fs1 unavailability)|
| Dec 3 2024 | 1 hr (planned) | Mandatory upgrade of the slurm controller, the database, and the client components on all batch nodes, kubernetes nodes, and interactive nodes.
|Nov 18 2024|8 days (unplanned)|StaaS GPFS disk array outage (partial /gpfs/slac/staas/fs1 unavailability)|
|Oct 21 2024	|10 hrs (planned)| Upgrade to all S3DF Weka clusters. We do NOT anticipate service interruptions.
|Oct 3 2024	|1.5 hrs (unplanned)| Storage issue impacted home directory access and SSH logins
|Jul 10 2024	|4 days (planned)| Urgent electrical maintenance is required in SRCF datacenter
|Jun 26 2023	|5 days (planned)| Everything down due to power outage|
|Jan 15 2023 | 2 days (unplanned) | Fix: one weka server rebooted. Underlying issue under investigation. Symptom: sdfdata hanging on several nodes.|


## Monitoring

[Grafana](http://grafana.slac.stanford.edu)

[Ganglia](http://ganglia.slac.stanford.edu)

[Nagios](http://nagios.slac.stanford.edu)
<!---
[InfluxDb](http://influxdb.slac.stanford.edu)

[Prometheus](http://prometheus.slac.stanford.edu)
-->

## Roadmap :id=roadmap

Please see our [Technology Migration Timeline](https://docs.google.com/spreadsheets/d/1ZIZC7g9TghhBINfdOD2JoNQCR5SSlj6TQaPqWPxPzQA/edit?usp=sharing)
(Select the TIMELINE tab)

## Slurm Dashboard

[sdf-slurm-summary](https://grafana.slac.stanford.edu/d/YW8wlINMk/sdf-slurm-summary?orgId=1&refresh=60s&theme=light&kiosk ':include :type=iframe width=100% height=850px')

