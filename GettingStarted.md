# Getting Started at S3DF

This document will guide you through the basics of using S3DF's clusters, storage systems, and services.

## Get a S3DF Account

To utilize the S3DF facilities, you must first [acquire a S3DF account](accounts.md#account), and your user account should be associated with a S3DF allocation to run jobs

## Connect to S3DF

The documentation will guide you to [access S3DF](accounts.md#connect)

## Computing Resources 
S3DF offers a variety of high-performance computing resources that are accessible. 

### [roma](systems.md#roma)
### [milano](systems.md#milano)
### [ampere](systems.md#ampere)
### [turing](systems.md#turing)
### [ada](systems.md#ada)

## Storage Resources
To ensure long-term consistency, the [S3DF directory structure](storage.md) features immutable paths that are independent of the underlying file system organization and technology.


## Software

- The [software](software.md) available within S3DF plays a crucial role and encompasses a broad scope. Whenever feasible, S3DF prioritizes the use of pre-built, packaged software, such as RPMs from reputable repositories.

- In addition, S3DF utilizes Lmod to manage software packages installed through alternative methods. Through Lmod, S3DF provides support for a select number of software packages that are widely utilized by the SLAC communities.

- S3DF encourages experts outside of the SCS to leverage Lmod for providing, supporting, maintaining, and sharing the software tools they develop.  

## Running Jobs
There are three different ways of [run jobs](run.md) on S3DF
- [Interactive](interactive-compute.md): Commands that you issue are executed immediately.
- [Batch](batch-compute.md): Jobs are submitted to a queue and are executed as soon as resources become available.
- [Service](service-compute.md): Long-lived jobs that run in the background waiting for data to analyze.

## Data Transfers
s3dfdtn.slac.stanford.edu is a load-balanced DNS name which points to a pool of dedicated data transfer nodes. It is open to everyone with an S3DF account. Common tools like scp/sftp/rsync are available for casual data transfers. For serious large volume data transfer, you may consider bbcp and globus. You can refer to [this](managedata.md) for detailed information on data transfers in S3DF

The following graph provides a comprehensive overview of the S3DF facilities.

![Resource](assets/Resource.png)

## Getting Help
There are many [resources](help.md) available to assist you in utilizing S3DF effectively. The S3DF support team is always here to help you with any questions or challenges you may encounter. 

