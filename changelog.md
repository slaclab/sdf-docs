# Status & Outages

## Outages

### Current

*** AS OF FRIDAY FEBRUARY 9TH 4:26PM PST ***

**Filesystems in S3DF mounted under `/sdf/data` are currently unavailable. We are troubleshooting a communication issue between the underlying NVMe and spinning disk subsystems. Please do not access pathnames under `/sdf/data`. Any type of job or task that attempts to access `/sdf/data` will fail. Existing data is safe and has not been lost. We will be posting periodic updates. Will post the next update tomorrow at 12:00PM PST. Thanks for your patience.**

### Upcoming

None

### Past

|When	|Duration | What	|
| --- | --- | --- |
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

