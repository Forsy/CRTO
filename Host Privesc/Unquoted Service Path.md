[Unquoted Service Paths - Privilege Escalation en Windows - Deep Hacking](https://deephacking.tech/unquoted-service-paths-privilege-escalation-en-windows/)


## Conditions

1. Has spaces in the path _and_ is also not quoted - this is condition #1 for exploitation.
```
wmic service get name,displayname,pathname,startmode | findstr /i /v "C:\Windows\\" | findstr /i /v """
```

2. If we can drop a binary into any of those paths, the service will execute it before the real one. Of course, there's no guarantee that we have permissions to write into either of them - this is condition #2
```
powershell Get-Acl -Path "C:\Program Files\Vulnerable Services" | fl
```
	Access : BUILTIN\Users Allow  CreateFiles, Synchronize

SharpUp will also list any services that match these conditions.
```
execute-assembly C:\Tools\SharpUp\SharpUp\bin\Release\SharpUp.exe audit UnquotedServicePath
```

> [!important] 
> Payloads to abuse services must be specific "service binaries", because they need to interact with the Service Control Manager.  When using the "Generate All Payloads" option, these have svc in the filename. 

3. 