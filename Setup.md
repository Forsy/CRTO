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

# AV Evasion

WSL
```
cd /mnt/c/Tools/cobaltstrike/arsenal-kit/kits/artifact

./build.sh pipe VirtualAlloc 277492 5 false false /mnt/c/Tools/cobaltstrike/artifacts

```