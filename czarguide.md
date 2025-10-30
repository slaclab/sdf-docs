# Beginner's Guide for Facility Czars

This guide is intended for facility czars to get started with managing their facility's repos, computing resources, user accounts, and more. The majority of czar tasks can be performed on [coact](https://coact.slac.stanford.edu) but this guide will cover some additional topics.

List of primary tasks for a facility czar:
* Create/manage repos for computing/storage resources for their facility
* Add/remove users to facility repos for accessing computing resources
* Add/remove users to Posix group for accessing storage resources (e.g. /sdf/data or /sdf/group)
* Inform facility users on how to access computing/storage resources on S3DF
* Commincate facility-wide issues or requests to S3DF admin team

> [!TIP]
> Facility czars play the role of an intermediary between S3DF general users and S3DF admin/support staff. Czars are the primary point-of-contact for users with S3DF issues/requests but not expected to provide full technical support; they can refer users to the [S3DF help Slack channel](slac.slack.com#comp-sdf).

## Management Systems in Coact

Coact is the primary interface for facility czars to manage their tasks. The most common tasks involve managing repos and their facility's users. To begin, log into your [coact](https://coact.slac.stanford.edu) account. The tabs in the top left: Facilities, Repos, and Requests each provide different options.

### Coact -> Facilities

In this section, czars can see an overview of their facility's compute and storage resources. Additionally, czars can add existing S3DF users to their facility and delegate additional czars.

### Coact -> Repos

In this section, czars can create repos and allocate computing resources to them. Additionally, czars can add/remove members to the different repos (useful if different users need access to different computing resources for different projects).

> [!NOTE]
> **Repos cannot be deleted in Coact!** This is a known limitation and should not be an issue for now as repos can be renamed and allocated to zero users aside from the facility czar. To delete a repo, please contact the S3DF admin team.

* To create a new repo use the "Request New Repo" button in the top right.
* To add a user to an existing repo, select the person icon next to the repo name to view the users for that repo. Then select the "Manage Users" button to add/remove users.
* To allocate comute resources for a repo, select the "Compute" tab and edit the "Total compute allocation" value for the desired repo/cluster name.

> [!TIP]
> Allocation values less than 100% will restrict the maximum number of CPUs/GPUs that can be used by that repo/cluster at a time as a fraction of the total owned resources by the facility.

### Coact -> Requests

In this section, czars can accept requests by users to join a facility and gain access to its repos. An email notification will be sent to czars when a user requests access to the facility. If an error occurs, it may be due to a new user not having a SLAC Unix account associated with coact. Accepting requests here only adds the user to the facility but does not automatically add them to any repos except "default".