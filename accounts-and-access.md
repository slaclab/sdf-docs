# Accounts and Access

## How do I get access to SDF? :id=access

If you are a SLAC employee, affiliated researcher, or user facility user, you are eligible for a SDF account.

!> SDF uses Windows Active Directory for authentication. As such, your existing SLAC Unix account will not work with SDF.

As we transition from our legacy authentication technologies, you will need a SLAC ID to utilise SDF (The SLAC ID account is the same as our SLAC Windows account):

If you do not already have a SLAC Windows account, you can...

- If you already have a SLAC Unix account, you can request one automatically one through our [Accounts Portal](https://ad-account.slac.stanford.edu). Once it has created a SLAC ID you may have to wait upto an hour for some of the backend systems to verify your account. When you can [ssh into SDF](#ssh) then your SDF account is ready!

or...

- Your SLAC sponsor can request a SLAC Windows account at this [Service Now Link](https://slacprod.servicenowservices.com/it_services?id=sc_cat_item&sys_id=17176b676ff12100aae0c6012e3ee4f7&sysparm_category=d65827c46fd921009c4235af1e3ee434) (SLAC login required)

!> __Please Note:__ If this is the first time you are using SDF, after creating your [SLAC ID](#access) you will need to [ssh](#ssh) into our systems prior to anything else (including launching [jupyter](software.md#jupyter) etc.) so that our automated setup can finish configuring your home directories etc. for you.

## How do I log onto SDF?

You can access SDF via [SSH](#ssh) or via a [web portal](interactive-compute.md) using your SLAC credentials.


## How do I SSH?  :id=ssh

We recommend that you connect to our load balanced SSH service at

```
sdf-login.slac.stanford.edu
```

?> __Note:__ Our load balanced endpoint at `sdf-login` does not currently forward kerberised keys, as such only password and ssh-key authentication is support at this time.

Otherwise, you can also log in individually to our current pool of servers at

```
sdf-login01.slac.stanford.edu
sdf-login02.slac.stanford.edu
```

### Using a Terminal

You can use any SSH client, such as [OpenSSH](www.openssh.com) or [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/) and use the Standard TCP port 22 to connect to the servers above.

The following example shows us using the `ssh` command to login to one of the SDF SSH login servers. It asks for our password (which we enter, followed by `Enter`) and shows a successful login.

?> The `$` character in terminal prompt examples signify your input prompt and provides an example of the command you should type in the text preceeding it.

```bash
$ ssh sdf-login01.slac.stanford.edu
ytl@sdf-login02.slac.stanford.edu's password:
<enter SLAC password>
Last login: Mon Aug 10 18:48:49 2020 from ocio-pcXXXXX.slac.stanford.edu
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

?> __Note:__ Only 'SLAC National Accelerator Laboratory' is currently supported as a login mechanism for SDF Ondemand. If you select any other provider in CILogon, you will recieve a user mapping error. If you selected 'remember this selection' and chose something other than SLAC for Identity Provider, you will have to visit [logout](/logout ':ignore') or clear your browser cookies to be able to select SLAC from the CILogon list again

As long as you keep your web browser open, or are not using your browsers private browsing feature, you should only need to authenticate again about once a day.

?> We are currently working on providing delegated access to SDF such that you can use CILogon to authenticate with your home institution's computer account so that you need not have to log on with your SLAC account.

From there, you will be presented a prompt for your password, just like as [above](#using-a-terminal).



## How to I access my group/collaboration's data?

SDF uses Unix POSIX groups for access. All existing Unix groups from centos7.slac.stanford.edu or rhel6-64.slac.stanford.edu are available in SDF. To view all groups known to SDF, you can use this script:
```
[user@sdf-login01 ~]$ /usr/bin/listgroups 
```

To view all groups you are a member of, you can use this command:
```
id
```
To view all groups that someone else is a member of, you can use this command:
```
id [username]
```
(replace [username] with the username you wish to look up. The output includes the GID (Group ID) and group name.  The GID is the significant part and it's what controls access; the group name is just a convenient way for humans to refer to the GID without remembering numbers.

## Great! What now?

!> __TODO__ add some links and describe

- determine where your data is
- see what compute resources are available to me
- launch a batch job
- buy more storage or compute
- transfer my data in/out of SDF

