# Accessing S3DF

There are three primary ways to access S3DF resources:

![S3DF users access](assets/S3DF_users_access.png)

In order to access S3DF, you must first obtain a [SLAC Account](accounts.md). You will then need to [register your affiliation](coact.md#what-is-coact) with S3DF. Once approved, you will be able to use any of the methods below to use S3DF resources.

?> S3DF is currently in the process of deprecating the usage of SLAC UNIX accounts. Please obtain a [SLAC Account](accounts.md) prior to accessing S3DF.


## SSH

You can connect using any SSH client, such as [OpenSSH](www.openssh.com) or [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/),
to connect to the S3DF load-balanced bastion pool `s3dflogin-mfa.slac.stanford.edu`.
These hosts require multi-factor authentication; for more information on working with MFA systems,
please see [SSH and MFA](sshmfa_user.md).

Example:
```
ssh <slac_account_username>@s3dflogin-mfa.slac.stanford.edu
```

?> Note that these nodes do not have access to storage (except for your home directory). From these bastion hosts, you should hop to an [Interactive Node](interactive-compute.md#interactive-pools) to access S3DF batch compute and storage.

?> Windows users may see an error message about a "*Corrupted MAC on input*" or "*message authentication code incorrect.*" The workaround is to add "*-m hmac-sha2-512*" to the ssh command, i.e. `ssh -m hmac-sha2-512 <username>@s3dflogin-mfa.slac.stanford.edu`


## NoMachine

S3DF NoMachine provides a remote desktop that is designed to be more performant displaying X11 graphics over slower connection speeds. NoMachine also preserves desktop state across multiple sessions, e.g. it can resume a virtual desktop even if a user's internet connection is dropped.

?> SLAC IT NoMachine (accessed via nx*.slac.stanford.edu) and S3DF NoMachine (accessed via s3dfnx.slac.stanford.edu) are two different services, with access to different storage and network domains. Please ensure that you are connecting to the correct NoMachine service when attempting to access S3DF resources via NoMachine.

The S3DF NoMachine cluster can be accessed via:

* **NoMachine desktop client:**

  The NoMachine client downloads and installation instructions for supported operating systems are located here: [https://download.nomachine.com/everybody/](https://download.nomachine.com/everybody/).
  
  Once installed, connect to the S3DF NoMachine server pool by entering the following settings in the Add Connection form:

    * Name: Enter a name for the NoMachine connection in string format (e.g., "S3DF NoMachine")
    * Host: `s3dfnx.slac.stanford.edu`
    * Port: `22`
    * Protocol: `SSH`
  
  ![NX-connection](assets/nx-connection.png)
  ![NX-session](assets/nx-session.png)

* **S3DF NoMachine web client:**

  The S3DF NoMachine cluster can also be accessed in a browser by going to the following link: [https://s3dfnx.slac.stanford.edu:4443/](https://s3dfnx.slac.stanford.edu:4443/)

  Enter your SLAC UNIX credentials to access the S3DF NoMachine web client.

  ?> The login method for S3DF NoMachine connections will be updated to use SLAC Account Single Sign-On (SSO) and Duo Multi-factor Authentication in the near future. For more information about SLAC SSO and MFA, see: [https://it.slac.stanford.edu/support/KB0010216](https://it.slac.stanford.edu/support/KB0010216)

## OnDemand

Open Ondemand is a web-based portal for accessing S3DF resources. You may:
1. Utilize the Ondemand web-based terminal to access S3DF Interactive nodes.
2. Utilize GUI-based scientific applications such as Jupyter notebooks and CryoSPARC.
3. Monitor and manage your batch jobs running in S3DF.

Log in to S3DF Ondemand at [https://s3df.slac.stanford.edu/ondemand](https://s3df.slac.stanford.edu/ondemand). You can find more information about using OnDemand in the [OnDemand reference](interactive-compute.md#ondemand).
