# Status & Outages

Feb 2025 SRCF I/II Outage
=========================

The SRCF datacenter building that houses the S3DF system has two urgent issues that need to be addressed. The work is needed to ensure that we can provide resilient power and cooling to the equipment in SRCF. Work to resolve these issues will impact the availability of S3DF, services S3DF supports, and other SCS managed systems within the datacenter.

The work will need to occur over 2 separate days in early February 2025: **Feb 4th 2025 and Feb 6th 2025**. Due to the nature of the work (see below for details), some parts of S3DF will be unavailable for certain periods during these two days. The system will be drained of running jobs before the Feb 6th maintenance.

We understand the inconvenience this may cause to running workflows on S3DF and are actively working with the SRCF team to determine ways to mitigate the impact. Unfortunately, we CANNOT avoid the maintenance at this time, but certain selected systems and services will be partly operational during one or both of these maintenance periods.

Outage 1: SRCF1 UPS-B Phase 1
==========================

What: The UPS-B Phase 1 system has a faulty control switch that needs replacement. Since this impacts the ability to switch between UPS and Utility power, the equipment cannot be worked on unless power is turned off completely. The S3DF racks impacted contain the interactive services for S3DF.

Why: The faulty control switch on the UPS is preventing the UPS from being maintained - it has several (currently redundant) components that have failed and that need to be replaced. Until the control switch issue is resolved, the UPS remains in danger of failing, especially during critical outages when it needs to remain fully operational.

**When: February 4th from 9:45 AM to 11:00 AM PST.**

Impact: All equipment in the impacted rows will need to be powered down in preparation for that maintenance and will not be operational. This impacts:
1. **S3DF Interactive services (all IANA nodes). This includes all Facility specific interactive nodes as well.**
2. **On-Demand services that access IANA nodes will be unavailable for the duration of of the outage.**

Outage 2: SRCF2 M2 Mechanical Substation
==================================

What: An 800A breaker on the M2 Mechanical Substation needs to be replaced. This will impact cooling and all house lighting in SRCF-II.

Why: The 800A breaker loss has resulted in a loss of redundant cooling in SRCF-II. Currently that portion of the data center is operating with only 2 chillers and needs a third chiller to be redundantly cooled. The third chiller cannot be brought online until the breaker is replaced and replacement of the breaker will need the entire substation to be powered down which impacts ALL chillers.

**When: February 6th from 7:00 AM to 5:00 PM PST**

Impact: All S3DF compute and storage systems will have to be in an idle state due to the lack of any cooling in the data center.
	
 1. **No batch jobs will run during the outage. A maintenance reservation will be set so that jobs will not run if it will overlap this time period.**
 2. **No access to login nodes and interactive services = SSH and OnDemand will be unavailable.**
 3. **SDF Data (/sdf/data) and DDN (/fs/ddn) filesystems will be unavailable**
 4. **Platform services (Kubernetes and Web services) will remain online BUT any applications dependent on SDF Data or DDN filesystems will be scaled down to prevent them from running**
 5. **Networking access will be intermittent.**

Since this is a long outage, we are unable to keep all S3DF services up and running during the outage. We will also use this opportunity to ensure existing S3DF systems and services are made more resilient.

1. We will be setting a reservation in Slurm for the duration of the outage. This means any jobs that are scheduled to start in the outage window will not run. **Only jobs that complete before 7AM on 2/6/25 will run.**
2. **All OnDemand access to S3DF will be unavailable**
3. **All Kubernetes services that are dependent on impacted filesystems will be scaled down so they do not run:**

- All of /fs/ddn/ will go down for maintenance on the 6th February. All attempts to read or write from your containers to /fs/ddn will hang. Dependent upon your application, it may also timeout and fail.
- The /sdf/data mount and subfolders will remain up during the outage on the 6th February. However, the backing stores for /sdf/data WILL go down for maintenance (specifically Ceph, which is used to tier data to slower media). If your application tries to read data from /sdf/data that is not 'recent' (and hence only held in Ceph) then the application will appear to hang as it attempts to read that data. Similar to the /fs/ddn access, your application may also timeout. All writes are expected to work as normal (since it will not go to Ceph).
- From experience, most workloads will automatically recover (especially if it locks indefinitely awaiting the filesystem to return). Once the filesystems are back up, you should check your pods to ensure everything is functioning as you expect (comprehensive readiness and liveness problems will help).
- Due to the extensive number and variation of workloads, we cannot predict how your application will react. If you are unsure about how your application will react to the prolonged I/O hangs from the /sdf/data and /fs/ddn filesystems, we recommend that you scale your relevant workloads down prior to the outage and spin them back up again after we give the ok. This can be achieved with the kubectl scale ... --replicas=0 command (and --replicas > 0 to spin them back up).

## Outages

### Current

### Upcoming

### Past

|When	|Duration | What	|
| --- | --- | --- |
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

