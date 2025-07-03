# Status & Outages

## Outages

### Current

### Upcoming

The Stanford Facilities team need to conduct an evaluation of the SRCF datacenter transformers which feed the compute portions of SDFData and the S3DF Kubernetes resources.
This work will require a **full outage of all S3DF services on July 7th 2025 from 4AM to 8PM PDT.**
We will also use this maintenance opportunity to implement:

#### S3DF New Core Network

1.6 Tbps aggregate to the SLAC backbone

Up to 800 Gbps to each S3DF Top-Of-Rack switch

#### Storage Upgrades

NFS improvements in terms of performance and reliability

New metrics for better observability

Better memory allocation

#### All S3DF storage, compute, interactive and hosted applications will be unavailable for the duration of the outage. This includes:

Login Bastions

OnDemand/Jupyter

Interactive pools

Kubernetes and VMware services and applications

DTNs

All filesystems and Object Storage: Home, Data, Scratch, k8s, S3

#### All Compute CPU and GPU clusters will be unavailable. The slurm batch scheduler will prevent scheduling of jobs that conflict with the July 7th 4AM to 8PM outage window.

#### For maintainers/developers of S3DF Kubernetes workloads:

As with previous planned maintenance outages, we plan to pause Kubernetes vCluster workloads in S3DF prior to gracefully powering down the worker nodes. This should preserve state and once the Kubernetes worker nodes are back online, we will resume the workloads and services should come back online. Please verify that your workloads are operational once the outage window is complete.


Leading up to the outage, more details will shared on our website: https://s3df.slac.stanford.edu/#/changelog?id=outages. During the outage we will provide status updates on the progress on the Confluence page at: https://confluence.slac.stanford.edu/spaces/S3DFSTATUS/pages/479600957/S3DF-Status+Home and on the #comp-sdf Slack channel.
We are prioritizing this outage because transformer failures may result in unscheduled power outages for critical S3DF infrastructure. 

Thank you

S3DF Team


|When	|Duration | What	|
| --- | --- | --- |
| July 7th 2025 | 18 hrs (planned) | The Stanford Facilities team need to conduct an evaluation of the SRCF datacenter transformers. All S3DF services will be unavailable.
### Past

|When	|Duration | What	|
| --- | --- | --- |
| Feb 6th 2025 | 17 hrs (planned) | An 800A breaker on the M2 Mechanical Substation had to be replaced. The entire substation was powered down resulting in a significant loss of datacenter cooling.
|Dec 26 2024| 12 days (unplanned)|One of our core networking switches in the data center failed and had to be replaced. The fall-out from this impacted other systems and services on S3DF. Staff worked through the night on stabilization of the network devices and connections as well as recovery of the storage subsystem.|
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

