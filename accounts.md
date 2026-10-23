# Accounts

S3DF uses SLAC Account credentials for authentication and authorization. To use S3DF you need:

1. A **SLAC Account** (the Windows/Active Directory account issued by SLAC IT).
2. A **UNIX account**, requested separately. A SLAC Account no longer comes with a UNIX account.
3. **S3DF access**, granted when you register your account with S3DF.

Once registered, you can then [access S3DF resources](access.md).

!> If you have only a SLAC Account, you will not be able to get S3DF access. You must also have a UNIX account. See [Requesting a UNIX account](#unix-account).

## Getting a SLAC Account (existing S3DF users)

If you are currently using S3DF with only a Unix account, please use this [self-service application to create your SLAC Account](https://ad-account.slac.stanford.edu).
If the application reports you already have an existing SLAC Account, contact the [SLAC IT Service Desk](https://it.slac.stanford.edu/support) and request re-enablement or password reset.

## Getting a SLAC Account (new S3DF users)

If you are a SLAC employee, affiliated researcher, or experimental facility user, you are eligible for an S3DF account.

1. Obtain a **SLAC System ID** (SID number):

  * SLAC employees should already have a SLAC System ID.

  * Affiliated users/experimental facility users should obtain a SLAC System ID via the Scientific Collaborative Researcher Registration [process form](https://it.slac.stanford.edu/identity/scientific-collaborative-researcher-registration).

2. Take the appropriate SLAC **cyber-security training course(s)** via the [SLAC training portal](https://slactraining.slac.stanford.edu/how-access-the-web-training-portal):

  * All SLAC/Stanford employees or term employees of SLAC or the University: "CS200: Cyber Security Training for Employees".

  * All lab users and non-SLAC/Stanford employees: "CS100: Cyber Security for Laboratory Users Training".

  * Depending on your role, you may be required to take additional cybersecurity training. Consult with your supervisor or SLAC Point of Contact for more details.

3. Ask your [SLAC Point of Contact](contact-us.md#facpoc) to submit a ticket to SLAC IT requesting a SLAC Account on your behalf.

4. Once you have received a SLAC Account, **request a UNIX account**. See [Requesting a UNIX account](#unix-account) below.

5. Once you have both a SLAC Account and a UNIX account, you must **register with S3DF**:

  a) Log into the [Coact User Portal (https://coact.slac.stanford.edu)](https://coact.slac.stanford.edu) using your SLAC Account via the "SLAC Account" option.  

  b) Click on "Repos" in the menu bar.  

  c) Click the "Request Access to Facility" button and select your appropriate facility affliation from the dropdown.  

  d) Include your affiliation and other contextual information for your request in the "Notes" field, then click submit.  

  e) A computing Czar for the S3DF Facility you requested access to will review your request. **Once approved by a facility czar**, you shall receive an email of successful registration.

?> Your S3DF facility computing czar may have already pre-registered your account in S3DF so that the above step of Requesting access to a Facility in Coact is not necessary. In such cases, you will instead receive an email asking for you to log in to https://coact.slac.stanford.edu to activate your account.

## Requesting a UNIX account :id=unix-account

A SLAC Account does not include a UNIX account. You need both before you can be enabled for S3DF.

To request a UNIX account, you or your supervisor should submit a request using the [SLAC Computer Account Request form](https://slacprod.servicenowservices.com/it_services?id=sc_cat_item&sys_id=17176b676ff12100aae0c6012e3ee4f7&sysparm_category=d65827c46fd921009c4235af1e3ee434&catalog_id=e0d08b13c3330100c8b837659bba8fb4):

* **Request Type**: "New Individual account"
* **Account Type**: "Heimdal (UNIX)"

Once your UNIX account has been created, continue with [registering with S3DF](#getting-a-slac-account-new-s3df-users).

## Managing your SLAC Account :id=managing-account

Please ensure that you comply with all SLAC training and cyber-security requirements to avoid having your account disabled. You will be notified of these requirements via email.
SLAC Accounts are also automatically disabled after 60 days of inactivity (no logins). 

If you need to renable your SLAC Account, please use this [Reactivation Service]( https://identity.slac.stanford.edu/reactivate).

You can change your password via the SLAC Account self-service password update site: https://adfs.slac.stanford.edu/adfs/portal/updatepassword

If you have forgotten your password and need to reset it, please contact the [SLAC IT Service Desk](https://it.slac.stanford.edu/support).

## Support for urgent account-related issues

Staff and users needing assistance outside of business hours should call the main IT Service Desk line at (650) 926-4357. They will be presented with a new menu for after-hours support:

Option 1: For Account Lockouts and Password Resets

Option 2: For all other issues

When a user selects Option 1, the system is designed to maximize the chance of reaching an on-call technician promptly. The user can choose to wait on hold or go directly to voicemail. If they wait, the system will cycle between the primary and secondary on-call staff members in 15-second intervals to avoid rolling to personal voicemail. If the caller is unable to reach the scheduled agents, they will be asked to leave a detailed voicemail. Total hold time will be two minutes if all scheduled agents are unable to answer the call.

The service level objective for these urgent off-hours account issues is to provide a response within 30 minutes during non-business hours (from 5 PM to midnight during weekdays and 8 AM - midnight on the weekends).
Between the hours of midnight and 8:00 AM, support will be provided on a best-effort basis.

 

