# Service Compute

[Contact us](contact-us.md) if you need resources for running
long-lived jobs such as websites, web applications, or
real-time/fast-feedback systems.


## S3DF Kubernetes

We provide kubernetes environments for scientific users of S3DF. Kubernetes provides an ecosystem to manage containerized applications and a unified and abstracted computing environment for deploying, scaling, and managing your applications and services without direct interaction with individual servers or operating systems.

### Why use Kubernetes?

Some of the benefits include:

* **Automation:**
Kubernetes automates routine tasks like starting new applications, scaling up or down based on demand, and replacing failed containers, reducing manual effort and improving efficiency. 
* **Scalability:**
It automatically scales applications by adding or removing containers to handle fluctuating traffic, ensuring consistent performance and optimal resource usage. 
* **High Availability & Resilience:**
Kubernetes provides self-healing capabilities by monitoring applications and automatically restarting, rescheduling, or replacing failed containers and redistributing workloads if a node fails. 
* **Portability:**
By abstracting away the underlying infrastructure, Kubernetes allows containerized applications to run consistently across various environments, including on-premises data centers, public clouds, and hybrid configurations, reducing vendor lock-in. 
* **Faster Deployment & Development:**
It enables faster release cycles and improves developer agility by simplifying the deployment of containerized and microservices-based applications. 
* **Efficient Resource Utilization:**
By running multiple containers on the same cluster nodes, Kubernetes optimizes resource use and can automatically scale down resources during low-traffic periods to save costs. 
* **Open Source Ecosystem:**
Kubernetes benefits from a large and active open-source community, leading to a rich ecosystem of tools and extensions for enhanced security, monitoring, and management

### How to request a Kubernetes Environment

S3DF uses Loft's vCluster, which are a fully functional virtual Kubernetes clusters. Each vcluster runs its own dedicated kubernetes API server and control plane, creating a strong isolation boundary, and can freely deploy CRDs (aka Operators), create namespaces, and manage cluster-scoped resources unrestricted.

* To request one file a ticket to s3df-help@slac.stanford.edu, specifying:
  * **Purpose:** like application to run
  * **Environment:** Production, interim, development.
  * **Facility:** Facility to which it will belong i.e. AD, Rubin, LCLS.
  * **vCluster Owners:** Users who should have access to the new vCluster.

* To access your kubernetes vcluster, go to https://k8s.slac.stanford.edu/<vcluster_name> to obtain a token for `kubectl`

## S3DF Dynamic Sites and Web Applications

S3DF is currently supporting websites and web applications for several groups,
programs, and experiments:

| Site/Application	| URL |
| :--- | :--- |
| USDF Rubin Science Platform (RSP) | https://usdf-rsp.slac.stanford.edu|
| LCLS | https://pswww.slac.stanford.edu|
| SuperCDMS | https://supercdms-dev.slac.stanford.edu|
| Cryo-EM E-Logbook | https://cryoem-logbook.slac.stanford.edu|

Dynamic content refers to a website or web application that is
typically generated on a per-client basis with information on how to
render the site fetched from a database or other server-side
resource. A dynamic site or application may also provide some method
of authentication for user logins, saved preferences, and other
functionality.

S3DF supports web applications deployed as
[containerized](https://www.docker.com/resources/what-container/)
workloads in Kubernetes. Please submit a request to migrate or deploy
containerized web applications in S3DF to
[s3df-help](mailto:s3df-help@slac.stanford.edu). We will allocate a
K8s virtual cluster for you and a DNS entry for your top-level
site. You will then be able to manage your own web applications within
the cluster. Eventually, the default naming scheme will be:

`https://<facilityname>.sdf.slac.stanford.edu/<webappname>`

?> The URL above assumes S3DF own its own subdomain, which is not
currently the case. For the time being, we'll work with you to find a
temporary URL without .sdf in the name.

## S3DF Static Sites

S3DF can make static content from specific directories publicly
available via HTTP. Static content refers to static HTML pages or
files that are served directly to the users as-is. This may include
(but is not limited to) image files, HTML/JavaScript files, and CSS
files, that a user can view or download directly by going to the site
via a browser. If you need this service, please contact
[s3df-help](mailto:s3df-help@slac.stanford.edu). If you are the Point
of Contact (PoC) for an S3DF facility, you may request this service on
behalf of your organization or group.

Hosted files or directories must be located under the appropriate user
or group `public_html` directory. This table shows the mapping between
the hosted S3DF filesystem locations and the public URLs to access
their contents:

| S3DF Host Path | URL |
| :--- | :--- |
| `/sdf/home/<u>/<username>/public_html` | https://s3df.slac.stanford.edu/people/&lt;username&gt;|
| `/sdf/data/<groupname>/public_html` | https://s3df.slac.stanford.edu/data/&lt;groupname&gt; |


> ***S3DF Public HMTL Terms and Conditions of Use***
> * This service is only for active S3DF users that maintain an affiliation with an S3DF facility.
> * All requests for S3DF public HTML sharing via home directories will be reviewed by SCS on a case-by-case basis.
> * submit requests via email to s3df-help@slac.stanford.edu or through the S3DF [Coact](https://s3df.slac.stanford.edu/coact)
portal
> * The use of this service is subject to SLAC’s “Acceptable Use of IT Resources” policy: https://policies.slac.stanford.edu/categories/information-technology/acceptable-use-information-technology-resources
> * Approval may be rescinded if the use is seen to violate SLAC Acceptable Use policies
> * Executable files (e.g. java, PHP, Tomcat) are not permitted, only static content.  Client side inline Javascript and stylesheets (CSS) are permitted.
> * Symlinks to locations not under `public_html` , either on the S3DF
filesystem or other network filesystems (e.g., SLAC AFS, SLAC GPFS,
SDF Lustre, etc.), are not allowed and such links will not resolve
when accessed via HTTP.
> * Purely for SLAC business purposes
> * Not for personal non-professional purposes
> * We do not implement any form of authentication for public HTML sharing via home directories
> * Stanford also provides personal website hosting for SLAC staff with a Stanford (SUNet) account: https://uit.stanford.edu/guide/website/personal

## S3DF Cron Tasks

A dedicated cron node is provided for managing scheduled cron tasks.

?> User cron jobs are enabled only for this cron node.

To access the cron node:
1. Log in to S3DF as normal.
2. From the S3DF node, connect via SSH to `sdfcron001`.
3. Use the `crontab` command as normal to manage cronjobs.

?> Cron jobs configured in the legacy crontab systems on the interactive S3DF nodes have been migrated to `sdfcron001`. If a task is missing, please open a support ticket.

Since interactive user connections are distributed between nodes in the S3DF environment and cron configurations are not shared between nodes, using the dedicated cron server simplifies the management of user cron jobs.
