# Status & Outages

## Outages


|When	|Duration | What	|
| --- | --- | --- |
|Jan 15 2023 | Unknown | sdfdata hangs on several nodes (unplanned)|
|Jun 26 2023	|5 days	| Everything down due to power outage (planned)|


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
|Feb 2023	|Deploy pre-ops Rubin acquisitions in SRCF-II	|No backup power in SRCF-II until after shutdown|
|Mar 2023	|Export sdfhome and sdfdata to SLAC	|Via NFS v4 to provide AFS-like features|
|Jun 2023	|SRCF-I and II power outage	|5-day shutdown starting on Jun 26th|
|Jul 2023	|Backup power available in SRCF-II	||
|		|Migrate PCDS services to S3DF	||
|		|Retire psana	||
|Aug 2023	|Retire all scientific computing clusters in B50	|SDF, Bullet, and all LSF clusters|
|Oct 2023	|Deploy federated identities	|Dependency on IAM ssh progress|
|Nov 2023	|Retire AFS	||
|		|Retire GPFS	||

## Slurm Dashboard

[sdf-slurm-summary](https://grafana.slac.stanford.edu/d/YW8wlINMk/sdf-slurm-summary?orgId=1&refresh=60s&theme=light&kiosk ':include :type=iframe width=100% height=850px')

