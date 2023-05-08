

dc.acme.corp   
web.acme.corp  
wkstn.acme.corp

Schema Admins        
Enterprise Admins    
Domain Admins        
Key Admins           
Enterprise Key Admins
DnsAdmins            
Sysadmins            



admin rc4 c2e0703b377aa3be5ad07a1319241d5a
pcotton sysadmins

sysadmins -> wkstn.acme.corp


privesc
ntlm cotton
dpapi



----------- 
ad.kato.org 
jmp.kato.org
db.kato.org 



```
 * NTLM     : cafd6970609208fed259fc5c89b8acac
	 * SHA1     : afb186767e473eb2f79c545a42f7d11b852861ab
	 * DPAPI    : 1aed5b7c0c62afef065f20af6621aa2d
```


admin rc4 
8a87b9e4bac0ad12010eb8888e771ff9

trusted
4515f05a4d913e2bf91575b29aede84e

paw.kato.esae
rdc.kato.esae 10.10.150.10



```
SourceName      : kato.org
TargetName      : acme.corp
TrustType       : WINDOWS_ACTIVE_DIRECTORY
TrustAttributes : FOREST_TRANSITIVE
TrustDirection  : Outbound
WhenCreated     : 10/6/2022 12:17:32 PM
WhenChanged     : 5/7/2023 8:17:27 AM

SourceName      : kato.org
TargetName      : kato.esae
TrustType       : WINDOWS_ACTIVE_DIRECTORY
TrustAttributes : FILTER_SIDS
TrustDirection  : Outbound
WhenCreated     : 10/6/2022 2:01:03 PM
WhenChanged     : 5/7/2023 8:17:28 AM
```
