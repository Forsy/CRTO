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

If using amsibypass payload remember to change the embeded download if using porxy/reverse portfwd

