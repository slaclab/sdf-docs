# Accounts and Access

## How to get an account :id=access

If you are a SLAC employee, affiliated researcher, or experimental
facility user, you are eligible for an S3DF account. ***S3DF authentication requires a SLAC Unix account. The legacy SDF 1.0 environment requires a SLAC Active Directory account. They are not the same password system.***


1. If you don't already have a SLAC UNIX account (that allowed logins to the rhel6-64 and centos7 clusters), you'll need to get one by following these instructions. **If you already have one, skip to step 2**:
  * Obtain a SLAC ID via the [Scientific Collaborative Researcher Registration process](https://it.slac.stanford.edu/identity/scientific-collaborative-researcher-registration)
  * Take Cyber 100 training via the [SLAC training portal](http://training.slac.stanford.edu/web-training.asp)
  * Ask your [SLAC POC](contact-us.md#facpoc) to submit a ticket to SLAC IT requesting a UNIX account. In your request indicate your SLAC ID, and your preferred account name (and second choice).
2. Enable the SLAC UNIX account into S3DF:
  * Log into [coact](https://s3df.slac.stanford.edu/coact) using your SLAC UNIX account and follow the instructions to enable your account in S3DF. If the account creation process fails for any reason, we'll let you know. Otherwise, you can assume your account will be enabled within 1 hour.

?> In some cases, e.g. for Rubin and LCLS, you may want to ask your
SLAC POC to add your username to the [POSIX
group](contact-us.md#facpoc) that manages access to your facility's
storage space. This is needed because S3DF is not the source of truth
for SLAC POSIX groups. S3DF is working with SLAC IT to deploy a
centralized database that will grant S3DF the ability to modify group
membership.


?> SLAC is currently working on providing federated access to SLAC
resources so that you will be able to authenticate with your home
institution's account as opposed to your SLAC account. We expect
federated authentication to be available in late 2024.

## Managing your UNIX account password

You can change your password yourself via [this password update site](https://unix-password.slac.stanford.edu/)

If you've forgotten your password and you want to reset it, [please contact the IT Service Desk](https://it.slac.stanford.edu/support)

Make sure you comply with SLAC training and cyber requirements to avoid getting your account disabled. You will be notified of these requirements via email.


## How to connect

There are three mechanisms to access S3DF:

1. **SSH**: You can connect using any SSH client, such as
[OpenSSH](www.openssh.com) or
[PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/), on the
standard TCP port 22, to connect to the S3DF load balanced bastion pool
`s3dflogin.slac.stanford.edu`. Note that these nodes do not have access to
storage (except for your home directory). From these bastion hosts, you
should hop onto an [Interactive
Node](interactive-compute.md#interactive-pools) to access S3DF batch compute
and storage.

?> Windows users may see an error message about a "*Corrupted MAC on
input*" or "*message authentication code incorrect.*"
The workaround is to add "*-m hmac-sha2-512* "to the ssh command, i.e.
`ssh -m hmac-sha2-512 <username>@s3dflogin.slac.stanford.edu`

2. **NoMachine**: NoMachine provides a special remote desktop that is
specifically designed to improve, compared to ssh, the performance of
X11 graphics over slow connection speeds. Another important feature is
that it preserves the state of your desktop across multiple
sessions, including when your internet session unexpectedly gets dropped. The login pool for NoMachine is
`s3dfnx.slac.stanford.edu`. You can find more information about this
access mode in the [NoMachine reference](reference.md#nomachine).

3. **OnDemand**: If you do not have a terminal handy or you want to
use applications like Jupyter, you can also launch a web-based
terminal using OnDemand:\
[`https://s3df.slac.stanford.edu/ondemand`](https://s3df.slac.stanford.edu/ondemand).\
You can find more information about using OnDemand in the [OnDemand
reference](reference.md#ondemand).

![S3DF users access](assets/S3DF_users_access.png)
