# Service Compute

[Contact us](contact-us.md) if you need resources for running
long-lived jobs such as websites, web applications, or
real-time/fast-feedback systems.

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


***S3DF Public HMTL Terms and Conditions of Use***

> [!IMPORTANT] 
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

## vClusters 

https://github.com/loft-sh/vcluster

### Description
Fully functional virtual Kubernetes clusters, Each vcluster runs inside a namespace of the underlying k8s cluster. Main advantages against creating a separate Ck8s cluster (k0s, k3s, k8s vanilla):
* vClusters may communicate with each other within the parent cluster.
* Doesn't require an additional dedicated nodes to run the apiServer, proxy, etcd, scheduler, and controller.
* Uses the underlying k8s cluster resources, such us CNI, CSI, metallb, multus, kyverno, ingress-controller, etc.
* Rollout upgrades: no downtime while upgrading the vcluster resources (syncers - which runs the vClusters apiServers- and etcd). Not affected by other vCluster upgrades.

And still ge the best of both worlds:
* **Granular Permissions**:
vCluster users operate with minimized permissions in the host cluster, significantly reducing the risk of privileged access misuse. Within their vCluster, users have admin-level control, enabling them to manage CRDs, RBAC, and other security policies independently.

* **Isolated Control Plane:**
Each vCluster comes with its own dedicated API server and control plane, creating a strong isolation boundary.

* **Customizable Security Policies:**
Tenants can implement additional vCluster-specific governance, including OPA policies, network policies, resource quotas, limit ranges, and admission control, in addition to the existing policies and security measures in the underlying physical host cluster.

* **Enhanced Data Protection:**
With options for separate backing stores, including embedded SQLite, etcd, or external databases, virtual clusters allow for isolated data management, reducing the risk of data leakage between tenants.

* **Full Admin Access per Tenant:**
Tenants can freely deploy CRDs, create namespaces, taint, and label nodes, and manage cluster-scoped resources typically restricted in standard Kubernetes namespaces.

* **Isolated yet Integrated Networking:**
While ensuring automatic isolation (for example, pods in different virtual clusters cannot communicate by default), vCluster allows for configurable network policies and service sharing, supporting both separation and sharing as needed.

* **Conflict-Free CRD Management:**
Independent management of CRDs within each virtual cluster eliminates the potential for CRD conflicts and version discrepancies, ensuring smoother operations and easier scaling as the user base expands.

### When to request a vCluster
* **Environment isolation:** When you need a separate environment (e.g., dev, test, staging, prod).

* **Team or project isolation:** When multiple teams/projects share the same physical cluster but need isolated namespaces, RBAC, and resources.

* **Version testing:** When you need to test a different Kubernetes version, operator, or dependency.

* **CI/CD pipelines:** When ephemeral clusters are required for integration tests or preview environments.

* **Security boundaries:** When stronger separation of permissions, policies, or workloads is required than namespace isolation alone can provide.

* **Multi-tenancy scenarios:** When multiple tenants (internal or external) must be isolated from one another.

* **Custom control plane extensions:** When testing custom controllers, CRDs, or API extensions.

* **Scaling management overhead:** When cluster quotas, network policies, or admission controls need to be fine-tuned for a specific workload.

* **Sandboxing experiments:** When developers need a safe space to try out cluster-level changes (like installing operators) without risking the shared cluster.

* **Migration/dry-run scenarios:** When validating cluster migrations, upgrades, or new tooling before rolling them out at scale.

### How to request a new vCluster
