# Coact

## What is Coact?

**What is Coact?**

[Coact](http://coact.slac.stanford.edu) is our portal for scientific resources and access management to S3DF. Facility czars control who gets access and how facility resources are distributed. Every new S3DF user must first login to coact (using their Unix account) and request S3DF access by specifying a facility. The facility czar must then approve the request before the user can login.

## Coact components and services

Coact interacts with the following components to manage scientific computing resources: Facilities, Repos, Requests, Facility Allocations, and Compute Allocations.

**Facilities**

Facilities correspond to groups that have contributed funding or purchased S3DF hardware resources. A Facility in Coact may be an organization, a SLAC facility, a project, or a program. A List of Facilities and their points of contact can be found on our [Contact Us](contact-us.md) page.

**Facility Allocation**

Facility allocations are the total Compute resources acquired by a Facility. A percentage of a Facilities compute allocation can be assigned to Repos created and managed by that Facility.

**Repos**

Coact Repos are associated with a Facility and constitute a grouping of Facility members as well as some subset of Facility compute resources allocated to that repo. A Coact Repo may represent a specific software project with an accompanying code repository, that the developers or maintainers deploy on S3DF infrastructure. It is ultimately up to Facility Czars how to manage repo organization, membership, and resource allocation.


**Requests**

Requests form the basis for how facility czars and facility members self manage purchased resources in S3DF. Users may request membership to a facility, to a repo, or request a new repo. Requests under a facility are sent to facility Czars who may confirm or deny requests.




**Compute Allocation**

A compute allocation is specified as a percentage of a facilities allocation, and can be adjusted per repo by czars under Repos -> Compute. Compute Allocations for a given repo can be adjusted for each cluster a facility has purchased resources in.

**Cluster**

A cluster is a homogenous set of computing nodes with the same hardware specifications and storage access. See [Clusters & Repos](batch-compute.md)
