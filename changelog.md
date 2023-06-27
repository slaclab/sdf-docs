# Status & Outages

## Outages

### Current

|When	|Duration | What	|
| --- | --- | --- |
|Jun 26 2023	|5 days (planned)| Everything down due to power outage|

### Upcoming

None

### Past

|When	|Duration | What	|
| --- | --- | --- |
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

|When	|What	|Notes|
| --- | --- | --- |
|Oct 2022	|Allow LCLS super users	||
|		|Deploy milano cluster	|11264 Milan cores|
|		|Deploy sdfdata	|POSIX (2.2 PB) and S3 (10 PB)|
|		|Link redundancy for all network devices	|200 Gb/s|
|Nov 2022	|Deploy coact for accounts & banking ||
|		|Device redundancy for all spine connectivity	|400 Gb/s|
|		|Mount LCLS fast-feedback on S3DF	||
|		|Open S3DF to LCLS users	||
|Jan 2023	|Open S3DF to all SLAC users	||
|Jun 2023	|SRCF-I and II power outage	|5-day shutdown starting on Jun 26th|
|Jul 2023	|Backup power available in SRCF-II	||
|		|Deploy pre-ops Rubin acquisitions in SRCF-II	||
|		|Export sdfhome and sdfdata to SLAC	|Via NFS v4 to provide AFS-like features|
|		|Migrate PCDS services to S3DF	||
|		|Retire psana	||
|Aug 2023	|Retire all legacy scientific computing clusters in B50 | Bullet, and all LSF clusters|
|		|Migrate SDF resources to S3DF ||
|Oct 2023	|Deploy federated identities	|Dependency on IAM ssh progress, may be delayed|
|Nov 2023	|Retire AFS	|Dependency on weka NFS v4, may be delayed|
|		|Retire GPFS	|Dependency on weka NFS v4, may be delayed|

## Slurm Dashboard

[sdf-slurm-summary](https://grafana.slac.stanford.edu/d/YW8wlINMk/sdf-slurm-summary?orgId=1&refresh=60s&theme=light&kiosk ':include :type=iframe width=100% height=850px')

