
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

```