# Status & Outages

## Outages

### Current

### Upcoming
|When	|Duration | What	|
| --- | --- | --- |
| Dec 3 2024 | 1 hr (planned) | Mandatory upgrade of the slurm controller, the database, and the client components on all batch nodes, kubernetes nodes, and interactive nodes. Impact on Users: All job submissions (sbatch/srun/squeue) and slurm database queries (sacct) ***during*** the upgrade window will fail. Any jobs that are running before the upgrade window will continue to run. Completed jobs during the window will be accounted for after the system is back up. We recommend planning your work accordingly to minimize disruption. |

### Past

|When	|Duration | What	|
| --- | --- | --- |
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

