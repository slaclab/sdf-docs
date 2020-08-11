# Accounts and Access

!> Please note that we are effectively treating the design and implementation of SDF as a green field deployment. As such certain technologies and tools may not be available. Please [contact us](contact-us.md) if you wish for anything to be added or removed.

## How do I get access to SDF?

If you are a SLAC employee, affiliated researcher, or user facility user, you are eligible for a SDF account.

!> SDF uses Windows Active Directory for authentication. As such, your existing SLAC Unix account will not work with SDF.

As we transition from our legacy authentication technologies, you will need a SLAC Windows account to utilise SDF:

If you do not have a SLAC Windows account, you can...

- If you already have a SLAC Unix account, you can request one automatically one through [Accounts Portal](https://oraweb.slac.stanford.edu/apex/slac/f?p=136). You may have to wait upto an hour for some of the backend systems to verify your account.
- You SLAC sponsor can request a SLAC Windows account at: https://slacprod.servicenowservices.com/it_services?id=sc_cat_item&sys_id=17176b676ff12100aae0c6012e3ee4f7&sysparm_category=d65827c46fd921009c4235af1e3ee434 (SLAC login required)


## How do I log onto SDF?

You can access SDF via [SSH](#ssh) or via a [web portal](interactive-compute.md) using your SLAC credentials.


## How do I SSH  :id=ssh

You can connect to our bastion SSH login servers at eitehr

- sdf-login01.slac.stanford.edu
- sdf-login02.slac.stanford.edu

!> _TODO_ use a load balanced name?

### Using a Terminal

You can use any SSH client, such as [OpenSSH](www.openssh.com) or [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/) use use the Standard TCP port 22 to connect to the servers above.

The following example shows us using the `ssh` command to login to one of the SDF SSH login servers. It asks for our password (which we enter, followed by `Enter`) and shows a successful login.

?> The `$` character in terminal prompt examples signify your input prompt and provides an example of the command you should type in the text preceeding it.

```bash
$ ssh sdf-login01.slac.stanford.edu
ytl@sdf-login02.slac.stanford.edu's password:
<enter SLAC password>
Last login: Mon Aug 10 18:48:49 2020 from ocio-pc94982.slac.stanford.edu
===============================================================================
                                NOTICE TO USERS

This is a Federal computer system and is the property of the United States
Government. It is for authorized use only. Users (authorized or unauthorized)
have no explicit or implicit expectation of privacy.

Any or all uses of this system and all files on this system may be intercepted,
monitored, recorded, copied, audited, inspected, and disclosed to authorized
site, Department of Energy, and law enforcement personnel, as well as
authorized officials of other agencies, both domestic and foreign.  By using
this system, the user consents to such interception, monitoring, recording,
copying, auditing, inspection, and disclosure at the discretion of authorized
site or Department of Energy personnel.

Unauthorized or improper use of this system may result in administrative
disciplinary action and civil and criminal penalties.  By continuing to use
this system you indicate your awareness of and consent to these terms and
conditions of use.  LOG OFF IMMEDIATELY if you do not agree to the conditions
stated in this warning.

===============================================================================
CENTOS 7.8.2003 3.10.0-1127.13.1.el7.x86_64 AMD EPYC 7542 32-Core Processor sdf-login01.slac.stanford.edu
===============================================================================
[ytl@sdf-login01 ~]$
```

### Using Open Ondemand :id=web-terminal

If you do not have a terminal handy (or one of the applications mentioned above), you can also use our [interactive](#interactive) logon to launch a web-based terminal using [Open Ondemand](https://openondemand.org/):

[Launch web based terminal to SDF](https://ondemand-dev.slac.stanford.edu/pun/sys/shell/ssh/sdf-login01.slac.stanford.edu).

After you click on the above link, you may be asked to log on our interactive environment - bouncing you to [CILogon](https://www.cilogon.org/) where you can select 'SLAC National Accelerator Laboratory' from the list. This will then redirect you to our Windows SAML ADFS authentication service where you can enter your username and password. You may be asked for a '2 factor' authentication using Duo.

As long as you keep your web browser open, or are not using your browsers private browsing feature, you should only need to authenticate again about once a day.

?> We are currently working on providing delegated access to SDF such that you can use CILogon to authenticate with your home institution's computer account so that you need not have to log on with your SLAC account.

From there, you will be presented a prompt for your password, just like as [above](#using-a-terminal).



## How to I access my group/collaboration's data?


?> _TODO_ unix groups etc.



## Great! What now?

- determine where your data is
- see what compute resources are available to me
- launch a batch job
- buy more storage or compute
- transfer my data in/out of SDF

