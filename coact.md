# Coact

## What is Coact?

[Coact](http://coact.slac.stanford.edu) is our portal for scientific resources and access management to S3DF. Through Coact, Facility Czars control who gets access and how facility resources are distributed. Every new S3DF user must first login to register with Coact and request S3DF access by specifying their affiliations. The facility Czar(s) must approve the request before the user can use S3DF.

## Coact Components and Services

S3DF defines a set of components to help manage scientific computing resources:


### Facilities

Facilities correspond to groups that have contributed funding or purchased S3DF hardware resources. A Facility in Coact may be an organization, a SLAC facility, a project, or a program. A List of Facilities and their points of contact can be found on our [Contact Us](contact-us.md) page.

### Facility Acquisition

A Facility's Acquisition is the total resources (compute servers, storage capacities etc) acquired by a Facility. A percentage of a Facilities compute Allocation can be assigned to Repos created and managed by that Facility. 

### Requests

Requests form the basis for how facility Czars and facility members to self manage resources in S3DF. Users may request membership to a facility, to a Repo, or request a new Repo. Requests under a facility are sent to facility Czars who may confirm or deny requests.


### Repos

A S3DF Repo is associated with a Facility and constitute a grouping of Facility members as well as some subset of Facility's resources allocated to that Repo. A Repo is an abstract description and may represent a grouping of batch compute; a (virtual) kubernetes cluster; a specific software project; etc. It is ultimately up to Facility Czars how to manage Repo organization, membership, and resource allocation.


### Repo Features

In order to more specifically define the infrastrucure that the Repo represents, a Repo may have Features assigned to it that defines what the Repo is for. Examples, include a Slurm feature to specify that the Repo should has batch resources associated with it; a netgroup and/or posixgroup to define ldap specific associations for the Repo; etc.

### Compute Allocation

A compute Allocation defined on a Repo with a Slurm Feature ties the Repo to a percentage of a facilities (batch compute) Allocation. This percentage can be adjusted on-the-fly per Repo by Czars within Coact (under Repos -> Compute). A Facility may over allocate their Repos (the sum of all Facility's Repos percentages exceed 100%) - however, should the instanenous usage of such batch compute exceed 100% of the Facility's Acquistion, then all of that Facility's slurm batch jobs will be held until the instaneous utilization falls below 100%.


### Cluster

A cluster is a homogenous set of computing nodes with the same hardware specifications and storage access. See [Clusters & Repos](batch-compute.md)
