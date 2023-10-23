# Video enumerando usuarios

Referencia vid1

#Comandos

```
#Enumerar solo usaurios con enum4linux
enum4linux -U <ip> | grep 'Users'

#Enumerar con net rpc
net rpc group members 'Domain Users' -W '<nombre dominio completo>' -I '<ip>' -U '%'

#Enumerar con Crackmapexec
poetry run crackmapexec smb <rango ip> --users
```



# Video enum4linux-ng

Referencia vid2

#Comandos

```
enum4linux-ng.py -As <target> -oY <output>
```
