# Accounts and Access

## How to get an account :id=account

### Eligibility for S3DF Accounts
SLAC employees, affiliated researchers, and experimental facility users are eligible for an S3DF account. 
?> Please note that S3DF authentication requires a SLAC UNIX account; this is different from the legacy SDF 1.0 environment, which required a SLAC Active Directory (Windows) account.

### Steps to Acquire an S3DF Account

#### Step 1: Obtain a SLAC UNIX Account
If you do not already have a SLAC UNIX account, follow these steps to get a SLAC UNIX account:

Get a SLAC ID:

Affiliated users/experimental facility users: Use the Scientific Collaborative Researcher Registration process to obtain your SLAC ID.
SLAC employees: You should already have a SLAC ID number.
Complete Cybersecurity Training:

Access the SLAC training portal and take the appropriate course:
All lab users and non-SLAC/Stanford employees: "CS100: Cyber Security for Laboratory Users Training".
All SLAC/Stanford employees or term employees of SLAC or the University: "CS200: Cyber Security Training for Employees".
Depending on your role, additional cybersecurity training may be required. Consult your supervisor or SLAC Point of Contact (POC) for specifics.
Request a UNIX Account:

Ask your SLAC POC to submit a ticket to SLAC IT requesting a UNIX account. Provide your SLAC ID and your preferred account name, along with a second choice in case the preferred username is unavailable.
Step 2: Register Your SLAC UNIX Account in S3DF
Log into the Coact S3DF User Portal using your SLAC UNIX account by selecting the "Log in with S3DF (unix)" option.
Click "Repos" in the menu bar.
Hit the "Request Access to Facility" button and select a facility from the dropdown list.
Provide your affiliation and other contextual information in the "Notes" field before submitting your request.
A czar associated with the S3DF facility you are accessing will review your request. Once approved, the registration process should complete within about one hour.
Additional Information
To access files and folders in facilities like Rubin and LCLS, request your SLAC POC to add your username to the POSIX group that manages access to that facility's storage space. Future updates will integrate access to facility storage into the S3DF registration process within Coact.

SLAC IT is actively working on enabling federated access to SLAC resources. This will allow users to authenticate to SLAC computing systems via their home institution accounts rather than requiring a SLAC account. Federated authentication is anticipated to be available by late 2024.


If you are a SLAC employee, affiliated researcher, or experimental
facility user, you are eligible for an S3DF account. ***S3DF authentication requires a SLAC UNIX account. The legacy SDF 1.0 environment required a SLAC Active Directory (Windows) account. These are not the same authentication system.***


1. If you don't already have a SLAC UNIX account (the credentials used to log in to SLAC UNIX clusters such as `rhel6-64` and `centos7`), you will need to acquire one by following these instructions. **If you already have an active SLAC UNIX account, skip to step 2**:
  * Affiliated users/experimental facility users: Obtain a SLAC ID via the [Scientific Collaborative Researcher Registration process](https://it.slac.stanford.edu/identity/scientific-collaborative-researcher-registration) form (SLAC employees should already have a SLAC ID number).
  * Take the appropriate cybersecurity SLAC training course via the [SLAC training portal](https://slactraining.slac.stanford.edu/how-access-the-web-training-portal):
      * All lab users and non-SLAC/Stanford employees: "CS100: Cyber Security for Laboratory Users Training".
      * All SLAC/Stanford employees or term employees of SLAC or the University: "CS200: Cyber Security Training for Employees".
      * Depending on role, you may be required to take additional cybersecurity training. Consult with your supervisor or SLAC Point of Contact (POC) for more details.
  * Ask your [SLAC POC](contact-us.md#facpoc) to submit a ticket to SLAC IT requesting a UNIX account. In your request indicate your SLAC ID and your preferred account name (include a second choice in case your preferred username is unavailable).
2. Register your SLAC UNIX account in S3DF:
  * Log into the [Coact S3DF User Portal](https://s3df.slac.stanford.edu/coact) using your SLAC UNIX account via the "Log in with S3DF (unix)" option.
  * Click on "Repos" in the menu bar.
  * Click the "Request Access to Facility" button and select a facility from the dropdown.
  * Include your affiliation and other contextual information for your request in the "Notes" field, then submit.
  * A czar for the S3DF facility you requested access to will review your request. **Once approved by a facility czar**, the registration process should be completed in about 1 hour.

?> To access files and folders in facilities such as Rubin and LCLS, you will need to ask your
SLAC POC to add your username to the [POSIX
group](contact-us.md#facpoc) that manages access to that facility's
storage space. In the future, access to facility storage will be part of the S3DF registration process in Coact.


?> SLAC IT is currently working on providing federated access to SLAC
resources, which will enable authentication to SLAC computing systems 
with a user's home institution account rather than a SLAC account. 
Federated authentication is expected to be available in late 2024.

## Managing your UNIX account password

You can change your password via [the SLAC UNIX self-service password update site](https://unix-password.slac.stanford.edu/).

If you have forgotten your password and need to reset it, [please contact the IT Service Desk](https://it.slac.stanford.edu/support).

Make sure you comply with all SLAC training and cybersecurity requirements to avoid having your account disabled. You will be notified of these requirements via email.


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
