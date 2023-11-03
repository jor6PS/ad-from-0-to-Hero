# Enumerando usuarios

```Bash
#Enumerar solo usaurios con enum4linux
enum4linux -U <ip> | grep 'Users'

#Enumerar con net rpc
net rpc group members 'Domain Users' -W '<nombre dominio completo>' -I '<ip>' -U '%'

#Enumerar con Crackmapexec
poetry run crackmapexec smb <rango ip> --users
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/find_user_list/vid.gif?raw=true "Enumerando usuarios con enum4linux, net rpc y crackmapexec")
