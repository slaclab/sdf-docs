# Status & Outages

## Outages

### Current

### Upcoming
|When	|Duration | What	|
| --- | --- | --- |
| Mar 24-27 2025 | 3 days (planned) | The HPSS tape archive system will be unavailable Monday March 24, 2025 at 6PM PDT until Thursday March 27, 2025 at 10PM PDT for a software upgrade from v8.3 to v10.3. Both writing data into HPSS or retrieval of data from HPSS will not be possible.
| Mar 25th 2025 | 14 hrs (planned) | The TFinity tape library will undergo preventative maintenance Tuesday March 25, 2025 from 8AM PDT to 8PM PDT. Access to the regular TSM backup system will be unavailable. Requests to restore files from tape should be submitted by emailing s3df-help@slac.stanford.edu and will be addressed after the maintenance period.

|When	|Duration | What	|
| --- | --- | --- |
| June 30th 2026 | 10:00-12:00 PDT (planned) | Disabling legacy Unix authentication for public-facing S3DF bastion services. Once complete, **SLAC Account with MFA will be required for s3dflogin.slac.stanford.edu, s3dfdtn.slac.stanford.edu and NoMachine s3dfnx.slac.stanford.edu.** 

If you are unsure of your SLAC Account status, use the following link to check:
https://ad-account.slac.stanford.edu
The app will give you the option of provisioning your SLAC Account OR report “You already have SSO (windows) account”.

You can test our SSH MFA workflow via the s3dflogin-mfa.slac.stanford.edu pool. We also provide an MFA-enabled SSH key management service. Full details can be found on this page: https://s3df.slac.stanford.edu/#/sshmfa_user
S3DF web services with central authentication already use MFA - this includes https://s3df.slac.stanford.edu/ondemand and https://coact.slac.stanford.edu .

If you are unable to authenticate with MFA it’s possible your SLAC account may require reactivation or a password reset.
Please send email to s3df-help@slac.stanford.edu for assistance. 

### Past

|When	|Duration | What	|
| --- | --- | --- |
| June 13th 2026 08:40-10:00 PDT | 1hr 20mins  (unplanned) | Weka filesystem for k8s entered a degraded state and stopped serving I/Os. Support team succesfully recovered the cluster.
| Jun 4 2026 | 45min (unplanned) | `/sdf/home`, `/sdf/group`, `/sdf/sw` outage during routine firmware upgrades for one model of server - An issue with the vendor's firmware upgrade tooling briefly stopped cooling fans in each server during each upgrade. A small percentage of servers overheated during this time, impacting `sdfhome` storage. |
| April 21st 2026 10:00-11:00 PDT | 1 hr (planned) | DTN nodes s3dfdtn.slac.stanford.edu, sdfdtn[001-006] will be rebooted during the maintenance window to apply security updates. This may interrupt currently-running transfers. Reboots will be done in batches to minimize disruption.
| February 4th 2026 | 9:00-13:00 PST (planned) | Shutdown the Globus node  “sdfdtn004” for a network card upgrade.
| March 18th 2026 11:00-12:00 PDT | 1 hr (planned) | DNS maintenance for s3dflogin s3dflogin-mfa s3dfdtn
| February 4th 2026 | 9:00-13:00 PST (planned) | Shutdown the Globus node  “sdfdtn004” for a network card upgrade.
| July 7th 2025 | 8 days (un)planned | The Stanford Facilities team need to conduct an evaluation of the SRCF datacenter transformers. All S3DF services will be unavailable.
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


## Monitoring Dashboards

[Grafana](http://grafana.slac.stanford.edu)

## Roadmap :id=roadmap

Please see our [Technology Migration Timeline](https://docs.google.com/spreadsheets/d/1ZIZC7g9TghhBINfdOD2JoNQCR5SSlj6TQaPqWPxPzQA/edit?usp=sharing)
(Select the TIMELINE tab)

## Slurm Dashboard

[sdf-slurm-summary](https://grafana.slac.stanford.edu/d/YW8wlINMk/sdf-slurm-summary?orgId=1&refresh=60s&theme=light&kiosk ':include :type=iframe width=100% height=850px')
