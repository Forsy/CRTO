check ps
check tickets
check groups  of pwned users
check pwnd groups localadmin acces to vms
```
powerpick Get-DomainGPOUserLocalGroupMapping -LocalGroup Administrators | select ObjectName, GPODisplayName, ContainerName, ComputerName | fl
```
check dpapi
check uncosntrained
check constrained
if cifs ticket does not work try alt service name ldap and dcsync if admin
check Resource-Based Constrained Delegation
check  Shadow Credentials
check certificates if kdd_error_padata.. restart dc if possible
check gpo
sql check impersonation and acces

1.  Oddly enough I was getting caught by AMSI as well. If you wanna just bypass AMSI to get ur payload running on the box you can use the following cradle (editado)
    ![Imagen](https://media.discordapp.net/attachments/866727478062743572/1102694221544181770/image.png?width=550&height=34)
    /bypass == file hosted on teamserver containing AMSI bypass
