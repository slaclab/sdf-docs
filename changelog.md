# Status & Outages

## Outages

### Current

### Upcoming

Start:  2024-07-10 06:00 PDT  (2024-07-10 13:00 UTC)

End:    2024-07-12 20:00 PDT  (2024-07-13 03:00 UTC)

Urgent electrical maintenance is required in SRCF, the datacenter hosting S3DF.

All S3DF services, including login nodes, batch systems, Kubernetes nodes,
storage, and networking, will be unavailable during the maintenance window.

**DDN Lustre storage will also be unavailable for up to 24hrs (2024-07-10 09:00AM PDT to 2024-07-11 09:00AM PDT)**
  This means logins to the sdf-login.slac.stanford.edu login cluster will be unavailable during that time.

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

