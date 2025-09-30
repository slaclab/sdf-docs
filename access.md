# Accessing S3DF

There are three primary ways to access S3DF resources:

![S3DF users access](assets/S3DF_users_access.png)

In order to access S3DF resources, you must first obtain a [SLAC Account](accounts-and-access.md) (formerly known as a SLAC Windows account).

?> S3DF is currently in the process of deprecating the usage of SLAC UNIX accounts. Please obtain a SLAC Account prior to accessing S3DF.


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

S3DF NoMachine provides a special remote desktop that is specifically designed to improve, compared to ssh, the performance of X11 graphics over slow connection speeds. Another important feature is that it preserves the state of your desktop across multiple sessions, including when your internet session unexpectedly gets dropped. The login pool for NoMachine is `s3dfnx.slac.stanford.edu`. You can find more information about this access mode in the [NoMachine reference](reference.md#nomachine).

?> SLAC IT NoMachine (accessed via nx*.slac.stanford.edu) and S3DF NoMachine (accessed via s3dfnx.slac.stanford.edu) are two different services, with access to different storage and network domains. Please ensure that you are connecting to the correct NoMachine service when attempting to access S3DF resources via NoMachine.

## OnDemand

Open Ondemand is a web-based portal for accessing S3DF resources. You may:
1. Utilize the Ondemand web-based terminal to access S3DF Interactive nodes.
2. Utilize GUI-based scientific applications such as Jupyter notebooks and CryoSPARC.
3. Monitor and manage your batch jobs running in S3DF.

Log in to S3DF Ondemand at [https://s3df.slac.stanford.edu/ondemand](https://s3df.slac.stanford.edu/ondemand). You can find more information about using OnDemand in the [OnDemand reference](interactive-compute.md#ondemand).
