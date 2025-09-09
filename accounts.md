# Accounts and Access

## How to get an account :id=account

### Eligibility for S3DF Accounts
SLAC employees, affiliated researchers, and experimental facility users are eligible for an S3DF account. 
?> Please note that S3DF authentication requires a SLAC UNIX account.

### Steps to Acquire an S3DF Account

#### Step 1: Obtain a SLAC UNIX Account
If you do not already have a SLAC UNIX account, follow these steps to [get a SLAC UNIX account](slac-unix-account.md)

#### Step 2: [Register Your SLAC UNIX Account in S3DF](slac-unix-account.md#register)


## How to connect  :id=connect 

There are three primary methods to access S3DF:

1. **SSH** (Secure Shell):

 - You can connect using any SSH client, such as [OpenSSH](www.openssh.com) or [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/), via standard TCP port 22 to reach the S3DF load-balanced bastion pool at s3dflogin.slac.stanford.edu
   
        ssh username@login-node-address
   
 - Please note that these bastion hosts do not have storage access except for your home directory. After connecting, you must hop onto an [Interactive
Node](interactive-compute.md#interactive-pools)to access S3DF batch compute resources and storage.  
   
        ssh username@pool-node-address
   
 - For Windows Users: If you encounter an error message regarding a “Corrupted MAC on input” or “message authentication code incorrect,” you can resolve this by adding “-m hmac-sha2-512” to your SSH command. For example:

        ssh -m hmac-sha2-512 <username>@s3dflogin.slac.stanford.edu

2. **NoMachine**:

 - NoMachine offers a specialized remote desktop solution that enhances X11 graphics performance over slow connections compared to SSH.
 - An added benefit is that it maintains your desktop state across sessions, even if your internet connection is dropped unexpectedly.
 - Use the login pool for NoMachine at s3dfnx.slac.stanford.edu. Additional details about this access method can be found in the NoMachine reference documentation [NoMachine reference](reference.md#nomachine)

3. **OnDemand**:

 - If you prefer not to use a terminal or want to run applications such as Jupyter, you can access a web-based terminal via OnDemand [`https://s3df.slac.stanford.edu/ondemand`](https://s3df.slac.stanford.edu/ondemand).
 - For further information on using OnDemand, please refer to the OnDemand reference documentation [OnDemand
reference](interactive-compute.md#ondemand).


![S3DF users access](assets/S3DF_users_access.png)
