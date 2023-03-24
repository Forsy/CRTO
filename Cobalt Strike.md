# Listeners

## egress and p2p

Egress: uses domain name to route traffic thorugh internet ex: DNS, HTTP


P2P: p2p as the name says lol ex: SMB,TCP

## SMB

*OPSEC:*
```
This default pipe name is quite well signatured.  A good strategy is to emulate names known to be used by common applications or Windows itself.  Use `PS C:\> ls \\.\pipe\` to list all currently listening pipes for inspiration.
```



# Payloads and Listeners

HTML:  egress x86
MS Office Macro: egress
Stager: egress all arch
Stageless: egress/p2p

Stageless Payload Generator

As above, but generates stageless payloads rather than stagers.  It has slightly fewer output formats, e.g. no PowerShell, but has the added option of specifying an exit function (process or thread).  It can also generate payloads for P2P listeners.

Windows Stager Payload

Produces a pre-compiled stager as an EXE, Service EXE or DLL.

Windows Stageless Payload

Produces a pre-compiled stageless payload as an EXE, Service EXE, DLL, shellcode, as well as PowerShell.  This is also the only means of generating payloads for P2P listeners.

Windows Stageless Generate All Payloads

Pretty much what it says on the tin.  Produces every stageless payload variant, for every listener, in x86 and x64.



https://buffered.io/posts/staged-vs-stageless-handlers/


