# llaps

LAPS agent for linux

This python script will set a randomly generated password for
root or other local account if the expiration date has passed
in your Active Directory. Mimics behavior of LAPS
(Local Administrator Password Solution) for Windows

Active Directory Attributes Modified:
  dsAttrTypeNative:ms-Mcs-AdmPwd - Where Password is stored
  dsAttrTypeNative:ms-Mcs-AdmPwdself.expirationTime - Expiration Time

Uses config settings, epoch time converter and password gen from macOSLAPS-Legacy https://github.com/joshua-d-miller/macOSLAPS-Legacy
Joshua D. Miller - josh@psu.edu - The Pennsylvania State University
Used under the The MIT License (MIT)

Samba machine password code provided by Andrew Bartlett https://samba.org/~abartlet/
based from discussion http://samba.2283325.n4.nabble.com/retrieve-machine-password-in-current-Samba-td4723249.html

All other code under CSIRO Open Source Software Licence Agreement (variation of the BSD / MIT License)
