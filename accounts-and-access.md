# Accounts and Access

## How to get an account :id=access

If you are a SLAC employee, affiliated researcher, or experimental
facility user, you are eligible for an S3DF account. These are the
steps to get into S3DF:

1. Obtain a SLAC ID via the [SLUO User
Form](https://oraweb4.slac.stanford.edu/apex/epnprod/f?p=134:1)
2. Take Cyber 100 training via the [SLAC training
portal](http://training.slac.stanford.edu/web-training.asp)
3. Ask your SLAC POC to submit a ticket to SLAC IT requesting a UNIX
account. In your request indicate your SLAC ID, your preferred account
name (and second choice), and the need for the account to be enabled
in S3DF.

?> SLAC is currently working on providing federated access to SLAC
resources so that you will be able to authenticate with your home
institution's account as opposed to your SLAC account. We expect
federated authentication to be available in 2023.

## How to connect

There are three mechanisms to access S3DF:

1. **SSH**: You can connect using any SSH client, such as
[OpenSSH](www.openssh.com) or
[PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/), on the
standard TCP port 22, to connect to the S3DF load balanced login pool
`s3dflogin.slac.stanford.edu`.

2. **NoMachine**: NoMachine provides a special remote desktop that is
specifically designed to improve, compared to ssh, the performance of
X11 graphics over slow connection speeds. Another important feature is
that it preserves the state of your desktop across multiple
sessions. The login pool for NoMachine is
`s3dfnx.slac.stanford.edu`. You can find more information about this
access mode in the [NoMachine reference](reference.md#nomachine).

3. **OnDemand**: If you do not have a terminal handy or you want to
use applications like Jupyter, you can also launch a web-based
terminal using OnDemand:\
[`https://s3df.slac.stanford.edu/ondemand`](https://s3df.slac.stanford.edu/ondemand).\
You can find more information about using OnDemand in the [OnDemand
reference](reference.md#ondemand).

![S3DF users access](assets/S3DF_users_access.png)
