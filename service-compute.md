# Service Compute

[Contact us](contact-us.md) if you need resources for running
long-lived jobs such as websites, web applications, or real-time/fast-feedback systems.

## S3DF Supported Sites and Web Applications

S3DF is currently supporting websites and web applications for several groups,
programs, and experiments:

| Site/Application	| URL |
| :--- | :--- |
| USDF Rubin Science Platform (RSP) | https://usdf-rsp.slac.stanford.edu|
| LCLS | https://pswww.slac.stanford.edu|
| SuperCDMS | https://supercdms-dev.slac.stanford.edu|
| Cryo-EM E-Logbook | https://cryoem-logbook.slac.stanford.edu|


## S3DF Publicly Accessible Content

S3DF can make static content from specific directories publicly available
via HTTP. If you need this service, pleasesubmit a SLAC ServiceNow request to
s3df-help, or email `s3df-help@slac.stanford.edu`. If you are the Point of Contact (PoC) for an S3DF facility, you may request this service on behalf of your organization or group.

Note: In the future, requests for static web content hosting will be managed via the S3DF [Coact](https://s3df.slac.stanford.edu/coact) portal.

#### Types of Content
- Static content refers to static HTML pages or files that are served directly to the users as-is. This may include (but is not limited to) image files, HTML/JavaScript files, CSS files, etc. that a user can view or download directly by going to the site via a browser.
- Dynamic content refers to a website or web application that is typically generated on a per-client basis, with information on how to render the site fetched from a database or other server-side resource. A dynamic site or application may also provide some method of authentication for user logins, saved preferences, and other functionality. S3DF supports web applications deployed as [containerized](https://www.docker.com/resources/what-container/) workloads in Kubernetes. Please submit a request to migrate or deploy containerized web applications in S3DF to [s3df-help](mailto:s3df-help@slac.stanford.edu).

#### Policies
Publicly accessible content hosted in S3DF is subject to the following policies:

- The [SLAC Acceptable Use of Information Technology Resources Policy](https://slac.sharepoint.com/sites/SLACPolicies/Shared%20Documents/SLAC-only%20Policies/IT-057-Acceptable%20Use%20of%20Information%20Technology%20Resources.pdf).
- `.htaccess` for `public_html` subdirectory configuration and access are not allowed. S3DF supports password-protected access using Basic Authentication for group space `public_html` subdirectories only. Please have the facility/group PoC contact [s3df-help](mailto:s3df-help@slac.stanford.edu) to enable password-protected access for those subdirectories.
- Hosted files or directories must be located under the appropriate user or group `public_html` directory (see below).
- Symlinks to other locations, either on the S3DF filesystem or other network filesystems (e.g., SLAC AFS, SLAC GPFS, SDF Lustre, etc.), are not allowed in `public_html`. Such links will not resolve when accessed via HTTP.

This table shows the respective hosted S3DF filesystem locations and public URLs to access their contents:

| S3DF Host Path | URL |
| :--- | :--- |
| `/sdf/home/<u>/<username>/public_html` | https://s3df.slac.stanford.edu/people/&lt;username&gt;|
| `/sdf/data/<groupname>/public_html` | https://s3df.slac.stanford.edu/data/&lt;groupname&gt; |
