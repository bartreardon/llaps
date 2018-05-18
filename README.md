# llaps

LAPS agent for linux

This python script will set a randomly generated password for
root or other local account if the expiration date has passed
in your Active Directory. Mimics behavior of LAPS
(Local Administrator Password Solution) for Windows

Modifies:

|Active Directory Attribute|Descriptoion|
|-------|-------|
|ms-Mcs-AdmPwd | Where Password is stored |
|ms-Mcs-AdmPwdExpirationTime | Expiration Time |

Uses config settings, epoch time converter and password gen from macOSLAPS-Legacy https://github.com/joshua-d-miller/macOSLAPS-Legacy
Joshua D. Miller - josh@psu.edu - The Pennsylvania State University
Used under the The MIT License (MIT)

Samba machine password code provided by Andrew Bartlett https://samba.org/~abartlet/
based from discussion http://samba.2283325.n4.nabble.com/retrieve-machine-password-in-current-Samba-td4723249.html

All other code under CSIRO Open Source Software Licence Agreement (variation of the BSD / MIT License)

# Usage

set default preferences you want directly or updating the instance (see example in main())

Available settings are:

|Setting|Description|default|
|-------|-----------|-------|
|LocalAdminAccount|Sets a local account to be the recipient of the password change|`root`|
|PasswordLength|Password length|`12`|
|DaysTillExpiration|How many days before the password needs to change|`60`|
|DomainController|FQDN of your domain controller||
|RemovePassChars|Characters to remove from generated passwords||
|ExcludeSets|Exclude an entire set of characters||

copy llaps to somwhere in yout $PATH (`/usr/local/bin` is a good place)

schedule llaps to run on whatever schedule is convenient
an example crontab might be:
`0 8,12,16 * * 1-5 /usr/local/bin/llaps >/dev/null 2>&1`
to run at 8am, 12pm and 4pm weekdays

llaps will read ms-Mcs-AdmPwdExpirationTime from the computers AD object and if the date has expired, will initiate a password change
it will generate a random password and attempt to write this to the computers ms-Mcs-AdmPwd property in AD and update the ms-Mcs-AdmPwdExpirationTime property to the new expiration time.
if the write is successful it will change the specified local account password to match.


