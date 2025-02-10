# Status & Outages

## Outages

### Current

### Upcoming

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

